# Code Reviews

## The Problem

> **Your team is only as good as your weakest reviewer.**

## The Solution

> Great code reviews take time to do, but they will improve not only your project but your knowledge of the project and **your relationship with your team.**

## How do you make it less personal?

See: [Egoless Programming](EGOLESS_PROGRAMMING.md)

## What is a code review?

Code Review, or Peer Code Review, is the act of consciously and systematically convening with one’s fellow programmers to check each other’s code for mistakes, and has been repeatedly shown to accelerate and streamline the process of software development like few other practices can. There are peer code review tools and software, but the concept itself is important to understand. Software is written by human beings. Software is therefore often riddled with mistakes. To err is, of course, human, so this is an obvious correlation. But what isn’t so obvious is why software developers often rely on manual or automated testing to vet their code to the neglect of that other great gift of human nature: the ability to see and correct mistakes ourselves.

## Why do we review code?

We all know that code reviews are important, but why? They can catch some bugs and prevent terrible design decisions from going to production but is that their only function?

A great code review has three important goals:

- Keeping the team up to date with a changing codebase.
- Improving the quality of the project.
- Providing feedback for the developer and/or learning something you didn't know as a reviewer.

## Keeping up to date with a changing codebase

Giving code reviews forces developers to read the parts of the code that they themselves didn't work on. This improves the team's overall knowledge of the codebase. As a result, task planning goes more smoothly and the accuracy of time/complexity estimations increases.

#### I. Find out the _why_ first

To be able to understand a code change, it must first be understood why it was made.

Identify the issue/ticket associated with this code change and read it thoroughly including the comments. Read the description of the pull request if there is any. This will give the necessary context not only to understand the changes themselves, but to judge if the changes fit the requirements.

Without context, for example, hardcoding a dot as the decimal separator for numbers seems reasonable for your US-only app, but if after reading the ticket, it would be clear that your company is expanding to other countries and now the user's locale needs to be involved in choosing the decimal separator.

If there is no issue/ticket, and no PR description, write down a description and include it as part of the review. If the purpose of the PR is misunderstood, the reviewee is likely to point that out.

#### II. Read, don't skim

Don't be content with a simple "looks good to me". All well-formatted code looks good when it's skimmed over! Read the changes and **really understand them**. Yes, it's difficult. Yes, it will take more time. Yes, it's worth it. It will also increase the chances of catching not-so-obvious project quality issues.

## Improving project quality

Having a second pair of eyes look at the code before it goes to production is a good way to catch _some_ bugs and ensure the code will be maintainable.

#### III. Always run the code

One-line change? Run the code. Just CSS changes? Run the code. Just translations? **RUN. THE. CODE.**

Do not kid yourself into thinking that everyone always compiles and runs the project after every change they make. We should... but we don't. You know, those times when you have just 5 minutes left before you need to leave the office, and you have just one more trivial change to make, but you don't have the time to verify it.

Ensuring that the project still compiles and runs without throwing exceptions is the least that can be done as a reviewer. It's a **simple sanity check**. So do it.

If there were any user-visible changes introduced, make sure they are seen with your own eyes. Click through the new UI components.

Run the tests. Yes, I know the CI is supposed to do that. But maybe there are flaky tests that will pass on CI by chance? Or maybe there is a bug that only appears on your macOS, but the CI is running Linux? Maybe somebody didn't follow the correct naming pattern for the test file and the test runner ignored the file altogether?

Do the changes include database migrations? End your review process by rolling them back, checking out master and checking if the project still runs.

#### IV. Do not nitpick

Somebody inserted two empty lines where they were only supposed to insert one? Don't mention it. The reviewee's **patience** to fix "problems" with their code **is limited** and we shouldn't want to waste it on trivial issues.

Instead, try to find an automated solution that is going to ensure all those trivial details are detected automatically and suggest that your team starts using it.

#### V. Focus on readability issues that can't be detected automatically

Once there are automated tools validating function name length and proper indentation, focus on the important stuff that only a human can catch.

Do those function/variable names make sense? Do they use the project's vocabulary consistently? Could they be confusing? Are there any ambiguous abbreviations?

Don't use acronyms or ambiguous names, if something is called sub_guest could be interpreted as subscribe_guest, guest_subscription or subscription_guest, name it what you mean, is this a subscription for guests or a feature to allow users to invite guests to subscribe?

Simply. **Don't name things in surprising ways**.

## Providing feedback for the developer

Good feedback is feedback that **reinforces somebody's good habits**, and helps notice and remove bad habits. For your feedback to have any impact at all, you need to **ensure that you are being listened to**.

#### VI. Always say something nice

Even with the most trivial code changes comments should say something positive. The more specific the positive feedback is, the better.

Here are some generic examples of good comments for inspiration:

- Good job! I tried my best to find bugs in your code, but couldn't.
- Thanks for fixing that typo, I wasn't aware this is the correct spelling of that word.
- I love how you named this function. It's immediately obvious what it does.
- Wow, that's neat. I wasn't aware of this feature of our programming language / this framework / this library.
- I like that you added all of this new code in a new file. It was tempting to put it in the existing file, but that would make the existing file way too big.

If you are afraid to sound silly for appreciating trivial things, ask yourself how you feel when you receive a code review. Are you excited? Or are you dreading it because you know that in the best case, it will be neutral silent approval, but in the worst case, it will be full of harsh criticism? Do you really want your coworkers to dread receiving reviews from you just because you are afraid of sounding silly?

Another important role of **positive feedback** is that it **makes the reviewee more open to your negative feedback**.

Do you have that one family member that uses every chance they see you to complain about you? You gained weight again, your sibling makes more money than you do, and you should smile more... How likely are you to actually consider their complaints as valid points that will inspire you to improve yourself? Not at all? Well, receiving only negative feedback from the same coworker for months feels the same.

#### VII. Avoid judgemental and bossy language

The easiest way to stop sounding judgemental and bossy is to **assume you are wrong**, and the reviewee is right. **Then ask questions** that will help you realize why you are wrong. After all, they probably spent much more time working on this code than is being spent on reviewing it. They are more likely to understand the details.

Do not say ~~_"don't do this, do that"_~~. You don't want to cultivate in your coworkers the ability to follow orders. You want them to think creatively and critically. Besides, nobody likes to be bossed around.

Instead, say _"what would you think about..."_. Signal that you are open to a conversation. People are more motivated to do something if they were involved in making the decision.

Do not say ~~_"why don't you just..."_~~. This phrase suggests that your solution is the obvious choice and the reviewee is stupid for not using it. It might trigger a defensive reaction that will make otherwise smart and reasonable people passionately defend a flawed position.

Instead, say _"have you considered...?"_, explain why your solution would be advantageous in this situation and follow up with a friendly invitation to prove you wrong, e.g. "...or did I miss something?".

Now, I am not saying you are actually always wrong. But **you are definitely not always right**. This approach will make it easier for both you and the reviewee to admit when either of you is wrong **without losing face**.

#### GitHub PR Reviews

GitHub has a feature that allows you to mark your pull request review as comment, accept, or request changes.

Avoid requesting changes unless you are absolutely certain something needs to be changed. Requesting changes is bossy language and doesn't leave much room for debate. Instead make comment reviews until all questions have been addressed, and then accept.

## Further Reading

[Giving better code reviews](https://medium.com/@mrjoelkemp/giving-better-code-reviews-16109e0fdd36#.9upgeqfvh)

[Google's Engineering Practices](https://google.github.io/eng-practices/review/reviewer/)
