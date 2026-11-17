# Ask first, build cheap, ship clean

## 1 · Ask first, build cheap, ship clean
_~0.5 min_

Hi everyone, I'm Mehedi, from the Mobile Team. This is the AI workflow I actually use every day, not the conference-poster version. Three tools: one checks code, one plans work, one chain ships it. Each stands on its own. My goal: you walk out with two or three things to try this week. And ignore that little footer for now. It comes back on slide 17.

Let's start with a document most of us have never read to the end.

## 2 · 39 rules. One long doc. Nobody wants to check them by hand.
_~1.25 min_

Quick show of hands. Who here has read the whole quality standard, start to finish? ... Okay. Now keep your hand up if you've actually checked your own code against every single rule in it.

[PAUSE — look at the hands]

Yeah. That's about what I expected, and honestly, that's the point of this slide.

I'm not knocking the standard. It's fine. Thirty-nine rules, in three tiers: nine LOW, thirteen MEDIUM, seventeen HIGH. The problem is that checking thirty-nine rules across a whole app, by hand, is a week of nobody's favourite work. So it just doesn't happen.

Each part of today is something I used to skip: checking, planning, writing it up. So that's the agenda. eqc-kit checks. /orchestrate plans. The ship chain ships.

Before the tools, four words you'll hear all talk.

## 3 · A skill is a playbook. Sub-agents are its helpers.
_~1 min_

Quick primer, because none of these tools have come up here before.

Claude Code is where I run all of this. It's an AI coding agent in your terminal.

A skill is a saved playbook. You type its name with a slash, and the main session follows it, the same way every time.

Sub-agents are its helpers. The main session hands one a single task and gets a short report back.

And haiku, sonnet, opus are three model sizes: cheap and fast, mid, biggest and priciest. A lot of today is about sending work to the cheapest one that can do it.

eqc-kit also works in four other AI coding tools, so you don't need Claude Code for that one.

With those four words, section one.

## 4 · 01 · eqc-kit
_~0.25 min_

Section one: eqc-kit. About ten minutes, then questions. This is the one I built myself, so I'll start with how that happened.

It started with one question.

## 5 · How I ended up building eqc-kit
_~1.25 min_

So, quick story. I was given the EQC docs and asked: are your projects compliant?

Fair question. So I sat down with the doc and checked it against the project, one rule at a time. Read a rule, look through the code, write it down, next rule. It was a tedious job.

Then I tried using AI. It helped, but it was still too much work, and I didn't totally trust what it told me.

So I started automating the whole thing. One thing led to another, and now I have this: eqc-kit.

It's not tied to our doc, by the way. You bring any written standard, and the tiers come from it. LOW, MEDIUM, HIGH like ours? Fine. Bronze, Silver, Gold? Also fine.

Install is one command, `npx eqc-kit init`. It asks a few questions, and they all have defaults, so you can just keep pressing Enter. In Claude Code you get slash commands. In the other tools you just say "eqc check".

Before I built it, I tried the two obvious ways. Here's how they compare.

## 6 · Three ways to check a project against the standard
_~2.25 min_

Manual review is where I started. It works if you're careful, but it's slow, and it's a one-off. Nobody does it twice.

Then I tried the obvious thing. Paste the doc into the AI and ask, "is my project compliant?" Here's what actually happened to me.

It said pass when it wasn't.

It lost track halfway through. Thirty-nine rules is a lot to hold in one go.

Ask it twice, get a different answer.

And it would fix things for now, and later, while working on a new feature, the AI would break the same rule again.

Every single time, it also burned tokens and time doing the same exploring from scratch.

The right column is what eqc-kit does about each of those. Every answer, pass, partial, fail or not applicable, points at the file that shows it. You can open the file and argue with it. It lists every rule first, so nothing gets skipped. Results are saved, so a re-check re-reads them instead of re-guessing, and a plain script turns the same answers into the same level. It remembers what already passed. And re-reading saved results costs nothing.

Now, the bottom line on the slide is the honest part. You need a written standard first. The first full check isn't cheap. And the agents can still be wrong, which is exactly why every answer comes with evidence you can read.

So what do you actually run?

## 7 · What you run, and where AI is used
_~2 min_

Four things. The top two use AI, the bottom two don't.

