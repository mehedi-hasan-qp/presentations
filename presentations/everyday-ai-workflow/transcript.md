# Ask first, build cheap, ship clean

| You see                          | Means                                   |
| -------------------------------- | --------------------------------------- |
| `# Section …` / `## Slide N · …` | Where you are. Don't read it.           |
| Plain paragraph                  | Say it out loud.                        |
| `> 🎬 DO:`                       | An action. Do it, don't say it.         |
| `> ⏸ PAUSE:`                     | Stop and let the audience answer.       |
| `> ✂️ CUTTABLE`                  | Say it only if you're on time.          |
| `> ⚠️ IF …:`                     | Backup: only if that condition happens. |
| `➡️ Next slide`                  | Press →                                 |

# Section 1 · eqc-kit (slides 1–11 · 15 min)

## Slide 1 · Ask first, build cheap, ship clean

⏱ ~0.5 min

Hi everyone, I'm Mehedi Hasan, from the Mobile Team here at QuestionPro.
This is the AI workflow I use every day. There are three tools.
One checks code.
One plans work.
One chain ships it.
Each one works on its own. My goal is simple: you leave with one thing to try, or an idea to build something of your own.
Btw, keep this small footer in mind: "Built with presentation-builder". I'll come back to it later.

Let's start with a standard most of us have never read to the end. Mostly, we read the highlights and scratched our heads.

➡️ **Next slide**

## Slide 2 · 39 rules. Nobody wants to check them by hand.

⏱ ~1.25 min

At QuestionPro, we take engineering quality seriously. But I don't think everyone has read the whole EQC docs end-to-end, I guess most of us read the highlights and titles, and thought about tackling one item at a time. I have my team's Mobile EQC doc 1.1 and the web team has EQC doc 2.0.

As you already know, EQC means Engineering Quality Checks. The Mobile EQC is our standard for mobile apps: React Native, Flutter, Android and iOS. It has thirty-nine rules in three tiers. Nine are LOW, thirteen are MEDIUM, and seventeen are HIGH.

The standard is good. The problem is the work. To check thirty-nine rules across a whole app by hand is slow and boring. So it does not happen.

Today this presentation has three parts. Each one is something I used to skip: checking, planning, and writing it up.

Before the tools, here are four things you will hear all talk.

➡️ **Next slide**

## Slide 3 · A skill is a playbook. Sub-agents are its helpers.

⏱ ~1 min

This is a quick primer, I know you all already know this, but I'm going through it anyway.

First, our best friend Claude Code, where I usually run all of this.

Skill: it's a saved set of instructions. You type its name with a slash, and it follows the playbook, does the same thing every time.

Sub-agent: it's a helper. The main session gives it one task, and it sends back a short report.

Now the models: you must already know haiku, sonnet and opus. Three models from 3 tiers.
A lot of today is about sending work to the cheapest model that can do it.

Everything you will see is a skill, a set of sub-agents, or both. Also, eqc-kit works in four other AI coding tools too. So for that one, you don't need Claude Code.

Now, let's start section one.

➡️ **Next slide**

## Slide 4 · 01 · eqc-kit

⏱ ~0.25 min

Section one is eqc-kit.

I built this one myself, so I will start with how it happened. This is the "ask first" part from the title: ask the standard before you change code.

It actually started with one question.

➡️ **Next slide**

## Slide 5 · How I ended up building eqc-kit

⏱ ~1.25 min

Here is the short story. Datta gave me the Mobile EQC and asked: are your projects compliant with the EQC?

So I took the standard and checked it against the project, rule by rule. It was slow, boring work.

Then I used AI. It helped, but it was still too much work, and I did not trust the answers.

So I started to automate the process. One thing led to another, and now I have eqc-kit.

FYI, it is not tied to the Mobile EQC doc only. But I will come back to that later.

Installing this is just one command. The setup asks a few questions. All of them have defaults, so you can just press Enter. There are no dependencies. But you'll need Node eighteen or newer.

