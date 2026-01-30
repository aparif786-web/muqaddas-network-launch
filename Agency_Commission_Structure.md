Here’s a well-structured **Agency Commission Structure** document, formatted for your `Agency_Commission_Structure.md`. This document outlines the commission logic and growth opportunities for agencies.

---

# Agency Commission Structure

**Effective Date:** [Insert date]

## Overview

This document outlines the commission structure for agencies collaborating with Muqaddas Network. Our goal is to incentivize agencies through an automated commission system that rewards performance and encourages growth.

---

## Commission Rates

### 1. **Automated Gap Commission Logic**
- Agencies will receive commissions based on their performance levels, structured as follows:
  - **12% Commission**: For agencies at Level 1.
  - **16% Commission**: For agencies at Level 2.
  - **20% Commission**: For agencies at Level 3.

*The commission percentage awarded will be calculated automatically based on the agency's performance metrics. [cite: 2026-01-09]*

---

## Agency Levels

### 2. **Advancement to Higher Levels**
- Agencies can progress through three levels:
  - **Level 1**: Entry-level agencies.
  - **Level 2**: Mid-tier agencies.
  - **Level 3**: Top-tier agencies.

*Agencies can achieve a maximum level of **20**, which corresponds to the highest commission rate of 20%. [cite: 2026-01-29]*

### 3. **Criteria for Advancement**
- To be promoted to **Agency Level 20**, agencies must meet specific performance criteria:
  - **Volume Requirement**: Agencies achieving a monthly sales volume of **$3,000** will qualify for direct promotion to Level 20.

*This incentivizes agencies to increase their sales volume and enhances their earning potential. [cite: 2026-01-09]*

---

## Implementation Logic

### 4. **Commission Calculation Logic**
```javascript
function calculateCommission(level, salesVolume) {
    const commissionRates = {
        1: 0.12, // 12%
        2: 0.16, // 16%
        3: 0.20  // 20%
    };

    if (salesVolume >= 3000) {
        return commissionRates[3]; // Promote to Level 20 and apply highest commission
    }

    return commissionRates[level] || 0; // Default to current level commission
}

// Example Usage
const currentLevel = 1; // Example: Level 1 agency
