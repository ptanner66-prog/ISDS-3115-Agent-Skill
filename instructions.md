# ISDS 3100: Information Systems Foundations
Fall 2026

**AI Lab: Vibe Coding and Agent Skill development**

| Department | Contact |
| :--- | :--- |
| **E.J OURSO COLLEGE OF BUSINESS**<br>SDEIS DEPARTMENT<br>Nicholson Extension<br>Baton Rouge, LA 70803 | **GABRIELE PICCOLI, PH.D.**<br>2219 Business Education Complex<br>Tel: +1 (225) 578-8184<br>gpiccoli@lsu.edu |

---

The goal of this semester project, to be completed with a pair-programming approach, is to practice what we learn in class. Specifically, the project focuses on the Generative AI portion of the course. We will practice vibe coding, and we will learn about (and create) agent skills. 

If you are wondering why, as a future manager, you should be learning to vibe code and to create agent skills, here is some food for thought:
* You may never write software for a living, but you will increasingly **direct** systems that do work for you. 
* Vibe coding and building agent skills are small, concrete examples of the core managerial move in the age of GenAI. 
* You must be able to clearly specify what a capable system should do, encode that specification so it runs consistently, and judge whether the output is achieving the expected levels of performance. 

You are the navigator. The AI can produce the code or automate the work, but you must decide what **performance** and **results** must be. That judgment is the part that doesn’t get automated. The more you practice, the better you become at it. These are frontier skills for a manager. Now is your time to develop them.

## General requirements and expectations
The two separate projects described here are independent. For each one you will be working in teams of two, but you will be able to change your partner once the vibe coding project is complete. 

> [!IMPORTANT]
> It is expected that you will act as a professional, reliable partner to your teammates. If your teammate on the vibe coding project does not share your same commitment to quality work, professionalism or learning, you should select a new teammate for the second project. 

## Pair programming
In this project you choose a collaborator and you work as paired programmers. Pair programming is an agile software development technique (see Chapter 10 of your book), where two programmers work together at a single workstation to complete a coding task (e.g., to vibe code a website). 

* **Driver Role:** One of the two developers takes the driver role and writes the code. In a vibe coding environment, the driver is not actually writing the code but instead prompting the generative AI system that writes the code. 
* **Navigator Role:** The other developer reviews the code as it is being typed and thinks at a higher level about the project, spotting the potential for bugs, architectural challenges, and new features.

## Calendar
> [!WARNING]
> All work is due on the day of the deadline at 11:59:59 PM unless otherwise communicated. There is a **30% penalty per day** of delayed submission on all work. 

The updated list of key dates and deadlines for the semester is available on Moodle.

## Grading and evaluation
See syllabus for grading percentage of each element of the semester project. 
* For the **vibe coding project** each person is assigned the grade relative to their own website (i.e., grading is individual). 
* On the **agent skills project** the team produces one artifact (i.e., one agent skill) and shares the same grade. 

We assume equal contribution to the final deliverable. It is your responsibility to reach out to the instructor or GA early in the project if you believe that your teammate is not contributing adequately to the effort. 

---

## Agent skill design and deployment
The second project consists in creating one agent skill for Claude Code. Working with your teammate, you will ideate, design, build, test, and deploy a single working skill. As noted in the general requirements, you may keep your partner from the vibe coding project or select a new one for this project. The team produces one artifact and shares one grade. 

An agent skill packages a repeatable task so that an AI agent can perform it reliably and consistently, without being re-taught each time (see Agent Skill Primer). So, this is an exercise in automating expertise with Generative AI. Building a skill is a design task as much as a coding task and minimal coding ability is required. However, it pays to have a clear understanding of computing concepts and you, as an IS professional, are best positioned to become a great agent skill writer.

### Requirements
You have free choice of topic. Your skill must be genuinely useful and appropriately scoped. It does not have to be a business or work skill. But it must help with a task you (or someone else) would normally have to repeatedly perform manually. A solid skill for this project is: 

* **a) repeatable:** it automates a task someone would do more than once, not a one-time request. Formatting *any meeting transcript* into structured minutes is a good example. Summarizing *one specific article* is a bad example; 
* **b) useful to a defined user:** it must be able to name a specific person (myself) or role (the secretary of AITP) who benefits from the skill. You design for that person; 
* **c) appropriately scoped:** the skill does one thing well. A focused skill that reliably does a single job beats an ambitious one that half-does five. When in doubt, narrow it. Formatting *any meeting transcript* into structured minutes - good example. Being an *office assistant* to help with secretarial tasks - bad example.