After that, in Claude Code, you get slash commands. In the other tools, it adds a block to AGENTS.md, so you just say "eqc check".

Now let me show you what checking one rule looks like, with AI prompting and with eqc-kit.

➡️ **Next slide**

## Slide 6 · One Mobile EQC rule: AI prompting vs eqc-kit

⏱ ~1.5 min

Let's use one real rule from the Mobile EQC. It is a MEDIUM rule: folder structure. Feature-first, and no god files. A god file is one huge file that does everything.

> ✂️ **CUTTABLE — say only if on time:**
> The rule lists the folders for each stack. For React Native, that is src/screens, src/features, src/components and src/navigation. Flutter, Android and iOS each have their own layout.

First, by hand. You find the rule, open the project, walk through the folders, and look for huge files. It works if you are careful. Then next time you do it all over again, plus the other thirty-eight rules.

The red box is what I tried next. I tried AI prompting. I pasted the standard in and asked. Here is what happened to me.
Each time, it explored the project from the start. It lost track. It said pass when it was not a pass. When I asked twice, I got two different answers. And later, when I built a new feature, the AI broke the same rule again.

The green box is eqc-kit.
The rule is already on its list. An agent for the MEDIUM rules checks the folders. The answer comes with the files that prove it, so you can open them and argue. The result is saved. Next time it is read back, not guessed again. And guard warns you if the rule stops passing.

Our app CXOTG passes this one.

One honest note. You need a written EQC doc. The first full check is not cheap. And the agents can still be wrong, so read the evidence.

So, now the question is, what do you actually run?

➡️ **Next slide**

## Slide 7 · What you run, and where AI is used

⏱ ~1.75 min

You run four things. The top two use AI. The bottom two do not.

First, `/eqc-check`. The first time, one agent reads your standard and lists every rule by tier. Then one agent per tier goes through the code, all at the same time. Each rule gets pass, partial, fail or not applicable. Each one comes with the file as proof.

> ✂️ **CUTTABLE — say only if on time:**
> If you already have a code map, like a graphify graph, it looks there first. It does this only if the map is newer than your last commit and your uncommitted changes. It never builds the map for you. And it checks everything it finds in the real code.

Then a plain script, with no AI, works out the level. The level is the highest tier where that tier, and every tier below it, has no fails. A fail in the lowest tier is HARD_FAIL. The script never reads your code. It only counts the answers.

It writes the report as Markdown. Next to it, you also get an HTML page. It is one file. You just open it in the browser.

Second, `/eqc-fix`. It ranks what to fix, with low effort and high gain first. Small fixes go to one fixer. For bigger fixes, opus writes a plan, you approve it, and cheaper models do the work. It asks you before it touches CI, packages, architecture or the top tier. And it never commits for you.

Third, `eqc guard`. This is my answer to "the AI fixed it, then broke it again". Each time results are saved, it remembers which rules passed. That is the baseline, and it only goes up. Guard fails if one of those rules stops passing, or if the level goes down. A rule that was already failing does not block you.

Last, `verify`, with git hooks. Some rules can be checked by a plain command, like "lint is clean". Those rules carry a command, like `npm run lint`.

> ✂️ **CUTTABLE — say only if on time:**
> The script runs them only for passing rules. So a known fail never blocks a commit. Only a new fail does.
>
> Hooks are opt-in. It is one command for each clone: `npx eqc-kit hooks`. On commit, it runs verify. On push, it runs verify, then guard. It will not replace hooks you already have, like Husky. It prints the lines for you to add. Anyone can skip hooks with no-verify, so put the same two commands in CI.

Why no AI in the hooks? It is too slow, it costs money on every commit, and you get a different answer each time.

Now let me show you two of these, and the report, on our app.

➡️ **Next slide**

## Slide 8 · Demo: check, report, and what to fix next

⏱ ~2.75 min

