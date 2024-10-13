# ASDE Algorithm Test

## Problem Description

Imagine Abhimanyu in the Chakravyuha. There are 11 circles in the Chakravyuha, each guarded by an enemy equipped with power levels k1, k2, ..., k11. Abhimanyu starts in the innermost circle with a certain amount of power `p` and must cross all 11 circles to reach the Pandavas' army.

### Given:
1. Each circle is guarded by an enemy with power `k1`, `k2`, ..., `k11`.
2. Abhimanyu starts with `p` power.
3. Abhimanyu can skip fighting an enemy `a` times.
4. Abhimanyu can recharge his power `b` times.
5. Battling in each circle results in a loss of power equal to the enemy's power.
6. If Abhimanyu's power is less than the enemy's power, he will lose the battle unless he skips or recharges.
7. Enemies at `k3` and `k7` regenerate once after their first battle, attacking again with half their initial power.

   Write an algorithm to find if Abhimanyu can cross the Chakravyuh and test it with two sets of test cases.

## Algorithm

The following algorithm determines if Abhimanyu can cross all 11 circles and reach the Pandavas' army.

```python
def can_abhi_cross(circles, p, a, b):
    skip_count = 0
    recharge_count = 0
    
    for i in range(len(circles)):
        enemy_power = circles[i]
        
        # If Abhimanyu faces the enemy at k3 or k7
        if i == 2 or i == 6:
            # First battle with full power enemy
            if p >= enemy_power:
                p -= enemy_power  # Successful battle
                regenerated_power = enemy_power / 2  # Regenerated power
                # Regenerated attack
                if p >= regenerated_power:
                    p -= regenerated_power
                else:
                    if recharge_count < b:
                        recharge_count += 1
                        p += regenerated_power  # Recharge for regenerated attack
                    else:
                        return False  # Lost the battle
            else:
                if skip_count < a:
                    skip_count += 1  # Use a skip for k3 or k7
                else:
                    return False  # Lost the battle

        else:
            # Normal battle scenario
            if p >= enemy_power:
                p -= enemy_power
            else:
                if skip_count < a:
                    skip_count += 1  # Use a skip
                else:
                    if recharge_count < b:
                        recharge_count += 1
                        p += enemy_power  # Recharge power
                    else:
                        return False  # Lost the battle

    return True  # Abhimanyu crosses all circles successfully
```
## Test Cases
### Test Case 1
circles1 = [30, 20, 40, 25, 10, 50, 60, 15, 10, 35, 20]  
p1 = 100   
a1 = 2   
b1 = 1   
print(can_abhi_cross(circles1, p1, a1, b1))  # Expected Output: False

### Test Case 2
circles2 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110]   
p2 = 150   
a2 = 3   
b2 = 2   
print(can_abhi_cross(circles2, p2, a2, b2))  # Expected Output: True
