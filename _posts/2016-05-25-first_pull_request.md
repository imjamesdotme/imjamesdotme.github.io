---
layout: post
title:  "First Pull Request"
date:   2016-05-25 22:30:00
author: James L
categories: git github
image: /assets/git-github-header.png
imageAlt: I'm James - First Pull Request
---

Up until recently, the only code I'd been dealing with on GitHub was my own. This has its benefits (git is an excellent & must have tool) but at the same time doesn't allow for the real utilisation of git & GitHub - _collaboration_. 

While investigating to see if someone had logged a bug on GitHub for a [Free Code Camp](https://www.freecodecamp.com) algorithm challenge, I stumbled upon an open [issue](https://github.com/FreeCodeCamp/FreeCodeCamp/issues/8524) that caught my interest.

As you can see from the link above, the issue was raised and the user goes as far to mention a solution to fix the issue. My first call was to see the defect for myself & explore the suggestion, which quickly turned out not to be the solution to the problem.

Even though my [pull request](https://github.com/FreeCodeCamp/FreeCodeCamp/pull/8530) was only a few lines of code, I learn a lot through this process & was also able to exercise my skill set.

**Debugging** - I initally viewed the live issue on my own handset (Nexus 6P) so I could see the issue for myself then moved across to Chrome's Dev Tools to debug the issue via the emulator.

**Communication** - Unlike during working hours where I frequently have to communicate issues, solutions & whatever else to people I know, when contributing to an Open Source project (or any other project where you don't know people) the ability to communicate clearly is hugely important. You _must_ ensure you message reaches other parties so that's its clear & easy for them to understand exactly what your explaining. This is a skill that can certainly take time to hone but as I've learnt, it's one of the most important tools in the box.

**Documentation** - Be able to read and follow instructions (this is every developers job, right?). Free Code Camp has a full set of [documentation](https://github.com/FreeCodeCamp/FreeCodeCamp/blob/staging/CONTRIBUTING.md) for contributing.

**Git & GitHub** - As previously mentioned, before this pull request I'd only been using git & GitHub for my own code. Being able to put what I've learnt/read/experimented with into practise was a great moment for me. From creating my first fork, right back to submitting the pull request, there was quiet a buzz to the whole process.

**Testing** - In my current job role, I help with  Quality Assurance on a regular basis, so this was no stranger. I tested the fix via Chrome's built in emulator with as many devices as I could (unfortunately I had no other devices to test against at the time). I then tested locally using their pre-configured tests run via an npm command (these tests are later run by Travis CI when you submit the pull request) & finally the code was reviewed by a member of the repository before being merged.

Even though this contributions was small, the learnings & gains were highly valuable and I encourage anyone who hasn't attempted a pull request to give it a shot! My plan for the future is to try and contribute more to the Free Code Camp repository as I progress through the rest of the course.