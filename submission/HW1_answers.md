Task 1

When considering a reward scale, you often want to ensure that max(reward_for_failure) < min(reward_for_success).

In this case, min(reward_for_success) happens if the agent successfully solves the grid on step 1280.  
The episodic reward is thus 1 - 0.9 * (1280 / 1280) = 0.1.
There is also a separate reward of 0.5 for picking up the key, which is required for the episode to be successful.

The max(reward_for_failure) happens if the agent picks up the key, but does not attempt to pick up any other objects.
Then the agent just performs other random actions (other than pick up) until the time expires.
This provides the key pickup reward of 0.5 and nothing else.  

Assume that the penalty for a bad pickup is x.  This penalty can be applied a maximum of 1279 times (as the first pickup is successful).
Combining all of this, we have:
max(reward_for_failure) = 0.5
min(reward_for_success) = 0.6 - 1279 * x

To ensure that max(reward_for_failure) < min(reward_for_success), we have:
0.5 < 0.6 - 1279 * x
-0.1 < -1279 * x
1279 * x < 0.1
x < 0.000078

As a round number, I selected 0.00005.

Note that this is worst case analysis.
The penalty could be an order of magnitude or two higher without affecting performance as the agent learns not excessively pickup objects.  
Poorly scaled dense positive rewards tend to impact training more than poorly scaled dense negative rewards.