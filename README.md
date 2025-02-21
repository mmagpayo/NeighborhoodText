# NeighborhoodText
An idea inspired by my neighborhood watch captain

# Overview
The idea is to create an easy way for a group of neighbors to have their own SMS group chat. My neighborhood watch captain collected the neighbor's phone numbers and had to create a new group chat everytime a new person wanted to join the chat. This was a problem because chat history would be lost and the new group chats would get confusing and cluttered. I wanted to find a way to create an SMS group chat where neighbors could join and leave the chat as needed. 

# Goals

My main goal is to practice and build a POC. 

A couple of sub goals:

### Non-programming stuff (mostly)
- Communication check. Write a well-communicated README that explains what I want to do, how I want to do it, and probably how I'm revising it along the way.
- Step out from VS Code and try out [Cursor](https://www.cursor.com/). I know it's not a huge leap, but I want to try a little AI help.
- That being said, try not to use too much AI. Cursor is trying to write this README for me and I need to keep fighting the urge to accept all the autocompletes.
- DevContainers. I really think the idea is novel and I hope it lends itself to simulating the production container as close as possible.
- Git check. How small are my commits? Too small? Too big? This one is probably too big already.
- Be realistic about how much I can actually do by myself. I can see myself managing a team to get this project done, so I'm using it as a reflection of how much I can do by myself with everything else going on in my daily life.

### Programming stuff
- Writing some Python. Trying out some of the newer features I didn't get to use in my last job. Getting more reps.
- Working with the Twilio API. I've never used an API for SMS messaging in the way that I have it in my mind. I think I can do it with Twilio, but I can already foresee some non-technical roadblocks (mainly the A2P 10DLC restrictions)
- Try out FastAPI. I've only worked with Django and Flask before.
- Get some reps with GitHub Actions
- Polish up my Docker/Kubernetes skills.

Let's see how it goes.

# How I'd like this to work
I think the flow should go as follows:
1. The neighborhood captain/chat owner creates a new group chat
    * A new phone number is provisioned for the Neighborhood Text
    * The captain invites neighbors to sign up to be part of the Neighborhood Text
2. A neighbor signs up to be part of the Neighborhood Text
    * The neighbor receives a text with a link to sign up
    * The neighbor clicks the link and is asked to enter their phone number, name, and address
    * The captain is notified of the new neighbor and either:
        * The neighbor's request is approved:
            * The neighbor's phone number is added to the Neighborhood Text
        * The neighbor's request is denied:
            * The neighbor is notified that they are not part of the Neighborhood Text
3. The captain and all other neighbors can now text each other

<br>

There probably needs to be some sort of admin panel or dashboard for things like:
* Seeing all the neighbors who are part of the Neighborhood Text
* Being able to add/remove neighbors from the Neighborhood Text
* There's probably a money component involved since we gotta pay Twilio for the number and messages
* Delegating more captains or assigning a new captain
* Basically RBAC :weary:

# Architecture
### Alpha
Some thoughts I'm jotting down here:
* NeighborhoodText service sits between a UI and the Twilio API
* It should be responsible for the sign up of the captain and the neighbors
* It should be responsible for provisioning a new phone number by interacting with the Twilio API
* Once the number is provisioned and neighbors are signed up, Twilio should handle the SMS stuff.
* Probably will need to store everything in a DB. Relational probably makes sense, I can see where I might want to use a KV store later on. Maybe the 10DLC as a key, value is a list of all the phone numbers belonging to the group?

> As I'm thinking about this more, my initial POC is probably building out this NeighborhoodText service exposing a REST API. As I'm not versed in building front-ends, I'll probably use AI to build it for me. I will probably just Dockerize it with a plain Docker file then move to a Docker Compose file as I see fit. 
