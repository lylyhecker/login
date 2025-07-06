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

## 👨‍💻 Tác giả

* Mr Hecker
* Email: [mrhecker878@thecultofosirisnfp.site](mailto:mrhecker878@thecultofosirisnfp.site)
* Project dùng Firebase Hosting, Authentication, và (tuỳ chọn) Firestore

---

## 📜 Giấy phép

MIT License © 2025
