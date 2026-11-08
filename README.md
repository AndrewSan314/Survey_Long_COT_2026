# Long-CoT Survey Papers

Danh mục làm việc cho phần **Research Role (A) & Related Work**, cập nhật bản tiếng Việt ngày 08/11/2026: **24 paper nghiên cứu** (19 Long-CoT trực tiếp) và **9 survey** đối chiếu taxonomy.

- **[Đọc trước: Tổng hợp chi tiết literature theo A1–A4](papers/literature-review.md)** — 24 paper, 16 hướng nhỏ; có cơ chế phương pháp, thiết lập/metric, kết quả, đóng góp, hạn chế, nhận xét đối chiếu và vị trí nguồn.
- [Hồ sơ paper đầy đủ và vị trí nguồn](papers/research-role.md): số liệu chi tiết, scope, nhận xét phương pháp và primary/secondary role.
- [Phân tích bổ sung và 8 câu hỏi nghiên cứu](papers/research-directions.md): tài liệu mở rộng, không thay thế đầu ra literature review.
- [Related Work: phạm vi, taxonomy và cách dùng 9 survey](papers/related-work.md).
- [Bản thảo LaTeX/BibTeX để nhập Overleaf](overleaf/README.md) và [PDF xem trước](overleaf/draft-main.pdf).
- [Hướng dẫn bổ sung paper qua pull request](CONTRIBUTING.md).

Các nhóm nhỏ là đề xuất tổ chức literature của nhóm, có thể điều chỉnh khi thêm paper. Danh mục phân biệt paper Long-CoT trực tiếp, nghiên cứu suy luận liên quan và công trình nền tảng; số liệu là kết quả tác giả báo cáo, chưa được nhóm tái lập.

**Bố cục PDF theo phân công:** Literature Review nằm trước, gồm đúng bốn nhóm A1–A4; mỗi nhóm có hướng nhỏ, paper tiêu biểu và tổng hợp kết quả/hạn chế. Related Work nằm sau, tập trung vào phạm vi và cách phân loại của chín survey. Phần RQ/phân tích mở rộng được giữ trong tài liệu bổ sung, không đưa vào PDF chính.

**Mức chi tiết hiện tại:** 24 hồ sơ trong PDF/Markdown đều nêu model, benchmark và cách đọc metric theo thiết lập đã báo cáo, kèm vị trí nguồn. Có 16 phân tích subgroup, bốn bảng đối chiếu trong A1–A4 và bảng crosswalk chín survey. Nhận xét tổng hợp được ghi riêng với kết quả tác giả; không dùng chênh lệch điểm giữa các setup khác nhau để xếp hạng phương pháp.

| Yêu cầu | Đầu ra để kiểm tra |
| --- | --- |
| Paper theo A1–A4, ưu tiên Long-CoT trực tiếp | [Bản tổng hợp 24 paper](papers/literature-review.md), có nhãn phạm vi |
| Bài toán, phương pháp, kết quả, đóng góp | Bốn trường ghi rõ cho từng paper; bổ sung thiết lập/metric, hạn chế, nhận xét và vị trí nguồn |
| Hướng nhỏ dựa trên phương pháp | 16 subgroup; distillation và data synthesis/selection được nêu tường minh |
| Survey cho Related Work | [Chín survey](papers/related-work.md), tách scope và taxonomy |
| Bản thảo LaTeX để ghép vào bài nhóm | [Nguồn và cách build](overleaf/README.md), [PDF](overleaf/draft-main.pdf) |
| Repo để thành viên bổ sung | [Quy trình pull request](CONTRIBUTING.md) |

**Ngôn ngữ:** Nội dung LaTeX/PDF, bảng và chú thích dùng tiếng Việt; giữ terminology, tên paper/model/dataset và ký hiệu chuyên môn. Nguồn và số liệu vẫn theo bản tổng hợp ngày 07/11/2026; chuyển ngôn ngữ không đồng nghĩa đã cập nhật literature mới.

| Nhóm | Số paper chính | Các hướng nhỏ và paper tiêu biểu |
| --- | --- | --- |
| **A1 Training/Data** | 6 | RL (R1, Kimi); SFT (s1, LIMO); data synthesis/selection và curriculum (Light-R1); efficiency RL (Arora & Zanette); distillation/Long2short (dẫn chéo R1, Kimi) |
| **A2 Inference/Control** | 5 | Dừng sớm (DTSR, REFRAIN); phát hiện bẫy/restart và search (TAAR, MCTSr); quản lý context (Recursive Models); budget forcing/độ sâu khám phá (dẫn chéo s1, TIP, FSF) |
| **A3 Analysis** | 8 | Discourse/faithfulness (ReasoningFlow, Lanham); graph/failure (CoT2Graph, FSF); scaling limits (ZebraLogic); overthinking/underthinking/self-doubt (Chen, Wang, Peng) |
| **A4 Evaluation/Benchmark** | 5 | Long-horizon stress test (LongCoT, SPaRC); chỉ số redundancy (CoTJudger); process error/critique (ProcessBench, CriticBench) |

