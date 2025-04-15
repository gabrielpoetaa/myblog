---
layout: post
title: "Ports, Tunnels, and Databases: Making Supabase Public with Docker on WSL"
feature_image: /assets/images/posts/2025-04-14-Ports_Containers_and_conflicts/ngrok.png
categories: misc
---

I’ve been setting up a local environment to test a Retrieval-Augmented Generation (RAG) application, and I wanted to use PostgreSQL through Supabase to store chat history and eventually build a knowledge base for my RAG. Supabase seemed like the perfect open-source fit for testing purposes—it bundles everything I needed and more. But installing it locally ended up being trickier than I expected.

I already had WSL2 running Ubuntu on my local machine, with Docker set up and working smoothly. Using the docker-compose file provided by Supabase, I spun everything up without a hitch. Supabase was running locally in no time—but things got a bit tricky when I tried to make the database accessible to my RAG app, which is hosted in the cloud. To test this connection as fast as I could, I used <a href="https://ngrok.com/" target="_blank" style="text-decoration:none; color:inherit; font-weight:bold;">ngrok</a> to tunnel the PostgreSQL port from my local machine to the internet—this way, my cloud-hosted RAG app could reach the database directly for testing - That’s when I ran into a classic Docker issue:

`Bind for 0.0.0.0:5432 failed: port is already allocated`

At first, I couldn’t figure out why this was happening. I was inside WSL, using isolated containers—so why was port 5432 already taken?

### **Digging into the problem**

First thing I did was check which process was using that port. On Windows, I ran:

`netstat -ano | findstr :5432`

That showed me the PID, which I then inspected using:

`tasklist /FI "PID eq 21548"`
<br>
<br>
<br>
And there it was: `com.docker.backend.exe`. Turns out Docker Desktop itself—running on Windows—was already using port 5432, likely from a previous setup or container I had forgotten about.

### **Understanding how port mapping works in WSL**

This is when it clicked: even though I was running docker-compose from inside WSL, the Docker engine was still running on Windows, via Docker Desktop. So when a container exposes a port (like 5432), Docker tries to bind that port on the host machine—the Windows environment.

If the port is already taken on the host, Docker can’t bind to it, and the container fails to start.

That means: running Docker in WSL doesn't isolate you from host-level port conflicts.

### **The fix: explicit port mapping**

The solution was simple but required a good understanding of what was going on. I updated my docker-compose.yml like this:

`ports:`<br>
`"5433:5432"`

Now the container still listens on port 5432 internally, but exposes it as 5433 on the host. This avoids the conflict and still allows external tools (like ngrok or any external app) to connect to PostgreSQL without issues.

### **Testing with ngrok**

With the new port mapping, I tested the external access:

`ngrok tcp 5433`

<!--
![Image of a computer around the year of 1960](assets/images/posts/2025-04-14-Ports_Containers_and_conflicts/ngrok.png){: style="display: block; margin: 0 auto; height: 300px;"} -->
<br>
<br>

![Image of a computer around the year of 1960]({{site.url}}/assets/images/posts/2025-04-14-Ports_Containers_and_conflicts/ngrok.png){: style="display: block; margin: 0 auto;"}

<br>
<br>

This time, it worked perfectly. I could connect to the local PostgreSQL database from another machine using the ngrok host. Connection successful, RAG tests running smoothly.
<br>
<br>
<br>
This little hiccup—a simple port conflict—taught me more than I expected. It pushed me to better understand how Docker interacts with WSL and the host OS, how port mapping works in docker-compose, and how to troubleshoot process conflicts in Windows. These are the types of lessons you don’t fully grasp until you go through the pain of debugging them yourself. And the best part? I now feel more confident setting up container-based environments, both for development and production.
