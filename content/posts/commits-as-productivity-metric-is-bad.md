+++
title = 'Commits as a Productivity Metric is Bad'
date = 2023-09-15T14:00:00-07:00
categories = ['dev', 'management', 'productivity', 'perf']
author = 'Colin'
+++

I've noticed an unfortunate trend lately where companies are using the number of code changes (commits) as a way to measure developer productivity. This is a terrible idea for a few reasons. First, it encourages developers to submit code that's not ready, which can lead to bugs and other problems. Second, it discourages developers from working on complex or challenging problems. Third, it can lead to developers cutting corners on testing. And fourth, it can create a toxic competitive environment among developers. We need to find better ways to measure productivity.

Using the number of commits as a measure of developer productivity can encourage a bad behavior of leaving bugs in the code and committing before code is ready. While we would hope that bugs are found through either existing tests or a code reviewer, in reality this will often not be the case. Reviewers might not have all of the context of the code to understand fully if there's a bug, and even if they do, they're human and therefore fallible. And there's now a great incentive to not properly test your code. If a bug is found, you get to make another commit to either fix the bug (we now have doubled our commit count for this change), or roll it back to resubmit as a new commit (we have now tripled our commit count). Maybe this speeds up development because we're committing earlier, but we're also not being careful with what we do.

As far as testing goes, there's also now a great incentive to not test right away or to not test fully. If you spend a lot of time writing a change and carefully testing all of the use cases and submitting that in one change, you only get one change worth of commits. However, if you create your change and add no tests or the bare minimum amount of tests, you can write more tests later as additional commits. Even better, you can split those tests up and add them piecemeal to boost your numbers. This isn't very good for a product, but good for productivity metrics.

Complexity is not taken into account for a metric like this. How could it? Some changes may be very simple but require a huge number of lines added or removed. Others could be a change that takes days to debug and track down and end up with a 5 character change. Number of lines doesn't correlate to complexity. This makes difficult problems something to be avoided. If you work on a problem for 3 days tracking down and fixing something very tricky and your teammates are all making 2-3 changes per day during that time, you're now 4-6x behind them in your productivity metric. Who would want to take on difficult problems? There becomes an incentive to not do so.

One of the issues with using the number of commits as a productivity metric is that they're often done as a relative number. Say you have 5 members on the team. 4 of the members on average use a lot of the above methods and are producing around 150 commits a year. The last member takes on harder problems that take a long time to figure out. They test things fully and rarely have to roll back. The number of code changes they make is lower, but the quality of the changes is much  higher. They only produce 75 changes in a year. Now there's an issue for that developer due to the stark difference in raw changes made.

It can be worse when the metric is known by developers. They start hoarding simple changes.

<div class="ascii-box" id="box1" markdown="1">
*"Oh hey, I can get this done real fast to unblock me, mind if I take that bug from you?"*
*"No, I can get it in soon, don't take it."*
</div>

 Suddenly there's competition for changes rather than collaboration. Projects can be slowed down waiting for changes from people who have claimed them. Resentment and hostility can arise if someone "steals" another's bugs. When we move from collaboration on our projects to competition, the projects suffer as we have incentive for our peers to "lose".

Encouraging the artificial increase in the number of commits also introduces another problem. Change is where bugs happen. Code without bugs only gains bugs when it is changed. Changing code more frequently has a higher chance of introducing bugs. The quality of your systems is decreased when developers have a reason to change the code as often as possible.

Measuring performance of software developers is as difficult as the work software developers perform. I can sympathize with wanting an easy to pull, data-driven metric to quickly evaluate the performance of a developer. Unfortunately, there really isn't a simple way to do this. While there is probably a problem if a developer never commits code at all (maybe they're more of a manager at that point and you haven't recognized that), it's not always the case that low commit counts equates to low productivity. Using commit counts as a measurement adds a lot of stress to developers and teams, reduces quality of code that is committed, and makes work a bit more hostile than it needs to be. Instead, we should probably measure developer productivity on delivered solutions and weigh things based on difficulty of work. I would recommend throwing away commit counts completely, and just see what end deliverables a developer produced. If they have a project that they completed in time or faster and happened to do it with less than the standard number of commits, they should be praised rather than punished.
