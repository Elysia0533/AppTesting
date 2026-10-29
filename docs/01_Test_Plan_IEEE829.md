# KẾ HOẠCH KIỂM THỬ PHẦN MỀM (TEST PLAN – IEEE 829)

- **Đề tài:** Kiểm thử và đánh giá chất lượng ứng dụng đọc truyện đa định dạng vBook trên nền tảng Android
- **Học phần:** Đánh giá và Kiểm định chất lượng phần mềm – `CSE703010-1-1-26(COUR01)`
- **Giảng viên hướng dẫn:** TS. Trịnh Thanh Bình
- **Sinh viên thực hiện:** Trần Tiến Đức – **MSSV: `23010777`** (Thực hiện cá nhân)

---

## 1. Lịch sử cập nhật

| Ngày | Phiên bản | Nội dung cập nhật | Người lập |
| :-: | :-: | :--- | :--- |
| 01/09/2026 | 1.0 | Lập kế hoạch kiểm thử ban đầu cho ứng dụng vBook | Trần Tiến Đức (`23010777`) |
| 18/10/2026 | 2.0 | Bổ sung chiến lược kiểm thử tự động, bảo mật và hiệu năng | Trần Tiến Đức (`23010777`) |
| 28/10/2026 | 2.1 | Hoàn thiện kết quả Vòng 2, Ma trận truy vết RTM và đánh giá ISO/IEC 25010 | Trần Tiến Đức (`23010777`) |

---

## 2. Mục tiêu và Phạm vi kiểm thử (Test Scope)

### 2.1. Trong phạm vi (In-Scope)
- **Kiểm thử chức năng (`TC_FUNC_01..27`):** Đăng ký/Đăng nhập (Firebase & Local PBKDF2), Quản lý hồ sơ, Kệ sách cá nhân, Nhập tệp cục bộ (`.epub`, `.pdf`, `.txt`, thư mục Manga & `chapter.json`), Khám phá & tải sách Google Drive, Trình đọc đa định dạng, Đọc giọng nói TTS, Trợ lý dịch thuật Ellie (Gemini AI), Cộng đồng và Thống kê đọc.
- **Kiểm thử bảo mật (`TC_SEC_01..13`):** Mã hóa mật khẩu PBKDF2-HMAC-SHA256 (120.000 vòng + salt 16 bytes), tự động nâng cấp tài khoản cũ (Legacy Migration), phân quyền RBAC trên Cloud Firestore Rules, chặn tấn công Path Traversal, Zip Bomb (`> 64MB` hoặc tỷ lệ nén `> 100x`), thực thi kịch bản JS trong Isolate Sandbox, chống XXE/External DTD và SQL Injection.
- **Kiểm thử hiệu năng (`TC_PERF_01..07`):** Đo lường định lượng thời gian Bulk Insert, Unchanged Rescan, FTS Query (`p50`, `p95`) và Paging trên tập dữ liệu 5.000 bản ghi SQLite.
- **Kiểm thử giao diện & Tương thích (`TC_UI_01..04`):** Chế độ Sáng/Tối, kiểm tra không tràn viền (0 overflow) trên các độ phân giải `320x640`, `360x720`, `393x800`, `412x800`, `640x320` với tỷ lệ phóng chữ `1.0x`, `1.3x`, `1.5x`.
- **Kiểm thử tĩnh & Tự động hóa (`TC_AUTO_01..04`):** `flutter analyze` và `flutter test` (42 tệp test suite / 402 test cases).

### 2.2. Ngoài phạm vi (Out-of-Scope)
- Cổng thanh toán trực tuyến (ứng dụng không thu phí).
- Kiểm thử chịu tải hạ tầng đám mây của Google (Firebase / Google Drive).
- Kiểm thử trên thiết bị iOS vật lý.

---

## 3. Chiến lược kiểm thử đa tầng (Test Strategy)

| Cấp độ / Loại kiểm thử | Kỹ thuật áp dụng | Công cụ thực thi | Tiêu chí hoàn thành |
| :--- | :--- | :--- | :--- |
| **1. Kiểm thử tĩnh (Static Analysis)** | Phân tích cú pháp, kiểu dữ liệu và quy tắc Linting | `flutter analyze` (`flutter_lints`) | `0 issues found!` (0 lỗi, 0 cảnh báo) |
| **2. Kiểm thử đơn vị & Giao diện tự động** | Hộp trắng (CFG, phủ nhánh) & Hộp đen (EP, BVA) | `flutter test` (42 tệp `*_test.dart`) | `402 / 402` test cases đạt `Passed` |
| **3. Kiểm thử chức năng hệ thống** | Hộp đen (EP, BVA, Decision Table, State Transition) | Máy ảo Android (Pixel 5 API 34) & Thiết bị thật | `27 / 27` ca `TC_FUNC` và `4 / 4` ca `TC_UI` đạt `Passed` |
| **4. Kiểm thử Bảo mật & Hiệu năng** | Kiểm thử xâm nhập (Fuzzing/Injection) & Benchmark | `sqflite_common_ffi`, Security Test Suite | `13 / 13` ca `TC_SEC` và `7 / 7` ca `TC_PERF` đạt `Passed` |

---

## 4. Điều kiện chấp nhận (Entry / Exit / Acceptance Criteria)

- **Tiêu chí bắt đầu (Entry Criteria):** Mã nguồn biên dịch sạch với `flutter analyze` đạt 0 lỗi; cơ sở dữ liệu mẫu và môi trường giả lập Android sẵn sàng.
- **Tiêu chí kết thúc & Nghiệm thu (Exit & Acceptance Criteria):**
  1. Thực thi đủ **100%** các ca kiểm thử đã thiết kế (55 kịch bản hệ thống + 402 bài test tự động).
  2. Tỷ lệ đạt (Pass Rate) ở vòng kiểm thử hồi quy đạt **>= 98%** (Thực tế đạt **100%**).
  3. **100%** lỗi mức `Critical` và `High` phải được sửa triệt để và đóng (`Closed`).
