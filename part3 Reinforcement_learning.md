
================================================================================
Q-LEARNING EXPERIMENT REPORT
Student Name: [Your Name]
Date: 2026-02-22
================================================================================

EXPERIMENT 1: DEFAULT CONFIGURATION OBSERVATIONS
================================================================================

Settings from your screenshot:
- Grid Size: 10x10 (with default barriers)
- Alpha: 0.10
- Gamma: 0.90  
- Epsilon: 0.10
- Iteration shown: 255-297

YOUR OBSERVATIONS (based on screenshots):
--------------------------------------------------------------------------------

From Screenshot 1 (Iteration 255):
- Robot position: from (1,2) to (2,2)
- Action taken: 1 (DOWN)
- Old Q-value: -0.10
- New Q-value: -0.20
- Reward: -1.0
- Episode not done yet

From Screenshot 2 (Iteration 296-297):
Iteration 296:
- Robot position: from (0,0) to (0,0) (hit wall/stayed put)
- Action taken: 0 (UP)
- Old Q-value: -0.50
- New Q-value: -0.95
- Reward: -5.0 (wall penalty)

Iteration 297:
- Robot position: from (0,0) to (0,0)
- Action taken: 2 (LEFT)
- Old Q-value: 0.00
- New Q-value: -0.50
- Reward: -5.0

Key Observations:
1. The robot starts at (0,0) and is still learning
2. It receives -5.0 for hitting walls (learns to avoid them)
3. Q-values are negative initially (exploration phase)
4. After ~300 iterations, still hasn't reached goal consistently

================================================================================
EXPERIMENT 2: UNDERSTANDING THE Q-VALUES
================================================================================

What the numbers mean:
--------------------------------------------------------------------------------
- Negative Q-values (-0.1 to -0.95): The robot is still learning, hasn't found high rewards yet
- Wall penalty (-5.0): Teaches robot to avoid obstacles
- Action encoding: 
   0 = UP
   1 = DOWN (seen in iteration 255)
   2 = LEFT (seen in iteration 297)
   3 = RIGHT

Learning Progress:
- Early iterations: Random exploration, many wall hits
- Mid iterations (255): Starting to move, still getting small penalties
- Current state: Building Q-table gradually

================================================================================
EXPERIMENT 3: HYPERPARAMETER IMPACT ANALYSIS
================================================================================

Based on your configuration (Alpha=0.10, Gamma=0.90, Epsilon=0.10):
--------------------------------------------------------------------------------

ALPHA = 0.10 (Learning Rate)
- Moderate learning speed
- Each new experience updates Q-values by 10%
- Balances old knowledge vs new experiences
- From logs: oldQ=-0.50 → newQ=-0.95 shows 90% weight on new info

GAMMA = 0.90 (Discount Factor)
- Values future rewards highly
- Robot considers long-term consequences
- Good for maze navigation where future steps matter

EPSILON = 0.10 (Exploration Rate)
- 10% chance of random action
- 90% follows learned policy
- From iteration 255: followed policy (DOWN)
- From iteration 296: random? (UP into wall)

================================================================================
EXPERIMENT 4: ENVIRONMENT INTERACTION PATTERNS
================================================================================

From the logs, we can see the robot's behavior:
--------------------------------------------------------------------------------

Pattern 1: Exploration at (0,0)
- Multiple attempts from start position
- Tries different actions (UP, LEFT)
- Learns that boundaries give -5.0 penalty

Pattern 2: Movement after learning
- By iteration 255, robot is moving DOWN from (1,2)
- Shows some path learning is happening
- Still receiving -1.0 step penalties

Pattern 3: Q-value evolution
- Starting values: 0.00
- After wall hits: -0.50, -0.95
- After moves: -0.10 → -0.20 (small updates)

================================================================================
EXPERIMENT 5: Q-TABLE VISUALIZATION ANALYSIS
================================================================================

From your second screenshot, the Q-Table Graphical View:
--------------------------------------------------------------------------------

What you should observe when you click [View Q-Table]:

