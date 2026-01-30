

# Training Manual for Muqaddas Network

**Effective Date:** [Insert date]

## Introduction

Welcome to the Muqaddas Network Training Manual. This guide will help you understand how to earn stars, convert them to coins, and participate in our charity initiatives.

---

## 1. How to Earn Stars

### What are Stars?
Stars are the primary currency within the Muqaddas Network platform. Users can earn stars through various activities.

### Ways to Earn Stars:
1. **Daily Login**: Earn stars simply by logging into your account daily.
2. **Participating in Events**: Join live events, challenges, or competitions to earn bonus stars.
3. **Referrals**: Invite friends to join the platform and earn stars for each successful referral.
4. **Content Creation**: Share quality content (videos, posts, etc.) that engages the community.
5. **Completing Tasks**: Participate in educational modules or community tasks to earn stars.

### Star Earning Formula:
```javascript
// Example: Calculate stars earned from activities
const calculateStars = (activity) => {
  const starRates = {
    dailyLogin: 10,
    eventParticipation: 50,
    referral: 100,
    contentCreation: 25,
    taskCompletion: 15
  };
  
  return starRates[activity] || 0;
};

// Usage
const starsEarned = calculateStars('eventParticipation'); // Returns 50
```

---

## 2. How to Convert Stars to Coins

### What are Coins?
Coins are the withdrawable currency that can be converted to real money (INR/USD).

### Conversion Rate:
- **1 Coin = 10 Stars**
- **Minimum Conversion**: 50,000 Stars = 5,000 Coins

### Conversion Process:
```javascript
// Star to Coin conversion logic
const convertStarsToCoins = (stars) => {
  const CONVERSION_RATE = 10; // 10 stars = 1 coin
  const MIN_STARS = 50000;
  
  if (stars < MIN_STARS) {
    return {
      success: false,
      message: `Minimum ${MIN_STARS} stars required for conversion`
    };
  }
  
  const coins = Math.floor(stars / CONVERSION_RATE);
  
  return {
    success: true,
    coins: coins,
    remainingStars: stars % CONVERSION_RATE
  };
};

// Example usage
const result = convertStarsToCoins(50000);
// Returns: { success: true, coins: 5000, remainingStars: 0 }
```

### Steps to Convert:
1. **Navigate to Wallet**: Go to your account wallet section
2. **Select Convert**: Click on "Convert Stars to Coins"
3. **Enter Amount**: Input the number of stars you wish to convert
4. **Confirm**: Review and confirm the conversion
5. **Receive Coins**: Coins will be credited to your account instantly

---

## 3. Charity Trigger Mechanism

### What is the Charity Trigger?
The Charity Trigger is an automatic system that donates 100% of earnings above ₹50,000 to charity causes (cancer patients and orphans).

### How It Works:

```javascript
// Charity trigger implementation
const processCharityTrigger = (totalEarnings) => {
  const CHARITY_THRESHOLD = 50000; // ₹50,000
  const CHARITY_PERCENTAGE = 1.0;  // 100%
  
  if (totalEarnings <= CHARITY_THRESHOLD) {
    return {
      userAmount: totalEarnings,
      charityAmount: 0,
      triggered: false
    };
  }
  
  // Amount above threshold goes to charity
  const excessAmount = totalEarnings - CHARITY_THRESHOLD;
  const charityAmount = excessAmount * CHARITY_PERCENTAGE;
  
  return {
    userAmount: CHARITY_THRESHOLD,
    charityAmount: charityAmount,
    triggered: true,
    message: `₹${charityAmount} donated to charity automatically`
  };
};

// Example
const earnings = 75000;
const result = processCharityTrigger(earnings);
// Returns: {
//   userAmount: 50000,
//   charityAmount: 25000,
//   triggered: true,
//   message: "₹25000 donated to charity automatically"
// }
```

### Key Points:
1. **Threshold**: ₹50,000 is the maximum you can withdraw
2. **Automatic**: The system automatically triggers when earnings exceed ₹50,000
3. **100% Donation**: All excess amount goes directly to charity
4. **Transparency**: All donations are tracked on the live charity counter
5. **Immutable**: This rule cannot be changed or bypassed

### Example Scenarios:

