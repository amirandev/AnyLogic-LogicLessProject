Creating an **AnyLogic** project named "Dragrace" involves designing a simulation where two cars compete on a road, guided by a traffic light. Here's a step-by-step guide to achieve this:

---

### **1. Create the Project**
1. Open AnyLogic and create a new project named **Dragrace**.
2. In the **Main** agent, add the following components:
   - **Road**: Represent the racing track.
   - **Cars**: Add two cars (use rectangles or imported car images for visuals).
   - **Traffic Light**: Add an oval or a traffic light image.

---

### **2. Set Up the Road**
1. Use the **Line** or **Polyline** element to draw a straight road on the canvas.
2. Add labels or decorations to make the road look visually appealing.

---

### **3. Add Cars**
1. Place two **Rectangle** shapes (or car images) on the road to represent the cars. Name them `car1` and `car2`.
2. Add a **Variable** to each car to store their current speed. For example:
   - Name: `speedCar1` and `speedCar2`
   - Type: `double`
3. Add another **Variable** for each car to track their position:
   - Name: `positionCar1` and `positionCar2`
   - Type: `double`

---

### **4. Add Traffic Light Logic**
1. Add a **Boolean Variable** named `isGreen` to represent the traffic light state. Set its default value to `false`.
2. Add a **Button** or a **Statechart** to toggle `isGreen` to `true` when the race starts.

---

### **5. Create Movement Logic**
1. Use an **Event** or a **Statechart** to move the cars on the road. For example:
   - Add an **Event** named `updatePositions` with a **Cyclic trigger** (e.g., every 0.1 seconds).
   - In the event's **Action** section:
     ```java
     if (isGreen) {
         positionCar1 += speedCar1;
         positionCar2 += speedCar2;
         
         // Update car positions visually
         car1.setX(positionCar1);
         car2.setX(positionCar2);
         
         // Check for race completion
         if (positionCar1 >= roadLength || positionCar2 >= roadLength) {
             stopRace();
         }
     }
     ```

2. Define the `stopRace()` function:
   ```java
   void stopRace() {
       isGreen = false;
       // Determine the winner
       String winner = (positionCar1 >= roadLength) ? "Car 1" : "Car 2";
       traceln("The winner is: " + winner);
       // Reset positions for the next race
       resetRace();
   }
   ```

3. Define the `resetRace()` function:
   ```java
   void resetRace() {
       positionCar1 = 0;
       positionCar2 = 0;
       car1.setX(positionCar1);
       car2.setX(positionCar2);
       
       // Randomize speeds
       speedCar1 = uniform(10, 20); // Random speed for car1
       speedCar2 = uniform(10, 20); // Random speed for car2
   }
   ```

---

### **6. Run the Simulation**
1. In the **Experiment** section, create a **Simulation Experiment**.
2. Initialize the positions and randomize the speeds in the **Main** agent's **On startup** section:
   ```java
   resetRace();
   ```
3. Set the traffic light to green to start the race:
   ```java
   isGreen = true;
   ```

---

### **7. Run the Cars 3 Times**
1. Add a **Counter** variable `raceCount` initialized to `0`.
2. Update the `stopRace()` function to increment the race count:
   ```java
   raceCount++;
   if (raceCount < 3) {
       resetRace();
       isGreen = true; // Start next race
   } else {
       traceln("All races completed.");
   }
   ```

---

This setup ensures the cars run 3 races, each time with random speeds, and displays the winner of each race in the console. Let me know if you need more help! 🚗🚦
