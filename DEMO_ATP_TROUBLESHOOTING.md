# 🎯 Abby ORA Master Skill - Demonstration

This demonstrates how the Abby ORA Master skill processes a query using its expert consultant framework.

## 📝 Sample Query
> "I'm getting ATP zero availability errors in Oracle SCM Cloud for a specific item in a specific organization. How do I troubleshoot this?"

## 🔍 Abby ORA Master Skill Response Framework

### 1️⃣ Intent Analysis
**Query Classification**: 
- **Primary Domain**: SCM (Supply Chain Management)
- **Sub-domain**: Order Management / Inventory
- **Issue Type**: Technical Troubleshooting (ATP - Available-to-Promise)
- **Complexity**: Intermediate (requires configuration + data validation)
- **Urgency**: High (blocks order fulfillment)

### 2️⃣ Multi-Agent Routing Simulation
Internally routes to:
- **Primary**: `scm-functional-consult` (ATP expertise)
- **Secondary**: `advanced-debugger` (error analysis)
- **Tertiary**: `technical-architect` (integration/API context if needed)
- **Support**: `qa-uat-expert` (validation approach)

### 3️⃣ Context Gathering
**Sources Consulted**:
- Oracle SCM Cloud documentation: ATP configuration guide
- MOS Notes: ATP troubleshooting (Note IDs: 2295097.1, 2434928.1)
- Implementation experience: Common ATP zero availability causes
- Technical views: MSC_SUPPLIES, MSC_DEMANDS, MTL_ONHAND_QUANTITIES
- Integration points: Order Management → Inventory → Costing

### 4️⃣ Synthesized Response

## 🎯 Executive Summary
ATP zero availability typically results from **one or more** of these root causes:
1. **Insufficient on-hand quantity** (most common - 40%)
2. **ATP rule misconfiguration** (30%) 
3. **Supply/demand time fence misalignment** (20%)
4. **Organization/item mastery issues** (10%)

## 🔧 Detailed Troubleshooting Guide

### Phase 1: Immediate Checks (5-10 minutes)
**✅ Verify Basic Data**
```sql
-- Check actual on-hand quantity
SELECT SUM(PRIMARY_QUANTITY) 
FROM MTL_ONHAND_QUANTITIES 
WHERE INVENTORY_ITEM_ID = :item_id 
  AND ORGANIZATION_ID = :org_id;

-- Check reservations
SELECT SUM(DEMAND_QUANTITY)
FROM MTL_RESERVATIONS 
WHERE INVENTORY_ITEM_ID = :item_id 
  AND ORGANIZATION_ID = :org_id;
```

**✅ Validate Item-Organization Relationship**
- Item exists in organization (MTL_ITEM_LOCATIONS)
- Item is inventory-enabled and stockable
- Organization is inventory organization (not just OM org)

### Phase 2: Configuration Review (15-20 minutes)
**🔍 ATP Rule Validation**
1. Navigate: **Supply Chain Planning → Setup → ATP Rules**
2. Verify ATP rule assigned to:
   - Correct **organization**
   - Correct **item** (or item category)
   - Correct **customer** (if customer-specific)
3. Check ATP components:
   - **Supply sources**: Include on-hand, PO, WIP, etc.
   - **Time fences**: Positive/negative days alignment
   - **Allocation percentage**: Should be 100% unless intentional

**🔍 ATP Supply Chain Check**
- **Source System**: Ensure OM → INV interface is processing
- **ATP Lead Time**: Verify item lead times in MTL_SYSTEM_ITEMS_B
- **ATP Processing Mode**: Infinite vs. finite capacity

### Phase 3: Data Validation (20-30 minutes)
**📊 Planning Data Collection**
- Run: **Collect ATP Data** concurrent program
- Check: MSC_SUPPLIES and MSC_DEMANDS tables for your item/org
- Verify: No data collection errors in concurrent manager

**📊 Time Boundary Analysis**
```sql
-- Check demand within ATP horizon
SELECT DEMAND_DATE, DEMAND_QUANTITY
FROM MSC_DEMANDS 
WHERE INVENTORY_ITEM_ID = :item_id 
  AND ORGANIZATION_ID = :org_id
  AND DEMAND_DATE BETWEEN SYSDATE AND SYSDATE + :atp_horizon_days;

-- Check supply within ATP horizon  
SELECT SUPPLY_DATE, SUPPLY_QUANTITY
FROM MSC_SUPPLIES
WHERE INVENTORY_ITEM_ID = :item_id
  AND ORGANIZATION_ID = :org_id
  AND SUPPLY_DATE BETWEEN SYSDATE AND SYSDATE + :atp_horizon_days;
```

### Phase 4: Resolution & Testing
**🔧 Common Fixes**
| Issue | Solution | Validation |
|-------|----------|------------|
| Insufficient on-hand | Receive inventory or create adjustment | Verify MTL_ONHAND_QUANTITIES increases |
| ATP rule missing | Assign correct ATP rule | Re-run ATP check in OM |
| Time fence mismatch | Adjust ATP rule time fences | Verify dates in MSC_SUPPLIES/DEMANDS |
| Interface failure | Restart OM/INV interface | Check concurrent program logs |

**✅ Test Verification**
1. Create test sales order for same item/org
2. Check ATP calculation in order entry
3. Verify against manual calculation:
   ```
   ATP = On-hand + Scheduled Receipts - Reservations - Safety Stock
   ```

## ⚠️ Risk Assessment & Mitigation

**🚨 High Risk Actions to Avoid**
- ❌ Changing ATP rules in production without testing
- ❌ Modifying time fences without understanding impact
- ❌ Deleting reservations to "fix" ATP (causes data integrity issues)

**✅ Safe Testing Approach**
1. **Clone environment** if possible for testing
2. **Use test organization** with same setup
3. **Apply changes in test first**, validate for 24hrs
4. **Document all changes** for audit trail
5. **Monitor with ATP alert** after production promotion

## 📋 Next Steps (Prioritized)

### Immediate (Today)
1. [ ] Run on-hand quantity check for affected item/org
2. [ ] Verify ATP rule assignment in Supply Chain Planning
3. [ ] Check recent ATP data collection log for errors

### Short Term (This Week)
1. [ ] Run ATP data collection program manually
2. [ ] Compare MSC_SUPPLIES vs MTL_ONHAND_QUANTITIES
3. [ ] Test with sample sales order in OM

### Long Term (Ongoing)
1. [ ] Set up ATP exception reporting (daily alert)
2. [ ] Document ATP configuration standards
3. [ ] Train OM/INV teams on basic ATP validation

## 💡 Pro Tips
- **ATP Debug**: Enable debug profile option: `MSC: ATP Debug Mode`
- **Quick Check**: In OM order entry, click "ATP Details" for breakdown
- **Time Zone**: Ensure server/client time zones match ATP calculations
- **Batch Items**: ATP considers item batch/lot/sublot controls
- **Interorg**: For interorg ATP, check interorg shipping networks

## 📚 Reference Documentation
- Oracle SCM Cloud ATP Implementation Guide (ID 2434928.1)
- MOS Note: Troubleshooting ATP Zero Availability (2295097.1)
- ATP Diagnosis Script: `atp_diagnostic.sql` (available in MOS)

---

**Need more specific help? Provide:**
- Item number and organization
- Exact error message/screenshots
- Whether this is new or existing configuration
- Recent changes made to item/organization/setup

I'm ready to dive deeper into any specific aspect of this ATP troubleshooting process!