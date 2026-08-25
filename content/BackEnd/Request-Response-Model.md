---
title: Request Response Model
---

> [!Note]
> you see this everywhere
> but Simple, Classic

- Client **makes a request**
- Server **parse** the **request**(tries to give it meaning)
  - **Parse** means this is where it start and this is where it ends
  - **Serialization** changing the content(request) to something I can understand
- Server *process* the request
- Server *sends* a response
- Client *parse* the response and consumes it.

## What is a request ?

Since the backend and the frontend(client) have to agree what is it.
Its not just send one thing and end it there it's continuous stream of data
so you have to understand where the data start and ends. This is **parsing**.

Also What is the language of the request is is

- XML
- JSON
- binary

## Where can I find this model ?

Sort answer is **like everywhere**

- Web
- HTTP
- DNS
- [[SSH]]
- ls (list directories)
- remote procedure call
(the abstraction of taking request to execute a function to a remote server)
- SQL and Database
  - you send query to the database the database process your SQL code
  and give you the response
- [[API]] REST/SOAP/GraphQl(created by META tries not to be chatty)

## What is Anatomy of Request/Response model

A request is defined by both the **client** and **server**
Request is defined by the protocol(where it start and end) and
by the message format(is this XML, JSON or other)

> [!Example]
> If you send an Image you can **send it as one file** or you can **send
> it as a bunch of files**  
> If you send it as one if internet is down for one second your whole Image
> is lost so it's not ==resumable==  
> But if you send it in chunk you only have to send the chunk you haven't
> send already so you can resume.

## What is the *downside* of this model?

In  Notification service this model wouldn't work why?

- because the client has to make a request but in notification service
the client doesn't know when the notification comes
- the only way to make request/response method work is when the client
says **does the notification arrived?** a bunch of time until it gets
the response saying the notification is arrived here is it. Since you don't know
if the notification have arrived you are going to get a bunch of empty response
and this is very bad design.

## Demo

Code time

```zsh
curl --trace out.txt http://google.com
```

This command do is make get request to google.com and `--trace`
make it so that we can see everything that it do in the middle
of the request and puts it in `out.txt`

Next pattern [[Synchronous Vs Asynchronous]]
