# AGENTS.md

Delight — a gesture-based table-projection dining-experience prototype
(Create React App, `react-scripts`). It uses React Router, framer-motion, and
react-three-fiber, with a Firebase Realtime Database backend. Standard commands
are in `README.md`: `npm install`, then `npm start` (dev server on port 3000).

## Cursor Cloud specific instructions

`node_modules` is installed by the startup update script (`npm install
--prefix repos/delighting`).

- Start the dev server headless: `BROWSER=none PORT=3000 npm start` (from the
  repo root). It compiles with ESLint warnings only ("webpack compiled with 1
  warning"); that is the effective lint gate for the app.
- The home route `/` (`Recognize`) is gesture/presence driven and polls Firebase
  for a table's `people` count; with no webcam and no Firebase write it just
  shows "시작" and waits. To exercise the experience without a camera, navigate
  routes directly (`/manual`, `/intro`, `/mood`, `/order`) or use the keyboard
  shortcuts wired in `App.js`: `i`→intro, `m`→manual, `o`→order, `1`→questions.
  The glowing ring following the cursor is the app's custom `Pointer`, not a bug.
- Firebase config (`src/firebase.js`) reads `REACT_APP_*` env vars for
  apiKey/auth/etc. but hard-codes `databaseURL`. Without those env vars the app
  still renders; only live Realtime DB reads/writes are unavailable, so
  presence-triggered auto-navigation on `/` won't fire (navigate manually).
- Standalone `eslint src` reports 3 pre-existing errors in legacy files not in
  the build graph (`src/components/Relation/Person.js`,
  `src/routes/Mood/Picnic.js`); they don't affect `npm start`. Do not treat
  these as setup breakage.
