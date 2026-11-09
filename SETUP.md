# Disclosure Day: standalone version with a live class leaderboard

Players need no Claude or Google account. Each browser signs in anonymously in the background, and the class leaderboard lives in a free Firebase project you own.

Files in this folder:
- `index.html`: the whole game. The only thing to change is the `FIREBASE_CONFIG` block near the top of the script.
- `firestore.rules`: the database security rules to paste into Firebase.

## 1. Create the Firebase project (about 10 minutes, free)

1. Go to https://console.firebase.google.com and sign in with any Google account.
2. Click **Create a project**, name it (e.g. `disclosure-day`), and turn **Google Analytics off**. Create it.
3. **Turn on anonymous sign-in:** left menu **Build → Authentication → Get started → Sign-in method → Anonymous → Enable → Save**.
4. **Create the database:** **Build → Firestore Database → Create database**. Choose **production mode**, location **asia-southeast1 (Singapore)**, then **Create**.
5. **Add the security rules:** in Firestore, open the **Rules** tab, delete what is there, paste the whole of `firestore.rules`, and click **Publish**.
6. **Get the web config:** click the gear icon → **Project settings → General**. Under **Your apps**, click the **Web** icon (`</>`), give it a nickname, leave Hosting unticked, and click **Register app**. Copy the `firebaseConfig = { ... }` values it shows.

## 2. Paste the config into the game

Open `index.html` in any text editor (Notepad works), find the block that starts `const FIREBASE_CONFIG = {`, and replace each `PASTE...` value with yours. Save.

These values are meant to be public: anyone who loads a Firebase web app can see them. The security comes from the rules in step 5, which only let each player write their own row with scores the game can produce.

## 3. Put the game online

Pick one:

- **GitHub Pages (free, permanent):** create a public repository, upload `index.html`, then **Settings → Pages → Deploy from a branch → main / (root) → Save**. After a minute the game is at `https://<your-username>.github.io/<repo-name>/`.
- **Netlify Drop (free, fastest):** sign up at https://app.netlify.com, then drag this whole folder onto https://app.netlify.com/drop. You get a link like `https://<random-name>.netlify.app`.

Then in Firebase go to **Authentication → Settings → Authorized domains → Add domain** and add your site's domain (e.g. `your-username.github.io` or `random-name.netlify.app`).

## 4. Run it in class

- Share the game link. Players open it on a phone or laptop and play (about 5 minutes).
- On the projector, open the same link and click the **Live leaderboard** tab (or add `#live` to the link). It ranks firms by cash and updates as each player closes their quarter.
- When everyone has finished, click **Reveal: social welfare**.

## Clearing the board between classes

In the Firebase console, open **Firestore Database → Data**, click the `scores` collection's menu (three dots) and choose **Delete collection**. Each browser keeps one row, so a player who replays replaces their own earlier score.

## Limits

The free Spark plan allows 50,000 reads and 20,000 writes a day, far more than a class needs. A player who clears their browser data gets a new anonymous ID and could post a second row.
