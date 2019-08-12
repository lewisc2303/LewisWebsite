+++
title =  "Multithreading in Scala"
date = 2019-08-11T22:18:22+02:00
tags = []
featured_image = ""
description = ""
+++

# Multi-Threading in Scala

I am continuing the Udemy 'Rock the JVM' advanced Scala course and so this Blog will cover threads and how to use them on the JVM.

### What is a Thread?

Wikipedia says that "a thread of execution is the smallest sequence of programmed instructions that can be managed independently" 

So a JVM thread is essentially a space where code execution can occur and each thread has its own stack. These threads are then mapped to the OS threads to execute the computation.

### The Thread class

You can instantiate a Thread class like any other class in Java/Scala which takes a Runnable class with a run method.

However threads are unpredictable when used without caution as you cannot predict which thread will be run first or for how long due to the JVM set up and the fact that it shares OS threads with other things happening on your computer. Therefore the `helloThread.start()` and `goodbyeThread.start()` will produce the `Hello`s and `Goodbye`s in an unpredictable order.

```
object Threads extends App  {
  //thread instance
  val thread = new Thread(new Runnable {
    override def run(): Unit = println("running thread")
  })

  //initialise the run method on the thread
  thread.start()

  //blocks until a thread finishes running
  thread.join()

  //different runs make different result due to thread scheduling
  val helloThread = new Thread( () => (1 to 5).foreach(_ => println("hello")))
  val goodbyeThread = new Thread( () => (1 to 5).foreach(_ => println("Goodbye")))

  helloThread.start()
  goodbyeThread.start()
}
```

### Pools

Due to threads being computation heavy to start up, pools of thread are often used keep stationary amount of threads available for use and re-use.

### The race condition

A race condtion occurs when the order of execution using shared state is not performed in the appropriate order and causes weird results and errors.

A way around this is to use the `.syncronized()` method on an Object. This locks the object from being used by any other thread whilst it is being used in a thread execution.

This is the reason why referential transparency and immutability should be strived for when concurrent programming.

# The Producer and Consumer Pattern

This pattern is a way of guarenteeing thread execution to be be ordered despite the natural unordered nature of threads.

### Wait and Notify

whilst an object is in a syncronized state and there is a lock on the object's monitor and you can use the follow methods to control the lock:

- `.wait()` : Causes the current thread to wait until another thread invokes the `.notify()` method.

- `.notify()` : Wakes up all threads that are waiting on this object's monitor. And then the remaining threads compete in a usual manner for execution.

### Example

The example below shows the producer and consumer model with a buffer in between to queue and dequeue computation.

The monitor lock is performed on the buffer object:

- When the buffer is empty, the consumer should wait
- When the buffer is full, the producer should wait
- In between, both can compete for the lock

```
object ProdCons extends App {

  def prodConsLargeBuffer() = {
    val buffer: mutable.Queue[Int] = new mutable.Queue[Int]
    val capacity = 3

    val consumer = new Thread(() => {
      val random = new Random()
      while(true){

        //syncronised lock on the buffer
        buffer.synchronized{
          if (buffer.isEmpty) {
            println("[Consumer] buffer empty, waiting...")
            //buffer waits if empty
            buffer.wait()
          }
          val x = buffer.dequeue()
          println("[Consumer] consumed " + x )

          //notifies producer that there is empty space in buffer
          buffer.notify()
        }
        //to simulate random execution time, sleep for random time
        Thread.sleep(random.nextInt(500))
      }
    })

    val producer = new Thread(() => {
      val random = new Random()
      var i = 0

      while(true) {
        //syncronised lock on the buffer
        buffer.synchronized {
          if (buffer.size == capacity) {
            println("[Producer] Buffer is full, waiting...")
            //buffer waits if full
            buffer.wait()
          }

          //when atleast one empty space in buffer
          println ("[Producer] produciing " + i)
          buffer.enqueue(i)

          //notifies consumer that there is atleast one value in the buffer
          buffer.notify()

          i += 1
        }
        //to simulate random execution time, sleep for random time
        Thread.sleep(random.nextInt(500))
      }
    })

    //start the threads
    consumer.start()
    producer.start()
  }

  prodConsLargeBuffer()

}
```

# References

- https://rockthejvm.com/
- http://blog.jamesdbloom.com/JVMInternals.html#jvm_system_threads