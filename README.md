<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MyDocKey</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Inter', sans-serif; }
    body {
      background: linear-gradient(135deg, #4f46e5, #3b82f6);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 1rem;
    }
    .card {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(12px);
      border-radius: 20px;
      padding: 2rem;
      width: 100%;
      max-width: 450px;
      text-align: center;
      box-shadow: 0 8px 30px rgba(0,0,0,0.2);
      color: white;
      animation: fadeIn 0.4s ease-out forwards;
    }

    /* Custom CSS Logo */
    .logo-container {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 10px;
      margin-bottom: 1rem;
    }
    .doc-icon {
      width: 24px; height: 28px;
      border: 2px solid #fff;
      border-radius: 3px;
      position: relative;
    }
    .doc-icon::before {
      content: "";
      position: absolute;
      width: 12px;
      height: 2px;
      background: white;
      top: 6px;
      left: 4px;
      border-radius: 1px;
      box-shadow: 0 6px white, 0 12px white;
    }
    .lock-icon {
      width: 20px; height: 20px;
      border: 2px solid #10b981;
      border-radius: 4px;
      position: relative;
      background: rgba(16, 185, 129, 0.2);
    }
    .lock-icon::before {
      content: "";
      position: absolute;
      top: -8px;
      left: 4px;
      width: 8px;
      height: 8px;
      border: 2px solid #10b981;
      border-radius: 50%;
    }
    .logo-text {
      font-size: 1.5rem;
      font-weight: 700;
      letter-spacing: 0.5px;
    }

    p.subtitle { font-size: 0.9rem; margin-bottom: 1rem; opacity: 0.85; }

    .tabs {
      display: flex;
      justify-content: center;
      background: rgba(255,255,255,0.15);
      border-radius: 12px;
      margin-bottom: 1.5rem;
      overflow: hidden;
    }
    .tab {
      flex: 1;
      padding: 0.7rem;
      cursor: pointer;
      font-weight: bold;
      transition: 0.3s;
    }
    .tab.active { background: white; color: #2563eb; }
    .tab-content { display: none; }
    .tab-content.active { display: block; }

    input, button {
      width: 100%;
      padding: 0.8rem;
      margin-bottom: 0.8rem;
      border: none;
      border-radius: 12px;
      font-size: 1rem;
    }
    input { background: rgba(255, 255, 255, 0.85); color: black; }
    button { background: white; color: #2563eb; font-weight: bold; cursor: pointer; transition: 0.2s; }
    button:hover { background: #f3f4f6; }

    a.download-btn {
      display: inline-block;
      margin-top: 1rem;
      padding: 0.8rem 1rem;
      background: white;
      color: #2563eb;
      font-weight: bold;
      border-radius: 12px;
      text-decoration: none;
    }

    .helpdesk { font-size: 0.8rem; margin-top: 0.8rem; color: #e0e7ff; opacity: 0.85; }
    .credit { font-size: 0.65rem; opacity: 0.6; margin-top: 0.5rem; }

    .toast {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: white;
      color: black;
      padding: 10px 15px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      display: none;
    }
    .toast.show { display: block; }

    /* Popup */
    .popup-overlay {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0,0,0,0.6);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 99999; /* Make sure it's clickable and on top */
    }
    .popup-box {
      background: white;
      color: black;
      max-width: 500px;
      padding: 2rem;
      border-radius: 16px;
      text-align: center;
      box-shadow: 0 8px 20px rgba(0,0,0,0.3);
      animation: fadeIn 0.3s ease;
    }
    .popup-box h2 { margin-bottom: 1rem; color: #2563eb; }
    .popup-box p { font-size: 0.95rem; margin-bottom: 1rem; color: #374151; line-height: 1.5; }
    .popup-box button {
      background: #2563eb;
      color: white;
      border: none;
      padding: 0.7rem 1.5rem;
      border-radius: 12px;
      cursor: pointer;
      font-weight: bold;
    }

    @keyframes fadeIn { from {opacity: 0; transform: scale(0.95);} to {opacity: 1; transform: scale(1);} }
  </style>
</head>
<body>

  <!-- Popup -->
  <div class="popup-overlay" id="welcome-popup">
    <div class="popup-box">
      <h2>Welcome to MyDocKey 🔐</h2>
      <p>My name is Shubham (BCA student) and I built this platform to help students securely upload and access their files anywhere — without needing Gmail or sharing personal information.</p>
      <p>Your privacy is my top priority: your documents are encrypted and stored securely, and even I (the developer) cannot access them.</p>
      <p>Just remember your username & password to access your documents anytime until they expire.</p>
      <button onclick="closePopup()">Got it!</button>
    </div>
  </div>

  <!-- Main Card -->
  <div class="card">
    <div class="logo-container">
      <div class="doc-icon"></div>
      <div class="lock-icon"></div>
      <div class="logo-text">MyDocKey</div>
    </div>

    <p class="subtitle">Securely upload & access your files — no Gmail login required.</p>

    <div class="tabs">
      <div class="tab active" onclick="showTab('upload')">Upload</div>
      <div class="tab" onclick="showTab('download')">Download</div>
    </div>

    <!-- Upload Tab -->
    <div class="tab-content active" id="upload">
      <input id="username" type="text" placeholder="Choose username" required>
      <input id="password" type="password" placeholder="Set password" required>
      <input id="file" type="file" required>
      <label for="expiry">Select Expiry Date</label>
      <input id="expiry" type="date" required>
      <button onclick="uploadFile()">Upload</button>
    </div>

    <!-- Download Tab -->
    <div class="tab-content" id="download">
      <input id="dl-username" type="text" placeholder="Enter username" required>
      <input id="dl-password" type="password" placeholder="Enter password" required>
      <button onclick="downloadFile()">Download</button>
      <div id="download-link"></div>
    </div>

    <p class="helpdesk">Helpdesk: <a href="mailto:helpdesk.mydockey@yahoo.com" style="color:#fff; text-decoration: underline;">helpdesk.mydockey@yahoo.com</a></p>
    <p class="credit">Created by Shubham (BCA student)</p>
  </div>

  <div id="toast" class="toast"></div>

  <!-- Firebase & Script -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import { getFirestore, doc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";
    import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-storage.js";

    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT_ID.appspot.com",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    const storage = getStorage(app);

    async function uploadFile() {
      const username = document.getElementById("username").value.trim();
      const password = document.getElementById("password").value.trim();
      const fileInput = document.getElementById("file");
      const expiry = document.getElementById("expiry").value;

      if (!username || !password || !fileInput.files.length || !expiry) {
        showToast("⚠️ Please fill all fields.");
        return;
      }

      const file = fileInput.files[0];
      const fileRef = ref(storage, `uploads/${username}_${file.name}`);
      await uploadBytes(fileRef, file);

      await setDoc(doc(db, "users", username), {
        password: btoa(password),
        filePath: `uploads/${username}_${file.name}`,
        fileName: file.name,
        expiry: expiry
      });

      showToast("✅ File uploaded! Auto-deletes after " + expiry);
    }

    async function downloadFile() {
      const username = document.getElementById("dl-username").value.trim();
      const password = document.getElementById("dl-password").value.trim();

      if (!username || !password) {
        showToast("⚠️ Enter username & password.");
        return;
      }

      const docRef = doc(db, "users", username);
      const docSnap = await getDoc(docRef);

      if (!docSnap.exists()) {
        showToast("❌ No file found.");
        return;
      }

      const data = docSnap.data();
      if (btoa(password) !== data.password) {
        showToast("❌ Incorrect password.");
        return;
      }

      const today = new Date().toISOString().split("T")[0];
      if (data.expiry < today) {
        showToast("⏳ File expired.");
        return;
      }

      const fileURL = await getDownloadURL(ref(storage, data.filePath));
      document.getElementById("download-link").innerHTML =
        `<a class="download-btn" href="${fileURL}" download="${data.fileName}">⬇ Download File</a>`;
    }

    function showTab(tab) {
      document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      document.querySelector(`.tab[onclick="showTab('${tab}')"]`).classList.add('active');
      document.getElementById(tab).classList.add('active');
    }

    function showToast(message) {
      const toast = document.getElementById("toast");
      toast.textContent = message;
      toast.classList.add("show");
      setTimeout(() => toast.classList.remove("show"), 3000);
    }

    // Make closePopup global
    window.closePopup = function () {
      document.getElementById("welcome-popup").style.display = "none";
      localStorage.setItem("popupClosed", "true");
    };

    // Show popup only first time
    window.addEventListener("load", () => {
      if (localStorage.getItem("popupClosed") === "true") {
        document.getElementById("welcome-popup").style.display = "none";
      }
    });
  </script>
</body>
</html>
