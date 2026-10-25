FREE_BOL COMPLETE UPDATE PACKAGE
================================

WHAT IS INCLUDED
- index.html: current Free_bol frontend with existing chat features plus 25 MB file attachment flow and configured FreebolBot hook.
- backend/: server-side FreebolBot endpoint, Firebase Admin SDK, room presence heartbeat, rate limit, and environment template.
- database.rules.json and storage.rules: example rules to review before deploying.

FEATURES ALREADY IN THE FRONTEND
- Public rooms and user-created rooms
- Anonymous sign-in and realtime messages
- Online presence, status, avatar/emoji, typing indicator
- Buddies and private chats
- Emoji picker, text emoticons, buzz
- Translation / translation suggestions
- Photo messages
- Voice/video calling (requires working Firebase rules and HTTPS)
- Message reporting and invite/share links
- 25 MB Firebase Storage file uploads with progress
- FreebolBot integration (requires deploying backend and setting its URL)

IMPORTANT LIMITATIONS
This package cannot be live on GitHub Pages until you upload/commit the frontend and configure Firebase. I cannot push to your GitHub repository from this chat. A static HTML page cannot safely host an AI API key; the backend is required. The bot heartbeat is active only while its backend service is running. File uploads require Firebase Storage enabled and matching Storage rules. Review and test all rules before production; public-room messages are readable by signed-in users and private chats are not end-to-end encrypted.

ONE-TIME SETUP
1. Extract this ZIP.
2. In GitHub repo https://github.com/freemartindia-source/freebol, replace the existing root index.html with this package's index.html and commit to main. Do not upload it only as index_updated.html.
3. In Firebase Console for project freebol-f779c, enable Authentication > Sign-in method > Anonymous and enable Storage.
4. Review database.rules.json and storage.rules. In Firebase Console > Realtime Database > Rules, merge the message type=file fields into your current rules (do not blindly overwrite existing call/report/profile rules). Publish the rules. In Storage > Rules, apply/review storage.rules.
5. Deploy backend/ to a Node.js host (Render Web Service is one option). Root directory: backend. Build command: npm install. Start command: npm start. Use Node 20+.
6. Add these environment variables in the backend host:
   - OPENAI_API_KEY = your server-side API key (secret; never put in GitHub/frontend)
   - OPENAI_MODEL = gpt-4.1-mini (or a model enabled for your API account)
   - FIREBASE_DATABASE_URL = https://freebol-f779c-default-rtdb.asia-southeast1.firebasedatabase.app
   - FIREBASE_SERVICE_ACCOUNT_JSON = complete service-account JSON for the Firebase project, pasted as a single-line JSON value
7. Ensure the service account is from project freebol-f779c and has permissions to access Authentication and Realtime Database. Keep this value secret.
8. Once deployed, open https://YOUR-SERVICE.onrender.com/health. It should return ok:true and configured:true.
9. In root index.html, replace https://YOUR-RENDER-SERVICE.onrender.com/bot with your actual HTTPS backend URL ending in /bot. Commit this change.
10. Wait for GitHub Pages deployment; hard refresh with Ctrl+Shift+R. Test in two browsers: text chat, private chat, photo, 25 MB file, and bot reply when alone in a public room.

RULES NOTE
The included database.rules.json is an illustrative baseline, not a guaranteed drop-in replacement for every existing feature/rule in your Firebase project. Compare it with your currently deployed rules before publishing. The current frontend sends type=file messages; rules that only allow msg/buzz/img will reject them. Storage uploads will fail until Storage is enabled and rules permit authenticated users to upload/read only their allowed paths.
