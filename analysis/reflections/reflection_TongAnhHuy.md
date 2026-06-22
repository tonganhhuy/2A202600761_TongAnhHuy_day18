# Individual Reflection — Lab 18

**Tên:** Tống Anh Huy  
**Module phụ trách:** M1, M2, M3, M4, M5 (Toàn bộ Pipeline)

---

## 1. Đóng góp kỹ thuật

- **Module đã implement:** 
  - Module 1: Chunking (Semantic, Hierarchical, Structure-Aware)
  - Module 2: Hybrid Search (BM25 + Dense Search via Qdrant + RRF Fusion)
  - Module 3: Reranking (CrossEncoder với BAAI/bge-reranker-v2-m3)
  - Module 4: Evaluation (RAGAS với Custom LLM và Local Embeddings)
  - Module 5: Enrichment (Combined Single-Call và các hàm riêng lẻ)
- **Các hàm/class chính đã viết:**
  - `chunk_semantic`, `chunk_hierarchical`, `chunk_structure_aware` trong [m1_chunking.py](file:///d:/Vin_AI_Train/Day_18/2A202600761_TongAnhHuy_day18/src/m1_chunking.py)
  - `segment_vietnamese`, `BM25Search`, `DenseSearch`, `reciprocal_rank_fusion` trong [m2_search.py](file:///d:/Vin_AI_Train/Day_18/2A202600761_TongAnhHuy_day18/src/m2_search.py)
  - `CrossEncoderReranker` trong [m3_rerank.py](file:///d:/Vin_AI_Train/Day_18/2A202600761_TongAnhHuy_day18/src/m3_rerank.py)
  - `evaluate_ragas`, `failure_analysis` trong [m4_eval.py](file:///d:/Vin_AI_Train/Day_18/2A202600761_TongAnhHuy_day18/src/m4_eval.py)
  - `_enrich_single_call` và các hàm làm giàu trong [m5_enrichment.py](file:///d:/Vin_AI_Train/Day_18/2A202600761_TongAnhHuy_day18/src/m5_enrichment.py)
- **Số tests pass:** 
  - M1: 13/13 tests pass
  - M2: 5/5 tests pass
  - M4: 4/4 tests pass
  - M5: 10/10 tests pass
  - M3: 5/5 tests pass

## 2. Kiến thức học được

- **Khái niệm mới nhất:** 
  - Contextual Prepend (Anthropic style): Prepend tiêu đề và ngữ cảnh của tài liệu vào đầu từng chunk để giảm tỷ lệ mất ngữ cảnh khi tìm kiếm.
  - Reciprocal Rank Fusion (RRF): Thuật toán kết hợp danh sách xếp hạng của nhiều phương pháp tìm kiếm (Dense + Sparse) dựa trên thứ hạng mà không cần chuẩn hóa điểm số gốc.
- **Điều bất ngờ nhất:** 
  - Khả năng tương thích ngược của mô hình Gemini qua giao thức OpenAI Client thông qua base URL `https://generativelanguage.googleapis.com/v1beta/openai/` giúp chuyển đổi nhà cung cấp mô hình cực kỳ nhanh chóng.
- **Kết nối với bài giảng (slide nào):** 
  - Bài giảng ngày 18 về Production RAG, phần Advanced Chunking & Hybrid Search.

## 3. Khó khăn & Cách giải quyết

- **Khó khăn lớn nhất:**
  1. Lỗi xung đột thư viện `celery` toàn cục trên máy tính chạy Python 3.12 gây lỗi import `formatargspec` trong `inspect.py`.
  2. Lỗi `Windows fatal exception: access violation` khi import `sentence_transformers` do sự không tương thích của thư viện `torchvision` trên hệ điều hành Windows.
  3. Tốc độ kết nối và tải mô hình nặng `bge-reranker-v2-m3` (2.24 GB) trực tiếp từ Hugging Face Hub.
- **Cách giải quyết:**
  1. Loại trừ plugin celery khi chạy test bằng cách thêm cờ `-p no:celery`.
  2. Gỡ bỏ hoàn toàn `torchvision` bằng lệnh `pip uninstall torchvision` vì dự án RAG dạng văn bản này không cần xử lý ảnh, giúp chấm dứt triệt để lỗi Access Violation của PyTorch.
- **Thời gian debug:** ~45 phút.

## 4. Nếu làm lại

- **Sẽ làm khác điều gì:** Sẽ kiểm tra sự tương thích của PyTorch/Torchvision ngay trên máy tính Windows trước khi cài đặt thêm các thư viện học máy lớn khác.
- **Module nào muốn thử tiếp:** Muốn nghiên cứu sâu hơn về cơ chế tối ưu hóa chi phí token bằng kỹ thuật chunk enrichment (Combined Mode).

## 5. Tự đánh giá

| Tiêu chí | Tự chấm (1-5) |
|----------|---------------|
| Hiểu bài giảng | 5/5 |
| Code quality | 5/5 |
| Teamwork | 5/5 |
| Problem solving | 5/5 |
