# Abby ORA Skills - Usage Examples

This document shows how non-technical and new users can leverage Abby ORA Skills to solve Oracle Fusion Cloud challenges.

---

## Example 1: Oracle API Integration (Vague Question from Non-Tech User)

### ❌ User Question (Vague/Unclear)

> "I want to get data from Oracle but I don't know how. Our IT team says we need to use API but I don't understand what that means. We have inventory numbers and need to pull them into our Excel spreadsheet somehow."

### ✅ How Abby ORA Responds

```markdown
## 🔍 Understanding Your Need

It sounds like you want to automatically pull inventory data from Oracle Fusion Cloud into Excel - without needing to write code or understand technical APIs.

## 📋 What You Can Do (No Technical Knowledge Required)

### Option 1: Use Oracle's Built-in Export
1. Go to Oracle Fusion Cloud → Inventory Management
2. Navigate to "On-hand Quantity"
3. Use the "Export" button (spreadsheet icon)
4. Choose Excel format

### Option 2: Set Up Scheduled Reports (For Ongoing Needs)
Your IT team can set up:
- Scheduled data extracts that email you Excel files
- Power Automate connector to pull data automatically

### Option 3: REST API (If You Have Developer Help)
When your IT team is ready, here's what they need:
- Endpoint: `/fscmRestApi/resources/inventory_onhand`
- Authentication: OAuth 2.0
- No coding needed if they use a tool like Postman or Make.com

## 💡 Recommendation

Start with Option 1 (Export) for immediate needs. For automation, ask your IT to explore Oracle's "Scheduled Processes" feature - no API work required!

## ⚠️ Questions to Ask Your IT Team
1. "Can we set up automatic daily inventory reports?"
2. "Is our Oracle environment set up for REST API access?"
3. "Do we have Oracle Integration Cloud (OIC) available?"
```

---

## Example 2: Debugging an ATP Issue

### ❌ User Question (Problem without Cause)

> "Our order management team can't confirm orders. They keep getting errors saying 'ATP not available' but we definitely have inventory. The warehouse says the items are there but Oracle won't let us sell them. This is urgent - we have a customer waiting!"

### ✅ How Abby ORA Responds

```markdown
## 🚨 ATP Issue - Urgent Resolution

I understand this is blocking order fulfillment. Let me help you systematically diagnose and resolve this.

## 🔍 Step 1: Quick Checks (Do These First)

### Check 1: On-hand Quantity
Run this query (ask your IT or DBA to run):
```sql
SELECT item, organization, on_hand
FROM mtl_onhand_quantities
WHERE item = 'YOUR_ITEM_NUMBER';
```

### Check 2: ATP Rule Assignment
Navigate in Oracle:
1. Supply Chain Planning → Planning Setup → ATP Rules
2. Check if your organization has an ATP rule assigned

### Check 3: Current Reservations
```sql
SELECT *
FROM mtl_reservations
WHERE inventory_item_id = YOUR_ITEM_ID
AND demand_source_type = '1';  -- Sales Order
```

## 📊 Most Common Causes & Fixes

| Cause | Frequency | Fix |
|-------|-----------|-----|
| No ATP rule assigned | 35% | Assign ATP rule to org |
| Supply/Demand not collected | 30% | Run "Collect ATP Data" concurrent program |
| Organization-item not linked | 20% | Check item-master relationship |
| Zero safety stock configured | 10% | Review safety stock settings |
| Future demand consuming ATP | 5% | Review scheduled orders |

## ⚡ Immediate Actions

1. **Run ATP Data Collection** (most common fix):
   - Navigate: Tools → Run ATP Collection
   - Select: "Full ATP Collection"
   - Run for affected organization

2. **Verify ATP Rule**:
   - Go to: Supply Chain Planning → ATP Rules
   - Check your org is listed

3. **Test with Sample Order**:
   - Create a test sales order
   - Check if ATP passes now

## 📋 Questions for Your Oracle Consultant
1. "When was the last ATP collection run?"
2. "Has anything changed in our planning parameters recently?"
3. "Are we using ATP beyond quantity or also ATP beyond date?"

## 🔧 If Still Not Working
Escalate to your Oracle support with:
- Screenshot of the error
- Item number and organization
- Output from the queries above
- Results of ATP data collection
```

---

## Example 3: Functional Understanding - Business Logic Q&A

