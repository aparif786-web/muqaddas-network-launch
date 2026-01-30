

### **1. Daily_Tax_Reward_Policy.md**

```markdown
# Daily Tax Reward Policy

**Effective Date:** [Insert date]

## Overview
This policy outlines the tax reward system for hosts who receive gifts on the Muqaddas Network platform.

## Policy Details
- If a host receives **₹3,00,000** in gifts, they will be rewarded:
  - **3,000 points** for each day they stay live for **2 hours**.

## Eligibility Criteria
- Hosts must be active and engage with their audience for a minimum of 2 hours daily.
- Points will be credited at the end of each day of compliance.

## Implementation
```javascript
// Function to calculate tax rewards
function calculateDailyTaxReward(giftAmount, hoursLive) {
    const rewardPoints = 3000;
    const threshold = 300000; // ₹3,00,000

    if (giftAmount >= threshold && hoursLive >= 2) {
        return rewardPoints;
    }
    return 0; // No rewards
}
```

## Reporting
- Hosts will receive a weekly report detailing their points accumulation based on the daily tax reward policy.

---

**Last Updated:** [Insert date]
```

---

### **2. Gifting_Tier_Return.md**

```markdown
# Gifting Tier Return Policy

**Effective Date:** [Insert date]

## Overview
This policy outlines the tiered reward system for hosts receiving high-value gifts on the Muqaddas Network.

## Policy Details
- Hosts receiving high-value gifts will receive bonus points that increase proportionally:
  - Gifts of **₹5,00,000** will yield a **25%** increase in reward points.
  - Gifts of **₹10,00,000** will yield a **50%** increase in reward points.

## Implementation
```javascript
// Function to calculate gifting tier rewards
function calculateGiftingTierReward(giftAmount) {
    let rewards = 0;

    if (giftAmount >= 1000000) {
        rewards = giftAmount * 0.50; // 50% reward on ₹10,00,000
    } else if (giftAmount >= 500000) {
        rewards = giftAmount * 0.25; // 25% reward on ₹5,00,