`/eqc-check`. The first time, one agent reads your doc and lists every rule. Then one agent per tier goes through the code, in parallel. If you already have a code map, say a graphify graph, it looks there first, but only if the map is up to date, and it confirms everything in the real code.

Then a plain script, no AI, works out your level. Level just means the highest tier with no fails at or below it. The script never reads your code. It just counts the answers. And new: next to the Markdown report, you also get an HTML page. One file, you just open it in the browser.

`/eqc-fix` ranks what to fix, low effort and high gain first. Small stuff goes to one helper. Bigger stuff gets a plan, and you approve it before anything happens. It never commits for you.

Then `eqc guard`. This is my answer to "the AI fixed it, then broke it again". It remembers every rule that has passed. If one of those stops passing, guard fails. A rule that was already failing won't block you. Only something that used to pass and now doesn't.

And last, `verify`, plus git hooks. Some rules a plain command can check, like "lint is clean". Those can run on commit and push, if you opt in.

[CUTTABLE if running late] Hooks are opt-in, one command per clone, `npx eqc-kit hooks`. It won't override hooks you already have. And anyone can skip hooks, so put the same checks in CI too.

Why no AI in the hooks? Too slow, costs money on every commit, and you'd get a different answer each time.

Enough talking. Let me show you two of these, and the report it writes, on our app.

## 8 · Demo: check, report, and what to fix next
_~2.75 min_

Watch for three things: the first part is instant, the report is just a file, and the fix list starts with the cheap wins.