### ❌ User Question (Concept Confusion)

> "Our finance team is arguing about something called 'Cost Inventory' vs 'Receipt Inventory'. I think they're the same thing but they show different numbers. My manager asked me to explain why our inventory value in the balance sheet doesn't match what we see in the inventory report. I don't understand Oracle at all but I need to explain this in tomorrow's meeting. Please help!"

### ✅ How Abby ORA Responds

```markdown
## 📚 Understanding Oracle Inventory Cost vs Receipt Value

**Short Answer**: They're measuring different things - this is normal, not an error!

## 🏗️ The Core Difference

| Term | What It Means | When to Use |
|------|---------------|--------------|
| **Cost Inventory** | Value based on **average cost** or **standard cost** | Financial reporting, balance sheet |
| **Receipt Inventory** | Value based on **actual receipt price** | Operational tracking, purchasing analysis |

## 📊 Why Numbers Are Different

### Scenario Example:
- You ordered 100 units at $10 each = $1,000 receipt value
- But your average cost is $9.50 = $950 cost inventory
- **Difference**: $50 (the "inventory valuation adjustment")

### This is NOT a problem - it shows:
1. ✅ You have inventory received at current prices
2. ✅ Your accounting uses standard/average cost method
3. ✅ The difference is normal and tracked in "Cost Variance"

## 🎯 What Each Report Shows

### Inventory Valuation Report (Finance)
- Shows: Cost inventory
- Purpose: Balance sheet, financial statements
- Formula: Quantity × Average Cost

### Inventory Transaction Report (Operations)
- Shows: Receipt inventory
- Purpose: What we paid, vendor analysis
- Formula: Quantity × Actual Receipt Price

## 📝 Talking Points for Your Meeting

> "The two numbers represent different things:
> - **Receipt value** shows what we paid for incoming inventory (operational)
> - **Cost value** shows the accounting value using our standard costing method (financial)
> - The difference is normal and tracked in our cost variance accounts
> - This is actually a best practice - it helps us see both purchasing trends and financial accuracy"

## 🔍 If You Need to Investigate Further

Questions to ask your functional consultant or accountant:
1. "What cost method are we using? (Average, FIFO, Standard?)"
2. "Are there any pending cost updates?"
3. "Should we run 'Update Inventory Costs' process?"

## ✅ Summary for Tomorrow

**Say this**: "These are two valid measurements for different purposes. The receipt value shows actual purchase prices - the cost value shows our accounting value using the standard costing method. The difference is normal and represents the cost variance between what we paid and our average cost. This is actually a sign of good inventory management - we're tracking both perspectives."
```

---

## Example 4: Q&A Analysis - Complex Business Question

### ❌ User Question (Analysis Request)

> "Our VP wants to know why our supply chain costs increased 15% this quarter. I have access to Oracle but I don't know what reports to run or what data to pull. She needs this for the board meeting next week. Can you tell me exactly what I should look at and how to explain it?"

### ✅ How Abby ORA Responds

```markdown
## 📊 Supply Chain Cost Analysis - VP Request

This is a common request - let me give you exactly what you need for the board meeting.

## 🎯 The 4 Key Areas to Analyze

### 1. Purchase Price Variance (PPV)
**What**: Difference between what we expected to pay vs. what we actually paid
**Report**: Cost Management → Cost Reports → Purchase Price Variance
**Board Talking Point**: "We paid X% more/less than anticipated due to [supplier/commodity reasons]"

### 2. Landed Cost Changes
**What**: Total cost including freight, duties, handling
**Report**: Procurement → Analytics → Spend Analysis
**Board Talking Point**: "Logistics costs increased Y% due to [shipping route changes/fuel costs]"

### 3. Inventory Valuation Changes
**What**: How our inventory value has changed
**Report**: Cost Management → Inventory Valuation → Valuation Summary
**Board Talking Point**: "Inventory value increased Z% due to [new products/safety stock changes]"

### 4. Supplier Cost Changes
**What**: Which vendors changed prices
**Report**: Procurement → Supplier Analysis → Price Performance
**Board Talking Point**: "Top 5 suppliers accounted for X% of cost increase"

## 📋 Data to Prepare (With Timestamps)

Create a simple Excel with these columns:
| Category | Last Quarter | This Quarter | Change % |
|----------|--------------|--------------|----------|
| Material Cost | $X | $Y | Z% |
| Freight | $X | $Y | Z% |
| Duties/Tariffs | $X | $Y | Z% |
| Storage | $X | $Y | Z% |
| **Total** | $X | $Y | **Z%** |

## 💡 Recommended Approach

1. **Run the 4 reports above** this week
2. **Identify top 3 drivers** of the 15% increase
3. **Prepare 1-slide summary** for each driver
4. **Include actions** you're taking to address it

## 📝 Sample Board Slide Text

> "Supply chain costs increased 15% this quarter primarily due to:
> 1. Raw material price increases from key suppliers (+8%)
> 2. Freight rate changes (+4%)
> 3. Inventory valuation adjustments (+3%)
>
> Actions in progress:
> - Renegotiating contracts with top 3 suppliers
> - Evaluating alternate logistics providers
> - Reviewing safety stock levels to optimize"

## 🔧 Need More Help?

If you need specific report instructions or help interpreting data, just ask me which report you need step-by-step guidance for!
```

