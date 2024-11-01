---
title: Synchronous-Vs-Asynchronouns
---

> [!Question]
> Can I do work while waiting ?

So synchronous and Asynchronous came from the idea. Are the client and the
server in sync? But as a programmer we don't need(care) that if they are or not
we just care if I can do other work while I'm waiting for a request.

## Synchronous I/O

- Caller send a request and blocks
  - until the request is done calculating in the server and
  get answer the caller is blocked
  - the process is blocked
- Caller can't execute any code
- When the Receiver responds, the Caller unblocks

Context switching
is when a process is blocked they take it out of the processor
and take another process that is not blocked and execute on that.

> [!Example]
> Program as the OS to read a file  
> The programs tread is taken off the CPU  
> Read Complete the program can resume execution

But as you can see here the program asking the OS to read file shouldn't
be context switched and taken off because he is not the one doing the job
the OS is. He is there just waiting.

## Asynchronous I/O

Caller sends a request
Caller can work other things until it gets a response

> [!Question]
> How can it know when it's done?

There are two ways

- Check if the response is ready every time
  - while response == ready:
    - ask_receiver("is the response ready")
  - **node.js use this if it can**
- When it response is ready call this function(callback)
- Spin up a thread and let that thread do the job I'm asked to do.
  - As a consumer we would be thinking it is non blocking

  ```javascript
  doWork()
  readFile("test.txt",readFileFinished(file))
  doWork2()

  function readFileFinished(file){
  }
  ```

In Async and promises when the client give a request to compute the
backend immediately responds with "I here your request here is a job
Id you can move on doing other job" and then it puts the request in
a queue because the backend might be doing other jobs right now.