| Total Earnings | User Receives | Charity Receives | Triggered |
|----------------|---------------|------------------|-----------|
| ₹30,000 | ₹30,000 | ₹0 | No |
| ₹50,000 | ₹50,000 | ₹0 | No |
| ₹75,000 | ₹50,000 | ₹25,000 | Yes |
| ₹100,000 | ₹50,000 | ₹50,000 | Yes |

---

## 4. Payout Process

### Minimum Payout Requirements:
- **Minimum Stars**: 50,000 Stars
- **Minimum Coins**: 5,000 Coins (equivalent to ₹5 or $5 USD)

### Payout Timeline:
- **Processing Time**: Within 5 minutes of request
- **Availability**: 24/7 instant payouts

### Payout Implementation:
```javascript
// Payout processing logic
const processPayout = async (userId, amount) => {
  const MIN_PAYOUT = 5000; // Minimum 5000 coins
  const MAX_PAYOUT = 50000; // Maximum ₹50,000
  
  // Validate amount
  if (amount < MIN_PAYOUT) {
    return {
      success: false,
      error: `Minimum payout is ${MIN_PAYOUT} coins`
    };
  }
  
  // Check charity trigger
  const charityCheck = processCharityTrigger(amount);
  
  // Process payout
  const payout = {
    userId: userId,
    requestedAmount: amount,
    payoutAmount: charityCheck.userAmount,
    charityAmount: charityCheck.charityAmount,
    timestamp: new Date().toISOString(),
    status: 'PROCESSING'
  };
  
  // Execute payment
  await executePayment(payout);
  
  // Update charity counter
  if (charityCheck.triggered) {
    await updateCharityCounter(charityCheck.charityAmount);
  }
  
  return {
    success: true,
    payout: payout
  };
};
```

---

## 5. Best Practices

### For Earning Stars:
1. **Consistency**: Log in daily to maximize star earnings
2. **Engagement**: Participate actively in community events
3. **Quality Content**: Focus on creating valuable content
4. **Referrals**: Build your network through genuine referrals

### For Conversions:
1. **Accumulate**: Wait until you have sufficient stars before converting
2. **Monitor**: Keep track of your star balance regularly
3. **Plan**: Convert strategically based on your financial needs

### For Charity Participation:
1. **Understand**: Know how the charity trigger works
2. **Transparency**: Track your contributions on the live counter
3. **Impact**: Feel proud of your automatic contribution to helping others

---

## 6. Technical Support

### Common Issues:

**Issue: Stars not converting**
```javascript
// Troubleshooting
const troubleshootConversion = (stars) => {
  if (stars < 50000) {
    return "Insufficient stars. Minimum 50,000 required.";
  }
  if (!isUserVerified()) {
    return "Account verification required.";
  }
  return "Contact support for assistance.";
};
```

**Issue: Payout delayed**
- Check internet connection
- Verify bank details
- Contact support if delay exceeds 10 minutes

### Contact Support:
- **Email**: support@muqaddasnetwork.com
- **Phone**: [Insert phone number]
- **Live Chat**: Available 24/7 on the platform

---

## 7. Compliance & Security

### Data Protection:
- All transactions are encrypted
- Personal information is protected
- Compliance with financial regulations

### Fraud Prevention:
```javascript
// Fraud detection system
const detectFraud = (transaction) => {
  const flags = {
    unusualAmount: transaction.amount > 100000,
    rapidTransactions: transaction.frequency > 10,
    suspiciousPattern: checkPattern(transaction)
  };
  
  if (Object.values(flags).some(flag => flag)) {
    return {
      flagged: true,
      requiresReview: true
    };
  }
  
  return { flagged: false };
};
```

---

## Conclusion

This training manual provides all the essential information you need to successfully earn, convert, and understand the charity mechanisms within Muqaddas Network. For any questions or clarifications, please contact our support team.

**Remember**: Every transaction above ₹50,000 automatically helps cancer patients and orphans. Together, we're making a difference! 💚

---

**Version**: 1.0  
**Last Updated**: [Insert date]  
**Next Review**: [Insert date]

---

This training manual follows software development best practices by:
- Providing clear code examples
- Including error handling
- Documenting processes thoroughly
- Offering troubleshooting guidance
- Maintaining version control
