# Err: FirebaseError: missing or insufficient permission
Xảy ra khi gặp vấn đề liên quan đến phân quyền truy cập/chỉnh sửa dữ liệu trong firebase

## Xử lý
Thay đổi quyền hạn trong Firebase Rule:

### Option 1 
No authentication for incoming request ( not recommended, xử dụng trong quá trình phát triển only hoặc khi chưa có auth)
```dart
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write;
    }
  }
}
```

### Option 2
Sử dụng khi request có auth
```dart
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write;
    }
  }
}
```


