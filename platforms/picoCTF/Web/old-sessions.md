# 🧩 Challenge: Old Sessions

## 🏷 Platform

picoCTF

## 📂 Category

Web Exploitation

---

## 📌 Description

Bài này nói về việc quản lý session không đúng cách.
Nếu session không hết hạn hoặc không bị xoá khi logout, attacker có thể lợi dụng để truy cập lại tài khoản.

---

## 🔍 Analysis

* Website sử dụng **session để xác thực người dùng**
* Khi login, server cấp một session (thường qua cookie)
* Nếu session **không hết hạn (no timeout)** → vẫn dùng lại được

👉 Điều này dẫn đến:

* Người dùng logout nhưng session vẫn tồn tại
* Hoặc đóng trình duyệt nhưng session không bị xoá

➡️ Attacker có thể:

* Mở lại trình duyệt
* Hoặc dùng lại cookie cũ
* Và vẫn đăng nhập được mà không cần password

---

## ⚙️ Exploitation

### Bước 1: Login bình thường

* Truy cập web
* Đăng nhập tài khoản

### Bước 2: Quan sát session

* Mở DevTools → Application → Cookies
* Thấy session ID (ví dụ: `session=abc123`)

### Bước 3: Thử logout / đóng tab

* Logout hoặc đóng trình duyệt

### Bước 4: Reuse session

* Mở lại trang
* Hoặc gắn lại cookie cũ

👉 Nếu vẫn đăng nhập → chứng tỏ:

* Session **không bị invalid**
* Không có timeout

---

## 🏁 Flag

```
(paste flag của bạn ở đây)
```

---

## 📚 Lessons Learned

* Session phải có:

  * Timeout (hết hạn)
  * Invalidate khi logout

* Nếu không:

  * Dễ bị **Session Hijacking**
  * Hoặc **Session Fixation**

---

## 🔐 Mapping thực tế

Lỗi này thuộc:

* OWASP A02: Broken Authentication / Session Management

Trong thực tế:

* Rất nhiều web cũ dính lỗi này
* Đặc biệt là hệ thống nội bộ hoặc web không update

---

## 🔗 Tools Used

* Browser DevTools
* Cookie inspection

---

## 🚀 Notes

Đây là dạng bài rất cơ bản nhưng cực kỳ quan trọng trong Web Security.
Hiểu rõ session sẽ giúp giải nhiều bài nâng cao hơn sau này.