Watch for three things. The first part is instant. The report is just a file. And the fix list starts with the cheap wins.

> 🎬 **DO (demo) — part 1:**
>
> 1. Switch to the terminal in our mobile app repo.
> 2. Run `/eqc-check` with no arguments.
> 3. Point at the level and say "hold that number, it's on the next slide".
> 4. Read one fail's evidence line out loud.

> ⚠️ **IF** part 1 breaks: show ./screenshots/eqc-check-scorecard.png, then say: "Here's the same scorecard from this morning; the live one says the same thing."

First one. It is instant. No agents, no tokens. It only reads the saved results. Here is the level, and every fail comes with its evidence. Please hold that number.

> 🎬 **DO (demo) — part 2:**
>
> 1. Switch to the browser tab with `docs/eqc/COMPLIANCE.html`.
> 2. Scroll once: level and tier progress, what needs attention, every rule by tier.

> ⚠️ **IF** part 2 breaks: show ./screenshots/eqc-compliance-report.png, then say: "This is the page it writes next to the Markdown report; it's just a file, no setup."

Now the same results as one page. The level and progress are at the top. Then what needs attention. Then every rule. There is no setup. It is just a file.

> 🎬 **DO (demo) — part 3:**
>
> 1. Back in the terminal, run `/eqc-fix`.
> 2. Read the top three suggestions and why they're low effort, high gain.
> 3. Cancel at the prompt.

Now `/eqc-fix`. This is the ranked list. The top ones are cheap because they are small. I will cancel here. We will not fix anything live today.

> ⚠️ **IF** part 3 breaks, or the ranked list hasn't appeared in ~30 s: cancel, show ./screenshots/eqc-fix-ranked.png, then say: "Here's the ranked list from my last run; same output, no waiting."

> 🎬 **DO:** Switch back to the slides.

Here's what those fixes added up to on our app.

➡️ **Next slide**

## Slide 9 · Our mobile app against the Mobile EQC: Compliance level: HARD_FAIL → MEDIUM

⏱ ~1.75 min

One fix moved all our console logs to our Logger: fifty-eight files.

And here is the level you saw in the terminal. Against the Mobile EQC, our compliance level went from HARD_FAIL to MEDIUM, in about five days. After one fix across about eighty-five files, all two thousand nine hundred twelve tests still passed.

The rest is not on the slide. Fixing the ESLint errors alone got us from HARD_FAIL to LOW. That was fifty-four errors in thirty files.

> ✂️ **CUTTABLE — say only if on time:**
> Thirty-four Platform.OS checks became Platform.select().

All in, we made twenty-seven recorded fixes. Twenty-five are done and two are partial.

> ✂️ **CUTTABLE — say only if on time:**
> We also changed FlatList windowSize on thirty-three lists. And we added Crashlytics error handling in seventeen files.

Today we have thirty-three passes, two partial, and four fails.

> ✂️ **CUTTABLE — say only if on time:**
> My favourite story is the i18n rule. It took seven audits and six rounds of fixes, because each audit found more hardcoded English. In the end, I added a custom ESLint rule so it cannot come back.

The four fails are honest.
Three are big architecture moves, not quick wins. One is a state migration across a hundred and twenty-three files. One is a data-fetching library. One is certificate pinning. TypeScript cannot pass, because the project must stay JavaScript. So the kit records it as a fail and says why. I prefer an honest fail to a fake pass.

Also, the audit found a hardcoded secret in the code. I will not say which one. But, it is handled.

➡️ **Next slide**

## Slide 10 · Not tied to the Mobile EQC. Bring your own standard.

⏱ ~1 min

You may think eqc-kit only works with the Mobile EQC. It isn't tied to it. eqc-kit is just a tool. The standard, the EQC doc, is yours.

It is built to take your team's own written standard, and to adapt to it.

It reads the standard and lists every rule. It takes the tiers from your standard. Ours are LOW, MEDIUM and HIGH. Yours may be something else. It uses whatever tiers you have.

