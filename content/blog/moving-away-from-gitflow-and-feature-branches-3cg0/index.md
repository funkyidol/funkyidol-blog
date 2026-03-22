---
title: "Moving Away from Gitflow and Feature Branches"
date: 2025-07-17
summary: "Intro   As the title suggests, this post is a case study on how Gitflow and traditional..."
draft: false
tags: []
canonicalURL: "https://dev.to/funkyidol/moving-away-from-gitflow-and-feature-branches-3cg0"
---
## **Intro**

As the title suggests, this post is a case study on how Gitflow and traditional feature branching have been hindering our current development process. I'll share the attempts I'm making to resolve some of the key issues we're facing as an Android development team.

## **Current Setup & Issues**

### **The Setup**

We are a small, fully-remote team of developers who have been using Gitflow as our Git branching model, coupled with a standard Merge Request (MR) and Code Review process.

* **Code Repository & Planning:** We use GitLab as our code repository, leveraging its issues feature for planning and tracking our development work.  
* **Workflow:** All planned work first moves into our Kanban board, gets assigned, and is then picked up based on priority. Tickets are broadly defined, with one issue per feature or significant piece of work, regardless of its size.  
* **Development Process:** Once a developer picks up a task:  
  * They create a Gitflow-style feature branch in the format feature/\<issue-id\>-\<issue-title\> from our dev branch.  
  * We maintain Gitflow-style branches for our active development, beta, and production channels, using release tags to mark each public beta and production release.  
  * Developers work in isolation within their feature branches until the assigned work is completely done, tested, and verified. Although we might switch between branches for urgent bugs or enhancements, the core feature work remains siloed.  
  * Consequently, a feature—regardless of whether it takes a day, a week, or two weeks—is never merged back into dev until its Merge Request is created, and the code is thoroughly tested, reviewed, and approved by other team members.

### **Issues Faced**

* **Delayed Shipping:** Features face multiple bottlenecks, remaining unshipped until development, testing, review, merging, *and* re-testing are all complete.  
* **Review Process Overheads:** The process is further complicated by potential issues raised during reviews and inevitable merge conflicts.  
* **Code Review Quality:** Reviewing becomes challenging and less effective when Merge Requests contain hundreds of new or modified lines.  
* **Availability Challenges:** Other team members are not always consistently available to review such large code changes in one go.  
* **Merge Conflict Headaches:** We often face the painstaking task of fixing merge conflicts, trying not to mess up the original developer's work.  
* **Ineffective dev Merges:** While we try to regularly merge dev into active feature branches, this doesn't guarantee a conflict-free merge when integrating other people's work.  
* **Release Delays:** Ultimately, our feature releases end up getting delayed because they're waiting on multiple rounds of merges and approvals.

## **Search for a Solution**

* **Problem Identification:** After being repeatedly impacted by our current process, I wanted to find possible ways to fix this problem.  
* **Belief in Solved Problem:** I was sure this must be a solved problem, as we couldn't be the only small team facing this issue.  
* **Inspiration from Dave Farley:** Luckily, around this time, I came across a video by Dave Farley discussing a similar topic and how feature branching often goes against the philosophy of Continuous Integration (CI).  
* **Deep Dive:** This led me down a rabbit hole in search of alternative solutions to make our development process faster, without duplicated work or additional delays.

## **Learnings**

Here are some key learnings from my deep dive:

* **Code reviews don't primarily check for stability.** Their main purpose is to ensure the code adheres to team-defined standards.  
* **Delaying releases for code reviews doesn't ensure stable output.** Only thorough testing guarantees stability.  
* **Merge Requests were primarily introduced for open-source projects** where contributors were not given direct access to push code to stable branches.  
* **Merge Requests and code reviews are often considered "process gates."** These can slow down the overall development process without adding significant benefits to the quality of the deliverable or its underlying implementation.

## **Shortlisted Ideas**

After reviewing a bunch of reference material and having multiple discussions with other people in this field, I found the following three solutions that, when integrated, might work for our team:

### **Vertical Slicing**

* No more single, monolithic tickets per feature.  
* Each feature is meticulously broken down into smaller tasks, ensuring only small chunks of work are completed and committed.  
* Each major feature or change is considered an epic, and then sub-tasks are created to slice out smaller, logical chunks.

