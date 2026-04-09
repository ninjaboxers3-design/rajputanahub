<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Profile</title>

  <style>
    @font-face {
      font-family: 'FuturaBook';
      src: url('FuturaCyrillicBook.ttf') format('truetype');
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'FuturaBook', Arial, sans-serif;
    }

    body {
      background: #000;
      color: #fff;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 24px;
    }

    .box {
      width: 100%;
      max-width: 560px;
      text-align: center;
    }

    h1 {
      font-size: 3.5rem;
      margin-bottom: 30px;
      text-transform: uppercase;
      letter-spacing: 2px;
    }

    .avatar-wrap {
      margin-bottom: 24px;
    }

    .avatar {
      width: 140px;
      height: 140px;
      border-radius: 50%;
      object-fit: cover;
      border: 2px solid #333;
      background: #1a1a1a;
    }

    input[type="text"],
    input[type="file"] {
      width: 100%;
      margin-bottom: 18px;
      padding: 18px 20px;
      border-radius: 14px;
      border: 1px solid #333;
      background: #1a1a1a;
      color: #fff;
      font-size: 1.05rem;
      outline: none;
    }

    input[type="text"]:focus {
      border-color: #f39c12;
      box-shadow: 0 0 0 3px rgba(243,156,18,0.15);
    }

    .btn {
      width: 100%;
      padding: 18px;
      border: none;
      border-radius: 14px;
      background: #f39c12;
      color: #000;
      font-size: 1.05rem;
      cursor: pointer;
      margin-bottom: 14px;
    }

    .btn:hover {
      background: #ffad33;
    }

    .back-link {
      display: inline-block;
      margin-top: 10px;
      color: #f39c12;
      text-decoration: none;
    }

    .back-link:hover {
      text-decoration: underline;
    }

    #msg {
      min-height: 24px;
      margin-top: 10px;
      color: #ff6b6b;
    }
  </style>
</head>
<body>
  <div class="box">
    <h1>Profile</h1>

    <div class="avatar-wrap">
      <img id="profileAvatar" class="avatar" src="" alt="Profile Picture" />
    </div>

    <input type="text" id="username" placeholder="Change Username" maxlength="20" />
    <input type="file" id="profilePic" accept="image/*" />

    <button class="btn" id="saveBtn">Save Changes</button>

    <div id="msg"></div>

    <a href="index.html" class="back-link">Back to Home</a>
  </div>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
    import { getAuth, onAuthStateChanged, updateProfile } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
    import {
      getFirestore,
      doc,
      getDoc,
      setDoc,
      updateDoc,
      deleteDoc,
      serverTimestamp
    } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";
    import {
      getStorage,
      ref,
      uploadBytes,
      getDownloadURL
    } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-storage.js";

    const firebaseConfig = {
      apiKey: "PASTE_YOURS",
      authDomain: "PASTE_YOURS",
      projectId: "PASTE_YOURS",
      storageBucket: "PASTE_YOURS",
      messagingSenderId: "PASTE_YOURS",
      appId: "PASTE_YOURS"
    };

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);
    const storage = getStorage(app);

    const profileAvatar = document.getElementById("profileAvatar");
    const usernameInput = document.getElementById("username");
    const profilePicInput = document.getElementById("profilePic");
    const saveBtn = document.getElementById("saveBtn");
    const msg = document.getElementById("msg");

    const defaultAvatar = "https://via.placeholder.com/140?text=%20";
    let currentUser = null;
    let oldUsername = "";

    function validUsername(name) {
      return /^[a-zA-Z0-9_]{3,20}$/.test(name.trim());
    }

    onAuthStateChanged(auth, async (user) => {
      if (!user) {
        window.location.href = "login.html";
        return;
      }

      currentUser = user;

      const profileRef = doc(db, "profiles", user.uid);
      const profileSnap = await getDoc(profileRef);

      if (profileSnap.exists()) {
        const data = profileSnap.data();
        usernameInput.value = data.username || user.displayName || "";
        oldUsername = (data.username || "").toLowerCase();
        profileAvatar.src = data.photoURL || defaultAvatar;
      } else {
        usernameInput.value = user.displayName || "";
        oldUsername = (user.displayName || "").toLowerCase();
        profileAvatar.src = defaultAvatar;
      }
    });

    saveBtn.addEventListener("click", async () => {
      msg.textContent = "";

      if (!currentUser) return;

      const newUsername = usernameInput.value.trim();
      const normalizedNew = newUsername.toLowerCase();

      if (!validUsername(newUsername)) {
        msg.textContent = "Username must be 3-20 letters, numbers, or underscores.";
        return;
      }

      try {
        let photoURL = "";

        const oldProfileRef = doc(db, "profiles", currentUser.uid);
        const oldProfileSnap = await getDoc(oldProfileRef);
        if (oldProfileSnap.exists()) {
          photoURL = oldProfileSnap.data().photoURL || "";
        }

        const file = profilePicInput.files[0];
        if (file) {
          const imageRef = ref(storage, `profilePictures/${currentUser.uid}/${file.name}`);
          await uploadBytes(imageRef, file);
          photoURL = await getDownloadURL(imageRef);
        }

        if (normalizedNew !== oldUsername) {
          const newUsernameRef = doc(db, "usernames", normalizedNew);
          const newUsernameSnap = await getDoc(newUsernameRef);

          if (newUsernameSnap.exists()) {
            msg.textContent = "Username already picked.";
            return;
          }

          if (oldUsername) {
            await deleteDoc(doc(db, "usernames", oldUsername));
          }

          await setDoc(newUsernameRef, {
            uid: currentUser.uid,
            username: newUsername,
            createdAt: serverTimestamp()
          });
        }

        await updateProfile(currentUser, {
          displayName: newUsername,
          photoURL: photoURL || null
        });

        await setDoc(doc(db, "profiles", currentUser.uid), {
          username: newUsername,
          email: currentUser.email,
          photoURL: photoURL || "",
          updatedAt: serverTimestamp()
        }, { merge: true });

        oldUsername = normalizedNew;
        profileAvatar.src = photoURL || defaultAvatar;
        msg.style.color = "#6ee7a8";
        msg.textContent = "Profile updated successfully.";
      } catch (error) {
        msg.style.color = "#ff6b6b";
        msg.textContent = error.message || "Something went wrong.";
      }
    });
  </script>
</body>
</html>
