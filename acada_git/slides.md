% ACADA weekly get together - git, workflows, CI and ACS
% Dominik Neise
% 07.10.2020

---

# Who am I?

- Dominik Neise
- worked for ~10 years on FACT
- physicist
- since 6 months in ACADA

## Who are you ? - I assume:

- you are developers (not managers) :D
- you are to achieve more with less work in our gitlab! :D

## What can you expect of the next 20minutes?

- intro to the simplest git workflow I know: [The Feature Branch Workflow][1]
- intro to ACS component development + testing in Python


# What is a workflow?

 * A bunch of steps & a set of common ideas we agree on
 * should make us more efficient
 * at best: should not add more work
 * I propose here the **most simple** git workflow I know


# The points - The [The Feature Branch Workflow][1]

 1. one central branch (be it `main`, `master` or `dev`)
 2. We agree: The `main` always works
 3. Nobody pushes into the `main` - not even jedi masters.
 4. New features are developed in shortlived **feature branches**
 5. New features are discussed, agree upon and merged via **pull requests**
 6. pull requests are reviewed, but automatic tests prove that code works!
 7. Tackle the dependecy issue via releases

I've put together a little live show for your entertainment.

# Danger zone

Life Demo Time


<https://github.com/dneise/workflow_showcase>


# Part 1

## 1. One central Branch

* Developers use this branch to branch from.

## 2. It always works

* Developers can trust the `main`; if their PR does not work. It's their own fault.
  Not a faulty master to begin with.

* **But** End-users do not use the `main`, they should use released versions.

## 3. Nobody pushes into the `main`

* This is just to ensure 2. Everybody goes through a PR.

# Part 2

## 4. Features grow on feature branches

* This is where the name comes from.
* feature branches are shortlived.
* They should branch off the current master, not the master of 3 months ago.

## 5. Discuss; Agree; Merge

* This is the heart of the workflow.
* By discussing in the open, agreeing and merging, only PRs, which are proven to work,
  we create an inclusive, fearfree work environment, where everybody can give their best.

# Part 2.5

## 6. Automatic tests

* Proper reviewing takes similar time as proper writing.
* We do not have that time.
* So we use tools to help us.
* What a machine can review, must be reviewed by a machine!
* Automatic tests -> prove that the code works correctly.
* Linters, Static code analysis -> Style & Smell
* Complexity Metrics -> Handle with care :D

In the best of all worlds, reviewers can even be non-coders.

# Part 3

## 7. Releases

We release our software (e.g. a sub-system) whenever we think it reached a certain level of maturity.

* So there is no reason to not merge a PR. No reason to wait. If something is better, merge it.
* Downstream users have stable releases to use.
* No need to be afraid of downstream dependencies breaking.

# Part 4

## misc statements - to make everybodies day a bit better

* Do not review until perfection. If it is better than `main`: merge it.
* Dedicated Refactoring PRs (every friday?) can be used to tidy up.
* Some reviewers fix tiny things themselves instead of pointing them out
  and waiting for the original dev to fix them.
  This can safe huge amounts of time. And it just feels nice.
* Nobody owns code.
* Everybody owns the code.
* Everybody is responsible if ACADA does not work. We are a team.
* Everybody may propose improvements and (try to) implement them.
* If you see a problem; open an issue - speak up. We need your knowledge!


# live demo: random closing remarks

* Everything was discussed in the open.

* People with issues, do not need to find out who is a stakeholder in this case is.
  Stakeholders will monitor repos, they are interested in.

* Documentation, which is online and can be linked to, is worth a lot.

* Not all teams need to follow the same workflow, but it reduces surprises.

* This workflow does not only work for source code.
  Documentation is also: written, reviewed, tested and released.

* There are different workflows, none is perfect, this was just one of them.

* This workflow is supposed to work for many different team sizes.
  (I use it in projects where I am working alone.)

* Nothing here used Emails, Slack, other chats.

# A nice talk if you have 25 more minutes

Frossie Economou from Rubin Observatory made a nice statement about
how to collaborate well in her talk ["Deployment automation as a key stage in the development lifecycle"][2]
It is only 25 minutes. Check it out!

<!--
# Life Demo

Talking points
- show an empty (or almost empty?) repo.
- point out that even the empty repo has been setup with continous integration from the very start
- We start by opening an issue:
    - Here "Diana" realized that our software is not working according to the requirements.
    - "Dominik" (as ususal) is a little confused and does not quite understand.
    He points out that to his understanding the software works fine.
    - "Diana" then clarifies her issue, by pointing directly to a specific point in the documentation,
    thus avoiding further misunderstandings a saving everybody a lot of time.
    - "Dominik" now understands what the problem is and assigns the issue to himself, as he is planning to fix it.

- As you see, the whole issue and answer is happing in the open. Everybody else in the company is able to follow the
issue and hop into the discussion, if need be.

- Furthermore we saw, that linking directly into existing internal documentation can be really helpful.

- There was no email involved here. "Diana" did not need to find out, who is responsible for this project and whom to email and whom to include, since they might also be stakeholders in this issue.
The responsibility is inverted, stakeholders are expected to "watch" a repository they are involved in, not random people are expected to understand which person is involved in which project.

# Pull requests

- In the meantime "Dominik" started to fix the issue. So he checked out the master branch, fixed the issue and pushed the fix directly into the master branch, right? NO!

- Dominik created locally on his machine a feature branch and fixed the issue.
- Then he pushed the feature branch to the server and opened a pull request, thus asking the team to accept this fix and merge it into the master.
- His job is mostly done at this point, so he goes and gets a coffee.

- **What if he forgot to create a feature branch and puched directly into the master? That happens to me a lot!**
- In this project the master branch is protected. Nobody (not even the owner) can push into the master
- the only way to get stuff in, is via an accepted PR.

- **But, we cannot afford to review PRs all the time, otherwise we cannot get on with our own work!**
- Help us Travis!
- Continous Integration and Automatic Testing are the two siblings helping us out.

- In the meantime, CI & AT automatically checked out the feature branch (triggered by opening a PR), build the software, installed it, and ran the test suite. In addition they ran static code analysis, code coverage analysis, code complexity analysis and other tools like this.
- Now "Diana" realizes that somebody has mentioned her issue in a PR. So she goes and reviews it.
- "Diana" does not have a degree in software design, but she can well understand test results and she knows when stuff is spelled wrong.
- She realizes that "Dominik" fixed indeed the issue, but his code is not well documented, the functions are named `func1` and `func3` and he uses single letter variable names l and O.
- Just as "Diana" is about to write a couple of comments, pointing out his mistakes, she realizes that they are a team.
    So she quickly cheks out the code, adds a few comments, fixes some english spelling errors and renames the varaibles.
    She is not afraid to do so, since 1.) we can always revert and 2.) CI and AT will show if she made a mistake.

- At some point "Dominik" realizes somebody reviewed his PR. He is happy to see somebody fixed his spelling errors.
Even some docu was added. Great!
- Since he cannot formally approve a PR opened by himself, he just posts a friendly note about this.
- "Diana" sees that the tests still pass - phew she did not break anything - and "Dominik" also likes her improvements.
- So they both agree this is a great fix and it should be merged into the master.

# Releases

At some point "Manny" the manager scrolls through the closed issues and realizes that a lot of progress has been
made since the last release of the software 4 days ago. Even some API changes were made.

**But wait, API changes in the master? Are you crazy? How can downstream users work on this?**

The master is not supposed to be used by downstream processes or people. This is what releases are for.
So "Manny" prepares a new release. He might

-->

[1]: https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow
[2]: https://www.video.uni-erlangen.de/clip/id/20086
