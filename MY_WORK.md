# 📝 MY_WORK: Student Information, Development Log, Reflection & Answers

> This is the **only file** your instructor reads to grade Parts 3 and 4 (documentation and video). Everything you write here must be **in your own words**.

---

## 👤 Student Information

| Field | Your Answer |
|-------|-------------|
| **Full Name** | Abdulelah Abdullah Almalki |
| **Student ID** | 446050920 |
| **University Email** | 446050920@std.psau.edu.sa |
| **GitHub Username** | Abdulelah999 |
| **Repository Link** | https://github.com/Abdulelah999/OS-Assignment1-Starter-481 |
 
---

## 🎥 Video Link

**Video Link**: [ضع رابط الفيديو هنا بعد رفعه على اليوتيوب أو قوقل درايف وتأكيد أنه عام]

---

# Part A: Development Log

### Entry 1 - [October 5, 2026, 3:00 PM]
**What I did**: Forked the starter repository and initialized project settings.

**Details**:
- Forked `makopt/OS-Assignment1-Starter-481` to my GitHub account.
- Configured the student ID to `446050920` in `SchedulerSimulation.java`.
- Verified local compilation and successful execution.

**Challenges**: Needed to verify correct JDK version setup.

**Solution**: Configured the Java environment path properly.

**Time spent**: 30 minutes

---

### Entry 2 - [October 7, 2026, 4:15 PM]
**What I did**: Implemented Feature 1 (Process Priority).

**Details**:
- Added a random priority field (1-10) to the Process class.
- Updated ready queue messages to display process priority upon queue entry.

**Challenges**: Ensuring the scheduling queue order remained strictly FIFO as required.

**Solution**: Kept queue behavior as FIFO while only appending priority visualization.

**Time spent**: 45 minutes

---

### Entry 3 - [October 9, 2026, 5:30 PM]
**What I did**: Implemented Feature 2 (Context Switch Counter).

**Details**:
- Created a static context switch counter variable.
- Incremented the counter every time a new process starts execution and printed the total at termination.

**Challenges**: Avoiding double-counting during queue rotations.

**Solution**: Tied the increment strictly to the execution switch phase.

**Time spent**: 40 minutes

---

### Entry 4 - [October 11, 2026, 6:00 PM]
**What I did**: Implemented Feature 3 (Waiting Time Tracking and Summary Table).

**Details**:
- Used `System.currentTimeMillis()` to track start and completion times.
- Calculated waiting time and turnaround time accurately.
- Formatted and printed the final summary execution table.

**Challenges**: Resolving duplicate entries and formatting artifacts in the terminal table.

**Solution**: Applied a HashSet filter to process printing and ensured proper completion timestamping.

**Time spent**: 1 hour and 30 minutes

---

### Entry 5 - [October 13, 2026, 8:00 PM]
**What I did**: Final testing and verification of the entire simulation.

**Details**:
- Tested multiple simulation runs with unique student ID seeds.
- Verified terminal output alignment and accuracy of computed metrics.

**Challenges**: Ensuring clean output rendering across different terminal sizes.

**Solution**: Standardized spacing and column alignment in the summary printer.

**Time spent**: 30 minutes

---

## Development Log Summary
**Total time spent on assignment**: 4 hours
**Most challenging part**: Debugging the tabular output rendering and ensuring unique process rows.
**Most interesting learning**: Understanding how Java threads simulate CPU scheduling and time-slicing mechanics.
**What I would do differently next time**: Start documenting earlier during each coding session.

---

# Part B: Reflection

## Question 1: What did you learn about multithreading?
Through this assignment, I gained a practical understanding of how Java manages concurrent threads using `Runnable` and `Thread.start()`. I learned how the main thread coordinates execution using `Thread.join()` to ensure all processes complete before printing the summary. Simulating work delays with `Thread.sleep()` provided a clear visualization of CPU time slicing. It was fascinating to see how multiple processes share resources concurrently while maintaining independent states. Overall, this experience bridged the gap between theoretical operating system concepts and actual Java code implementation.

## Question 2: What was the most challenging part of this assignment?
The most challenging part of this assignment was debugging the tabular output formatting and ensuring that completion times were correctly tracked for every process. Initially, the table displayed duplicate entries or placeholder characters because processes were re-queued multiple times in the Round-Robin queue. Tracking down where the process map updated and making sure `setCompletionTime` triggered correctly required careful analysis of the scheduler loop. Overcoming this hurdle taught me the importance of inspecting state transitions step by step.

## Question 3: How did you overcome the challenges you faced?
I overcame these challenges by systematically debugging the code using targeted print statements to trace process execution flow and queue states. I also carefully re-read the assignment instructions and the `README.md` file to ensure my implementation matched the expected behavior. Testing the program after every small modification allowed me to isolate errors quickly and verify the fix. Furthermore, breaking down the logic into manageable pieces made complex scheduling mechanics much clearer.

## Question 4: How can you apply multithreading concepts in real-world applications?
Multithreading concepts are essential in modern software development, such as in web browsers where separate threads handle rendering, network requests, and user input simultaneously. In video games, threads manage background asset loading, physics calculations, and rendering loops without freezing the interface. Operating systems rely heavily on multithreading and CPU scheduling algorithms like Round-Robin to allocate processor time fairly among active applications. These real-world systems mirror the core principles of concurrency and scheduling that I implemented in this simulation.

---

# Part C: Technical Answers

## Question 1: Thread vs Process
A process represents an independent execution environment with its own memory space, whereas a thread is the smallest unit of execution within a process that shares memory with other threads. We used threads in this assignment because creating lightweight threads has much lower overhead and allows efficient communication compared to heavy separate processes. In `SchedulerSimulation.java`, this is demonstrated where each simulated `Process` object is executed by spawning a real Java thread using `new Thread(process)`.

## Question 2: Ready Queue Behavior
In Round-Robin scheduling, when a process cannot finish within its allotted time quantum, it is preempted, re-added to the back of the ready queue, and resumes later. For example, process `P8` required multiple quanta to finish, appearing multiple times in the ready queue output before its final completion. Re-queueing is crucial for fairness because it prevents long-running processes from monopolizing the

**Explanation of example:**
This output snippet shows that process `P8` used its 5000ms quantum but still had remaining burst time, so the scheduler automatically re-queued it at the back of the ready queue to wait for its next turn.

## Question 3: Thread Lifecycle
1. **New**: P1 enters this state when `new Thread(process)` is instantiated right before starting.
2. **Runnable**: P1 becomes runnable once `thread.start()` is called, making it eligible for CPU allocation.
3. **Running**: P1 enters the running state when the scheduler selects it to execute its quantum.
4. **Waiting**: P1 enters a waiting/sleeping state when `Thread.sleep()` simulates its execution progress.
5. **Terminated**: P1 reaches this state after completing its remaining burst time and finishing execution.

## Question 4: Real-World Applications

### Example 1 (operating-system level): Operating-System CPU Scheduler
**Description**: The OS kernel schedules active user applications across CPU cores using time quanta to ensure system responsiveness and fairness.
**Why Round-Robin works well here**: It prevents any single misbehaving program from freezing the entire operating system by giving every process equal time slices.

### Example 2: Multiplayer Video Game Server
**Description**: A game server manages dozens of connected player actions simultaneously by cycling through updates using time-sliced threads.
**Why Round-Robin works well here**: Round-Robin ensures that every player's input gets processed predictably and fairly without noticeable server lag.





CPU, ensuring all processes get equitable turn access.

Example from my output:
