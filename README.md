## 📄 `README.md` – Hướng dẫn mở và deploy project Firebase Web

# 🔥 Firebase Web Project

Đây là dự án web được triển khai bằng Firebase Hosting.  
Bạn có thể mở, chỉnh sửa và deploy lại dễ dàng chỉ với vài bước.

## 🧰 Yêu cầu

- Node.js (https://nodejs.org)
- Firebase CLI (`npm install -g firebase-tools`)

---

## 🚀 Cách chạy project trên máy local

### Bước 1: Clone project

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
````

### Bước 2: Cài Firebase CLI (nếu chưa cài)

```bash
npm install -g firebase-tools
```

### Bước 3: Đăng nhập Firebase

```bash
firebase login
```

### Bước 4: Khởi chạy local (chạy thử project tại localhost)

```bash
firebase serve
```

Mở trình duyệt và truy cập:

```
http://localhost:5000
```

---

## ☁️ Cách deploy lên Firebase Hosting

### Bước 1: Build project (nếu dùng React/Vue/Svelte)

```bash
npm run build
```

> Nếu chỉ dùng HTML/CSS/JS thuần thì bỏ qua bước này.

### Bước 2: Deploy lên Firebase Hosting

```bash
firebase deploy
```

Sau đó Firebase sẽ trả cho bạn 1 đường link như:

```
✔ Hosting URL: https://your-project-name.web.app
```

---

## 💡 Ghi chú

* Nếu deploy lần đầu, nhớ chạy `firebase init` để chọn project và thư mục `public/` hoặc `build/`
* Nếu có lỗi `npm not recognized` hoặc `ExecutionPolicy`, xem file hướng dẫn [ở đây](https://go.microsoft.com/fwlink/?LinkID=135170)

---

## 😱 Demo về 1 thẻ

``` <!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chùa Thiên Mụ - Travel Dex</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-gray-100 font-sans">
  <!-- Navigation Bar -->
  <nav class="bg-white shadow-md p-4 flex justify-between items-center">
    <div class="flex items-center space-x-4">
      <a href="index.html" class="text-xl font-bold text-blue-600">Travel Dex</a>
      <a href="collection.html" class="text-gray-600 hover:text-blue-600">Bộ sưu tập</a>
    </div>
    <div class="flex items-center space-x-4">
      <span id="username" class="text-gray-600">Đang tải...</span>
      <a href="#" onclick="logout()" class="text-gray-600 hover:text-red-600">Đăng xuất</a>
    </div>
  </nav>

  <!-- Main Content -->
  <div class="container mx-auto p-6">
    <!-- Card Header -->
    <h1 class="text-3xl font-bold text-center text-blue-600 mb-6">Name-Topic</h1>

    <!-- Card Content -->
    <div class="bg-white rounded-lg shadow-lg p-6 flex flex-col md:flex-row items-center">
      <img src="https://via.placeholder.com/300x200?text=Chùa+Thiên+Mụ" alt="Name" class="w-full md:w-1/3 rounded-lg mb-4 md:mb-0 md:mr-6">
      <div>
        <h2 class="text-2xl font-semibold text-gray-800 mb-2">Chùa Thiên Mụ</h2>
        <p class="text-gray-600 mb-2">......</p>
        <p class="text-gray-600 mb-2">......</p>
        <p class="text-gray-600 mb-2">......</p>
      </div>
    </div>

    <!-- Action Buttons -->
    <div class="flex justify-center space-x-4 mt-6">
      <button id="save-card-btn" onclick="saveCard()" class="bg-blue-600 text-white px-6 py-2 rounded-full hover:bg-blue-700 transition flex items-center">
        <i class="fas fa-save mr-2"></i> Lưu thẻ
      </button>
      <a href="collection.html" class="bg-gray-600 text-white px-6 py-2 rounded-full hover:bg-gray-700 transition flex items-center">
        <i class="fas fa-book mr-2"></i> Bộ sưu tập thẻ
      </a>
    </div>
  </div>
  <!-- Footer Navigation -->
  <footer class="bg-white shadow-md p-4 fixed bottom-0 w-full flex justify-around">
    <a href="index.html" class="text-gray-600 hover:text-blue-600"><i class="fas fa-home text-2xl"></i></a>
    <a href="collection.html" class="text-gray-600 hover:text-blue-600"><i class="fas fa-map text-2xl"></i></a>
    <a href="#" onclick="refresh()" class="text-gray-600 hover:text-blue-600"><i class="fas fa-sync-alt text-2xl"></i></a>
  </footer>
  <!-- Firebase SDK -->
  <script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-auth-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.14.1/firebase-firestore-compat.js"></script>
  <script>
    // Initialize Firebase
    const firebaseConfig = {
      apiKey: "AIzaSyDOhTKHU4P3jJ7aTkvSiewNoHu1_KXkcrU",
      authDomain: "loginandsignin-4932b.firebaseapp.com",
      projectId: "loginandsignin-4932b",
      storageBucket: "loginandsignin-4932b.appspot.com",
      messagingSenderId: "863133586719",
      appId: "1:863133586719:web:81eb32db8e08e8d89e8c2a"
    };
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();
    const db = firebase.firestore();

    // Check auth state
    auth.onAuthStateChanged((user) => {
      console.log('Auth state changed:', user ? `User ${user.uid}` : 'No user');
      if (user) {
        document.getElementById('username').textContent = user.displayName || user.email;
      } else {
        window.location.href = 'login.html';
      }
    });

    // Save card to Firestore via REST API
    async function saveCard(attempt = 1, maxAttempts = 3) {
      console.log(`saveCard attempt ${attempt} of ${maxAttempts}`);
      try {
        const user = auth.currentUser;
        if (!user) {
          console.warn('No user authenticated');
          alert('Vui lòng đăng nhập để lưu thẻ!');
          window.location.href = 'login.html';
          return;
        }

        console.log('User authenticated, UID:', user.uid);
        const card = {
          id: 'idname',
          name: 'name',
          image: 'Link Picture',
          description: '....',
          rarity: 1,
          location: 'Location'
        };

        console.log('Preparing REST API request for card:', card);
        const token = await user.getIdToken();
        const url = `https://firestore.googleapis.com/v1/projects/loginandsignin-4932b/databases/(default)/documents/users/${user.uid}/cards/${card.id}`;
        const response = await fetch(url, {
          method: 'PATCH',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': `Bearer ${token}`
          },
          body: JSON.stringify({
            fields: {
              id: { stringValue: card.id },
              name: { stringValue: card.name },
              image: { stringValue: card.image },
              description: { stringValue: card.description },
              rarity: { integerValue: card.rarity },
              location: { stringValue: card.location }
            }
          })
        });

        if (!response.ok) {
          const errorData = await response.json();
          throw new Error(`HTTP ${response.status}: ${errorData.error?.message || 'Unknown error'}`);
        }

        console.log('Card saved successfully via REST API:', card.id);
        alert('Đã lưu thẻ name vào bộ sưu tập!');
      } catch (error) {
        console.error(`Attempt ${attempt} failed:`, error);
        if (attempt < maxAttempts && (error.message.includes('network') || error.message.includes('400'))) {
          console.log(`Retrying saveCard, attempt ${attempt + 1}`);
          await new Promise(resolve => setTimeout(resolve, 1000));
          return saveCard(attempt + 1, maxAttempts);
        }
        console.error('Final error saving card:', error);
        alert('Lỗi lưu thẻ: ' + error.message + '. Vui lòng kiểm tra kết nối mạng hoặc thử lại sau.');
      }
    }

    // Bind saveCard to button
    document.addEventListener('DOMContentLoaded', () => {
      const saveButton = document.getElementById('save-card-btn');
      if (saveButton) {
        console.log('Binding click event to save-card-btn');
        saveButton.addEventListener('click', saveCard);
      } else {
        console.error('Save button not found in DOM');
      }
    });

    // Logout function
    function logout() {
      auth.signOut().then(() => {
        console.log('User signed out');
        window.location.href = 'login.html';
      }).catch((error) => {
        console.error('Logout error:', error);
        alert('Lỗi đăng xuất: ' + error.message);
      });
    }

    // Refresh function
    function refresh() {
      window.location.reload();
    }
  </script>
</body>
</html>
```
---

## 🐞 Lỗi


                                                            😁 **Lỗi thường gặp khi cài đặt**
   
                                    npm : File C:\Program Files\nodejs\npm.ps1 cannot be loaded because running scripts is disabled on this system. For
                                      more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
                                      At line:1 char:1
                                      + npm install -g firebase-tools
                                      + ~~  
                                      + CategoryInfo          : SecurityError: (:) [], PSSecurityException
                                      + FullyQualifiedErrorId : UnauthorizedAccess
  ✅ **BƯỚC 1: Cài Node.js**
      Đây là thứ chứa npm, nên không có nó thì firebase cũng bó tay.
          
          👉 **Vào**: https://nodejs.org
          
        Chọn LTS version (khuyến nghị cho ổn định)
          
        Tải và cài đặt như phần mềm bình thường (bấm Next tới sáng).

  ✅ **BƯỚC 2: Kiểm tra sau khi cài**

        Mở lại Terminal / PowerShell mới (nên tắt hết cửa sổ cũ trước) và gõ:
        
            node -v
            npm -v
    
        Nếu nó in ra phiên bản (ví dụ: v18.18.2), nghĩa là ổn rồi.
    
        **🛠️ Nếu vẫn lỗi:** Thêm vào PATH thủ công
          Nhấn Win + S → Gõ Environment Variables
          Bấm "Environment Variables…"
          Ở khung bên dưới ("System variables") → Chọn dòng Path → Nhấn Edit
          Nhấn New, dán vào đường dẫn Node.js (thường là):
    
    C:\Program Files\nodejs\

    Nhấn OK → OK → OK
    
    
  ✅ **Cách 3: Mở PowerShell với quyền admin và đổi policy**
  
  Nhấn Start → Gõ PowerShell → Click phải → Run as administrator
  
  Chạy lệnh sau:
  
  powershell
```
  Set-ExecutionPolicy RemoteSigned
```
  Khi được hỏi:
  ```
  Do you want to change the execution policy?
```
  → Gõ: Y → Enter

---

## 👨‍💻 Tác giả

* Mr Hecker
* Email: [mrhecker878@thecultofosirisnfp.site](mailto:mrhecker878@thecultofosirisnfp.site)
* Project dùng Firebase Hosting, Authentication, và (tuỳ chọn) Firestore

---

## 📜 Giấy phép

_MIT License © 2025_

_NoCopyRight_