---

## Example 5: Business Logic - Process Flow Explanation

### ❌ User Question (How Does It Work)

> "I work in Procurement and I've been asked to set up a new purchasing process for our company. I understand the business part but not how Oracle works. We need a process where:
> - Employees request things
> - Manager approves
> - We buy from approved vendors only
> - Different approval amounts for different managers
>
> Can you explain how to set this up in Oracle in simple terms? I need to explain this to our IT team."

### ✅ How Abby ORA Responds

```markdown
## 🛒 Setting Up Your Procurement Process in Oracle Fusion

Great question! Let me break this down in simple terms so you can explain it to IT.

## 📖 Understanding the Flow

Here's what you want (simplified):

```
Employee Request → Manager Approval → Purchase Order → Vendor → Receiving
```

## 🏗️ The 5 Oracle Modules You'll Use

| Step | Oracle Module | What It Does |
|------|---------------|--------------|
| 1 | **Requisition** | Employee creates request |
| 2 | **Approval** | Workflow engine handles approvals |
| 3 | **Purchase Orders** | Approved requests become POs |
| 4 | **Payables** | Vendor invoice matching |
| 5 | **iProcurement** | Employee self-service interface |

## 🎯 Configuration Guide (Share with IT)

### Step 1: Set Up Approval Rules
**What**: Rules for who approves what
**IT Action**:
- Navigate: Workflow → Approval Management
- Create rules based on:
  - Amount thresholds
  - Job level / Manager level
  - Department

### Step 2: Configure Suppliers
**What**: Only use approved vendors
**IT Action**:
- Navigate: Procurement → Suppliers
- Set up approved supplier lists
- Configure "Qualified Suppliers Only" flag

### Step 3: Set Up Requisition Templates
**What**: Standard request formats by department
**IT Action**:
- Navigate: iProcurement → Administration → Templates
- Create templates per department

### Step 4: Configure Purchasing Options
**What**: Global settings
**IT Action**:
- Navigate: Procurement → Procurement Options
- Set approval limits, document controls

## 📝 IT Checklist to Give Them

```
□ Approval rules configured (by amount & job level)
□ Approved supplier lists created
□ Requisition templates built
□ Purchase order types defined
□ User security roles assigned
□ Test with sample transactions
□ Train employees on iProcurement
```

## 💡 Key Concept to Remember

**"In Oracle, everything flows from setup"** - The system only works as well as your configuration. Take time on steps 1-4 and the day-to-day will be smooth.

## 🔧 Questions to Ask Your IT Team

1. "What's our current approval workflow?"
2. "Who has purchasing authority and at what levels?"
3. "Do we have preferred vendors we must use?"
4. "What's our standard PO process today?"

---

## Summary

These examples show how Abby ORA Skills helps users:

| Scenario | What Abby ORA Does |
|----------|-------------------|
| **API/Technical** | Translates technical concepts into simple business terms |
| **Debugging** | Provides systematic troubleshooting with common causes |
| **Functional** | Explains concepts with real examples and visual aids |
| **Business Analysis** | Gives specific reports to run and talking points for leadership |
| **Process Setup** | Provides IT-ready requirements and configuration guides |

**All responses are in plain language - no technical jargon without explanation!**

---

*Developed by: Abhinav Verma | Email: Abbykkv@gmail.com*