[DEMO — switch to the terminal in our mobile app repo and run `/eqc-check` with no arguments. Point at the level and say "hold that number, it's on the next slide". Read one fail's evidence line out loud. Switch to the browser tab with `docs/eqc/COMPLIANCE.html` and scroll once: level and tier progress, what needs attention, every rule by tier. Back in the terminal, run `/eqc-fix`, read the top three suggestions and why they're low effort, high gain, and cancel at the prompt. If the ranked list hasn't appeared after ~30 s, cancel and show the fallback screenshot. Switch back to the slides]

So, first one. Instant. No agents, no tokens, it's just reading the saved results. There's the level, and every fail left comes with its evidence. Hold that number.

Now the same thing as a page. Level and progress at the top, then what needs attention, then every rule. No setup, it's a file.

And now `/eqc-fix`. Here's the ranked list. These top ones are cheap because they're small and easy to contain. I'm cancelling here. We are not fixing anything live today.

[IF PART 1 BREAKS: show ./screenshots/eqc-check-scorecard.png — "Here's the same scorecard from this morning; the live one says the same thing."]

[IF PART 2 BREAKS: show ./screenshots/eqc-compliance-report.png — "This is the page it writes next to the Markdown report; it's just a file, no setup."]

[IF PART 3 BREAKS, or the ranked list hasn't appeared in ~30 s: cancel, then show ./screenshots/eqc-fix-ranked.png — "Here's the ranked list from my last run; same output, no waiting."]

Before I flip: one of those fixes moved all our console logs over to a proper Logger. How many files did that touch? Shout out a number.

[PAUSE — take a few numbers]

## 9 · Our mobile app went from HARD_FAIL to MEDIUM in about 5 days
_~1.75 min_

Fifty-eight files. Whoever said the closest number, well done.

And the level you saw in the terminal: MEDIUM, right there in the title. Thirty-three pass, two partial, four fail.

Some context. We started at HARD_FAIL, which just means a rule in the lowest tier failed. Fixing the ESLint errors alone, fifty-four of them across thirty files, got us to LOW. All in, twenty-seven recorded fixes in about five days. Twenty-five done, two partial. We also added Crashlytics error handling across seventeen files.

The tests stayed green the whole way. About eighty-five test files touched, and all 2,912 tests passing.

My favourite story is the i18n rule. Seven audits, six rounds of fixes, because every audit found more hardcoded English. In the end I added a custom ESLint rule so it can't come back.

Those four fails are honest. Three are big architecture moves, not quick wins. TypeScript can't pass, because the project has to stay JavaScript. So the kit records it as a fail and says why. I'd much rather have an honest fail than a fake pass.

Oh, and the audit found a hardcoded secret in the codebase. I'm not saying which one. It's handled.

That's eqc-kit. Questions before we move on?

## 10 · Questions? (eqc-kit)
_~2 min_

That's section one. Any questions on eqc-kit? If you're stuck for one, think about which tier your project would land in today, or which of your rules a plain command could check, like lint.

[PAUSE — Q&A, ~2 min; move on at 15 minutes into the talk]

eqc-kit checks code against a standard. Next is how I get bigger work done without burning my best model.

## 11 · 02 · /orchestrate
_~0.25 min_

Section two: /orchestrate. It's a separate tool, so you can use it without eqc-kit. About twelve minutes, then questions.

Same as before, I'll start with why I built it. It came out of a habit I had with plan mode.

## 12 · Why I built /orchestrate
_~1.5 min_

This one comes straight out of my day-to-day work.

I kept going back to plan mode. Every time, I asked Claude to split the long work into phases, hand each phase to a sub-agent on a model that matches how hard that piece is, and interview me before starting.

It was the same prompt and the same instructions, over and over again, for every big task. So I started building this skill.

The main reason I built it is tokens. Most pieces of a big task don't need the biggest model. If each piece goes to the cheapest model that can do it, you spend fewer.

I don't have a number for that, and I'll come back to it in a couple of slides.

Before the skill, I used three other ways. Here's how they compare.

## 13 · Four ways to run a big task with AI
_~2.75 min_

These are the three things I used before. The first three columns are how each one worked for me day to day. It's not a feature list from the docs.

First, the long prompt. It works, but I pasted it every time. One model did everything, and nothing stopped it before it started editing. Next session, it was gone.

Plan mode is good at planning. But I still typed the phases, the sub-agents, the models and the "interview me" part every time. Once I approved, one model built the whole thing and checked its own work. And the plan only lived in that chat.

/goal keeps going until the goal is met. It doesn't ask me anything first. It starts working right away, there's no model choice, and it checks itself.

The last column is /orchestrate, and the next two slides explain it. On the OK row, the difference is that its gate can't be skipped. Even "just go" written into the goal doesn't skip it. One thing on the interview row: it says "if needed" because for tiny goals, it takes a fast lane and skips the questions. The verifier still runs.

Now the bottom line, which is the honest part. On a small task, all that planning and checking is overhead you don't need. It has to run on opus or sonnet. On haiku, it stops and asks you to switch. And you still read the report at the end.

So what's it actually like to use?

## 14 · How /orchestrate runs a big task, phase by phase
_~2.5 min_

This is the whole thing in one table. I'll go through it quickly.

GRILL is the interview I used to ask for by hand. One question at a time, and it gives you its recommended answer, so most of the time I just say yes. If the goal is tiny, it skips this.

PLAN splits the goal into tasks and scores each one. Scoring is the next slide. It also decides up front who owns which file, so three helpers working at the same time don't step on each other.

PREVIEW is the part I care about most. It shows you the full plan and stops. I'll show you that live in a minute.

EXECUTE. The orchestrator doesn't write the code, the helpers do. The one exception is a fix of five lines or less per task, and only for a bug the verifier found. Then a cheap haiku verifier re-runs the checks, and a separate reviewer reads the diff.

CLOSE tells me which models actually did the work. Everything lives in a plan file, so I can stop, close the laptop, and run `/orchestrate resume` the next day. It suggests a commit, but it never makes one.

[CUTTABLE if running late] There are also shortcuts it isn't allowed to take, and each one sounds reasonable in the moment. "I'll do this quick fix myself"? It hands it to a helper. "Approval was given in advance"? It shows the preview anyway. "Small repo, I'll just read it"? It reads at most two files of a hundred lines per phase itself, and sends a scout for the rest. "I'll run the tests to be sure"? The verifier does that. "This agent sets its own model"? It passes the model anyway.

The part of PLAN I want to show you is how it picks the model.

## 15 · How it picks a model for each task
_~2 min_

Let's try one first. Which model would you give the task "add a config entry with exact steps"?

[PAUSE — take a few answers]

Haiku. It's clear, it's one file, and it doesn't need much thinking.

That's how scoring works. Three questions per task: how unclear is it, how much does it touch, how hard is it to think through. Zero to two each, and you add them up.

Big tasks get split first. Opus only gets a task that really can't be split, or anything that touches security, like auth, secrets, crypto or permissions. Those always go to opus, and a fresh opus reviewer goes through the diff looking for vulnerabilities.

The rule I like most is the one on screen: when it's unsure, it picks the cheaper model. If that was wrong, the task fails and moves up. That still costs less than sending everything to the big model just in case.

That's where the token saving comes from. I can't give you a number. Try it on one real task, and look at the model mix it reports at CLOSE.

[CUTTABLE if running late] And if a task fails, it climbs a ladder. A failed haiku task retries once on haiku, with the exact error and the current diff, then moves to sonnet. Sonnet retries once. Then the orchestrator either tries opus once, or works out the problem itself and re-scopes or splits the task. If that still fails, it pauses and reports to me. Every retry is logged in the plan file.

Now the gate itself, live.

## 16 · Demo: the preview gate
_~1.75 min_

The thing to watch: "just go" in the goal didn't skip the gate.

[DEMO — switch to the pre-staged terminal paused at PREVIEW. Walk the task table (task, score, tier) and point at the Tier column: the opus row carries its reason. Read the "Mix" line. Point at the line saying "just go" in the goal was ignored, then at "Approve, edit, or reject?". Reply "ok, but drop task 3" and show the re-preview with the plan changed, then reject, switch back to the slides. SPEAKER REMINDER: never type a bare "go" or "just go" at the prompt, that approves.]

I set this up before the talk, so you don't have to watch me answer GRILL questions. When I started it, I wrote "just go" into the goal. It's sitting at PREVIEW anyway, waiting for me, and it says so right here.

So there's every task, with its score and its tier. See this opus row? It says why it's on opus. And there's the Mix line, the model mix for this run. Nothing has run yet.

Now I'll reply "ok, but drop task 3". That counts as an edit. It changes the plan and shows it to me again, and you can see task 3 is gone. Only a plain yes approves. I'll reject, and we're out.

[IF IT BREAKS: show ./screenshots/orchestrate-preview.png — "Here's the preview from a real run; the bit to notice is that 'just go' in the goal didn't skip the gate."]

That's the check before anything runs. Here's what the checking after looked like on real runs.

## 17 · What happened when I used it
_~4.25 min (~1.75 content + 2.5 Q&A)_

Two "done" claims that weren't true, from my own runs. In a test-coverage audit, a sonnet helper wrote the list from memory and said it was done. The verifier found about sixty-five identifiers missing. The retry got the exact list and came back with zero missing.

Another time, a helper said line 143 of an end-to-end test was covered. A coverage refresh said it wasn't.

Verifiers get it wrong too. On one run, the final verifier raised a false alarm because its search matched numbers in a CSS file. So I still read the report.

Across about eleven runs, most of the work went to haiku and sonnet. One thing to be clear on: those runs, and the build with no escalations, all happened before I added the opus tier you saw on slide 15.

Now the right side. Remember the footer on slide 1? /create-presentation is the skill that built this deck, and /orchestrate built that skill. Five tasks plus two fixes. Nothing had to move to a bigger model, and there was one one-line fix during VERIFY.

Before any real work, an opus dry-run found fifteen issues in that skill, and thirteen got fixed. And the CSS false alarm I just mentioned came from this same build.

The facts in this deck come from a context file in the same folder, so it doesn't make numbers up. If a slide is wrong, that file is the place to check.

So, questions on /orchestrate? If you're stuck for one, think of a ticket on your board right now that would score zero to two.

[PAUSE — Q&A, ~2.5 min; move on at about 30 minutes in]

Last section is lighter: what happens after the code is written.

## 18 · 03 · The ship chain
_~0.25 min_

Section three, and this one's lighter. Each skill here is small on its own. The value is in how they connect.

Here's the chain.

## 19 · Each skill feeds the next
_~1.5 min_

The first four are skills in the install repo. The last is our CI.

It starts with /reflect. It runs at the end of a session and keeps CLAUDE.md, that's the agent's project notes, plus CONTEXT.md and the docs folder in line with what changed, so the why gets written down.

Next is /git-commit. It writes a Conventional Commit, that's the type, scope, summary format, shows you a preview, and waits for you to confirm. And no AI attribution trailer.

Then /send-pr, which writes a PR title and body that actually say something.

Then /release-notes. It reads the commits, the diffs, and the doc changes, and writes the release notes file.

And finally ci-pipeline, our CI, builds and ships from that file.

/git-commit is the highlighted one because it's the cheapest to start with. You could try it today, right after this talk.

The trick is that it's one piece of writing with several readers.

## 20 · One change, four write-ups, four readers
_~1.5 min_

Quick question for the room. Who reads your commit messages?

[PAUSE — take a few answers]

I heard a "nobody" in there. That's the usual answer. The real answer: more people than you think. On our dev builds, the last commit message becomes the tester note. So if your commit says "wip fix stuff," that's what QA reads.

So look at the table. The commit message is read by developers and testers, and /git-commit writes it. The pull request is read by reviewers, written by /send-pr. The release notes are read by managers, and the store note, the App Store or Play Store "What's new" text, by actual users. Both of those come from /release-notes, with CI copying the store note. It's the same facts every time, rewritten for each reader as they move down the chain.

Which means commits get written with the next step in mind.

[IF SLIDE 21 IS CUT, say instead: "Here's a real one." and go to slide 22.]

## 21 · Commits are written for the release notes
_~0.75 min_

[CUTTABLE if running late]

These quotes come straight from each skill's instruction file. They're two halves of a contract. The commit skill writes each line so it can be reused later, technical and product-facing. The /release-notes skill trusts, but verifies. It doesn't trust commit messages alone, so it reads the code diffs and doc changes too. Same idea as the verifier in section two.

The why comes from /reflect. /release-notes reads CLAUDE.md and CONTEXT.md because they often explain why a change happened.

Here's a real one.

## 22 · Demo: v1.9.4 notes beside their commits
_~1.5 min_

Watch for one commit line turning into a sentence a manager, or even a user, can actually read.

[DEMO — open docs/RELEASE_NOTES_v1.9.4.md in the left pane, run `git log` for the v1.9.4 range in the right pane, pick one commit and find where it shows up in the notes, scroll to the App Store / Play Store release-note block and read it out loud, switch back to the slides]

So here's the commit, written for developers: "fix, android: restore hardware back button navigation on SDK 36." Here's the same change in the release notes, written for a manager: "Android Back Button Fixed, Android 16 slash SDK 36." And down here, in the store block, it's written for someone who just wants to know why the app updated overnight: "Fixed the Android back button and improved app stability." One change, three write-ups.

[IF IT BREAKS: show ./screenshots/release-notes-v1.9.4.png — "Here are the two side by side; same commit, two very different audiences."]

And this file isn't optional.

## 23 · No release notes, no build
_~1 min_

If that file isn't there, the build fails. Simple as that. CI wants `RELEASE_NOTES_v<version>.md`, and our staging and production builds copy the store note straight out of it.

The pipeline goes like this. Dev builds go to Firebase. Staging goes to TestFlight and Play internal testing. And prod gets promoted to the stores.

For me, this is the difference between a habit and a process. The chain is enforced by CI, not just recommended on some wiki page that nobody opens.

Let's pull the three sections together.

## 24 · Ask first, build cheap, ship clean
_~0.75 min_

One sentence each.

Ask first, that's eqc-kit: agents check your code against your own standard, a plain script works out the level, big fixes wait for your OK, and the guard stops passing rules from slipping back.

Build cheap, that's /orchestrate: every task gets a score before it gets a model. You approve the plan, cheaper models do the building, and a verifier checks.

Ship clean, that's the ship chain: write the commit for whoever reads it next, and it becomes the PR, the release notes and the store note, with CI making sure.

You don't need all three. Pick two.

## 25 · Pick two. Try them this week.
_~0.75 min_

Pick the two that match your pain. Quality doc nobody checks? `npx eqc-kit init`. Big ticket coming up? `/orchestrate`. Commit messages that just say "fix"? `/git-commit`, today. It's the five-minute win.

The install line is a prompt. Paste it into Claude Code and you get /orchestrate and /git-commit. It's my repo, so read INSTALL.md first if you like. No rush to copy it, the same lines stay up on the next slide, all through Q&A.

Thanks. Last round of questions.

## 26 · Questions? (final)
_~2 min_

Thank you all, really. I'm happy to take anything across the three sections. And if it's quiet: which two are you trying first?

[PAUSE — Q&A, ~2 min; leave this slide up so the commands and the install line stay on screen]
