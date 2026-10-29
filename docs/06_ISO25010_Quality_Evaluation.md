# ĐÁNH GIÁ CHẤT LƯỢNG PHẦN MỀM THEO TIÊU CHUẨN ISO/IEC 25010

Dựa trên kết quả thực nghiệm từ **55 kịch bản kiểm thử hệ thống** và **402 bài kiểm thử tự động**, chất lượng ứng dụng **vBook Reader (`v1.1.0+2`)** được đánh giá toàn diện theo 8 đặc tính của mô hình **ISO/IEC 25010**:

| Đặc tính chất lượng (ISO/IEC 25010) | Mức đạt | Bằng chứng thực nghiệm từ dự án |
| :--- | :-: | :--- |
| **1. Tính phù hợp chức năng (Functional Suitability)** | **100%** | Toàn bộ 13 Use Case (Tài khoản, Kệ sách, Google Drive, Đọc đa định dạng EPUB/PDF/TXT/Manga, TTS, Dịch AI Ellie, Cộng đồng) đều đạt `27/27` ca `TC_FUNC`. |
| **2. Hiệu năng xử lý (Performance Efficiency)** | **95%** | Trên tập `5.000` bản ghi SQLite: Tìm kiếm FTS đạt `p50 = 7,87 ms`, `p95 = 12,18 ms` (`< 50 ms`); Quét lại kho không đổi đạt `785 ms`; Duyệt phân trang đạt `871 ms`; Chèn mới 5.000 bản ghi đạt `14.956 ms`. |
| **3. Tính tương thích (Compatibility)** | **100%** | Hỗ trợ đồng thời nhiều định dạng tệp (`.epub`, `.pdf`, `.txt`, Manga folder/`chapter.json`) và đồng bộ trơn tru với Firebase Auth, Cloud Firestore, Google Drive API, Google Gemini API. |
| **4. Tính khả dụng (Usability)** | **98%** | Giao diện Material 3 hỗ trợ Dark/Light Mode; vượt qua toàn bộ bài kiểm thử co giãn khung hình (`320x640` → `640x320`) với tỷ lệ phóng chữ `1.0x`, `1.3x`, `1.5x` mà không tràn viền (`0 overflow`). |
| **5. Độ tin cậy (Reliability)** | **96%** | Kiến trúc Offline-First hoạt động ổn định khi mất mạng; cơ chế `Generation Token` chống đua lệnh khi chuyển thư mục nhanh; bắt lỗi ngoại lệ kênh Isolate an toàn. |
| **6. Tính bảo mật (Security)** | **100%** | Vượt qua `13/13` ca `TC_SEC`: băm mật khẩu PBKDF2 120.000 vòng, phân quyền RBAC bằng Custom Claims & Firestore Rules, chặn đứng Path Traversal, Zip Bomb, XXE và SQL Injection. |
| **7. Khả năng bảo trì (Maintainability)** | **100%** | Mã nguồn đạt `0 issues` khi chạy `flutter analyze`; hệ thống 42 tệp test tự động (402 tests) cho phép kiểm thử hồi quy toàn bộ ứng dụng chỉ trong `33 giây`. |
| **8. Tính khả chuyển (Portability)** | **95%** | Biên dịch thành công bản cài đặt Universal Release APK (`app-release.apk`) tương thích đa kiến trúc (`arm64-v8a`, `armeabi-v7a`, `x86_64`); tầng SQLite hỗ trợ cả Android lẫn máy tính qua FFI. |

---

## Kết luận Nghiệm thu

Ứng dụng **vBook Reader (`v1.1.0+2`)** đã hoàn thành **100% kế hoạch kiểm thử** (`55/55` System Test Cases và `402/402` Automated Test Cases đạt `Passed`, `0` lỗi tồn đọng), đáp ứng đầy đủ các tiêu chí chấp nhận chất lượng của học phần **Đánh giá và Kiểm định chất lượng phần mềm**.
