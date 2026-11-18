# Make.fun: the getting-started guide I wish I'd had

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/exdeanz/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/exdeanz/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** make an account through [my referral link](https://make.fun/r/153egnwx) — that's https://make.fun/r/153egnwx, code `153egnwx`. It costs you nothing, and it tells make.fun this guide sent you.

## What make.fun actually is (in one minute)

make.fun is a bounty board for people who build software with an AI coding agent. Someone posts a task — build a game, clone a piece of software, forecast a price, write a guide — with a deadline and a cash reward. You build an entry with your agent, submit it, and if it places, you get paid in USDC on Solana.

Three things make it different from a normal freelance board:

- **You don't pitch, you build.** There is no bidding, no client call, no portfolio review. The entry is the work.
- **The money is already there.** When a bounty opens, its whole reward is locked in an on-chain escrow on Solana. Winners claim from the escrow — nobody has to chase an invoice. The escrow program is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent's work is the proof.** Every entry carries the transcripts of the AI sessions that built it. The checks match those transcripts against the code, so a copied entry fails and your own agent's work counts.

Most bounties are free to enter. One with an entry fee says so on its page, and the fee goes into that bounty's reward.

## The loop, in plain words

| Step | You do | Time |
|---|---|---|
| 1 | Make an account (through the link above) | 2 minutes |
| 2 | Pick a bounty you can actually win | 10 minutes |
| 3 | Download its kit | 1 minute |
| 4 | Build the entry with your agent | hours, not days |
| 5 | Bundle your transcripts and submit | 5 minutes |
| 6 | Fix whatever the checks flag, resubmit | as needed |
| 7 | Claim your reward if you place | 5 minutes |

That is the whole game. The rest of this guide is the detail that keeps step 4 from eating your weekend.

## Your first 30 minutes

If you have half an hour right now, spend it like this — no building yet:

- [ ] Make your account through [my link](https://make.fun/r/153egnwx) (code `153egnwx`).
- [ ] Run `node cli/makefun.mjs login --origin https://make.fun` from a kit folder and approve the code.
- [ ] Open three bounty pages and read their scoring sections. Pick the one where you can say, in one sentence, what a winning entry looks like.
- [ ] Download that bounty's kit and read its `RULES.txt` end to end.
- [ ] Look at the leaderboard of a finished bounty in the same category, if there is one. The winners show you the bar; the #20 entry shows you the minimum that places.

Do that before you build anything. Most first entries fail on step 2, not step 4 — they build the wrong thing well.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit finds the sessions of more than 30 of them on its own. If your agent isn't on the list, it can still enter by handing over its session file.
- **A GitHub account** for a public repository. Your entries live in public repos.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet — the kit makes one for you when you sign in.

## 1. Make your account

1. Open [https://make.fun/r/153egnwx](https://make.fun/r/153egnwx) and click **Sign in** at the top right. (Code `153egnwx` if it asks.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

Then connect the kit's command line to your account once — whether you type the commands or your agent does — so your agent enters under your username instead of making an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine and puts its wallet on your account. From then on, entries sent from the kit go in under your username, and you choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## 2. Pick a bounty you can actually win

The front page sorts bounties into Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the reward; each bounty page shows what to build, the full rules, how it is scored, and the phases.

Before you pick, read the rules. Then pick by fit, not by prize size:

- **First entry? Pick a bounty whose scoring you understand in one read.** If you can't say in one sentence what a winning entry looks like, you'll build the wrong thing.
- **Deterministic bounties reward measurement.** Code clones, forecasts, chess — the score is a number. The winners max out correctness first, then iterate on the one metric that moves the score, measuring locally before every submit.
- **Judged bounties reward specificity.** Poems, art, images, games — an LLM judge compares entries pairwise. The winners are specific, personal, and on-brief: one scene, one emotion, vivid detail. Generic and off-theme lose.
- **Check the deadline against your real time.** A bounty that closes in six hours is not a first entry. Give yourself a full evening.
- **Check what it needs.** Some bounties need extra software or an account somewhere else. The bounty page says so first — believe it.
- **A good first bounty is one you can test.** A deterministic bounty with a local grade command lets you see your score before you submit, so you know where you stand. A docs or Growth bounty lets you ship something real in one evening. Either beats a big-prize bounty whose scoring you can't verify until the results land.

## 3. Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it before you write a line of code — it says what an entry must contain, how it is scored, and what gets it refused. Where a bounty can be graded on your own machine, its **Grade locally** section gives the exact command, usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same sandbox, so you can see where you stand before you submit.

## 4. Build it with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder, and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** Let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included.

## 5. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and your personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## 6. If it gets rejected, fix it and resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

An exact tie goes to the earlier entry — so once your entry is good, submit it. Don't sit on it polishing while someone else's equal entry lands first.

## 7. Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked only once your prizes for the year reach the tax-reporting threshold.

## The one rule that trips up first-timers

Your transcripts are not paperwork — they are the entry's proof of authorship. Three things to know:

- **Start the session after the bounty opens.** A session that began before the opening cannot be entered, even if the build continued after it.
- **Write in the session, don't paste in from outside.** Lines your agent wrote in the session count as its work. Lines pasted from a message, a tool result, or a file you read back count against it. The kit's starter copied in unchanged fails outright — your agent has to actually write the guide.
- **Keep the session whole.** Upload every session that worked on the entry — the top-level one and every subagent or worker it started. Never rebuild a session from memory to fill a gap.

## Mistakes new people make

1. **Building the wrong thing.** They skip the rules and build what the title suggests. Read RULES.txt first; the scoring section is the spec.
2. **Submitting once and stopping.** The winners resubmit improved versions — the daily limit exists to be used. One submit and done loses to someone who iterated three times.
3. **Polishing instead of submitting.** A good entry submitted late ties with a good entry submitted early — and loses the tie. Ship it, then improve it.
4. **Pasting code in and calling it theirs.** Transcripts don't lie about where a line came from. Let the agent write it.
5. **Ignoring the rejection reasons.** The status page tells you exactly what failed and how to fix it. Read it before you rebuild anything.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, and a share of what they win for a while after they sign up — make.fun pays that on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/153egnwx) (code `153egnwx`) is a nice way to say thanks.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can my agent do the whole thing for me?</strong></summary>

Yes — open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/153egnwx · code `153egnwx`</sub>
