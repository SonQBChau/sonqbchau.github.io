---
title: The Pragmatic Programmer
tags: [book, summary]
published: 'October 26 2023'
layout: ../../layouts/BlogLayout.astro
---

*Disclaimer: This is not a book review, but rather a summary of the key takeaways from the book.*

### Provide Options, Don’t Make Lame Excuses

It is up to you to provide solutions, not excuses. Before you tell something can’t be done, stop and listen to yourself. How’s it going to sound to your boss?

### Don’t Leave "Broken Windows" Unrepaired

Don't do: "All the rest of this code is crap, I’ll just follow suit."

### Be a Catalyst for Change

Work out what you can reasonably ask for. Develop it well. Once you’ve got it, show people, and let them marvel.

### Remember the Big Picture

Constantly review what’s happening around you, not just what you personally are doing.

### Independence or Decoupling

Easy to design, build, test, and extend

### Minimize Coupling

Systems (or codes) with many unnecessary dependencies are very hard to maintain and tend to be highly unstable. “Simple” changes to one module that propagate through unrelated modules in the system.

### DRY — Don’t Repeat Yourself

Keep the low-level knowledge in the code and reserve the comments for other, high-level explanations. Foster an environment where it’s easier to find and reuse existing stuff than to write it yourself.

### Write Shy Code

Modules that don’t reveal anything unnecessary to other modules and that don’t rely on other modules’ implementations. What does it take to build and link a unit test?

### Write "Lazy" Code

Be strict in what you will accept and promise as little as possible in return.

### If It Can’t Happen, Use Assertions to Ensure That It Won’t

Your first line of defense is checking for any possible error, and your second is using assertions to try to detect those you’ve missed.

### Dynamic Configuration

Use metadata to describe configuration options for: the choice of algorithms, database products, middleware technology, and user-interface style, tuning parameters, user preferences, the installation directory, and so on.

### Estimating Project Schedules

- Check requirements
- Analyze risk
- Design, implement, integrate
- Validate with the users
You almost always get better results if you say: “I’ll get back to you” and spend some time going through the steps above.

### Prototype to Learn

Its value lies not in the code produced, but in the lessons learned.

### Choose an Editor

Know it thoroughly and use it for all editing tasks.

### Use the Power of Command Shells

Play around with your command shell, and you’ll be surprised at how much more productive it makes you.

### Automation

Use script `make` or `cron` job to avoid mistakes for repeating tasks.

### What to Test

- Unit testing
- Integration testing
- Validation and verification
- Resource exhaustion, errors, and recovery
- Performance testing
- Usability testing

### Make Quality a Requirements Issue

Give your users something to play with early, their feedback will often lead you to a better eventual solution.

### Gently Exceed Your Users’ Expectations

Give them that little bit more (but don't overdo it) than they were expecting. Listen to your users as the project progresses for clues about what features would really delight them. Some things you can add relatively easily that look good to the average user include:

- Balloon or ToolTip help
- Keyboard shortcuts
- A quick reference guide as a supplement to the user’s manual
- Colorization
- Log file analyzers
- Automated installation
- Tools for checking the integrity of the system
- The ability to run multiple versions of the system for training
- A splash screen customized for their organization

### Communicate

Helps teams communicate as one: generate a brand. When you start a project, come up with a name for it.

### Invest Regularly in Your Knowledge Portfolio

The more different things you know, the more valuable you are.

- Learn a new language: Different languages solve the same problems in different ways. By learning several different approaches, you can help broaden your thinking.
- Read a technical book.
- Read non-technical books, too.
- Take classes.
- Participate in tech groups: find out what people are working on outside of your company.
- Experiment with different environments: play with Unix or Windows, terminal or IDE

### Sign Your Work

Written by a real professional. A Pragmatic Programmer.
