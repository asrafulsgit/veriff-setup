# 🔐 Veriff Identity Verification Integration (React + Node.js)

---

## ✅ Complete Process (Start to Finish)

### 1. 🚀 Sign up for Veriff
- After signing up, get your **API key** from the Veriff dashboard.

---

### 2. 🛠️ Set Up Your Backend (Node.js + Express)
- Create a `POST` API endpoint:  
  `Ex: POST /api/veriff/session`
- Use Veriff’s API to **create a session** and return the `session.url` to the frontend.
- Make sure to **keep your Veriff API key private** and use it only in the backend.

---

### 3. 📦 Install Veriff SDK in Your React App
```bash
npm install @veriff/js-sdk
```

### 4. Call your backend from React
- Send a request from your React app to:
  `POST /api/veriff/session`
- Your backend will respond with the session.url.

### 5. Initialize and mount Veriff SDK in React
- Use the received session.url to initialize Veriff in a div container using the SDK:
```
import Veriff from '@veriff/js-sdk';

const veriff = Veriff({
  host: 'https://stationapi.veriff.com',
  parentId: document.getElementById('veriff-container'),
  onSession: (err, response) => {
    if (err) console.error(err);
    else console.log('Verification complete:', response);
  },
});

veriff.setSessionURL(sessionUrl);
veriff.mount();
```

### 6. User completes verification
- Veriff shows the camera and ID upload interface to the user in the browser.
- The user goes through the full verification flow (document + selfie).
  
### 7. (Optional) Handle verification result
- You can provide a callback URL when creating the session (from the backend).
- Alternatively, set up webhooks in the Veriff dashboard to receive real-time status updates like:
  - approved
  - declined
  - resubmission_requested

### 8. Check status of the verification (if needed)
- Use Veriff’s API to query the session status manually by session ID.
- This is helpful if you're not using webhooks or need to re-check results.
