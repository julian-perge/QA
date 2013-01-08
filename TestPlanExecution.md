Running Test Plans
==

Prerequisites: you must have a github account; we're using github to store test results, and to keep track of issues.

Configure bitcoind/Bitcoin-Qt to log timestamps in its debug.log file (see the [sample.bitcoin.conf](https://github.com/bitcoin/QA/blob/master/sample.bitcoin.conf); put it
in the [data directory](https://en.bitcoin.it/wiki/Data_directory)).

What should you test?
--

Generally, testers are recruited by developers or QA leads by asking for help on the bitcointalk forums,
in IRC chat, in pull request comments, on twitter, etc.

The developer or QA lead will create the test plan in a repository here at github, usually by forking the
main bitcoin/QA repository. So you can look at its forking history to see testing activity or find things
that might need more testing.


Test procedure
--

1. Fork the github repository that has the test plan you'll be working on.<br/>
  ![github fork](http://dl.dropbox.com/u/38065353/Github_ForkButton.jpg)
2. Do what it says in the test plan.
3. File any issues **in the main bitcoin/bitcoin repository issue tracker!** If you just poke the
Issues button in your forked test plan repository the developers will never see them.
4. Edit the copy of the test plan in your repository with the results of your testing. Feel free to add
notes, etc.
5. Save a copy of the debug.log file(s) created by bitcoind/Bitcoin-Qt in case the developers need them to
find issues or to prove that you tested what you said you tested in order to claim a testing bounty.

When you have finished running the test plan, either submit a pull request (easiest and probably best)or
send a message to the person who created the test plan to let them know you've finished testing.

Bounties
--

First: do not expect to get rich as a bitcoin reference implementation QA tester. Your main motivation for helping
test should be to move the Bitcoin project forward, not to make money. Think of bounties as thank-you tips for
tackling a job that most people don't want to do.

If there is a bitcoin bounty for running a test plan, then the developer or QA lead will decide how to distribute
the funds. If you think they are being unfair, try to stay calm and be constructive: suggest how they might do
a better job next time. This is all a big experiment; don't forget that you are part of the process and
will help make it succeed or fail.
