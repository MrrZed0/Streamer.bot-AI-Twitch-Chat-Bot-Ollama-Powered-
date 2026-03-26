# 🤖 Streamer.bot AI Twitch Chat Bot (Ollama Powered)

A fully custom **AI Twitch Chat Bot** built for **Streamer.bot** that uses your **local Ollama AI server** instead of cloud APIs.

This bot responds like a real streamer, understands your channel context, and interacts naturally with chat.

---

## 🚀 Features

* 🧠 Uses **Ollama (local AI)** — no OpenAI, Gemini, or paid APIs required
* 🎮 Responds like a real **Twitch streamer (not an AI assistant)**
* 💬 Smart chat behavior:

  * No repetitive greetings
  * Matches chat energy
  * Natural, human-style replies
* 📅 Uses real-time data:

  * Stream title
  * Current game
  * Channel description
  * Date & time (`actionQueuedAt`)
* 👤 Viewer awareness:

  * Detects if user is following
  * Detects subscriber status
  * Affiliate / Partner awareness
* 📢 Auto follow reminder:

  * If viewer is **NOT following**, bot adds:

    > *"i see you are not following me yet dont forget to hit that follow button"*
* ✂️ Auto message splitting:

  * Splits long responses into **500 character chunks**
* 🧾 Chat memory:

  * Tracks users for 20 minutes to avoid spammy greetings

---

## 🖥 Requirements

* [Streamer.bot](https://streamer.bot/)
* [Ollama](https://ollama.com/)
* A local model installed (example):

```bash
ollama run gemma2:9b
```

---

## ⚙️ Setup

### 1. Install Ollama Model

Example:

```bash
ollama pull gemma2:9b
```

---

### 2. Set Ollama URL in Streamer.bot

Default used in script:

```text
http://192.168.2.58:11434/v1
```

Change this if needed using argument:

```
ollamaBaseUrl
```

---

### 3. Add C# Script to Streamer.bot

* Create a new **C# Inline Action**
* Paste the full script
* Trigger it using:

  * Twitch Chat Message
  * or command (ex: `@botname`)

---

### 4. Required Arguments

Make sure these are available in your action:

```
message
userName
broadcastUserName
streamTitle
game
```

---

### 5. Optional / Advanced Arguments

```
targetIsAffiliate
targetIsPartner
targetIsFollowing
targetIsSubscribed
createdAt
actionQueuedAt
```

---

### 6. Channel Bio (Recommended)

Set once using:

```csharp
CPH.SetGlobalVar("streamerChannelBio", "Your Twitch bio here", true);
```

---

## 💬 Sending Split Messages

The script outputs:

```
aiResponse1
aiResponse2
aiResponse3
aiResponse4
aiResponse5
aiResponseCount
```

### Example flow in Streamer.bot:

Send:

```
%aiResponse1%
```

Then add conditions:

If:

```
%aiResponseCount% >= 2
```

Send:

```
%aiResponse2%
```

Repeat for 3–5.

---

## 🧠 Personality System

Default personality:

```
streamer
```

Set it using:

```csharp
CPH.SetGlobalVar("smartbotPersonalityTwitch", "streamer", true);
```

### Behavior:

* Talks like a real streamer
* No “AI assistant” language
* No “How can I help you?”
* No robotic responses

---

## 🔥 Smart Behavior

### 👋 Greeting Logic

* First message in 20 mins → small greeting allowed
* Same user chatting → no repeated greetings

---

### 📢 Follow Reminder

Only triggers if:

```
targetIsFollowing == false
```

---

### 🧾 Chat Awareness

* Tracks recent users (20 min window)
* Prevents spammy repeated intros

---

### 📅 Time Awareness

Uses:

```
actionQueuedAt
```

Example AI awareness:

* "late night stream vibes"
* "weekend grind"
* "yo it's already March??"

---

## 🧪 Example Output

User:

```
@bot what game is this?
```

Bot:

```
@user yo this is some chaos right now 😂 been grinding this all stream
```

(Not robotic, no AI mention, fully natural)

---

## ⚠️ Notes

* This script uses `HttpClient`
* If your Streamer.bot C# environment throws errors:

  * You may need an alternative HTTP method (PowerShell or external script)

---

## 🚀 Future Upgrades (Ideas)

* 🎯 Time-of-day mood system (morning/night energy)
* 🎮 Game-specific personalities
* 🧠 Chat memory summaries
* 🔊 TTS integration
* 🎭 Dynamic streamer personality switching

---

## 💜 Credits

Built for Streamer.bot users who want:

* Full control
* No API costs
* Real streamer-style AI interaction

---

## ⭐ If you like this

Give it a ⭐ on GitHub and share it with other streamers!
