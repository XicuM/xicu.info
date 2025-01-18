---
title: "discord-bot"
date: 2024-11-03T00:06:49+02:00
hideMeta: true
ShowBreadCrumbs: true
comments: true
draft: false
tags: ["Python"]
github: https://github.com/XicuM/discord-bot
icon: "/projects/discord-bot/bot.png"
cover:
    image: "/projects/discord-bot/revolutions.jpg"
---

**discord-bot** is a simple Discord bot designed to gamify the server of *La Caverna Ecléctica*. The bot responds to various commands and acts based on the channel where the user is located.

In response to the Covid-19 crisis, I created *La Caverna Ecléctica* in late 2020 as a means to communicate with my friends and foster ideas and creativity among them, thus creating a fun and modern online community. With this goal in mind, different activities are organized on the Discord server, including:

- The **weekly program** (:warning: INTERRUPTED): A weekly program of up to 4 participants discussing various topics. Members can sign up for the participant list using a bot command.

- The **workroom**: A virtual space where members connect to keep each other company while working on their personal projects. It is inspired by the workroom created by Jaime Altozano on his Discord server. As time passes in the room, the bot awards points to the members and assigns roles based on their activity:
  - **nini** (not working not studying): less than 1 hour.
  - **novice**: between 1 and 2 hours.
  - **initiated**: between 2 and 6 hours.
  - **padawan**: between 6 and 24 hours.
  - **entrepreneur**: between 24 and 120 hours.
  - **businessman**: between 120 and 720 hours.
  - **magnate**: between 720 and 5040 hours.
  - **life master**: more than 5040 hours.

In addition to assisting members in the weekly program and the workroom, the bot also sends a welcome message to new members.

# Server Structure

The channel structure of the server is as follows:

## ℹ INFORMATION

### #general
Here general information and announcements about the server are shared. Only administrators and the bot can post in this channel.
**Available Commands**:
- `!act`: Updates the general description of the server.

## 🗨 WEEKLY PROGRAM

### #participate
In this channel, members can manage their participation in the weekly program.
**Available Commands**:
- `!help`: Shows the list of available commands.
- `!unirme`: Adds the user to the participant list for the weekly program.
- `!cancel`: Removes the user from the participant list.
- `!fecha`: Changes the date of the weekly program.
- `!clear`: Clears the participant list.

### #chat
This is the text channel used during the weekly program.
**Available Commands**:
- `!help`: Shows the list of available commands.
- `!preg -add <topic> <preg>`: Adds a question to the list of questions for a topic.
- `!preg <topic>`: Shows a random question from a topic in the list. With the topic `random`, a random question from any topic is displayed.
- `!enc -add <topic> <enc>`: Adds a survey to the list of surveys for a topic.
- `!enc <topic>`: Shows a random survey from the list. With the topic `random`, a random survey from any topic is displayed.

### 🔈on air
This is the voice channel used during the weekly program.

## 🖊 WORKROOM

### #notes
This is the text channel where users can leave notes to remember important things. Users can also request the number of hours they have spent in the workroom.
**Available Commands**:
- `!help`: Shows the list of available commands.
- `!horas`: Shows the total hours the user has spent in the workroom, as well as the rank they have been assigned.

### 🔈meeting
This is the voice channel used during the workroom.

## ⚙ ADMIN

### #ideas
In this channel, administrators can share ideas and suggestions for improving the server.

### #direct
In this channel, administrators can send direct messages to server members as if they were sent by the bot.
**Available Commands**:
- `!dm <user> <message>`: Sends a direct message to a user.

### #testbench
This channel is specifically for bot testing.
**Available Commands**:
- `!clear`: Clears messages from the channel.