After that, the flow is the same: the check, the report, the fixes, and the guard.

It needs one thing: a written standard.

➡️ **Next slide**

## Slide 11 · Questions? (eqc-kit)

⏱ ~2 min

Any questions about eqc-kit?

> ⏸ **PAUSE:** Q&A, ~2 min; questions come in the chat or by unmuting, read chat questions aloud; move on at 15 minutes into the talk

> ⚠️ **IF** no questions: say "Then let's move on."

eqc-kit checks code against a standard. Next is how I get bigger work done without using my best model for everything.

➡️ **Next slide**

# Section 2 · /orchestrate (slides 12–18 · 15 min)

## Slide 12 · 02 · /orchestrate

⏱ ~0.25 min

Section two is /orchestrate. It is a separate tool. You can use it without eqc-kit. It takes about twelve minutes, then questions.

Like before, I will start with why I built it. It came from a habit I had with plan mode. This is the "build cheap" part from the title: give each piece to the cheapest model that can do it.

➡️ **Next slide**

## Slide 13 · Why I built /orchestrate

⏱ ~1.5 min

This one comes from my daily work.

I kept going back to plan mode. Every time, I asked Claude to split the long work into phases. I asked it to give each phase to a sub-agent, on a model that fits how hard that piece is. And I asked it to interview me before it started.

It was the same prompt, the same instructions, again and again, for every big task. So I started to build this skill.

The main reason is tokens. Most pieces of a big task do not need the biggest model.
If each piece goes to the cheapest model that can do it, you spend fewer tokens.

I do not have a number for that. I will come back to it on slide sixteen.

Now let me compare it with plan mode and /goal, on one task.

➡️ **Next slide**

## Slide 14 · One "forgot password" task, three ways to run it

⏱ ~2.75 min

Here is a task every app has: forgot password. It has an API endpoint, a reset email, a reset screen, and tests. It touches auth. That matters in a moment.

The two red boxes show how plan mode and /goal worked for me every day. They are not a feature list from the docs.

Plan mode writes a plan and waits for my OK. That is good.
But I type the phases, the sub-agents, the models and the "interview me" part myself, every time. After I approve, one model builds all four parts and checks its own work.

/goal tells Claude Code to keep working until a goal is met. It starts right away. It asks no questions. One model builds all. It checks itself.

The green box is my skill /orchestrate. It first asks me a few questions, one at a time. Then it splits the work and gives each piece a score. The email template is simple, so it goes to haiku. The reset screen has real UI logic, so it goes to sonnet. The auth work touches security. Anything on the security side always goes to opus. The tests get a score the same way.

This split is an example to show the rules. It is not a real run.

Now, checking. A cheap haiku verifier runs the checks again. A sonnet reviewer reads the reset screen. And because the auth part is security, a fresh opus security reviewer reads that diff, to look for weak spots.

Nothing is built until I say yes. Writing "just go" in the goal does not skip that OK. I will show you that live in a few minutes.

Next big task: with plan mode or /goal, I type my asks again. With /orchestrate, it is the same skill, one command.

One honest note.
For a small task, this is too much overhead. So, I gave it a "fastlane" mode. For a smaller task, it sets the goal, shows it to you for a short glance and just does it. You'll still read the report at the end.

Here are the phases it goes through.

➡️ **Next slide**

## Slide 15 · How /orchestrate runs a big task, phase by phase

⏱ ~2.5 min

There are five phases. I will go fast.

GRILL is the interview I used to ask for by hand. It asks one question at a time, and gives a recommended answer with each. So most of the time I just say yes. If you have a code map, its helpers search that before they search the files. Tiny goals take a fast lane and skip this.

PLAN splits the goal into tasks and gives each one a score. Scoring is on the next slide. At most three helpers run at once. Each file has one owner, so they do not get in each other's way.

