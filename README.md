# AnyLogic-LogicLessProject

Let's break down the steps for creating a simple AnyLogic model for a drag race, including two cars, a traffic light, random speeds, and determining the winner after three races.

### Step 1: **Create a New Model in AnyLogic**
1. Open AnyLogic.
2. Click on **File** > **New** > **Model**.
3. Name your model `DragRace` and choose the appropriate options for your model (for example, "Discrete Event").

### Step 2: **Create the Car Agent Type**
1. Right-click on **Agent Types** in the **Projects** pane, and select **New Agent Type**.
2. Name it `Car` and click **OK**.
3. In the `Car` agent:
   - Add a **Parameter** named `speed` to represent the car's speed.
   - Set the speed to be a random value. In the **Initial Value** for the `speed`, type: `random(50, 100)` (this generates a random value between 50 and 100).
   - Create a **Statechart** to represent the car’s movement (optional, but can be useful for controlling stages in the race).

### Step 3: **Create the Main Agent (Race Environment)**
1. Right-click on **Agent Types** in the **Projects** pane and select **New Agent Type**.
2. Name it `Main` (this will be the race environment) and click **OK**.
3. Inside the **Main** agent, you will handle the race logic, traffic light, and other elements of the simulation.

### Step 4: **Add the Traffic Light (Statechart)**
1. In the **Main** agent, create a **Statechart** to model the traffic light.
   - Add two states: `Red` and `Green`.
     - In the `Red` state, the light should be red.
     - In the `Green` state, the light should be green.
   - Use a **Timer** to control the state transitions.
     - Set a timer (for example, 3 seconds) to randomly switch between the two states: `Red` and `Green`. When the light turns green, the race starts.

### Step 5: **Create Two Cars in the Main Agent**
1. Inside the **Main** agent, create two `Car` agents. These will represent the two cars in the race.
   - Drag the `Car` agent from the **Agent Types** and place them in the **Main** agent.
   - Name them `car1` and `car2`.

### Step 6: **Implement the Random Speed for Cars**
1. In the **Main** agent, before the race begins, set the speed of each car.
   - For each car (car1 and car2), use the `random(50, 100)` function to assign the random speed value. This can be done in the **On entry** section of the car's logic or when the race starts.
     - Example for `car1`:
       ```java
       car1.speed = random(50, 100);
       ```

### Step 7: **Race Logic**
1. **Traffic Light Control:**
   - In the **Main** agent, use the **Statechart** to switch between `Red` and `Green` states. When the traffic light turns green, both cars should start the race.
   - Use a **Delay** or **Timer** in the **Statechart** to simulate the delay before the green light.
   
2. **Car Movement:**
   - After the green light, both cars should start moving. Use a **MoveTo** block or direct movement using **x** and **y** coordinates for the cars.
   - The car will move from one point to another (e.g., from the starting point to the finish line).
   - Set the movement speed to the random speed defined for each car.

### Step 8: **Implement the Three Races**
1. Set up a counter in the **Main** agent to track the number of races.
   - Create a variable named `raceCount` and set its initial value to `0`.
   - Each time a race finishes, increment the `raceCount` by 1.
   - Use a **Condition** to check if the race has been completed three times (e.g., `raceCount >= 3`).
   
2. **Race Completion:**
   - After each race, check which car reaches the finish line first. You can use a **Time** variable or check if the cars’ position exceeds the finish line point.

### Step 9: **Determine the Winner**
1. After all three races are completed, compare the times or positions of the cars to determine the winner.
   - You can use a **Timer** to track the time taken by each car for each race.
   - After the third race, compare the times and output the winner.
   
   Example logic for determining the winner:
   ```java
   if (car1.time < car2.time) {
       // car1 is the winner
       displayWinner("Car 1 wins!");
   } else if (car2.time < car1.time) {
       // car2 is the winner
       displayWinner("Car 2 wins!");
   } else {
       // It's a tie
       displayWinner("It's a tie!");
   }
   ```

### Step 10: **Display the Winner**
1. Add a **Text box** or **Message** in the **Main** agent to display the result after three races.
   - You can use **Message** to show who the winner is: `Message("Car 1 wins!")`.

### Step 11: **Run the Model**
1. Click the **Run** button to simulate the drag race.
2. The cars should start racing when the traffic light turns green. After three races, the winner should be displayed.

### Additional Tips:
- You can use **Animation** to visually represent the cars moving on a path or road.
- You can also add extra features, such as random weather conditions affecting the car's speed or road conditions.

This step-by-step guide will help you create a drag race simulation with random speeds, a traffic light controlling the start, and a winner determined after three races in AnyLogic.
