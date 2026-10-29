# NHẬT KÝ THEO DÕI VÀ XỬ LÝ LỖI (DEFECT TRACKING LOG)

Trong Vòng kiểm thử 1 (trên bản dựng Alpha `v1.0.0`), quá trình kiểm thử đã phát hiện **06 khiếm khuyết kỹ thuật gốc (Defects)** làm thất bại 8 kịch bản kiểm thử hệ thống và làm nghẽn 2 kịch bản. Toàn bộ 6 lỗi đã được khắc phục triệt để và xác nhận đóng (`Closed`) ở Vòng kiểm thử 2 (`v1.1.0+2`).

---

## 1. Thống kê phân bố lỗi theo mức độ nghiêm trọng (Severity)

| Mức độ nghiêm trọng | Số lượng | Tỷ lệ (%) | Ca kiểm thử bị ảnh hưởng (Vòng 1) | Đã đóng (Closed) | Còn mở (Open) |
| :--- | :-: | :-: | :--- | :-: | :-: |
| **Critical (Nghiêm trọng)** | 2 (`DEF-01`, `DEF-02`) | 33,33% | 3 TC Fail, 1 TC Blocked | 2 | 0 |
| **High (Mức độ cao)** | 3 (`DEF-03`, `DEF-04`, `DEF-05`) | 50,00% | 4 TC Fail, 1 TC Blocked | 3 | 0 |
| **Medium (Trung bình)** | 1 (`DEF-06`) | 16,67% | 1 TC Fail | 1 | 0 |
| **Low (Thấp)** | 0 | 0,00% | 0 | 0 | 0 |
| **TỔNG CỘNG** | **6 Defects** | **100%** | **8 TC Fail, 2 TC Blocked** | **6 (100%)** | **0** |

---

## 2. Danh mục chi tiết 06 Defect kỹ thuật và Bản vá xác minh

| Mã lỗi | Mức độ | TC bị ảnh hưởng (Vòng 1) | Mô tả lỗi & Nguyên nhân gốc rễ (Root Cause) | Giải pháp khắc phục (Fix) | Tệp Unit Test xác minh (Retest) | Trạng thái |
| :-: | :-: | :--- | :--- | :--- | :--- | :-: |
| **`DEF-01`** | **Critical** | `TC_FUNC_01`, `TC_SEC_01`, `TC_SEC_02` | **Lộ mật khẩu Plaintext:** Bản dựng cũ lưu mật khẩu gốc dạng chuỗi thô trong `SharedPreferences`. | Áp dụng thuật toán băm **PBKDF2-HMAC-SHA256** (120.000 vòng + salt 16 bytes) và tự động nâng cấp (Legacy Migration) khi đăng nhập. | [`test/sec_001_local_account_test.dart`](../test/sec_001_local_account_test.dart) | **Closed** |
| **`DEF-02`** | **Critical** | `TC_SEC_09`, `TC_FUNC_13` *(Blocked)* | **Xung đột luồng thực thi kịch bản JS nguồn truyện:** Kịch bản JS chạy quá thời gian hoặc trả về Promise bất đồng bộ không được bắt giữ làm treo luồng gọi. | Chuẩn hóa kênh `VBookEngine`, bắt giữ tường minh các mã lỗi `EXEC_TIMEOUT`, `PARSE_ERROR`, `ASYNC_UNSUPPORTED`. | [`test/vbook_engine_channel_test.dart`](../test/vbook_engine_channel_test.dart) | **Closed** |
| **`DEF-03`** | **High** | `TC_FUNC_17`, `TC_FUNC_13` *(Blocked)* | **Lỗi đua lệnh (Race Condition) khi chuyển thư mục Google Drive:** Phản hồi mạng của thư mục cũ trả về muộn ghi đè lên danh sách của thư mục mới. | Bổ sung định danh phiên truy vấn (**Generation Token**), tự động loại bỏ các phản hồi thuộc phiên cũ khi người dùng làm mới hoặc đổi thư mục. | [`test/explore_drive_race_test.dart`](../test/explore_drive_race_test.dart) | **Closed** |
| **`DEF-04`** | **High** | `TC_SEC_07`, `TC_SEC_08` | **Lỗ hổng Path Traversal & Zip Bomb trong PluginLoader:** Chưa kiểm tra ký tự vượt cấp `../` trong ID plugin và chưa giới hạn dung lượng giải nén ZIP. | Viết hàm `validatePluginId` kiểm tra Regex nghiêm ngặt; giới hạn giải nén tối đa **64MB** và tỷ lệ nén tối đa **100x**. | [`test/plugin_loader_security_test.dart`](../test/plugin_loader_security_test.dart) | **Closed** |
| **`DEF-05`** | **High** | `TC_SEC_03`, `TC_SEC_04`, `TC_SEC_05` | **Lỗ hổng phân quyền Cloud Firestore:** Quy tắc ban đầu chỉ kiểm tra `auth != null`, cho phép truy cập chéo hoặc tự ghi trường `role: 'admin'`. | Viết lại [`firestore.rules`](../firestore.rules) kiểm tra chặt `request.auth.uid == userId`, `email_verified == true` và `request.auth.token.admin == true`. | [`test/firestore.rules.test.cjs`](../test/firestore.rules.test.cjs) | **Closed** |
| **`DEF-06`** | **Medium** | `TC_FUNC_19`, `TC_SEC_12` | **Lỗi phân tích tệp EPUB chứa External DTD & Manga `chapter.json` dạng Map:** Trình đọc XML bị treo khi gặp thực thể ngoài và chưa nhận diện `chapter.json` dạng Map. | Khóa xử lý thực thể ngoài DTD khi đọc EPUB; nâng cấp [`LocalMangaParser`](../lib/services/local_manga_parser.dart) hỗ trợ cả JSON dạng `List` và `Map` kèm sắp xếp số tự nhiên. | [`test/local_manga_parser_test.dart`](../test/local_manga_parser_test.dart) | **Closed** |