PREVIEW is the part I care about most. It shows every task with its score and its model, then it stops. Only my reply counts. "Just go" in the goal is ignored. And "ok, but…" counts as an edit. I will show you this live soon.

EXECUTE and VERIFY. The orchestrator does not write the code. The helpers do. There is one exception: a fix of five lines or less in a task, and only for a bug the verifier found. A cheap haiku verifier runs the checks again. A sonnet reviewer reads the diff. For security tasks, an opus security reviewer does it.

CLOSE tells me which models did the work. Everything is saved in a plan file under docs/plans. So I can stop, close my laptop, and run `/orchestrate resume` the next day. It suggests a commit. It never makes one.

> ✂️ **CUTTABLE — say only if on time:**
> There are also shortcuts it is not allowed to take. Each one sounds fine in the moment. "I will do this quick fix myself"? It gives it to a helper. "Approval was given before"? It shows the preview anyway. "The repo is small, I will just read it"? It reads at most two files of a hundred lines per phase, and sends a scout for the rest. "I will run the tests to be sure"? The verifier does that. "This agent picks its own model"? It passes the model anyway.

The part of PLAN I want to show you is how it picks the model.

➡️ **Next slide**

## Slide 16 · How it picks a model for each task

⏱ ~2 min

Let's start with one example: "add a config entry with exact steps". That goes to haiku. It is clear, it is one file, and it needs little thinking.

This is how scoring works. There are three questions for each task.
How unclear is it?
How much does it touch?
How hard is it to think through?
Each gets zero to two. You add them up.

Big tasks are split first. Opus gets a task only if it really cannot be split, or if it touches security. That means auth, secrets, crypto or permissions. Those always go to opus. And a fresh opus reviewer reads the diff to look for weak spots. That is why the auth part of the forgot password task went to opus. It was because of security, not because of its score.

You can also ask for opus yourself. If a plan has more than two opus tasks, it asks you to confirm.

My favourite rule is the one on the bottom of the screen.
When it is not sure, it picks the cheaper model. If that was wrong, the task fails and moves up. That still costs less than sending everything to the big model, just in case.

This is where the token saving comes from. I cannot give you a number. Try it on one real task. Then look at the model mix it reports at CLOSE.

> ✂️ **CUTTABLE — say only if on time:**
> If a task fails, it goes up a ladder. A failed haiku task tries once more on haiku, with the exact error and the current diff. Then it moves to sonnet. Sonnet tries once more. Then the orchestrator either tries opus once, or finds the problem itself and re-scopes or splits the task. If that still fails, it pauses and tells me. Every retry is saved in the plan file.

Now let's see the gate itself, live.

➡️ **Next slide**

## Slide 17 · Demo: the preview gate

⏱ ~1.75 min

The thing to watch: "just go" in the goal did not skip the gate.

> 🎬 **DO (demo) — part 1:**
>
> 1. Switch to the pre-staged terminal paused at PREVIEW.
> 2. Walk the task table (task, score, tier) and point at the Tier column: the opus row carries its reason.
> 3. Read the "Mix" line.
> 4. Point at the line saying "just go" in the goal was ignored, then at "Approve, edit, or reject?".

> ⚠️ **Careful:** never type a bare "go" or "just go" at the prompt, that approves.

I set this up before the talk, so you do not need to watch me answer questions. When I started it, I wrote "just go" in the goal. It still stopped at PREVIEW. It is waiting for me, and it says so right here.

Here is every task, with its score and its tier. Look at this opus row. It says why it is on opus. And here is the Mix line: the model mix for this run. Nothing has run yet.

> 🎬 **DO (demo) — part 2:**
>
> 1. Type the reply "ok, but drop task 3" and show the re-preview with the plan changed.
> 2. Reject.
> 3. Switch back to the slides.

Now I reply: "ok, but drop task 3". That counts as an edit. It changes the plan and shows it to me again. You can see task 3 is gone. Only a plain yes approves. I will reject, and we are done.

