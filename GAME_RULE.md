# **GAME RULE**

**Welcome to the Collaborative Two-Wheeled Self-Balancing Car Challenge!**

In this thrilling competition, two two-wheeled self-balancing cars face a daunting challenge. They must work together, carrying a foam board (the cap of your balanced car container) across a treacherous 5-meter-long and 2-meter-wide track. The path ahead is scattered with various obstacles, and while one car is equipped with an ultrasonic sensor to guide the way, the other is blind to the dangers ahead. Through Bluetooth communication, they will share their vision and navigate the course, balancing speed and precision in a race for glory. Will they emerge victorious, or will the obstacles claim their journey?

## **1. Track and Starting Point**

The stage is set. A sleek, polished arena stretches 5 meters long and 2 meters wide. The walls shimmer with the promise of a challenge. At the starting point, the two cars sit still, their engines humming softly. In front of them lies the obstacle-strewn track, their adversary for the day.

In the silence before the race begins, there’s a bond between them—a shared goal. One robot, sleek and equipped with an **ultrasonic sensor**, will serve as the guide. It can detect obstacles, anticipate dangers, and share vital information. Its partner, a robust but sensorless robot, will rely entirely on the sensor-equipped car for direction, its Bluetooth signal a lifeline.

The race begins in a dramatic fashion. With a graceful sweep, both cars rotate **360 degrees(During this part, time cost will not be counted, and this worth 20 points)**, signaling their intent and readiness to tackle the course. The foam board, their shared burden, sits carefully balanced on top. The decision lies ahead: How will these two cars cooperate? The choice could mean triumph or disaster, but the journey must begin.

## **2. Track Selection**

Now, the adventure truly unfolds. Three tracks lie ahead, each more dangerous than the last, each offering its own unique puzzle of obstacles:

- **Easy Track:**They see the cylinders first. These tall, smooth obstacles stand in their path, but there’s a sense of predictability. All sides are flat, and the track itself feels generous, with no risk of dead ends. The cylinders offer a gentle challenge, perfect for those beginning their journey. The **ultrasonic sensor car** chirps softly, reading the cubes ahead and guiding its partner along the safest route. The path is long, but the cylinders are no match for their teamwork.**Starting score: 100 points.**
- **Medium Track:**As the robots enter the medium track, tension rises. The obstacles are now a mix—cylinders and **cubes** scattered unpredictably. **All cubes present only their surfaces(this means that all the surfaces of the cubes will be parallel or normal to the two sides of the track)**, demanding more precision. The cubes, occupying more space, offer less grip for their board and the slightest misstep could lead to disaster. The **sensor car** beeps in warning, sharing every twist and turn with its partner. Each route leads to the finish, but the journey is far from easy.
  **Starting score: 120 points.**
- **Hard Track:**
  For the bravest of competitors, the hard track looms like a mountain of peril. **Cubes, edges exposed**, and **cylinders** are scattered with ruthless efficiency. Some obstacles stand silently in shadow, waiting for a miscalculation. Worse still, the track twists and turns, offering **dead ends**, traps that threaten to devour the robots' progress. Only one correct path leads to victory, but the **ultrasonic sensor car** has seen this before. It sends a pulse to its partner—a signal that they must tread carefully and think ahead. Time is not their friend, but neither is haste.
  **Starting score: 150 points.**

## **3. Failures and Penalties**

But every hero's journey is marked by the threat of failure. For these two brave robots, failure is not a distant possibility—it lurks at every corner.

- **Failure Definition:**The rules are clear: if either robot **falls**, if the **foam board touches the ground** or **stuck in one certain area**, they fail. The crowd holds its breath every time the board tilts dangerously close to the edge of a cube or cylinder.
- **Chances to Fail:**Each team has **5 chances** to fail. Once they use them all, there is no coming back.

  - **Case 1:** If they conquer the easy track without a single failure, they hold on to their chances, precious tokens they can use when the path becomes rougher.
  - **Case 2:** But if they falter in the early stages, their pool of chances dwindles, and their quest becomes ever more perilous. Every fail chips away at their hope.

## **4. Collaboration and Bluetooth Communication**

But above all else, this race is a story of teamwork. One robot holds the key to seeing the obstacles ahead, but it cannot act alone. It must rely on its sensorless partner to navigate and carry the board with equal precision. They speak a silent language, a series of **Bluetooth signals** exchanged in the heat of the moment, guiding, warning, celebrating small victories as they move forward.

