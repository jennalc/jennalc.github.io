---
layout: post
author: Jenna Lau-Caruso
title: "Navigating Terminology Differences Between RTC and GitHub"
blog_description: "Examining the different spoken languages used to refer to similar source code concepts in Rational Team Concert and GitHub."
---

Having spent the majority of my professional years using Rational Team Concert (RTC) for all of my source control needs, I have recently been introduced to the GitHub world. One of the major hurdles in making this transition was trying understand where the common source control concepts lay between the two systems. The terminology used by each is entirely different, and in many cases common terms are used in a opposite way. Colleagues who come from GitHub to RTC express the same confusion. Both sides are often frustrated. None of us are speaking the same language.


After learning the GitHub vocabulary, the two systems are actually very similar. I hope this rough translation between the two can help other developers who may be struggling to move from one to the other.

## Terminology Mapping

Initially, I found it easiest to begin by mapping the terminology in RTC to the terminology in Git. The mapping is not exact, as each system has its own nuances which I will explore in detail later. But to start, here is the rough translation that helped to shape my understanding:

RTC | Git
--- | ---
Load Workspace Repository | Clone Repository
Flow with a Stream | Check out a Branch
Create a Change Set | Create a Branch
Check In | Commit and Push
Deliver | Merge
Refresh Pending Changes | Fetch
Accept Pending Changes | Pull

## Getting Source Code to your Local Machine


#### RTC

In RTC, to work with source code locally, you must first create a *repository workspace*, selecting the *stream* with which you want to flow. A repository workspace is your private copy of the source code. It is initially created on the server and can be *loaded* onto your workstation, which is referred to as your sandbox. The selected stream indicates which version of the source code you want to work with. For example, your project may have separate streams for each release track.


#### GitHub

In Git, to work with source code locally, you need to *clone a repository branch*. In this context, the *upstream branch* is akin to the RTC stream; the version of the source control that you are working with. The cloned repository on your local computer is the equivalent of your local sandbox in RTC.


## Making Code Changes


Now that you have your local copy of the code, you are free to make changes. In both systems, anything you do locally is private, affecting only your personal copy of the code. But what do you do when you are ready to contribute your code back to the project?


#### RTC 


In RTC, this is done using a *change set*. A change set is a group of related changes. To add changes to a change set, you check in the changes. This stores your change on the server copy of your repository workspace, but does not yet affect the code stream you are flowing with. You can check changes into a change set as many times as you want. Each time you check in code, the server copy of your repository workspace will be updated. When you are ready, give the change set a comment and associate it with the related *work item*. It is now ready for review. 


Reviews in RTC are tracked directly on the work item, using the *approvals* tab. Here you can add one or more reviewers and/or approvers, using the work item comments to track discussion on the code. Once your code has been reviewed and approved, you can deliver your change set. Delivering a change set automatically completes the change set, meaning that it can no longer be updated, and merges your code to the stream that your repository workspace is flowing with. If additional changes are required, a new change set must be created.


#### GitHub


In Git, the concepts are very similar, but the language used to describe the flow is different. Although not identical, the closest match to RTC's change set concept in Git is a *branch*. But wait... we have already seen the term *branch* used above to describe the version of source code you started with. The overloading of the word "branch" causes a lot of confusion for us RTC veterans. Having already made the logical connection between a branch in Git with a stream in RTC, we assume that branches are heavy, long-living entities. But this is not always the case. 


When working on an *issue* in Git, the best practice is to create a *branch* for the change. In this context, the branch is a short-living artifact intended to contain your changes until they can be merged into the *upstream branch*. A branch can either be created from the Git web interface, making it immediately visible to others working in the repository, or it can be created locally. To add changes to your branch, you *commit* the changes. Unlike in RTC, each commit is tracked with a message describing the contents of the commit. Committing code to a branch does not update the server-side copy of the branch. To do this, you must also *push* the changes to the branch.


To have the code reviewed and merge it into the upstream branch, you will need to create a *pull request*, selecting the branch you want to merge code into as the *base* and the branch containing your change as the *compare*.  The pull request is used to track technical discussions about the code as well as code review status. Once the code is reviewed and approved you can *merge* into the upstream branch. GitHub will automatically prompt you to delete the branch at this time. For additional changes, a new branch should be created.


#### Note


Although conceptually similar in many ways, there is one key differences between RTC change sets and GitHub branches.

- **RTC**: If there are multiple change sets in a repository workspace, all changes co-exist in the sandbox simultaneously. 
- **GitHub**: Branches are self contained. Locally, you will only see code from the branch you are currently working on. In order to "stack" multiple separate changes locally for unit testing, you must either create your second branch off the first branch, or create a test branch and merge all required branches into this branch. 


## Keeping your Local Copy Updated


Assuming that you are collaborating on a project, you will periodically need to update your local copy of the code.


#### RTC


To see if your local sandbox is up to date, *refresh* the *pending changes* view in the Eclipse IDE. All change sets in the stream which are not in your repository workspace will be listed. From here, you can *accept* all incoming change sets, or can accept specific change sets. Accepting the change sets will merge the change sets from the stream into your repository workspace. If there are any conflicts, you will need to resolve them.


#### GitHub


Similarly, to see if your local code is up to date, do a *fetch*. This allows you to review changes in the upstream branch before committing them to your local branch. To commit the changes, perform a *pull*. This will merge the commits from the upstream branch into your local branch. Like in RTC, if there are any conflicts, you will need to resolve them.


## Summary


Although we have only just scratched the surface, this should give you a starting point of navigating the differences in terminology used by RTC and GitHub. I hope this allows you to speak the language of both systems, giving you the foundation to build from.
