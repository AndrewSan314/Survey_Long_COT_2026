# Survey liên quan và cách phân loại literature

Cập nhật **07/11/2026**. Chín survey dưới đây là tập đối chiếu có chủ đích, không phải kết quả systematic review đầy đủ. Mã S0–S5 giữ nguyên từ repo; S6–S8 được bổ sung. Đọc theo phiên bản đã ghim; năm preprint và năm xuất bản có thể khác nhau.

| Mã và nguồn sơ cấp | Phạm vi và cách tổ chức literature | Dùng cho Related Work / liên hệ A1–A4 | Vị trí nguồn |
| --- | --- | --- | --- |
| **S1** — Chen et al., [Towards Reasoning Era](https://arxiv.org/abs/2503.09567v5) (2025) | Long-CoT: Deep Reasoning, Feasible Reflection, Extensive Exploration; các nhánh format/learning, feedback/refinement, scaling/internal/external. | Survey gần nhất về Long-CoT; giải thích đặc trưng suy luận, khác với cách nhóm ta gán vai trò đóng góp A1–A4. | Figures 2–3; §4–6 |
| **S2** — Li et al., [From System 1 to System 2](https://arxiv.org/abs/2502.17419v6) (2025) | Reasoning LLM theo features, methods, evolution; methods gồm structure search, reward modeling, self improvement, macro action, RFT. | Cung cấp bối cảnh mô hình và thuật toán, đặc biệt A1/A2; phạm vi rộng hơn vết Long-CoT. | Figure 2; §3.1–3.3 |
| **S3** — Zhang et al., [A Survey on Test-Time Scaling](https://arxiv.org/abs/2503.24235v3) (2025) | Bốn câu hỏi What / How / Where / How Well; phân biệt scaling song song, tuần tự, hybrid, internal và tuning/inference-based. | Khung so sánh compute, hiệu năng, controllability, scalability; hỗ trợ A1/A2/A4. Long-CoT tuần tự chỉ là một dạng scaling. | Figure 2; §2–5; §8.2 |
| **S4** — Wei et al., [When LLM Meets Tree Search](https://arxiv.org/abs/2608.30395v1) (2026) | Inference-as-search: node representation/granularity, evaluation function, MCTS dynamics và báo cáo compute. | Chi tiết cho A2 và verifier; không coi tree search và chuỗi dài là cùng một kỹ thuật. | §3.2–3.4; bảng so sánh phương pháp |
| **S5** — Lee & Hockenmaier, [Evaluating Step-by-step Reasoning Traces](https://arxiv.org/abs/2502.12289v3) (2025) | Tiêu chí factuality, validity, coherence, utility; evaluator rule-based, intrinsic, external. | Nguồn chính để phân biệt correctness đáp án với chất lượng từng bước trong A4 và phương pháp phân tích A3. | §3; §5 |
| **S0** — Ji et al., [A Survey of Test-Time Compute](https://arxiv.org/abs/2501.02497v3) (2025) | System-1 adaptation theo model/input/representation/output; System-2 reasoning theo feedback, test-time strategies, improvement training. | Bối cảnh chung cho A1/A2; phạm vi gồm cả thích nghi lúc test ngoài Long-CoT. | §3–4; §7 |
| **S6** — Qu et al., [A Survey of Efficient Reasoning for Large Reasoning Models: Language, Multimodality, and Beyond](https://arxiv.org/abs/2503.21614v2) (2025) | Theo lifecycle: inference, SFT, RL, pretraining. Inference chia length budgeting, system/model switch, parallel search. | Liên hệ A1/A2 qua giai đoạn can thiệp; A3 qua inefficiency; A4 qua nhu cầu đo utility/cost. | Figure 3; §2–6; §7.5 |
| **S7** — Sui et al., [Stop Overthinking](https://arxiv.org/abs/2503.16419v4) (2025) | Theo nơi can thiệp: model, reasoning output, input prompts; bổ sung dữ liệu, model compression và evaluation. | Cho thấy efficient reasoning đã được khảo sát rộng; không tuyên bố nhóm là survey đầu tiên nghiên cứu overthinking. | §3–7 |
| **S8** — Zhu & Li, [Towards Concise and Adaptive Thinking](https://arxiv.org/abs/2507.09662v1) (2025) | Training-free: prompting, pipeline, decoding, merging; training-based: fine-tuning, RL. | Đối chiếu A2/A1. Nêu rõ phạm vi loại trừ kiến trúc, model compression nói chung và multimodal efficiency. | §1 (What's not covered?); §3–4 |

## Luận điểm để viết Related Work

1. **Các survey đã có những trục phân loại khác nhau.** S1 mô tả đặc trưng Long-CoT; S2/S0 dùng khung System 1–2; S3 phân tích cách scale compute; S4 đi sâu search; S5 tập trung evaluation; S6–S8 tập trung efficiency/adaptivity.
2. **A1–A4 là cách tổ chức theo vai trò nghiên cứu.** Một paper có thể được đặt vào nhiều taxonomy trước: s1 vừa là SFT dữ liệu ít (A1), vừa có budget forcing (A2). Gán primary/secondary role giúp tránh đếm trùng và giữ rõ đóng góp trung tâm.
3. **Điểm nhấn đề xuất của bản thảo:** nối training/data → inference/control → phân tích hành vi/cơ chế → bằng chứng đánh giá. Đây là lựa chọn tổng hợp của nhóm, chưa phải tuyên bố novelty hay sự vượt trội đã được kiểm chứng.
4. **So sánh cần cùng điều kiện.** Ghi model, split, sampling và tổng chi phí; tách accuracy, process quality, efficiency, faithfulness. Token giảm không tự chứng minh latency/FLOPs giảm tương ứng.

## Quy trình cập nhật và mức kiểm chứng

- Tìm theo từ khóa Long-CoT / long chain-of-thought / reasoning efficiency / underthinking / test-time scaling; mở rộng từ survey và danh mục sẵn có. Ưu tiên nguồn tác giả, arXiv và proceedings.
- Chọn nghiên cứu đại diện cho một phương pháp hoặc hiện tượng; giữ công trình liên quan/nền tảng khi cần giải thích nguồn gốc phương pháp. Đây không phải corpus bao phủ mọi paper đến ngày cập nhật.
- Ngày 07/11 đã đọc các phần hỗ trợ nhận xét của **4 paper mới** và **3 survey mới**, ghim phiên bản; đối chiếu taxonomy của S0–S5 từ PDF sẵn có và spot-check R1 v2. Các bản ghi cũ được kế thừa, không tuyên bố đã tái kiểm toàn bộ số liệu trong lượt này.
- Số liệu là tác giả báo cáo, chưa tái lập thí nghiệm. Không xem đồ thị trích bằng LLM là bằng chứng trực tiếp về cơ chế nhân quả nội tại.

Bản LaTeX tương ứng: [related-work.tex](../overleaf/related-work.tex). Nguồn S0–S5 có [PDF trong repo](surveys/); S6–S8 dùng link phiên bản, không cần commit thêm bản PDF.
