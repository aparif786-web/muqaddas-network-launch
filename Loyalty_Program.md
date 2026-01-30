

```markdown
# Growth Milestones for Hosts

## Purpose
To enhance the power and engagement of hosts in the Muqaddas Network by providing rewards and incentives based on performance metrics.

## Milestone Structure

### Levels
- **Level 1**: Basic Host
- **Level 2**: Experienced Host
- **Level 3**: Elite Host
- **Level 4**: Legendary Host

### Requirements
- Hosts must receive a specific amount of gifts to level up.
- Each level unlocks higher commission percentages.

## Level Up Criteria
- **Level 1 to Level 2**: 100 Gifts
- **Level 2 to Level 3**: 500 Gifts
- **Level 3 to Level 4**: 1,000 Gifts

### Commission Percentage Increases
| Level       | Commission Percentage |
|-------------|-----------------------|
| Level 1    | 5%                    |
| Level 2    | 10%                   |
| Level 3    | 15%                   |
| Level 4    | 20%                   |

## Implementation
- Use a database to track the number of gifts received by each host.
- Implement an API endpoint to update and fetch host levels and rewards.
```

---

### **2. Level Up Rewards (Level_Up_Rewards.md)**

```markdown
# Level Up Rewards for Hosts

## Overview
Hosts can unlock rewards by accumulating gifts. The rewards increase with each level achieved.

## Reward Structure

### Level Rewards
- **Level 1**: Certificate of Achievement
- **Level 2**: Additional 5% commission on monthly earnings
- **Level 3**: Exclusive merchandise (t-shirt, mug)
- **Level 4**: Monthly bonus of ₹1,000

### Reward Distribution
- Rewards are automatically calculated and distributed at the end of each month based on the host's level.
- A notification system will inform hosts of their new level and rewards.

## Implementation
- Create a function to calculate rewards based on the host's current level.
- Schedule a monthly task to distribute rewards automatically.
- Notify hosts through email and in-app notifications.
```

---
