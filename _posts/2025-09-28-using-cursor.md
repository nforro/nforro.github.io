---
layout: post
title: "My experience using Cursor for development"
permalink: /using-cursor
category: AI
tags:
  - agentic AI
  - vibe coding
  - Cursor
---

Cursor is one of the AI-enhanced text editors that are getting a lot of attention these days.
After very positive reviews and recommendations from colleagues I decided to give it
a try and start using it regularly if it proves beneficial.

I'm not a fan of IDEs, I've been happily using plain Vim in a terminal emulator for decades.
Cursor is based on VSCode, so it does have a Vim editing mode, but the UI still feels bloated
and overwhelming and it would take me a long while to get used to it. But I quickly realized
I don't have to be using it as an IDE/editor, I can focus on the chat panel and use the editor
part just for marking context and reviewing and confirming changes. This proved to be quite usable.

Within our team we were researching and deciding which AI framework to use for our agentic AI project,
and I needed to come up with a proof of concept of an AI agent implemented in the BeeAI framework.
I thought it would be a great first task for Cursor. I added the official documentation and GitHub
project as resources, wrote a brief prompt and watched the magic happen.
The results were underwhelming. It seemed to ignore the provided resources and generated code
based on one of the official code examples that didn't do what I wanted. After a couple of iterations
I realized it would be way faster to do it myself. And so I did.

I didn't write it off as a complete failure though. I realized that every agentic system needs
one important thing to be successful - verification. I didn't have BeeAI Framework and its dependencies
installed on my local machine - I run everything in a container, which Cursor was unable to do,
so it couldn't run and test the code it generated, and I think that was one of the reasons why
it performed so poorly.

I quickly found Cursor is perfect for one-off tasks - the kind where I would normally search
for inspiration on StackOverflow. For example, "I need to do this and that, what is the most Pythonic way
to do it?" Or, "I need to achieve this, but I can't think of an algorithm/design pattern off the top
of my head, what are the possibilities?" Sometimes the generated code has issues and doesn't really work,
but it is good enough to give me the right idea(s), and that's what counts.

For another bigger task I decided to take a different approach. I needed to implement some MCP tools
for Jira interaction. This time I didn't add any resources, I just instructed Cursor to get inspired
by already existing MCP tools for GitLab that I implemented a while ago. The results were much better
and it took just a bit of polishing to make the code production-ready.

Experimenting further, I have a feeling that actually ending up using the generated code is more of
an exception. Quite often I find it more time consuming trying to convince the model to adjust the code
to my liking than just taking over and doing it manually. That being said, I expect this to shift
in the future as models improve and I get better at prompting.

PS: I quite dislike the over-the-top politeness, often praising a solution that is in fact objectively worse
and just happens to satisfy a particular niche of mine. No, I am not "absolutely right" every time.

![Meme](/assets/img/meme_pf.jpg)
