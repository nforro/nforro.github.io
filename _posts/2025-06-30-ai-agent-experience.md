---
layout: post
title: "Using an AI agent from Fedora packager perspective"
permalink: /ai-agent-experience
category: AI
tags:
  - agentic AI
  - Goose
  - packaging
  - Fedora
---

AI agent is a fancy name for a LLM that can use tools - it doesn’t just generate content, it acts.
Tools can be API calls, shell invocations or other software that let the agent observe and change
its environment to accomplish tasks. AI agents can recover from errors by trying alternative strategies
and refine their actions based on feedback.

I decided to experiment with [Goose](https://block.github.io/goose/) and use Google Gemini family of models.
Goose supports a decent number of LLM providers, but it is also possible to configure it to use self-hosted models.

I chose to run the agent in a throw-away Fedora-based container, with a persistent configuration
and working directory mounted inside. I'm not foolish enough to let it execute commands directly on my system.
While it is possible to run Goose in a manual approval mode and have it ask for confirmation before running
any command, I found it to be rather cumbersome, especially with less capable models that need multiple iterations
to perform a task successfully.

Speaking of models, there are huge differences between them. Generally, *flash* models are fast but less capable,
they need more specific prompts, more hints and it often takes them mutiple attempts to do the right thing.
On the other hand, *pro* models are slow, sometimes to the point of being unusable.

My biggest takeaway is to design prompts with the worst-performing models in mind, better models will benefit
from it as well. When designing the prompt, don't forget to set persona and introduce the environment:\
`You are a Fedora package maintainer working on a Fedora 42 system.`\
It may be good to set constraints - don't hesitate to explicitly prohibit some commands or behavior.
I had an agent modify a reproducer script in a way that it no longer triggered a bug - a valid solution
from a certain point of view, but clearly not what I was after. Once I let it know that the reproducer
script is constant and never to be modified, I got more useful outcome.

One issue I ran into, and this is probably Goose-specific and most likely fixable, once the agent manages to spawn
an interactive shell, for example using `mock --shell`, it hangs indefinitely. Usually, in an interactive
Goose environment, you can press *Ctrl+C* at any moment to interrupt the agent (and give it some feedback for example),
but that doesn't work when it hangs in this way.

Another issue I experienced was with nested quoting. The agent was trying to run a command with a quoted argument
in a shell in a mock chroot. To execute properly the command needed 3 levels of nested quoting, but not even
the best performing models were able to come up with a valid syntax. I had to instruct the agent to use temporary
script files to overcome this.

All things considered, I see a big potential in using AI agents for automating certain tasks. It's like automation
on steroids - instead of writing a script you craft a prompt that can cover much wider range of use cases.
Goose supports recipes - YAML files with instructions and prompts that can be parametrized, ideal for this purpose.