> ⚠️ **IF** the demo breaks: show ./screenshots/orchestrate-preview.png, then say: "Here's the preview from a real run; the bit to notice is that 'just go' in the goal didn't skip the gate."

That's the check before anything runs. Here's what I've actually built with it.

➡️ **Next slide**

## Slide 18 · What I've built with /orchestrate

⏱ ~4.25 min (~1.75 content + 2.5 Q&A)

I built eqc-kit's latest upgrade with /orchestrate. That is the code map, the HTML report and the guard you heard about earlier. I also built most of my skills and agents this way.

I only counted runs that finished. There are forty-eight, across eight projects, in about six weeks. On my own tools, that is thirteen of the forty-eight runs: skills, agents and eqc-kit's latest upgrade.

> ✂️ **CUTTABLE — say only if on time:**
> eqc-kit itself, version zero point one point zero, I built before /orchestrate existed. Only the latest upgrade went through it. It used one opus, two sonnet and one haiku builder. None moved up a model. And sixty of sixty tests passed.

Across these runs, the models were mostly haiku and sonnet. Opus shows up in a few.

Now the right side. Remember the footer on slide one? This deck was built with presentation-builder. And /orchestrate built presentation-builder.

So what is it? A Claude Code plugin. It has two skills. One makes a new deck. One changes a deck. It also has six agents, and each has one job. One reads my sources. One writes the outline and slide text. One writes the script. One builds the HTML. And two review it, one for content and one for design.

It took three runs and eighteen tasks. None moved up a model.

Verifiers can be wrong too. On one of those builds, the final verifier gave a false alarm, because its search matched numbers in CSS. So I still read the report.

> ✂️ **CUTTABLE — say only if on time:**
> The facts in this deck come from a context file in the same folder, so it does not make up numbers. If a slide is wrong, that file is the place to check.

Now, are there any questions about /orchestrate? Please ask.

> ⏸ **PAUSE:** Q&A, ~2.5 min; questions come in the chat or by unmuting, read chat questions aloud; move on at about 30 minutes in

> ⚠️ **IF** no questions: say "Then let's move on."

➡️ **Next slide**

# Section 3 · The ship chain (slides 19–27 · 10 min)

## Slide 19 · 03 · The ship chain

⏱ ~0.25 min

Section three is lighter. Each skill here is small on its own.
The value is how they connect. This is the "ship clean" part from the title: write it up once, so the next reader can use it.

Here is the chain.

➡️ **Next slide**

## Slide 20 · Each skill feeds the next

⏱ ~1.5 min

The first four are skills in the install repo. The last one is our CI.

First is /reflect. It runs at the end of a session. It keeps CLAUDE.md, CONTEXT.md and all the related docs in the folder, up to date with what changed. CLAUDE.md holds the agent's project notes. So the reason for each change gets written down.

Next is /git-commit. It shows you the message and waits for you to confirm. It writes a Conventional Commit: type, scope, summary. And it adds no AI attribution line. And it does most of its work with git and bash commands.

Then /send-pr. It writes a PR title and body that really say something.

Then /release-notes. It also reads the doc changes, not only the commits and the diffs.

Last is ci-pipeline, our CI. It builds and ships from that file.

/git-commit is highlighted because it is the cheapest one to start with. You can try it today.

The key idea is one piece of writing, with several readers.

➡️ **Next slide**

## Slide 21 · One change, four write-ups, four readers

⏱ ~1.5 min

More people read your commit messages than you think.
On our dev builds, the last commit message becomes the tester note. So if your commit says "wip fix stuff", that is what QA sees.

Now look at the table. Developers and testers read the commit message, and /git-commit writes it.
Reviewers read the pull request, and /send-pr writes it.
Managers read the release notes.
Users read the store note, the "What's new" text in the App Store or Play Store.

/release-notes writes both, and CI copies the store note. It is the same facts every time. They are rewritten for each reader as they move down the chain.

So we write commits with the next step in mind.

