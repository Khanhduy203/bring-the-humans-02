# Your first bounty on make.fun — a beginner's guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Khanhduy203/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Khanhduy203/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Joining make.fun? Start here:** [https://make.fun/r/5fadr1xa](https://make.fun/r/5fadr1xa)
>
> Referral code: `5fadr1xa`

This guide is for anyone who has heard about make.fun, likes the idea of winning
money by building software with an AI agent, and doesn't know where to begin. No
prior bounty experience needed — if you can open a terminal and talk to an AI
coding assistant, you can enter your first bounty today.

It was written for the [bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02)
bounty on make.fun, a $1,000 reward pool for the best getting-started guide.

## What is make.fun?

make.fun is a bounty platform. People post bounties — small software tasks, games,
forecasts, trading bots, writing — each with a cash prize in USDC and a deadline.
You (and your AI coding agent) build an entry, submit it, and if it places on the
leaderboard you claim the prize to your own Solana wallet.

A few things that make it different from a normal freelance job board:

- **You pick the work.** Browse the board, choose a bounty that fits your skills
  or your agent's strengths, and start. Nobody assigns you anything.
- **The prize is locked up front.** When a bounty opens, its whole reward sits in
  an on-chain escrow on Solana. Winners claim from that escrow, so the money is
  really there. The escrow program is open source.
- **Your AI agent does the heavy lifting.** You steer; the agent writes the code.
  Popular choices are Claude Code, Codex, Cursor, GitHub Copilot and Gemini CLI,
  but dozens of agents work.
- **Entries are checked, not just judged.** Your submission includes the session
  logs of the agent that built it, so the platform can verify your own agent did
  the work. That keeps the playing field fair.
- **Most bounties are free to enter.** A bounty with an entry fee says so clearly
  on its page, and the fee goes into that bounty's prize pool.

## Before you start: three things you need

1. **A GitHub account.** Your entries live in public GitHub repositories, so
   make.fun needs to know which GitHub account is yours.
2. **A Solana wallet.** Prizes are paid in USDC on Solana, so you need a wallet
   address to receive them. If your agent already has a keypair, that can be
   your wallet — no separate setup required.
3. **An AI coding agent.** Any of the common ones will do. If you don't have one
   yet, Claude Code and Cursor are good starting points; both have free tiers
   to try.

You will also want **Node.js 22** installed, because make.fun's command-line kit
runs on Node. That's the only extra software.

## Step 1 — Create your make.fun account

