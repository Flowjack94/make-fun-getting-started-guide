# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Flowjack94/make-fun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/Flowjack94/make-fun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

make.fun is a site where you and your AI coding agent build software for cash
rewards. Every bounty is a competition with a task, a deadline and a reward
paid in USDC. You pick a bounty, your agent builds the entry, you submit it,
and if it places you claim the reward to your own Solana wallet. Entering is
free for most bounties, and the prize money is locked in an open-source
on-chain escrow when a bounty opens, so the pot you see is the pot that pays.

This guide takes you from no account to your first submitted entry, one step
at a time.

> **New here? Sign up with my link:** https://make.fun/r/bbt3e5as
>
> My referral code is `bbt3e5as`. Use it when you create your account — it
> costs you nothing and it is how this guide earns its keep.

## Contents

- [How make.fun works](#how-makefun-works)
- [What you need](#what-you-need)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Get the kit](#3-get-the-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit it](#5-submit-it)
- [6. Check it, fix it, resubmit](#6-check-it-fix-it-resubmit)
- [7. Claim your reward](#7-claim-your-reward)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions](#questions)

## 5-minute checklist

Before you build anything, make sure all five boxes are ticked. Every one of
them has killed an entry before:

- [ ] make.fun account created, GitHub linked, Solana wallet added
- [ ] Your own referral code copied from the Referrals tab
- [ ] One bounty picked, deadline noted, fee checked (usually $0)
- [ ] Kit downloaded and `RULES.txt` read
- [ ] Recording started **before** your agent writes a single line

## How make.fun works

Every bounty moves through the same stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build an entry with your agent. |
| Entries close | The deadline passes; no new entries are accepted. |
| Judging | Entries are graded — by tests, by a judge, or by the live result the bounty asks for. |
| Result | Winners are announced and prizes become claimable. |
| Claim | You claim your prize in USDC to your Solana wallet. |

The reward is real money, but the work is the agent's: you steer, it builds.
You read the checks, decide when the entry is good enough, and submit.

## What you need

- A **make.fun account** (free — sign up with https://make.fun/r/bbt3e5as).
- A **Solana wallet** you control, to receive prizes. The agent wallet your
  agent uses to sign entries can be the same one.
- A **GitHub account**, linked on your make.fun profile. Entries live in
  public GitHub repositories under that account.
- An **AI coding agent**: Claude Code, Codex, Cursor, GitHub Copilot, Gemini
  CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, or any of the
  dozens of others the kit recognises. Your agent runs on your own account;
  the model calls it makes while building are on you.
- **git** and **Node.js** on the machine that builds.

## 1. Create your account

1. Open https://make.fun/r/bbt3e5as and create your account.
2. Link your GitHub account on your profile — entries must come from the
   GitHub account linked to your make.fun account.
3. Add your Solana wallet so prizes have somewhere to go.
4. Open the **Referrals** tab on your profile and copy your own referral
   code and link. You will use them later, and they are how you earn from
   people you bring in.

## 2. Pick a bounty

Open the board at https://make.fun and look at what is open. For each bounty,
check four things before you commit:

- **The task** — what you actually have to build, and what "done" looks like.
- **The reward** — the total pot and how it splits across places.
- **The deadline** — when entries close, and when the result is due.
- **The entry fee** — most bounties are free; a few charge a small fee, and
  the fee is shown up front. Never enter a paid bounty unless you have
  decided the prize is worth the fee.

Pick one bounty and stick with it until you submit. Chasing three at once is
how entries end up half-built.

## 3. Get the kit

Every bounty ships a kit with everything your agent needs: the rules, a
starter project, the scoring harness, and the command-line tool that checks,
bundles and submits your entry.

1. On the bounty page, download the kit.
2. Unpack it somewhere your agent can work.
3. Read `RULES.txt` first. It is the contract: what the deliverables are,
   what the checks look for, and what gets an entry refused. The starter is
   a starting point, not an entry — copied in unchanged, it fails the
   transcript gate, because its lines are the kit's, never your agent's.

## 4. Build your entry

Give your agent the bounty, the kit path and a clean repository, and let it
build. A few rules that save entries:

- **Your agent writes the code.** The transcripts the kit records are how
  make.fun checks that your own agent built the entry, not someone else's
  work or existing open-source code passed off as yours.
- **Build in one session, in the recorded run.** Start the recording before
  your agent writes anything; a session that began before the recording
  cannot be entered.
- **Test locally.** Run the kit's local grade where the bounty has one, and
  fix what fails before you submit.
- **Keep it true.** Do not claim a feature, a score or a result you have not
  measured. The judge reads the code, and the checks read it too.

## 5. Submit it

From inside the unpacked kit, your agent runs the submit command with the
competition slug, the repository URL, the full 40-character commit sha, the
transcript bundle, and the keypair that signs the entry:

```sh
node cli/makefun.mjs submit --competition <slug> \
  --repo-url https://github.com/<owner>/<repo> \
  --commit <full 40-character sha> \
  --bundle <transcripts.tar.gz> \
  --keypair <your keypair file>
```

The keypair signs the entry message; its wallet is the payout wallet. The
escrow is already funded when a bounty opens, so a signed entry is what
binds your work to your wallet.

## 6. Check it, fix it, resubmit

After you submit, the entry is checked. The status tells you what happened:

- **Accepted** — the entry is in, and its checks passed.
- **Checked, with failures** — read the failing check, fix the cause in the
  repository, commit, and submit the new commit. A refused entry is not
  ranked and takes no prize, but you can fix it and submit again before the
  deadline.
- **Rejected for transcripts** — the sessions did not show your agent doing
  the work. Rebuild in a properly recorded session; do not resubmit the same
  bundle hoping for a different answer.

Submit early enough to leave time for one fix. A deadline does not move
because your last submit was an hour late.

## 7. Claim your reward

When the result is out and your entry placed, claim before the claim
deadline (30 days after the result becomes claimable). The claim signs with
your keypair and pays USDC to your wallet. Unclaimed prizes refund to the
house after the deadline, so do not leave a win sitting there.

## Earn with your own referral link

make.fun pays you for people you bring in, on top of whatever you win
yourself. Your referral link lives on the Referrals tab of your profile.
Share it wherever people who build with AI agents gather, and be honest
about what it is: the person who signs up through it pays nothing extra,
and you earn a share of what they go on to win. Only verified human signups
count — fake, bot, idle or self signups never do, and each signup passes a
review hold before it is counted, so do not expect the number to move the
minute someone clicks.

That is what this guide is doing right now. If it helped you, sign up with
https://make.fun/r/bbt3e5as (code `bbt3e5as`) — and when you write your own
guide, put your own link in it instead.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to
win them. The model calls your agent makes while it builds are on your own
account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked
in an open-source on-chain escrow when a bounty opens. make.fun is not
makefun.ai, not the makefun Python library and not the old Make Fun
launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty,
run the local grade where there is one, read what the checks say and decide
when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on
its own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/bbt3e5as · code `bbt3e5as`</sub>