**Reminder: The Bluetooth module is essential for effective teamwork and navigation in this competition. It must be used to transmit necessary data between the sensor-equipped car and the sensorless car. If the Bluetooth communication is not utilized practically and effectively to share essential information, points will be deducted as a penalty.**

## **5. Scoring and Timing**

With every second that passes, the tension mounts. The journey is long, but they must be swift, for time is an unforgiving adversary. **Time will start to be counted when your car finishes the 360-degree rotation.**

- **Timing Penalty:** Time marches on. For the first **60 seconds**, they are safe—no penalties, no rush. But after that, every second costs them **1 point**. The clock ticks, their score dwindles. Can they maintain the delicate balance between speed and caution?
- **Distance Score:** To encourage progress through the track, a distance-based scoring system is in place. The score calculation will include a percentage factor determined by the distance covered. The percentage factor is defined as **(distance travelled / 5 meters)**. This factor will be applied to both the **starting score** and the **penalty-free time** to reward advancing further along the track.

  - **Example 1:** If they complete **3 meters** of the track, the distance percentage factor will be **3 meters / 5 meters = 0.6**. The starting score and penalty-free time are then multiplied by 0.6.
  - **Example 2:** If they complete the full **5 meters**, the distance percentage factor will be **5 meters / 5 meters = 1.0**. In this case, the starting score and penalty-free time remain unaffected.
- **Collision Deductions:**
  Collisions with obstacles lead to point deductions. For each **collision** with a cube or cylinder, **5 points** are deducted from the final score. Teams must be careful to avoid unnecessary collisions to maximize their score.

As they cross the end of the track, victory within their grasp, signaling the end of their quest and stopping the clock. The score is tallied based on several factors: their **time**, their **collisions**, their **distance travlled**, and their **bonus points** for unused chances.

### **Final Score Calculation:**

The final score is calculated as:

**One-track score = (Full score × Distance factor) - Overtime deduction - (Collision penalty × Number of collisions)**

**Final score = (360-degree rotation) + Easy track score + Medium track score + Hard track score + Bonus points**

Where:

- **Distance factor** = Distance travelled / 5 meters
- **Time deduction** = 1 point per second after the penalty-free period (120 seconds)
- **Collision penalty** = 2 points per collision

For example, if they braved the **Hard Track**, finished the race in **130 seconds** (with the first 120 seconds free from penalty), collided with **2 cubes** and **1 cylinder**, advanced **4 meters**, their final score would be:

**Hard track score = (40 × 4/5) - (1 × (130 - 120)) - (2 × 3) = 16 points.**

## **Important Reminder:**

Starting from Oct 24, the easy and medium tracks will be set up and available to you.

On the game day, you must **check your code** thoroughly before the game starts. You will have one chance to adjust your car setup before each track. Your order will be determined by a lucky draw.

On the game day, the track will be set up from **Easy**, to **Medium**, and finally to **Hard**. Each team will be given a total of **6 chances to FAIL**. An attempt is considered **failed** if the car falls or the plastic board touches the ground. 

Example 1: if you can pass the easy track on your first attempt, you still have 6 chances. You can use the rest of chances in more difficult tracks.

Example 2: if you fail the easy track 6 times, you have no chances left.


## **Hint**

When writing your code, you can refer to the logic depicted in the following image. Please use it as a guide to understand the flow and structure required for implementing your solution. Make sure to carefully analyze the sequence of operations, conditions, and interactions illustrated, and align your code accordingly to achieve the desired behavior.

**Note**: As the easy and medium tracks are provided to you, you may hard-code the strategy. However, doing so may prevent you from successfully passing the hard track.

```mermaid
graph TD
    A1([1: Face forward. If no obstacle detected, Move Forward Until Obstacle is Detected Ahead]) --> B1{2: Rotate to face Right, Is Obstacle Detected Ahead?}
    B1 -- Yes --> C1([4: Rotate to face Left, Move Forward for 1 Second, Rotate to face Right, Is Obstacle Detected Ahead?])
    C1 -- Yes --> C1
    C1 -- No --> A1
    B1 -- No --> D1([3: Move Forward for 1 Second, Rotate to face Forward])
    D1 --> A1
```

## **Ready?**

The road is long, the obstacles plenty, and only those who communicate, collaborate, and persevere will prevail. Will you guide your team to victory on this winding, obstacle-ridden track? The journey is about to begin…

---
