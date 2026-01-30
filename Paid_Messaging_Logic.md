

```markdown
# Paid Messaging Logic for Muqaddas Network

**Effective Date:** January 15, 2026  
**Version:** 1.0

---

## 1. Purpose


---

## 2. Messaging Cost Structure

### 2.1 Cost Per Message
- **Cost**: 10 coins per message sent to a host
- **Currency**: Coins (convertible from stars)
- **Minimum Balance**: Users must have at least 10 coins to send a message

### 2.2 Implementation
```javascript
// Messaging cost configuration
const MESSAGING_CONFIG = {
  costPerMessage: 10,
  currency: 'COINS',
  minBalance: 10
};

// Check if user can send message
function canSendMessage(userBalance) {
  return userBalance >= MESSAGING_CONFIG.costPerMessage;
}

// Deduct coins for message
function deductMessageCost(userId, userBalance) {
  if (!canSendMessage(userBalance)) {
    return {
      success: false,
      error: 'Insufficient coins. Minimum 10 coins required.',
      currentBalance: userBalance
    };
  }
  
  const newBalance = userBalance - MESSAGING_CONFIG.costPerMessage;
  
  return {
    success: true,
    coinsDeducted: MESSAGING_CONFIG.costPerMessage,
    newBalance: newBalance,
    message: 'Message sent successfully'
  };
}
```

---

## 3. Message Flow

### 3.1 User Sends Message
```javascript
// Message sending logic
async function sendMessageToHost(userId, hostId, messageContent) {
  try {
    // Step 1: Validate user balance
    const user = await getUserById(userId);
    
    if (user.coins < MESSAGING_CONFIG.costPerMessage) {
      return {
        success: false,
        error: 'Insufficient coins',
        required: MESSAGING_CONFIG.costPerMessage,
        current: user.coins
      };
    }
    
    // Step 2: Deduct coins from user
    const deduction = await deductCoins(userId, MESSAGING_CONFIG.costPerMessage);
    
    // Step 3: Credit host (70% of message cost)
    const hostEarning = MESSAGING_CONFIG.costPerMessage * 0.70;
    await creditHost(hostId, hostEarning);
    
    // Step 4: Platform fee (25%)
    const platformFee = MESSAGING_CONFIG.costPerMessage * 0.25;
    await creditPlatform(platformFee);
    
    // Step 5: Charity allocation (5%)
    const charityAmount = MESSAGING_CONFIG.costPerMessage * 0.05;
    await creditCharity(charityAmount);
    
    // Step 6: Save message
    const message = await saveMessage({
      senderId: userId,
      receiverId: hostId,
      content: messageContent,
      cost: MESSAGING_CONFIG.costPerMessage,
      timestamp: new Date().toISOString()
    });
    
    // Step 7: Send notification to host
    await notifyHost(hostId, userId, messageContent);
    
    return {
      success: true,
      messageId: message.id,
      coinsDeducted: MESSAGING_CONFIG.costPerMessage,
      newBalance: user.coins - MESSAGING_CONFIG.costPerMessage
    };
    
  } catch (error) {
    console.error('Message sending error:', error);
    return {
      success: false,
      error: 'Failed to send message. Please try again.'
    };
  }
}
```

---

## 4. Revenue Distribution

### 4.1 Split Logic
```javascript
const REVENUE_SPLIT = {
  host: 0.70,        // 70% to host
  platform: 0.25,    // 25% platform fee
  charity: 0.05      // 5% to charity
};

// Calculate revenue distribution
function calculateRevenueSplit(messageCount) {
  const totalRevenue = messageCount * MESSAGING_CONFIG.costPerMessage;
  
  return {
    totalRevenue: totalRevenue,
    hostEarnings: totalRevenue * REVENUE_SPLIT.host,
    platformFee: totalRevenue * REVENUE_SPLIT.platform,
    charityContribution: totalRevenue * REVENUE_SPLIT.charity
  };
}

// Example
const split = calculateRevenueSplit(100); // 100 messages
// Returns:
// {
//   totalRevenue: 1000,
//   hostEarnings: 700,
//   platformFee: 250,
//   charityContribution: 50
// }
```

---

## 5. User Interface Implementation

### 5.1 Frontend Component
```javascript
// React component for messaging
import React, { useState } from 'react';

function MessageHost({ hostId, userCoins }) {
  const [message, setMessage] = useState('');
  const [sending, setSending] = useState(false);
  
  const handleSendMessage = async () => {
    if (userCoins < 10) {
      alert('Insufficient coins. You need at least 10 coins to send a message.');
      return;
    }
    
    if (!message.trim()) {
      alert('Please enter a message.');
      return;
    }
    
    setSending(true);
    
    try {
      const response = await fetch('/api/messages/send', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          hostId: hostId,
         
