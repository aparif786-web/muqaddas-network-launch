Here are the structured implementations for **Host_Claim_Manual.md** and **Guinness_Record_Mission.md** following software development best practices:

---

# Host_Claim_Manual.md

**Effective Date:** [Insert date]

## Purpose

This manual provides step-by-step instructions for hosts to claim their rewards from the 'Last Week' section in the Muqaddas Network application.

---

## How to Claim Your Weekly Rewards

### Prerequisites
- Active host account
- Completed hosting sessions during the previous week
- Minimum reward threshold met (if applicable)

### Step-by-Step Guide

#### Step 1: Navigate to Rewards Section
```javascript
// Navigation implementation
function navigateToRewards() {
    const rewardsSection = document.getElementById('rewards-section');
    rewardsSection.scrollIntoView({ behavior: 'smooth' });
}
```

1. Open the Muqaddas Network app
2. Tap on the **Profile** icon (bottom navigation)
3. Select **"My Rewards"** from the menu

#### Step 2: Access Last Week's Rewards
```javascript
// Fetch last week's rewards
async function getLastWeekRewards(userId) {
    const lastWeek = getLastWeekDateRange();
    
    const rewards = await fetch(`/api/rewards/weekly`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            userId: userId,
            startDate: lastWeek.start,
            endDate: lastWeek.end
        })
    });
    
    return await rewards.json();
}

function getLastWeekDateRange() {
    const today = new Date();
    const lastWeekEnd = new Date(today.setDate(today.getDate() - today.getDay()));
    const lastWeekStart = new Date(lastWeekEnd);
    lastWeekStart.setDate(lastWeekEnd.getDate() - 6);
    
    return {
        start: lastWeekStart.toISOString(),
        end: lastWeekEnd.toISOString()
    };
}
```

1. In the Rewards section, locate **"Last Week"** tab
2. View your accumulated rewards for the previous week
3. Check the breakdown:
   - Total stars earned
   - Bonus rewards
   - Charity contribution

#### Step 3: Claim Your Rewards
```javascript
// Claim rewards implementation
async function claimWeeklyRewards(userId, rewardId) {
    try {
        // Validate claim eligibility
        const isEligible = await validateClaimEligibility(userId, rewardId);
        
        if (!isEligible.valid) {
            return {
                success: false,
                error: isEligible.reason
            };
        }
        
        // Process claim
        const claimResult = await fetch(`/api/rewards/claim`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                userId: userId,
                rewardId: rewardId,
                timestamp: new Date().toISOString()
            })
        });
        
        const result = await claimResult.json();
        
        if (result.success) {
            // Update user balance
            await updateUserBalance(userId, result.amount);
            
            // Log transaction
            await logRewardClaim({
                userId: userId,
                rewardId: rewardId,
                amount: result.amount,
                timestamp: new Date().toISOString()
            });
            
            // Send notification
            await sendClaimNotification(userId, result);
        }
        
        return result;
        
    } catch (error) {
        console.error('Claim error:', error);
        return {
            success: false,
            error: 'Failed to process claim. Please try again.'
        };
    }
}

async function validateClaimEligibility(userId, rewardId) {
    // Check if reward is already claimed
    const alreadyClaimed = await isRewardClaimed(rewardId);
    if (alreadyClaimed) {
        return { valid: false, reason: 'Reward already claimed' };
    }
    
    // Check if claim period is valid
    const isWithinClaimPeriod = checkClaimPeriod(rewardId);
    if (!isWithinClaimPeriod) {
        return { valid: false, reason: 'Claim period expired' };
    }
    
    return { valid: true };
}
```

1. Tap the **"Claim Rewards"** button
2. Review the reward details in the confirmation dialog
3. Confirm by tapping **"Confirm Claim"**
4. Wait for processing (usually < 30 seconds)
5. Receive confirmation notification

#### Step 4: Verify Claim
```javascript
// Verify claim was successful
async function verifyRewardClaim(userId, rewardId) {
    const claimStatus = await fetch(`/api/rewards/status/${rewardId}`);
    const status = await claimStatus.json();
    
    return {
        claimed: status.claimed,
        claimDate: status.claimDate,
        amount: status.amount,
        transactionId: status.transactionId
    };
}
```

1. Check your updated balance in the wallet
2. View transaction history for the claim record
3. Screenshot for your records (optional)

### UI Component Example
```javascript
// React component for reward claiming
import React, { useState, useEffect } from 'react';

function WeeklyRewardsClaim({ userId }) {
    const [rewards, setRewards] = useState(null);
    const [claiming, setClaiming] = useState(false);
    
    useEffect(() => {
        loadRewards();
    }, []);
    
    async function loadRewards() {
        const data = await getLastWeekRewards(userId);
        setRewards(data);
    }
    
    async function handleClaim() {
        setClaiming(true);
        const result = await claimWeeklyRewards(userId, rewards.id);
        
        if (result.success) {
            alert('Rewards claimed successfully!');
            loadRewards(); // Refresh
        } else {
            alert(`Error: ${result.error}`);
        }
        
        setClaiming(false);
    }
    
    if (!rewards) return <div>Loading...</div>;
    
    return (
        <div className="rewards-claim">
            <h2>Last Week's Rewards</h2>
            <div className="reward-details">
                <p>Total Stars: {rewards.totalStars}</p>
                <p>Bonus: {rewards.bonus}</p>
                <p>Charity Contribution: {rewards.charity}</p>
           