### **Trunk-Based Development (TBD)**

* The team develops off of the same main branch without creating dedicated feature branches.  
* Developers push their changes directly to this main branch, and these changes are immediately available to everyone else when they pull.  
* This approach ensures the codebase is always merged and conflict-free at all times.  
* Combined with vertical slicing, commits become small, easy to merge, and straightforward to review.  
* It removes much of the ceremony around code merging and code reviews, as these now happen continuously, often multiple times a day.

### **Feature Flags**

* To hide unfinished and unstable work, feature flags are used to safely ship releases containing completed work from the main development branch.  
* Developers can toggle features on/off at any time to test work developed by others and themselves.  
* To ship a feature to users, once it's fully tested, its respective feature flag can either be entirely removed or migrated to a remote configuration flag to control public availability.  
* This practice is also known as "Dark Releases."

Some other solutions I researched but decided not to pursue for now:

* **Pair Programming:** Being a very small team, pair programming was never a viable option for us due to limited resource allocation. While it's a great concept popularized by Extreme Programming, it doesn't fit our current constraints.

## **Updated Process (as of July 2025\)**

Based on the shortlisted solutions above, I plan to introduce the following changes to our current development process:

### **GitLab Vertical Slicing**

* We will continue to create issues for features and tasks, but now, within each GitLab issue, we will create sub-tasks to define smaller, more manageable slices of work.  
* In GitLab, each sub-task gets its own unique ID. We will use this ID in our commit messages to connect the sub-task with the commit.  
* If a sub-task proves too large or lacks detail during development, we will create additional sub-tasks within the same ticket. The objective is always to ensure each sub-task represents a limited amount of work, resulting in minimal commits and changes.  
* One slicing strategy will be based on architectural layers. Every feature can be broken into a minimum of four sub-tasks, one for each:  
  * Data Layer  
  * Domain Layer  
  * UI Layer  
  * Integration of all three layers

### **dev-Based Development (Trunk-Based)**

* All development will happen directly on the dev branch. We will no longer use Gitflow-based feature branching.  
* Feature branches will only be used for rare, truly experimental work.  
* Developers are expected to self-test and self-review all code thoroughly *before* pushing to the origin.  
* Code reviews will happen continuously: every time new changes are pulled from the origin. There will be no more explicit code review flow; everyone is expected to review the changes being pulled.  
* Any code review comments will be communicated via the GitLab commit screen.  
* Commits should contain the sub-task ID in the commit message. If relevant, create a new sub-task if one is missing.  
* Commits should be pushed to the origin at least once a day.

### **Dark Releases with Feature Flags**

Implementing this process requires some project-level setup. This is critical to ensure unfinished features and changes are never accidentally shipped to the public.

* Feature Flags will live in their own independent data store (e.g., a dedicated feature flag service or a specific database table).  
* Feature Flags can be toggled on/off from a developer-only menu within the app.  
* Every new feature development will begin with the creation of its unique feature flag.  
* All Feature Flags will automatically be disabled for release builds to prevent accidental feature releases to the public.  
* Once a feature is completed and tested internally, its feature flag will either be fully removed or migrated to a remote configuration flag for controlled public availability.

## **Conclusion**

Moving away from our old Gitflow process is a big step for our Android team. By using Vertical Slicing, Trunk-Based Development, and Feature Flags, we aim to make our work smoother, remove roadblocks, and get new features out faster. 
We believe these changes will help us work together better, integrate code more often, and lead to better quality, fewer problems, and quicker releases. This is all about making our development process work best for our small, remote team, so we can deliver great features more easily and with more confidence. We also understand that this process is new, and we're open to making more changes as our team gets used to it and grows.

---
## References
[Gitflow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
[Continuous Integration vs Feature Branch Workflow - YouTube](https://www.youtube.com/watch?v=v4Ijkq6Myfc)
[Why Pull Requests Are A BAD IDEA - YouTube](https://www.youtube.com/watch?v=ASOSEiJCyEM)
[I’ve Found Something BETTER Than Pull Requests... - YouTube](https://www.youtube.com/watch?v=WmVe1QrWxYU)