### Deliverable
Your deliverable is a working agent skill, installed and tested in Claude Code, that meets the following minimum requirements:
*   A **well-formed SKILL.md** with valid frontmatter — a clear name and, most importantly, a precise description that tells Claude *when* to use the skill.
*   **Structured instructions** in the body that lay out, step by step, how the task should be performed. You must test the skill and ensure it performs consistently and doesn’t depend on the user prompt.
*   **One or more supporting resources** bundled with the skill (for example, an example output, a template, a reference file, or a short script).
*   **Demonstrated reliability** so that when we run the skill you provide it triggers correctly and produces consistent, correct results across at least two separate test runs with different inputs.

### Suggested workflow
The following is a suggested progression in the creation of the skill.
1. Ideate with your teammate and write one sentence describing exactly what your skill does and for whom.
2. Create the skill folder and SKILL.md (see Agent Skill Primer).
3. Draft the triggering description, then the step-by-step instructions.
4. Add your supporting resource (template, example, or script).
5. Install it, then test it by triggering it with real inputs. Watch what breaks.
6. Iterate, tighten the description and instructions until it works reliably across at least two different inputs.

---

## Agent Skill Primer
An agent skill is a packaged set of instructions that “teaches”[^1] an AI agent how to do a specific, repeatable task well, so it can do that task reliably every time, without being re-taught. 

Think of it as an instruction card you write once and hand to a very capable but literal assistant – one with limited ability to judge and fill in the blanks of what you want. The power of a skill, versus a one-shot prompt, is that instead of re-explaining “here’s how I like meeting minutes formatted” every single time, you create the skill once, and the agent reaches for it whenever minutes are needed. This is the defining characteristic of an agent skill. 

Whereas a prompt is a one-time instruction that works for that moment, given the current state of the context window, a skill differs in three important ways:
*   **Reusable.** You write the expertise once; it’s always available to the agent.
*   **Self-triggering.** The agent recognizes when the skill applies and uses it on its own.
*   **Packaged.** It can carry supporting materials with it so the agent has everything it needs.

> [!NOTE]
> In short: a prompt is *asking* the AI agent to do something once in a chat. A skill is *equipping* the AI agent with the capability to do something repeatedly and permanently. 

Technically, a skill is simply instantiated as a folder on your computer. Inside it, one file does the essential work, and everything else is optional support. The key element is the required `SKILL.md` file.[^2] This is the heart of the skill — a plain text file with two parts: 
* **a) the frontmatter:** a few lines at the very top, fenced by a three-dash marker (i.e., `---`), that carry a *name* and a *description*. The description is the most important thing you write, because it tells the agent when to use the skill. A vague description means the skill never triggers, or triggers at the wrong time. A precise one makes it fire exactly when it should.
* **b) the body:** written in plain Markdown below the frontmatter it is the step-by-step explanation of how the agent should complete the tasks and the instructions it must follow. This is written in English, not using code, as if you were talking to a smart new collaborator. A clear, ordered, and specific explanation of what a good result looks like is key.

Supporting files are optional for the skill, but you are expected to use them in this project (see project description). Supporting files are a powerful addition to the SKILL.md file because they give the agent access to extra materials. They are usually organized into folders called:
* *references/* (documents the agent can consult)
* *assets/* (templates or example outputs)
* *scripts/* (small programs the agent can run)

These keep the main instructions focused while giving the skill the instruments it needs to do the job well.

Skills in Claude Code live as folders on your filesystem, in one of two places:
*   **Personal:** These skills are stored in `~/.claude/skills/` and are available to you across all your projects.
*   **Project-specific:** These skills are stored in `.claude/skills/` inside a particular project folder and will be bundled with that project.

Once a skill is in place, there are two ways it gets used:
*   **Automatically:** Claude reads the description of each available skill and, when your request matches, uses the relevant skill on its own. This is why the description matters so much, it’s an automatic trigger.
*   **On demand:** You can invoke a skill directly by typing `/` followed by its name. This way the skill is “force called” into action.

You don’t upload anything to a server or fill out a form. A skill is just files in a folder that the agent knows how to read. The quality of the agent skill you develop depends on the three characteristics described in the project requirements. The skill must be a) repeatable; b) useful to a defined user; c) appropriately scoped.

To learn more about agent skills you can visit:
*   Anthropic’s own description: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
*   The Agentic Loop newsletter: https://www.pulsemcp.com/newsletter

---
[^1]: You should resist anthropomorphizing Generative AI systems and models, using terms like “think,” “understand,” and “teach.” Quoting the terms is a simple way to remind the reader (and yourself) that a computer system is not human. For simplicity we will not quote anthropomorphized terminology here. 
[^2]: As you enter the world of agent skills, and agentic AI in general, you need to become familiar with the *.md file type. An .md file uses Markdown syntax to create formatted text in a simple, plain-text format. It relies on easy symbols and is highly readable to humans while remaining lightweight and easy for GenAI models to ingest and parse. Markdown files are best viewed in an editor, such as Sublime Text, rather than word processors such as MS Word.