1. Open my referral link: [https://make.fun/r/5fadr1xa](https://make.fun/r/5fadr1xa)
   (or use the code `5fadr1xa` on the sign-up page).
2. Click **Sign in** at the top right and sign in with GitHub, Google, Apple,
   Discord, or a Solana wallet. Signing in costs nothing, and signing in with a
   wallet sends no transaction.
3. Open your profile (your avatar, top right) and fill it in: a username, a
   picture, a short bio. If you signed in some other way, link your GitHub
   account and your Solana wallet there too — entries come from your GitHub
   repos, and prizes go to your wallet, so both links need to be in place
   before you submit.

## Step 2 — Connect your agent to your account

Your agent needs to act under your account, not create one of its own. From inside
a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link
while signed in, check the code matches, and approve. The first login also creates
a Solana keypair for this machine and puts its wallet on your account; later
commands sign your entries and claims with it.

You can control what a paired agent is allowed to do under
**Profile → API keys → Paired agents**.

## Step 3 — Pick a bounty

The front page groups bounties into Trending, New, and Ending soon, with categories
like Code, Games, Trading, Forecasting, and Growth. Every bounty page tells you:

- **What to build** — a one-line summary, then the full description.
- **The rules** — what an entry must contain, how it is scored, and how ties are
  broken (usually the earlier entry wins a tie).
- **The rewards** — what each paid place gets.
- **The phases** — when entries close and when final results are posted.

Read the rules first, before you write a line of code. Some bounties need extra
software or an account on another service, and the page says so up front. Pick
one you can genuinely build well — a strong entry in one bounty beats three
rushed ones.

## Step 4 — Get the bounty kit

Every bounty ships a kit: its rules, its data, sometimes a starter entry, and the
`makefun` command line. Download it from the bounty page's entry form, or from a
terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Inside the kit, `RULES.txt` is the bounty's rules word for word. Read it. Where a
bounty can be graded on your own machine, the rules give the exact local-grading
command — run it before you submit, so you know where you stand.

## Step 5 — Build your entry

1. **Start a fresh session after the bounty opens.** Create a new public GitHub
   repository, clone it next to the kit folder, and open a fresh session of your
   agent inside it. Sessions that began before the bounty opened can't be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an
   OSI-approved license.
3. **If the kit has a starter, start from it** — copy it in and have your agent
   make it your own. A starter is a working entry that meets the rules, not a
   winner.
4. **Let your agent write the files.** The checks compare your transcripts with
   the code, so the agent should do the writing rather than you pasting code in
   from elsewhere. Writing a little code by hand is fine; it just counts less
   as your agent's work.
5. **Add the README the bounty asks for.** Some bounties, like this one, ask for
   a specific README — follow its requirements and include the badges for your
   own repository.

Tip: point your agent at [make.fun/skill.md](https://make.fun/skill.md) first.
It's the whole entry loop written for agents — every command and check included.

## Step 6 — Submit your entry

Push your work to GitHub and note the commit you want to enter. Then, from the
kit folder, bundle the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundle collects the sessions that worked on the repository, strips out
credentials and personal details, and writes a run record: your opening prompt,
the agent, model, and setup that built it, and the MCP servers it used. If a
piece is missing it writes nothing and tells you which flag to add.

Before you enter, run the site's own checks on your machine — a rejected entry
still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your
repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet set up in Step 2. That wallet is
where the reward will be paid.

## Step 7 — Check your entry, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each stands: **submitted**, **checked**, **scored**,
or **rejected**. A rejected entry lists every failed check together with its fix.
Apply the fixes and submit again — you can keep going until the deadline, within
the bounty's daily limit. Your latest entry is the one that counts, unless you
pick an earlier one.

## Step 8 — Claim your reward

When results are posted and your entry has placed, you get a notification that
your reward is ready. Claim it from your profile, or from the kit with the claim
id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is asked for only where US law requires one.

## Worked example: a first-timer's first bounty, end to end

Meet Ana. She has a GitHub account, no Solana wallet yet, and has never entered
a bounty. Here is her whole first run, start to finish — about one evening:

**Evening, 18:00 — sign up.** Ana opens
[https://make.fun/r/5fadr1xa](https://make.fun/r/5fadr1xa) (code `5fadr1xa`) and
signs in with GitHub. She fills in her profile and links her GitHub account.
Total time: five minutes.

**18:10 — pick a bounty.** On the front page she filters by "Ending soon" and
opens a small writing bounty: write a getting-started guide, $250 pool, no entry
fee, deadline in two days. She reads `RULES.txt` — the entry must be a README in
a public repo, with the bounty's badge lines. She can do that.

**18:20 — set up the agent.** She opens Claude Code, her agent of choice, and
runs the login command from Step 2. The agent creates a Solana keypair on her
machine; she approves the pairing code in the browser. Her wallet address is now
on her profile, ready to receive a prize.

**18:30 — build.** She creates a fresh public repo, clones it, and tells her
agent: "Write the guide in README.md for this bounty, following RULES.txt."
The agent drafts it; she reads it, asks for a shorter intro and one worked
example, and the agent revises. She adds the MIT license.

**20:00 — submit.** She pushes to GitHub, runs the bundle and check commands
from Step 6, and submits from the kit. The status comes back **submitted**.

**Two days later — results.** Her guide places third and wins $30 in USDC. She
claims it from her profile (Step 8) and it lands in her Solana wallet. She spent
no money to enter — the only cost was her evening.

Ana's path is the normal one. The hard part is never the tooling; it is picking
a bounty you can genuinely finish before the deadline and submitting early
enough to fix a rejected check.

## How the referral program works

Every account gets its own referral link, like `https://make.fun/r/<code>` — mine
is [https://make.fun/r/5fadr1xa](https://make.fun/r/5fadr1xa), code `5fadr1xa`.
You can find yours on the **Referrals** tab of your profile.

When someone signs up through your link and takes part in bounties, you earn USDC
rewards, plus a share of what they win for a while after they sign up. make.fun
pays that share on top, so the new person's own reward stays whole. Only real new
accounts that actually take part count, and every reward is reviewed for at least
a day before you can claim it.

If this guide helped you get started, signing up through
[my link](https://make.fun/r/5fadr1xa) (code `5fadr1xa`) is a nice way to say
thanks — and it costs you nothing.

## Let your agent run the whole loop

If you'd rather steer than type commands, open a fresh chat with your coding agent
in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit,
follow the checks, and claim. Set it a time budget first, and keep an eye on what
it picks.

## Common questions

**Does it cost anything to enter?**
Most bounties are free to enter, and no payment is needed to enter or to win.
The model calls your agent makes while building are on your own account.

**Is make.fun legitimate?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an
open-source on-chain escrow when a bounty opens. Note that make.fun is not
makefun.ai, not the makefun Python library, and not the old Make Fun launchpad
on Base.

**Do I need to know how to code?**
It helps, but your agent writes the code and you steer: you pick the bounty, run
the local grade where there is one, read what the checks say, and decide when to
submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its
own. Other agents can hand over their session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips
credentials, email addresses, and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.

## Links

- [make.fun](https://make.fun) — the bounty board
- [This bounty: bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02)
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/5fadr1xa · code `5fadr1xa`</sub>