> ⚠️ **IF** slide 22 is cut: skip it and go to slide 23, then say: "Here's a real one."

➡️ **Next slide**

## Slide 22 · Commits are written for the release notes

⏱ ~0.75 min

> ✂️ **CUTTABLE — say only if on time:**
> These quotes come from each skill's instruction file. They are two halves of a contract. The commit skill writes each line so it can be used again later. It is technical and also about the product. The /release-notes skill trusts, but checks. It does not trust commit messages alone. It also reads the code diffs and the doc changes.
>
> The reason comes from /reflect. /release-notes reads CLAUDE.md and CONTEXT.md, because they often explain why a change happened.

Here is a real one.

➡️ **Next slide**

## Slide 23 · Demo: v1.9.4 notes beside their commits

⏱ ~1.5 min

Watch for one commit line that becomes a sentence a manager, or a user, can read.

> 🎬 **DO (demo):**
>
> 1. Open docs/RELEASE_NOTES_v1.9.4.md in the left pane.
> 2. Run `git log` for the v1.9.4 range in the right pane.
> 3. Pick one commit and find where it shows up in the notes.
> 4. Scroll to the App Store / Play Store release-note block and read it out loud.
> 5. Switch back to the slides.

Here is the commit, written for developers: "fix, android: restore hardware back button navigation on SDK 36." Here is the same change in the release notes, written for a manager: "Android Back Button Fixed, Android 16, SDK 36." And here, in the store note, it is written for a user: "Fixed the Android back button and improved app stability." One change, three write-ups.

> ⚠️ **IF** the demo breaks: show ./screenshots/release-notes-v1.9.4.png, then say: "Here are the two side by side; same commit, two very different audiences."

And this file is not optional.

➡️ **Next slide**

## Slide 24 · No release notes, no build

⏱ ~1 min

No file, no build. The build fails. CI needs `RELEASE_NOTES_v<version>.md`. Our staging and production builds copy the store note from it.

The pipeline works like this. Dev builds go to Firebase. Staging goes to TestFlight and Play internal testing. Production is promoted to the stores.

For me, this is the difference between a habit and a process. CI makes the chain happen. It is not just a tip on a wiki that nobody opens.

Now let's put the three sections together.

➡️ **Next slide**

## Slide 25 · Ask first, build cheap, ship clean

⏱ ~0.75 min

One sentence for each.

Ask first is eqc-kit. Agents check your code against your EQC standard, like our Mobile EQC.
A plain script works out the level.
Big fixes wait for your OK. And the guard stops passing rules from slipping back.

Build cheap is /orchestrate.
Every task gets a score before it gets a model.
You approve the plan. Cheaper models build, and a verifier checks.

Ship clean is the ship chain.
Write the commit for the person who reads it next.
It becomes the PR, the release notes and the store note. And CI makes sure it happens.

➡️ **Next slide**

## Slide 26 · Pick any one. Try it. Or build your own.

⏱ ~0.75 min

Pick the one that matches your pain. You do not need all three.

Too much hassle to check and keep up EQC compliance?
Try eqc-kit: `npx eqc-kit init`.

Do you have a big ticket? Try `/orchestrate`.

Are your commit messages just "fix"? Try `/git-commit`. /git-commit is the quickest win: start today.

Or just take one of the ideas and build your own. Every tool today started as something I kept doing by hand.

The install line is a prompt. Paste it into your agent, and it sets up the skills. It is my repo, so you can read INSTALL.md first.

Thank you. Now, the last round of questions.

➡️ **Next slide**

## Slide 27 · Questions? (final)

⏱ ~2 min

Thank you all. I am happy to take any question about the three sections.

> ⏸ **PAUSE:** Q&A, ~2 min; questions come in the chat or by unmuting, read chat questions aloud

> ⚠️ **IF** no questions: say "Then thank you again."

> 🎬 **DO:** Leave this slide up so the commands and the install line stay on screen.

🏁 **End of talk**