Mỗi paper chỉ tính một primary role. Danh mục chọn paper đại diện, chưa phải systematic review bao phủ toàn bộ literature đến ngày cập nhật. Thư mục `overleaf/` chứa **bản LaTeX build local**; không cần link hay tài khoản Overleaf.

## Survey dùng để đối chiếu taxonomy

Giữ nguyên 6 survey đã có (S0–S5), bổ sung 3 survey về efficient/adaptive reasoning (S6–S8). Bảng phân tích cả 9 survey ở [Related Work](papers/related-work.md).

Các PDF được tải trực tiếp từ arXiv ngày 05/11/2026, giữ đúng phiên bản đã dùng trong báo cáo. Mã S0–S5 khớp với danh mục tài liệu tham khảo.

| Mã | Survey | Tác giả | Phiên bản | PDF | Nguồn |
| --- | --- | --- | --- | --- | --- |
| S1 | Towards Reasoning Era: A Survey of Long Chain-of-Thought for Reasoning Large Language Models | Qiguang Chen et al. | 2503.09567v5 | [PDF](papers/surveys/S1_Towards_Reasoning_Era_2503.09567v5.pdf) | [arXiv](https://arxiv.org/abs/2503.09567v5) |
| S2 | From System 1 to System 2: A Survey of Reasoning Large Language Models | Zhong-Zhi Li et al. | 2502.17419v6 | [PDF](papers/surveys/S2_From_System_1_to_System_2_2502.17419v6.pdf) | [arXiv](https://arxiv.org/abs/2502.17419v6) |
| S3 | A Survey on Test-Time Scaling in Large Language Models: What, How, Where, and How Well? | Qiyuan Zhang et al. | 2503.24235v3 | [PDF](papers/surveys/S3_Test_Time_Scaling_2503.24235v3.pdf) | [arXiv](https://arxiv.org/abs/2503.24235v3) |
| S4 | When LLM Meets Tree Search: A Systematic View of Inference as Search in Large Language Models | Jiaqi Wei et al. | 2608.30395v1 | [PDF](papers/surveys/S4_When_LLM_Meets_Tree_Search_2608.30395v1.pdf) | [arXiv](https://arxiv.org/abs/2608.30395v1) |
| S5 | Evaluating Step-by-step Reasoning Traces: A Survey | Jinu Lee & Julia Hockenmaier | 2502.12289v3 | [PDF](papers/surveys/S5_Evaluating_Step_by_Step_Reasoning_Traces_2502.12289v3.pdf) | [arXiv](https://arxiv.org/abs/2502.12289v3) |
| S0 | A Survey of Test-Time Compute: From Intuitive Inference to Deliberate Reasoning | Yixin Ji et al. | 2501.02497v3 | [PDF](papers/surveys/S0_Test_Time_Compute_2501.02497v3.pdf) | [arXiv](https://arxiv.org/abs/2501.02497v3) |
| S6 | A Survey of Efficient Reasoning for Large Reasoning Models: Language, Multimodality, and Beyond | Xiaoye Qu et al. | 2503.21614v2 | Nguồn trực tuyến | [arXiv](https://arxiv.org/abs/2503.21614v2) |
| S7 | Stop Overthinking: A Survey on Efficient Reasoning for Large Language Models | Yang Sui et al. | 2503.16419v4 | Nguồn trực tuyến | [arXiv](https://arxiv.org/abs/2503.16419v4) |
| S8 | Towards Concise and Adaptive Thinking in Large Reasoning Models: A Survey | Jason Zhu & Hongyu Li | 2507.09662v1 | Nguồn trực tuyến | [arXiv](https://arxiv.org/abs/2507.09662v1) |

S0–S5 giữ nguyên mã và PDF của báo cáo trước; bản Related Work hiện tại so sánh cả S0–S8. Các nguồn mới được đọc ngày 07/11/2026.

Các bản PDF giữ nguyên nội dung từ nguồn. Quyền tác giả và điều khoản sử dụng theo từng công trình và bản ghi arXiv tương ứng.
