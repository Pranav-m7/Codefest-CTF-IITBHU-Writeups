# IIT BHU Codefest CTF - Sanity Check Writeup (Misc)

![Category](https://img.shields.io/badge/Category-Misc-purple)
![Difficulty](https://img.shields.io/badge/Difficulty-Trivial-brightgreen)
![Points](https://img.shields.io/badge/Points-50--100-success)
![Platform](https://img.shields.io/badge/Platform-Discord-5865F2)

---

## 📋 Table of Contents

- [Quick Info](#-quick-info)
- [Challenge Description](#-challenge-description)
- [What is a Sanity Check?](#-what-is-a-sanity-check)
- [Solution Walkthrough](#-solution-walkthrough)
- [Flag](#-flag)
- [Key Takeaways](#-key-takeaways)
- [Discord Bot Commands](#-discord-bot-commands)

---

## 📊 Quick Info

| **Attribute**       | **Details**                                      |
|---------------------|--------------------------------------------------|
| **CTF Name**        | IIT BHU Codefest CTF                             |
| **Challenge**       | Sanity Check                                     |
| **Category**        | Misc (Miscellaneous)                             |
| **Difficulty**      | Trivial                                          |
| **Points**          | 50-100 (typical for sanity checks)               |
| **Keywords**        | CTF Walkthrough, Discord Bot, Sanity Check, Slash Commands, Server Verification |
| **Platform**        | Discord                                          |
| **Objective**       | Join the Discord server and interact with the bot |

---

## 🎯 Challenge Description

> **"Are you sane?"**

**Provided:** A Discord invitation link

This is a classic **Sanity Check** challenge—a warm-up designed to ensure participants can access the CTF's communication platform and interact with automated systems.

---

## 🧠 What is a Sanity Check?

### Purpose

Sanity Check challenges serve multiple purposes in CTFs:

1. **Platform Verification** - Ensure participants can access communication channels
2. **Bot Testing** - Verify that automated systems are working correctly
3. **Onboarding** - Familiarize players with the CTF infrastructure
4. **Free Points** - Give everyone an easy first solve to boost morale

### Characteristics

- **Trivial Difficulty** - Designed to be solved by everyone
- **No Technical Skills Required** - Simple interaction, no exploitation
- **Quick Solve** - Usually takes less than 5 minutes
- **High Solve Count** - Often the most-solved challenge in a CTF

> **CTF Tip:** Always start with Sanity Check challenges. They're free points and help you understand the flag format!

---

## 🛠️ Solution Walkthrough

### Step 1: Reconnaissance

Upon clicking the challenge link, I was redirected to the **official Codefest CTF Discord server**.

**Initial Observations:**

Entering the server, I immediately noticed:
- High volume of activity in the landing channel
- Other participants spamming various slash commands
- Multiple people interacting with the server's bot

**Chat Log Activity:**
```
User1: /sane
User2: /verify
User3: /flag
User4: /sane
User5: /verify
...
```

![Discord Server Activity](./assets/discord_activity.png)

**Analysis:**
- The challenge title "Are you sane?" hints at a `/sane` command
- Standard Discord verification often uses `/verify`
- CTF bots commonly respond to `/flag` commands
- The crowd behavior suggested trying multiple commands

---

### Step 2: Interaction

**Reasoning:**

This was clearly a standard **Sanity Check** challenge designed to:
1. Ensure players could join the communication platform
2. Test interaction with the Discord bot
3. Familiarize participants with slash commands

**Strategy:**

I decided to follow the crowd's behavior and attempt common Discord bot commands.

**Commands Attempted:**

```
/flag
/verify
/sane
```

**Why These Commands?**

| Command | Rationale |
|---------|-----------|
| `/flag` | Standard CTF bot command for retrieving flags |
| `/verify` | Common Discord verification mechanism |
| `/sane` | Directly related to challenge description "Are you sane?" |

---

### Step 3: The Trigger

While I am not 100% certain which specific command successfully triggered the response (as I was trying multiple variations in quick succession), one of them executed successfully.

**Most Likely Candidates:**

1. **`/sane`** - Given the challenge description "Are you sane?"
2. **`/verify`** - Standard Discord server verification function

**Bot Response:**

The Discord bot responded immediately with the flag.

**Response Method:**
- Likely via an **ephemeral message** (visible only to me)
- Or via **Direct Message (DM)** from the bot
- Ensures each participant gets their own flag confirmation

![Bot Response](./assets/bot_response.png)

---

### Step 4: Flag Retrieval

The bot's response contained the **cleartext flag** with no additional decoding or manipulation required.

**Flag Format:**
```
CodefestCTF{...}
```

**Flag Content:**
```
CodefestCTF{w3lcome_70_cod3f3s7}
```

**Flag Meaning:**
- `w3lcome` = "welcome" (leetspeak)
- `70` = "to" (leetspeak)
- `cod3f3s7` = "codefest" (leetspeak)
- Translation: **"Welcome to Codefest"**

---

## 🚩 Flag

```
CodefestCTF{w3lcome_70_cod3f3s7}
```

---

## 💡 Key Takeaways

> **What We Learned:**

### CTF Fundamentals

**1. Sanity Checks Are Essential**
- Always start with sanity check challenges
- They provide free points and confirm flag format
- Help you understand the CTF infrastructure

**2. Follow the Crowd (Sometimes)**
- In sanity checks, observing other participants' behavior is valid
- Community activity often hints at the solution
- Don't overthink trivial challenges

**3. Discord Bot Interaction**
- Modern CTFs often use Discord for communication
- Bots automate flag distribution and verification
- Slash commands (`/command`) are the standard interaction method

**4. Leetspeak in Flags**
- CTF flags often use leetspeak (1337 speak)
- Common substitutions: `3` = E, `7` = T, `0` = O, `1` = I
- Understanding leetspeak helps verify flag correctness

### Discord Bot Commands

**Common CTF Discord Bot Commands:**

| Command | Purpose | Example |
|---------|---------|---------|
| `/flag` | Retrieve challenge flag | `/flag sanity` |
| `/verify` | Verify server membership | `/verify` |
| `/sane` | Sanity check command | `/sane` |
| `/help` | List available commands | `/help` |
| `/submit` | Submit flag for verification | `/submit CodefestCTF{...}` |
| `/scoreboard` | View current standings | `/scoreboard` |

---

## 🧰 Tools & Platforms

### Required

| Tool | Purpose |
|------|---------|
| **Discord Account** | Access to the CTF server |
| **Web Browser / Discord App** | Interface for server interaction |

### Optional

| Tool | Purpose |
|------|---------|
| **Discord Developer Mode** | View message IDs, debug bot interactions |
| **Screenshot Tool** | Document bot responses |

---

## 📂 Repository Structure

```
.
├── assets/
│   ├── discord_invite.png     # Discord invitation screenshot
│   ├── discord_activity.png   # Server activity screenshot
│   └── bot_response.png       # Bot flag response screenshot
└── README.md                  # This writeup
```

---

## 🎓 Discord CTF Best Practices

### For Participants

**Do:**
- ✅ Join the Discord server immediately
- ✅ Read the rules and announcements channels
- ✅ Enable notifications for important channels
- ✅ Use slash commands to interact with bots
- ✅ Ask questions in designated help channels

**Don't:**
- ❌ Spam commands excessively (may get rate-limited)
- ❌ Share flags publicly in channels
- ❌ Harass other participants or organizers
- ❌ Use automated scripts to spam the bot

### Understanding Bot Responses

**Ephemeral Messages:**
- Only visible to you
- Disappear when you refresh/restart Discord
- Used for personal information like flags

**Direct Messages (DMs):**
- Private messages from the bot
- Permanent record of your interaction
- Check your DM inbox if you don't see a response

**Public Responses:**
- Visible to everyone in the channel
- Usually for general information
- Flags are rarely distributed this way

---

## 🔍 Troubleshooting

### Common Issues

**Problem:** Bot doesn't respond to commands

**Solutions:**
1. Check if you have the correct permissions
2. Verify you're in the right channel
3. Ensure the bot is online (green status)
4. Try the command again after a few seconds
5. Check your DMs for a response

**Problem:** Can't find the flag after bot response

**Solutions:**
1. Check for ephemeral messages (look for "Only you can see this")
2. Check your Discord DMs
3. Try the command again
4. Ask in the help channel

**Problem:** Command not recognized

**Solutions:**
1. Use slash commands (`/command`) not text commands (`!command`)
2. Type `/` to see available commands
3. Check the announcements for correct command syntax

---

## 📜 License

This writeup is licensed under the [MIT License](../LICENSE).

---

## 🙏 Acknowledgments

- **IIT BHU Codefest CTF** organizers for the welcoming sanity check
- The Discord community for the collaborative atmosphere
- Bot developers for smooth automation

---

## 🎉 Fun Facts

### Leetspeak Decoder

The flag `w3lcome_70_cod3f3s7` uses common leetspeak substitutions:

| Leetspeak | Character | Reason |
|-----------|-----------|--------|
| `3` | E | Resembles the letter E |
| `7` | T | Resembles the letter T |
| `0` | O | Resembles the letter O |

**Full Translation:**
```
w3lcome_70_cod3f3s7
↓
welcome_to_codefest
```

### Why "Sanity Check"?

The term comes from software engineering:
- **Sanity Test:** A quick test to verify basic functionality
- **Smoke Test:** Similar concept—"does it catch fire when turned on?"
- In CTFs: Ensures the infrastructure works before complex challenges

---

**Welcome to Codefest! 🎉**

[← Back to Main Index](../README.md)

---

## 💬 Community Tips

> **From experienced CTF players:**

- "Always do the sanity check first—it confirms the flag format!"
- "If the bot doesn't respond, wait 30 seconds and try again. Rate limiting is real."
- "Screenshot the flag immediately. Ephemeral messages disappear!"
- "Join the Discord early. Announcements often contain hints for other challenges."

---

**Remember:** Every CTF journey starts with a single sanity check. Welcome to the community! 🚀
