# MA TRẬN TRUY VẾT YÊU CẦU (REQUIREMENTS TRACEABILITY MATRIX – RTM)

Bảng ma trận truy vết đảm bảo **100% các Use Case nghiệp vụ** trong đặc tả yêu cầu đều được kiểm chứng bởi các **Ca kiểm thử hệ thống (`TC_FUNC`, `TC_SEC`, `TC_PERF`, `TC_UI`)** và các **Tệp kiểm thử tự động (`test/*_test.dart`)**.

| Mã UC | Tên Use Case nghiệp vụ | Ca kiểm thử Chức năng | Ca kiểm thử Bảo mật / Hiệu năng / UI | Tệp Kiểm thử Tự động (`test/`) | Trạng thái |
| :-: | :--- | :--- | :--- | :--- | :-: |
| **UC-C1** | Đăng nhập / Đăng xuất | `TC_FUNC_04`, `TC_FUNC_05` | `TC_SEC_01`, `TC_SEC_02` | `sec_001_local_account_test.dart` | **100% Pass** |
| **UC-C2** | Quản lý hồ sơ cá nhân | `TC_FUNC_06` | `TC_SEC_03` | `firebase_library_sync_test.dart` | **100% Pass** |
| **UC-U1** | Đăng ký tài khoản mới | `TC_FUNC_01`, `TC_FUNC_02`, `TC_FUNC_03` | `TC_SEC_01` | `sec_001_local_account_test.dart` | **100% Pass** |
| **UC-U2** | Khôi phục mật khẩu | `TC_FUNC_04` | `TC_SEC_04` | `sec_001_local_account_test.dart` | **100% Pass** |
| **UC-U3** | Khám phá danh mục truyện & Nguồn | `TC_FUNC_13`, `TC_FUNC_14`, `TC_FUNC_17` | `TC_PERF_01`, `TC_SEC_09`, `TC_SEC_10` | `explore_drive_race_test.dart`, `vbook_engine_channel_test.dart` | **100% Pass** |
| **UC-U4** | Tìm kiếm đa nguồn & Lọc truyện | `TC_FUNC_08`, `TC_FUNC_12` | `TC_PERF_02..06`, `TC_UI_02` | `unified_search_screen_test.dart`, `search_index_performance_test.dart` | **100% Pass** |
| **UC-U5** | Xem thông tin chi tiết truyện | `TC_FUNC_15` | `TC_UI_02`, `TC_UI_04` | `reader_download_layout_test.dart` | **100% Pass** |
| **UC-U6** | Đọc truyện trực tuyến & Dịch AI | `TC_FUNC_19`, `TC_FUNC_21..24` | `TC_SEC_12`, `TC_SEC_13`, `TC_UI_03` | `tts_player_container_test.dart`, `translator_bot_api_key_test.dart` | **100% Pass** |
| **UC-U7** | Tải chương truyện ngoại tuyến | `TC_FUNC_16`, `TC_FUNC_18` | `TC_SEC_08` | `google_drive_epub_download_test.dart` | **100% Pass** |
| **UC-U8** | Đọc truyện ngoại tuyến (Offline) | `TC_FUNC_11`, `TC_FUNC_20` | `TC_UI_01` | `local_manga_parser_test.dart`, `online_chapter_offline_test.dart` | **100% Pass** |
| **UC-U9** | Quản lý Kệ sách & Nhập tệp cục bộ | `TC_FUNC_07`, `TC_FUNC_09`, `TC_FUNC_10` | `TC_PERF_07` | `drive_incremental_publication_test.dart`, `local_manga_parser_test.dart` | **100% Pass** |
| **UC-U10** | Theo dõi tiến độ & Thống kê đọc | `TC_FUNC_11`, `TC_FUNC_20`, `TC_FUNC_27` | `TC_SEC_03` | `firebase_library_sync_test.dart` | **100% Pass** |
| **UC-A1** | Quản trị nguồn Drive & Cộng đồng | `TC_FUNC_25`, `TC_FUNC_26` | `TC_SEC_04..08`, `TC_SEC_11` | `firestore.rules.test.cjs`, `set_admin_claim_script.test.cjs`, `community_screen_test.dart` | **100% Pass** |