1. Color patterns:
   - Green cells = higher Q-values (good actions)
   - Red cells = lower Q-values (bad actions)
   - Gray hatched cells = walls/obstacles

2. Number patterns in each cell:
   - Top number: Q-value for UP action
   - Bottom number: Q-value for DOWN action
   - Left number: Q-value for LEFT action
   - Right number: Q-value for RIGHT action

3. Robot marker:
   - Yellow circle shows current position
   - Colored arrow shows last action direction

================================================================================
ANSWERS TO REFLECTION QUESTIONS
================================================================================

1. How does the agent adapt its behavior to reach the goal?
   ------------------------------------------------------------------------------
   Based on the logs, the agent:
   - Starts with random exploration (hitting walls, getting -5.0 penalties)
   - Gradually learns which moves lead to better outcomes
   - By iteration 255, shows purposeful movement (DOWN from (1,2))
   - Updates Q-values based on rewards received
   - Will eventually find path to goal after more iterations

2. What impact do hyperparameters have on learning?
   ------------------------------------------------------------------------------
   Alpha (0.10): 
   - Provides stable, gradual learning
   - Each experience has modest impact (10% update)
   - Prevents overreacting to single events

   Gamma (0.90):
   - Robot cares about future rewards
   - Will learn to take longer paths if they lead to goal
   - Important for maze navigation

   Epsilon (0.10):
   - Mostly exploits learned knowledge (90%)
   - Still explores occasionally (10%)
   - Good balance for continued learning

3. How do grid layout and obstacles influence learning?
   ------------------------------------------------------------------------------
   From the logs:
   - Walls at boundaries give -5.0 penalty
   - Robot quickly learns to avoid these positions
   - Starting at (0,0) is challenging (corner with 2 walls)
   - Need to learn sequence of moves to navigate around obstacles

4. What real-world challenges does this demonstrate?
   ------------------------------------------------------------------------------
   - Exploration vs Exploitation trade-off (explore new paths vs use known ones)
   - Learning from negative feedback (wall penalties)
   - Need for many iterations to learn optimal path
   - Importance of reward design (goal: +100, walls: -5, steps: -1)
   - Cold start problem (starting with no knowledge)

================================================================================
ETHICAL CONSIDERATIONS
================================================================================

Identified Risks:
--------------------------------------------------------------------------------
1. Reward Hacking Risk:
   - Robot might find unintended ways to get rewards
   - Example: Going in circles to avoid walls
   - Mitigation: Carefully designed reward structure

2. Safety During Learning:
   - In real world, exploration could be dangerous
   - Robot might try unsafe actions
   - Mitigation: Train in simulation first

3. Bias in Learning:
   - Robot might favor certain paths
   - Could learn suboptimal behaviors
   - Mitigation: Multiple training runs, diverse environments

Mitigation Strategies:
--------------------------------------------------------------------------------
1. Use simulation for initial training
2. Implement safety constraints
3. Regular validation of learned policies
4. Human oversight during deployment
5. Diverse training environments

================================================================================
FUTURE EXPERIMENTS TO TRY
================================================================================

Based on your current setup, try these next:

1. Increase Alpha to 0.5 - Watch for faster but possibly unstable learning
2. Decrease Epsilon to 0.01 - See if robot stops exploring too early
3. Create simple 5x5 maze without obstacles - Observe faster learning
4. Add more obstacles - See how complexity affects learning time

================================================================================
SCREENSHOTS DOCUMENTATION
================================================================================

Screenshot 1: "2026-02-22 215926.png"
- Shows: Main window with Memo #2 logs at iteration 255
- Key evidence: Robot movement from (1,2) to (2,2)

Screenshot 2: "2026-02-22 220437.png"  
- Shows: Q-Table Graphical View window
- Key evidence: Visual representation of learning

================================================================================
## Screenshots

![Screenshot 1]("Screenshot 2026-02-22 215926.png")

![Screenshot 2]("Screenshot 2026-02-22 220009.png")

![Screenshot 3]("Screenshot 2026-02-22 220437.png")
