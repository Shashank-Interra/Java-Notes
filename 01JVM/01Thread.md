Sure! Here's a **complete, clean set of notes on Threads in Java** suitable for an `.md` file:

---

# **Java Threads Notes**

## **1. What is a Thread?**

* A **thread** is the **smallest unit of execution** in a program.
* Each **process** can have multiple threads running concurrently.
* Threads share the **heap memory** but have their own **stack, program counter, and local variables**.

**Analogy:**

* A program = factory
* Thread = worker in the factory
* Workers share factory resources (heap) but have their own tools (stack, local variables)

---

## **2. Multithreading**

* **Multithreading** = running multiple threads **concurrently** in a program.
* Purpose: **Better CPU utilization and concurrent execution.**
* Types of execution:

  * **Parallel** → multiple threads run on multiple CPU cores simultaneously.
  * **Interleaved** → single core executes threads via **context switching**.

**Advantages:**

* Faster execution of independent tasks
* Better CPU/resource utilization
* Responsiveness in GUI applications

**Disadvantages:**

* Thread synchronization issues (race conditions, deadlocks)
* Increased complexity

---

## **3. Thread Life Cycle**

```
New -> Runnable -> Running -> Waiting/Blocked -> Terminated
```

* **New:** Thread object created but not started.
* **Runnable:** Thread ready to run, waiting for CPU allocation.
* **Running:** Thread executing its task.
* **Waiting/Blocked:** Thread paused, waiting for resource or signal.
* **Terminated:** Thread finished execution.

---

## **4. Creating Threads in Java**

**Method 1: Extending `Thread`**

```java
class MyThread extends Thread {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + " -> " + i);
        }
    }
}

public class Demo {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start(); // Starts the thread
        MyThread t2 = new MyThread();
        t2.start();
    }
}
```

**Method 2: Implementing `Runnable`**

```java
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + " -> " + i);
        }
    }
}

public class Demo {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        t1.start();
        Thread t2 = new Thread(new MyRunnable());
        t2.start();
    }
}
```

---

## **5. Common Thread Methods**

| Method            | Description                               |
| ----------------- | ----------------------------------------- |
| `start()`         | Starts a thread, calls `run()` internally |
| `run()`           | Contains the thread's execution code      |
| `sleep(ms)`       | Pauses thread for specified milliseconds  |
| `join()`          | Waits for another thread to finish        |
| `yield()`         | Temporarily gives CPU to other threads    |
| `getName()`       | Returns thread name                       |
| `setName(String)` | Sets thread name                          |
| `isAlive()`       | Checks if thread is running               |

---

## **6. Thread Synchronization**

* Multiple threads accessing **shared resources** may cause **race conditions**.
* **`synchronized`** keyword ensures only one thread can access a method/block at a time.

**Example:**

```java
class Counter {
    private int count = 0;

    public synchronized void increment() { // Only one thread at a time
        count++;
    }

    public int getCount() {
        return count;
    }
}

public class Demo {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();
        Thread t1 = new Thread(() -> { for(int i=0;i<1000;i++) counter.increment(); });
        Thread t2 = new Thread(() -> { for(int i=0;i<1000;i++) counter.increment(); });

        t1.start(); t2.start();
        t1.join(); t2.join();

        System.out.println("Final count: " + counter.getCount());
    }
}
```

---

## **7. Summary**

* **Thread** = smallest unit of execution.
* **Multithreading** = multiple threads executing concurrently.
* Threads **share heap memory** but have their own stack and PC.
* Threads can be created by:

  * **Extending `Thread`**
  * **Implementing `Runnable`**
* **Synchronization** is essential when multiple threads access shared resources.

---


