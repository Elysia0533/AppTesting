# Kiểm thử và Đánh giá Chất lượng Ứng dụng Đọc truyện Đa định dạng vBook trên Nền tảng Android

[![Flutter Analyze](https://img.shields.io/badge/flutter_analyze-0_issues-brightgreen)](#5-kết-quả-kiểm-thử-tự-động--benchmark)
[![Automated Tests](https://img.shields.io/badge/automated_tests-402%2F402_passed-success)](#5-kết-quả-kiểm-thử-tự-động--benchmark)
[![System Test Cases](https://img.shields.io/badge/system_test_cases-55%2F55_passed-blue)](./docs/04_System_Test_Cases.md)
[![ISO/IEC 25010](https://img.shields.io/badge/quality_standard-ISO%2FIEC_25010-orange)](./docs/06_ISO25010_Quality_Evaluation.md)

Kho lưu trữ hồ sơ kiểm định, tài liệu thiết kế kiểm thử (chuẩn **IEEE 829** & **ISO/IEC 25010**) và bộ kiểm thử tự động (**42 tệp Test Suite / 402 Test Cases**) cho ứng dụng **vBook Reader**.

---

## 1. Thông tin học phần & Sinh viên thực hiện

| Hạng mục | Chi tiết |
| :--- | :--- |
| **Trường / Khoa** | Đại học Phenikaa – Trường Công nghệ Thông tin Phenikaa |
| **Học phần** | Đánh giá và Kiểm định chất lượng phần mềm |
| **Lớp tín chỉ** | `CSE703010-1-1-26(COUR01)` |
| **Giảng viên hướng dẫn** | **TS. Trịnh Thanh Bình** |
| **Sinh viên thực hiện** | **Trần Tiến Đức** |
| **Mã số sinh viên** | **`23010777`** |
| **Hình thức thực hiện** | Cá nhân |
| **Đối tượng kiểm thử (SUT)** | Ứng dụng đọc sách/truyện đa định dạng **vBook Reader** (`v1.0.0` Alpha $
ightarrow$ `v1.1.0+2` Release) |

---

## 2. Danh mục Tài liệu Kiểm định Chất lượng Phần mềm (`docs/`)

Toàn bộ tài liệu đặc tả kiểm thử theo chuẩn **IEEE 829** và **ISO/IEC 25010** được tổ chức tại thư mục [`docs/`](./docs):

1. **[`01_Test_Plan_IEEE829.md`](./docs/01_Test_Plan_IEEE829.md)**: Kế hoạch kiểm thử phần mềm (Mục tiêu, Phạm vi In-scope/Out-of-scope, Lịch trình, Tài nguyên, Chiến lược kiểm thử 4 tầng, Tiêu chí Entry/Exit/Acceptance).
2. **[`02_Test_Design_Specification.md`](./docs/02_Test_Design_Specification.md)**: Thiết kế ca kiểm thử Hộp đen (*Phân vùng tương đương EP, Giá trị biên BVA, Bảng quyết định Decision Table, Chuyển trạng thái State Transition*) và Hộp trắng (*Đồ thị luồng điều khiển CFG, Độ phức tạp Cyclomatic $V(G)=6$, Basis Paths*).
3. **[`03_Requirements_Traceability_Matrix.md`](./docs/03_Requirements_Traceability_Matrix.md)**: Ma trận truy vết yêu cầu (RTM) ánh xạ 100% giữa 13 Use Case (`UC-C1` $
ightarrow$ `UC-A1`), 55 Ca kiểm thử hệ thống và 42 tệp Unit/Widget/Integration Test.
4. **[`04_System_Test_Cases.md`](./docs/04_System_Test_Cases.md)** & **[`04_System_Test_Cases.csv`](./docs/04_System_Test_Cases.csv)**: Đặc tả chi tiết và kết quả thực thi 55 Ca kiểm thử hệ thống (`TC_FUNC_01..27`, `TC_SEC_01..13`, `TC_PERF_01..07`, `TC_UI_01..04`, `TC_AUTO_01..04`).
5. **[`05_Defect_Tracking_Log.md`](./docs/05_Defect_Tracking_Log.md)**: Nhật ký quản lý vòng đời lỗi và phân tích nguyên nhân gốc rễ cho 6 Defect phát hiện ở Vòng 1 (`DEF-01` $
ightarrow$ `DEF-06`).
6. **[`06_ISO25010_Quality_Evaluation.md`](./docs/06_ISO25010_Quality_Evaluation.md)**: Báo cáo tổng kết kiểm thử và đánh giá 8 đặc tính chất lượng theo tiêu chuẩn quốc tế **ISO/IEC 25010**.

---

## 3. Cấu trúc Kho lưu trữ (Repository Structure)

```text
AppTesting/
├── README.md                                     # Tổng quan dự án kiểm định & hướng dẫn chạy test
├── docs/                                         # Bộ tài liệu kiểm định chuẩn IEEE 829 & ISO/IEC 25010
│   ├── 01_Test_Plan_IEEE829.md                   # Kế hoạch kiểm thử (Test Plan)
│   ├── 02_Test_Design_Specification.md           # Thiết kế kiểm thử Hộp đen & Hộp trắng (EP, BVA, CFG)
│   ├── 03_Requirements_Traceability_Matrix.md    # Ma trận truy vết yêu cầu (RTM)
│   ├── 04_System_Test_Cases.md                   # Đặc tả 55 Ca kiểm thử hệ thống (Markdown)
│   ├── 04_System_Test_Cases.csv                  # Dữ liệu 55 Ca kiểm thử hệ thống (CSV/Excel)
│   ├── 05_Defect_Tracking_Log.md                 # Nhật ký lỗi & Truy vết bản vá (DEF-01..DEF-06)
│   └── 06_ISO25010_Quality_Evaluation.md         # Đánh giá chất lượng theo mô hình ISO/IEC 25010
├── test/                                         # 42 tệp kiểm thử tự động (402 Unit/Widget/Integration tests)
│   ├── sec_001_local_account_test.dart           # Kiểm thử PBKDF2 SHA-256 & Legacy Migration (DEF-01)
│   ├── vbook_engine_channel_test.dart            # Kiểm thử cô lập Isolate JS & bắt lỗi (DEF-02)
│   ├── explore_drive_race_test.dart              # Kiểm thử chống đua lệnh Generation Token (DEF-03)
│   ├── plugin_loader_security_test.dart          # Kiểm thử chặn Path Traversal & Zip Bomb (DEF-04)
│   ├── firestore.rules.test.cjs                  # Kiểm thử phân quyền RBAC Firestore Rules (DEF-05)
│   ├── local_manga_parser_test.dart              # Kiểm thử Hộp trắng bộ đọc Manga & chapter.json (DEF-06)
│   ├── search_index_performance_test.dart        # Benchmark hiệu năng SQLite FFI 5.000 bản ghi
│   ├── unified_search_screen_test.dart           # Kiểm thử giao diện đa độ phân giải & Text Scale
│   ├── tts_player_container_test.dart            # Kiểm thử tương thích thanh điều khiển đọc giọng nói TTS
│   ├── translator_bot_api_key_test.dart          # Kiểm thử EP/BVA khóa API Google Gemini (AIzaSy & AQ.)
│   └── ... (cùng 32 tệp test chuyên biệt khác)
├── integration_test/                             # Kiểm thử tích hợp đầu-cuối trên thiết bị / máy ảo
├── lib/                                          # Mã nguồn đối tượng kiểm thử (SUT - vBook Reader)
├── firestore.rules                               # Quy tắc bảo mật Cloud Firestore
├── analysis_options.yaml                         # Cấu hình kiểm thử tĩnh Dart Linter
└── .github/workflows/sqa_ci.yml                  # Pipeline CI tự động chạy Analyze & Test
```

---

## 4. Kết quả Tổng hợp Kiểm thử (Vòng 1 vs. Vòng 2)

| STT | Nhóm kiểm thử | Số TC | Vòng 1: Pass | Vòng 1: Fail | Vòng 1: Blocked | Vòng 2: Pass (Final) | Tỷ lệ Đạt |
| :-: | :--- | :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | Tài khoản & Xác thực (Local PBKDF2 & Firebase) | 6 | 4 | 2 (`DEF-01`) | 0 | **6 / 6** | **100%** |
| 2 | Kệ sách, Nhập tệp & Tìm kiếm SQLite | 6 | 5 | 1 (`SQLi/FTS`) | 0 | **6 / 6** | **100%** |
| 3 | Khám phá & Đồng bộ Google Drive Cloud | 6 | 4 | 1 (`DEF-03`) | 1 (`Sync`) | **6 / 6** | **100%** |
| 4 | Trình đọc đa định dạng (EPUB/PDF/TXT/Manga) & TTS | 6 | 5 | 1 (`DEF-06`) | 0 | **6 / 6** | **100%** |
| 5 | Cộng đồng, Bình luận & Thống kê đọc sách | 3 | 3 | 0 | 0 | **3 / 3** | **100%** |
| 6 | An toàn & Bảo mật hệ thống (`TC_SEC_01..13`) | 13 | 9 | 3 (`DEF-02,04,05`) | 1 (`Crash`) | **13 / 13** | **100%** |
| 7 | Hiệu năng cơ sở dữ liệu (`TC_PERF_01..07`) | 7 | 7 | 0 | 0 | **7 / 7** | **100%** |
| 8 | Giao diện Responsive & Tự động hóa (`TC_UI`, `TC_AUTO`) | 8 | 8 | 0 | 0 | **8 / 8** | **100%** |
| **TỔNG** | **Kịch bản kiểm thử hệ thống (System Test Cases)** | **55** | **45 (81.8%)** | **8 (14.5%)** | **2 (3.6%)** | **55 / 55** | **100%** |
| **AUTO** | **Kiểm thử tự động (`flutter test` – 42 suites)** | **402** | **384** | **16** | **2** | **402 / 402** | **100%** |

---

## 5. Kết quả Kiểm thử Tự động & Benchmark Thực nghiệm

### Hướng dẫn chạy lại bộ kiểm thử

```bash
# 1. Cài đặt các gói phụ thuộc
flutter pub get

# 2. Chạy kiểm thử tĩnh (Static Code Analysis)
flutter analyze

# 3. Chạy toàn bộ 42 tệp kiểm thử tự động (402 test cases)
flutter test

# 4. Chạy riêng bài đo Benchmark hiệu năng SQLite 5.000 bản ghi
flutter test test/search_index_performance_test.dart
```

### Số liệu đo lường thực tế trên bản dựng `v1.1.0+2`

- **Kiểm thử tĩnh (`flutter analyze`):** `No issues found! (ran in 6.1s)`
- **Kiểm thử tự động (`flutter test`):** `00:33 +402: All tests passed!`
- **Benchmark SQLite FFI (`5.000` bản ghi metadata):**
  - Chèn hàng loạt lần đầu (`insert_ms`): **`14.956 ms`** (~2,99 ms/bản ghi, đạt ngưỡng `< 20.000 ms`)
  - Quét lại khi dữ liệu không đổi (`unchanged_rescan_ms`): **`785 ms`** (đạt ngưỡng `< 3.000 ms`)
  - Truy vấn tìm kiếm tiếng Việt trung vị (`query_p50_us`): **`7.872 µs`** (**`7,87 ms`**, đạt ngưỡng `< 50 ms`)
  - Truy vấn tìm kiếm phân vị 95% (`query_p95_us`): **`12.182 µs`** (**`12,18 ms`**, đạt ngưỡng `< 50 ms`)
  - Duyệt phân trang toàn bộ 5.000 bản ghi (`all_pages_ms`): **`871 ms`** (đạt ngưỡng `< 3.000 ms`)
