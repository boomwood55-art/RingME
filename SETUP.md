# RingMe: your personal to-do list that calls you

Just for you: no subscription, no ads, no credit card.

- **Your Google Calendar shows up as a to-do list** automatically.
- **Tap the circle** next to a task to tick it off. ✓
- **Write a task in the app** and it goes **straight into your Google Calendar**.
  When you tick it off, it shows up as "✓ Task name" in Google Calendar too.
- **When it's time, your phone rings like a call.** Answer it, and RingMe tells you what to do
  (it reads it out loud, or plays a voice message someone recorded for you).
  Tap **"Done, tick it off"** and it's checked off your list.

---

## Step 1: Put the app online (free, about 5 minutes)

Your phone needs an `https://` web address to install the app. GitHub Pages gives you one for free.

1. Make a free account at **github.com**.
2. Click **+ → New repository**, name it `ringme`, set it to **Public**, and click **Create**.
3. Click **"uploading an existing file"**, then drag in **everything inside the `ringme` folder**
   (`index.html`, `sw.js`, `manifest.webmanifest`, `SETUP.md`, and the `icons` folder). Click **Commit**.
4. Go to **Settings → Pages**. Under *Branch*, pick `main` and `/ (root)`, then click **Save**.
5. After about a minute your app is live at `https://YOUR-GITHUB-NAME.github.io/ringme/`

> Another option: **Netlify** (app.netlify.com/drop) lets you drag the folder in. It's also free and needs no card.

---

## Step 2: Get your free Google "Client ID" (about 10 minutes)

This lets the app read your calendar and add the tasks you write. Google Cloud does **not**
ask for a card for this.

1. Open **console.cloud.google.com** and sign in with the Google account that has your calendar.
2. At the top, click the project picker, then **New project**. Name it `RingMe` and click **Create**.
3. Go to **APIs & Services → Library**, search **Google Calendar API**, and click **Enable**.
4. Go to **APIs & Services → OAuth consent screen** (also called *Google Auth Platform*):
   - App name: `RingMe`. Use your email for both email fields.
   - Audience: **External**.
   - Under **Test users**, add **your own Gmail address**. Only you will be able to use it, which is what you want.
5. Go to **APIs & Services → Credentials → Create credentials → OAuth client ID**:
   - Application type: **Web application**
   - **Authorized JavaScript origins**: add `https://YOUR-GITHUB-NAME.github.io`
     (only the part before `/ringme`, with no slash at the end)
   - Click **Create** and copy the **Client ID**. It ends in `.apps.googleusercontent.com`.

---

## Step 3: Install it on your phone

**Android (recommended)**
1. Open your app link in **Chrome**.
2. Tap **⋮ → Add to Home screen → Install**. It now has its own icon, like a normal app.
3. Open RingMe. The **setup screens** walk you through everything:
   1. **Welcome:** tap **Get started**.
   2. **Connect Google Calendar:** paste your **Client ID** and tap **Connect Google Calendar**.
      The screen also shows the exact address to add in Google Cloud, with a **Copy** button.
      - You'll see "Google hasn't verified this app". That's normal for your own private app.
        Tap **Continue**.
      - **Tick both calendar boxes.** One lets RingMe see your calendar, and the other lets it
        add the tasks you write.
   3. **Let RingMe call you:** tap **Allow** (notifications) and **Test ring**.
   4. **Bonus: Claude:** optional (see below). Tap **Start using RingMe**.
4. To see the setup screens again: **Settings → Show setup steps again**.

**iPhone:** open the link in **Safari**, tap **Share → Add to Home Screen**, then open it from the
icon (notifications only work this way, on iOS 16.4 or newer). Android works more reliably.

---

## Using it

| You want to… | Do this |
|---|---|
| Add a task | Type it at the top, pick a day, and optionally a time. Tap **Add**. |
| Get a call for it | Give it a **time**. Tasks without a time go on the list but don't call you. |
| Save it to Google Calendar | Nothing to do: once connected, **every task you write goes to Google Calendar automatically**. If you're offline, it shows "⏳ Waiting for Google" and uploads on the next sync. |
| Tick a task off | Tap the **circle** on the left. Tap it again to undo. |
| Stop a calendar event from calling you | Tap the **🔔** on the right so it shows as crossed out. |
| Add a note or voice message | Tap the task's name. |
| Get calls earlier | **Settings → Call me → 10 minutes before** (or another option). |
| See new events from Google | Tap **Sync**. It also syncs by itself every 15 minutes while you're signed in. |

Google only keeps a browser app signed in for about an hour at a time, so you'll tap **Sync**
about once a day. Tasks you already have still call you when you're signed out or offline.

---

## Bonus: add tasks by talking to Claude

If Claude is connected to your Google Calendar, you can just tell Claude what to schedule.
It goes into Google Calendar, and RingMe picks it up and calls you.

1. Install the free **Claude** app (Play Store or App Store) and sign in.
2. In Claude, open **Settings → Connectors**, find **Google Calendar**, and tap **Connect**.
   Use the **same Google account** as RingMe. If your phone app doesn't show this, do it
   once at **claude.ai** on a computer. It then works on your phone too.
3. In a chat, say something like:
   > "Add 'Take vitamins' to my calendar today at 6 pm."
4. Open RingMe and tap **Sync**. The task shows up, and RingMe calls you at 6 pm.

> Why RingMe still needs its own Google permission (Step 2): Claude's connection to your calendar
> belongs to your Claude account, and other apps can't borrow it. RingMe needs its own permission
> to read your calendar and to save the tasks you type into it.

---

## ⚠️ One limit to know

Web apps are **not allowed to wake up a phone by themselves** once they are fully closed.
That's a rule of phone browsers, not a bug in RingMe.

- ✅ **RingMe open, even with the screen off or another app in front:** it rings.
- ✅ **Most reliable:** turn on **Keep screen awake** and leave RingMe open while the phone charges.
- ❌ **Swiped away:** no call until you open it again. A call missed by up to 15 minutes rings as soon as you open the app.

On Android, also go to **Settings → Apps → Chrome → Battery → Unrestricted**. This helps the
app keep running in the background.
