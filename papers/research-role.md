# Paper theo Research Role A1–A4

Cập nhật: **07/11/2026**. Danh mục làm việc gồm **24 paper**: **A1: 6, A2: 5, A3: 8, A4: 5**, với **19 Long-CoT trực tiếp, 4 nghiên cứu liên quan, 1 công trình nền tảng**. Các nhóm nhỏ là đề xuất tổng hợp của nhóm, không phải taxonomy do từng paper đặt ra.

Mỗi paper có một vai trò chính theo đóng góp trung tâm và có thể có vai trò phụ. Danh mục ưu tiên Long-CoT; MCTSr, ZebraLogic, ProcessBench và CriticBench cung cấp đối chiếu về tìm kiếm, độ phức tạp, phát hiện lỗi và phê phán; Lanham et al. cung cấp phương pháp can thiệp để khảo sát tính trung thực của CoT.

Số liệu dưới đây là kết quả tác giả báo cáo trong các thiết lập đã ghi, chưa được nhóm tái lập. Không dùng số đường đi thay cho tổng token/FLOPs; không đồng nhất tương quan quan sát hoặc đồ thị trích xuất với cơ chế nhân quả nội tại. `pp` là điểm phần trăm.

Đi tới: [A1](#a1-trainingdata) · [A2](#a2-inferencecontrol) · [A3](#a3-analysis) · [A4](#a4-evaluationbenchmark). Xem [bản thảo Related Work](../overleaf/related-work.tex), [PDF](../overleaf/draft-main.pdf) và [hướng dẫn đóng góp](../CONTRIBUTING.md).

**Quy tắc phạm vi:** Long-CoT ở đây là suy luận có deliberation mở rộng, khám phá hoặc tự kiểm tra; không đặt một ngưỡng token chung và không đồng nhất với đầu vào long-context. Chọn A1 khi đóng góp chính thay đổi dữ liệu/trọng số; A2 khi thay đổi thực thi lúc suy luận; A3 khi giải thích/kiểm tra một hiện tượng; A4 khi cung cấp benchmark hoặc giao thức/chỉ số đánh giá. Ví dụ s1 thuộc A1 nhưng budget forcing dẫn chéo A2; ZebraLogic có primary A3 và secondary A4. Không đếm lại paper khi dẫn chéo.

**Đọc trước:** [Tổng hợp literature theo A1–A4](literature-review.md) là bản tóm tắt đúng phân công và tương ứng với PDF chính. Tệp hiện tại là hồ sơ chi tiết: “Đọc phương pháp” giải thích cơ chế; “Nhận xét đối chiếu của nhóm” là diễn giải, không phải kết quả thực nghiệm mới. [Phân tích bổ sung](research-directions.md) trình bày 16 subgroup và 8 RQ ngoài PDF chính.

## A1 Training/Data

| Nhóm nhỏ đề xuất | Paper đại diện |
| --- | --- |
| A1.1 — RL hình thành năng lực reasoning | [DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](#rra1-deepseek-r1); [Kimi k1.5: Scaling Reinforcement Learning with LLMs](#rra1-kimi-k15) |
| A1.2 — SFT với dữ liệu được chọn lọc | [s1: Simple test-time scaling](#rra1-s1); [LIMO: Less is More for Reasoning](#rra1-limo) |
| A1.3 — Data synthesis/selection và curriculum | [Light-R1: Curriculum SFT, DPO and RL for Long COT from Scratch and Beyond](#rra1-light-r1) |
| A1.4 — RL hướng efficiency | [Training Language Models to Reason Efficiently](#rra1-efficient-rl); dẫn chéo Long2short của [Kimi k1.5](#rra1-kimi-k15) và self-training của [Chen et al.](#rra3-chen-overthinking) |
| A1.5 — Distillation và Long2short | Dẫn chéo [DeepSeek-R1](#rra1-deepseek-r1) và [Kimi k1.5](#rra1-kimi-k15); không thêm paper vào tổng số |

### rra1-deepseek-r1

**[DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](https://arxiv.org/abs/2501.12948v2)**

Tác giả: DeepSeek-AI.
Vai trò chính: **A1**; vai trò phụ: A3; nhóm nhỏ: A1.1: RL hình thành năng lực reasoning; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v2](https://arxiv.org/abs/2501.12948v2); Preprint (arXiv:2501.12948v2).

- **Bài toán:** Khảo sát sự phát sinh hành vi suy luận chuỗi dài qua pure RL không cần dữ liệu SFT khởi động và cách chuyển giao tri thức sang mô hình nhỏ.
- **Phương pháp:** DeepSeek-R1-Zero áp dụng thuật toán GRPO (không critic network) với reward dựa trên độ đúng đáp án và định dạng tag; DeepSeek-R1 kết hợp quy trình multi-stage (cold-start SFT, reasoning RL, rejection sampling tạo 800k mẫu, general RL) và chưng cất sang Qwen/Llama.
- **Kết quả tác giả báo cáo:** R1-Zero đạt 77.9% AIME24 và 95.9% MATH-500; DeepSeek-R1 (671B MoE) đạt 79.8% AIME24, 97.3% MATH-500, 71.5% GPQA Diamond; Distill-Qwen-32B đạt 72.6% AIME24.
- **Đóng góp:** Báo cáo hành vi tự kiểm chứng và tự phản tư phát sinh nội sinh trong thiết lập pure RL; đề xuất quy trình multi-stage giải quyết vấn đề đọc hiểu và ngôn ngữ; xác nhận hiệu quả chưng cất cho mô hình nhỏ.
- **Giới hạn:** Gặp khó khăn trong tác vụ tổng quát, pha trộn ngôn ngữ khi huấn luyện pure RL thuần túy, nhạy cảm với reward hacking nếu thiếu verifier tất định.
- **Vị trí nguồn:** arXiv:2501.12948v2, §2.1–2.3, §3, Table 2, Appendix B.3.3 và F. Không trộn số liệu/đánh số mục với v1.

- **Đọc phương pháp:** Tách hai thí nghiệm: R1-Zero khảo sát RL từ base không có SFT khởi động; R1 là pipeline nhiều giai đoạn để tăng tính hữu dụng. GRPO dùng so sánh reward trong nhóm rollout, không có nghĩa training không cần nhiều mẫu sinh.
- **Nhận xét đối chiếu của nhóm:** Dùng làm mốc cho capability-oriented RL và distillation. Không suy ra RL đã tạo toàn bộ tri thức từ đầu; base model và verifier vẫn là điều kiện thiết yếu. So sánh phải giữ đúng bản v2 và phân biệt Pass@1 với self-consistency.

Khóa BibTeX: `rra1_deepseek_r1` trong [references.bib](../overleaf/references.bib).

### rra1-s1

**[s1: Simple test-time scaling](https://arxiv.org/abs/2501.19393v3)**

Tác giả: Niklas Muennighoff; Zitong Yang; Weijia Shi; Xiang Lisa Li; Li Fei-Fei; Hannaneh Hajishirzi; Luke Zettlemoyer; Percy Liang; Emmanuel Candès; Tatsunori Hashimoto.
Vai trò chính: **A1**; vai trò phụ: A2; nhóm nhỏ: A1.2: SFT với dữ liệu được chọn lọc; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v3](https://arxiv.org/abs/2501.19393v3); Preprint (arXiv:2501.19393v3).

- **Bài toán:** Khảo sát xem năng lực suy luận chuỗi dài có thể được kích hoạt bằng lượng dữ liệu giám sát cực nhỏ hay bắt buộc phải dùng RL phức tạp và hàng trăm nghìn mẫu SFT.
- **Phương pháp:** Tinh chọn tập s1K (1,000 bài toán khó) với vết suy luận chưng cất từ Gemini 2.0 Flash Thinking Experimental; huấn luyện SFT chuẩn trên Qwen2.5-32B-Instruct; kết hợp kỹ thuật test-time budget forcing (chặn `</thought>`, chèn "Wait").
- **Kết quả tác giả báo cáo:** s1-32B không can thiệp đạt 50.0% AIME24; khi bật budget forcing đạt 56.7% AIME24, 93.0% MATH-500, 59.6% GPQA Diamond (tăng +30.0 pp AIME so với base 26.7%).
- **Đóng góp:** Minh chứng hiệu quả mẫu cao của phương pháp SFT tinh chọn tối giản trong thiết lập thử nghiệm; đề xuất cơ chế budget forcing đơn giản lúc suy luận.
- **Giới hạn:** Kết quả phụ thuộc vào base model và chất lượng vết giải từ teacher trong thiết lập đã thử; không chứng minh cơ chế tri thức của mọi mô hình.
- **Vị trí nguồn:** arXiv:2501.19393, §2.1, §3.1, §4.1, Table 1

- **Đọc phương pháp:** SFT trên s1K và budget forcing là hai thành phần khác nhau: phần đầu thay trọng số, phần sau ép kéo dài hoặc kết thúc generation. Chất lượng lựa chọn dữ liệu quan trọng hơn việc chỉ báo cáo số mẫu nhỏ.
- **Nhận xét đối chiếu của nhóm:** Dùng để nối A1 với A2: cần ablation SFT-only, control-only và kết hợp trên cùng checkpoint. Số mẫu fine-tuning không bao gồm chi phí tạo/lọc dữ liệu teacher; không xem đây là tổng chi phí xây dựng reasoning model.

Khóa BibTeX: `rra1_s1` trong [references.bib](../overleaf/references.bib).

### rra1-kimi-k15

**[Kimi k1.5: Scaling Reinforcement Learning with LLMs](https://arxiv.org/abs/2501.12599v4)**

Tác giả: Kimi Team.
Vai trò chính: **A1**; vai trò phụ: A3; nhóm nhỏ: A1.1: RL hình thành năng lực reasoning; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v4](https://arxiv.org/abs/2501.12599v4); Preprint (arXiv:2501.12599v4).

- **Bài toán:** Mở rộng học tăng cường (RL) lên ngữ cảnh siêu dài (128k tokens) cho văn bản và đa phương thức, kiểm soát độ ổn định gradient và tối ưu chi phí suy luận.
- **Phương pháp:** Warmup SFT kết hợp Online Policy Mirror Descent không dùng value model (value-head free), khai thác gradient âm từ vết giải lỗi, chính quy hóa relative entropy, CoT Reward Model (dùng suy luận CoT để phán quyết độ đúng đáp án cuối có giải trình JSON), và khung nén Long2short.
- **Kết quả tác giả báo cáo:** Đạt 77.5% Pass@1 AIME24, 96.2% MATH-500, 74.9% MathVista; CoT-RM phán quyết độ đúng đáp án cuối đạt độ chính xác ~98.5% trên mẫu kiểm tra thủ công của tác giả (so với ~84.4% của Classic RM); Long2short giảm độ trễ và độ dài chuỗi.
- **Đóng góp:** Báo cáo công thức mở rộng RL với chuỗi 128k tokens; áp dụng chính sách không value network kết hợp gradient âm; đề xuất phương pháp chưng cất Long2short.
- **Giới hạn:** Tiêu tốn chi phí hạ tầng tính toán lớn; CoT-RM đòi hỏi thêm compute khi chấm điểm so với outcome RM thông thường.
- **Vị trí nguồn:** arXiv:2501.12599v4, §2.2, §2.3.2, §2.3.5, Table 2, Figure 10

- **Đọc phương pháp:** Phân biệt context scaling trong RL với Long2short sau đó. CoT-RM dùng lập luận để chấm độ đúng đáp án cuối; tên gọi này không đồng nghĩa có nhãn reward đúng/sai ở từng bước của policy.
- **Nhận xét đối chiếu của nhóm:** Dùng để thảo luận chuyển giao năng lực từ long sang short traces. Accuracy của reward model trên mẫu spot-check không phải accuracy giải bài; cần tách compute của policy, rollout và reward model khi so sánh chi phí.

Khóa BibTeX: `rra1_kimi_k15` trong [references.bib](../overleaf/references.bib).

### rra1-limo

**[LIMO: Less is More for Reasoning](https://arxiv.org/abs/2502.03387v3)**

Tác giả: Yixin Ye; Zhen Huang; Yang Xiao; Ethan Chern; Shijie Xia; Pengfei Liu.
Vai trò chính: **A1**; vai trò phụ: A3; nhóm nhỏ: A1.2: SFT với dữ liệu được chọn lọc; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v3](https://arxiv.org/abs/2502.03387v3); Preprint (arXiv:2502.03387v3).

- **Bài toán:** Khảo sát giới hạn tối thiểu của dữ liệu SFT trong việc kích hoạt năng lực suy luận toán thi đấu đỉnh cao trên mô hình nền tảng.
- **Phương pháp:** Lọc câu hỏi 2 tầng (loại bài dễ, giữ bài DeepSeek-R1-Distill-32B giải đúng 1-3/32 lần); chấm điểm vết suy luận theo rubric 4 chiều (lập luận, tự kiểm tra, thăm dò, độ hạt thích ứng); huấn luyện SFT trên 817 mẫu chọn lọc nhất với Qwen2.5-32B-Instruct.
- **Kết quả tác giả báo cáo:** LIMO-32B đạt 63.3% AIME24, 95.6% MATH-500, 96.3% AMC23; khi chuyển sang base model yếu hơn (Qwen1.5-32B-Chat), hiệu năng AIME24 sụt giảm mạnh xuống 9.2% (-54.1 pp).
- **Đóng góp:** Báo cáo hiệu quả mẫu của SFT trên mô hình nền mạnh trong thiết lập đã thử; đề xuất rubric bốn chiều để tinh chọn vết giải.
- **Giới hạn:** Hiệu quả mẫu phụ thuộc vào năng lực của base model được thử nghiệm; thực nghiệm không cung cấp bằng chứng trực tiếp về cơ chế tiền huấn luyện.
- **Vị trí nguồn:** arXiv:2502.03387v3, §3, §3.1, §6.2, Table 1, §6.3.3

- **Đọc phương pháp:** LIMO lọc cả độ khó câu hỏi lẫn chất lượng vết giải. Một bộ dữ liệu nhỏ nhưng có self-verification và exploration khác với cắt ngẫu nhiên một tập SFT lớn xuống cùng số mẫu.
- **Nhận xét đối chiếu của nhóm:** Dùng để đối chiếu giả thuyết elicitation trên base mạnh với việc học năng lực mới. Thí nghiệm đổi base làm thay đổi nhiều yếu tố đồng thời; chưa cô lập được tri thức pretraining, instruction tuning và kiến trúc.

Khóa BibTeX: `rra1_limo` trong [references.bib](../overleaf/references.bib).

### rra1-light-r1

**[Light-R1: Curriculum SFT, DPO and RL for Long COT from Scratch and Beyond](https://arxiv.org/abs/2503.10460v4)**

Tác giả: Liang Wen; Yunke Cai; Fenrui Xiao; Xin He; Qi An; Zhenyu Duan; Yimin Du; Junchen Liu; Lifu Tang; Xiaowei Lv; Haosheng Zou; Yongchao Deng; Shousheng Jia; Xiangzheng Zhang.
Vai trò chính: **A1**; vai trò phụ: A4; nhóm nhỏ: A1.3: Data synthesis/selection và curriculum; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v4](https://arxiv.org/abs/2503.10460v4); Author-reported ACL 2025 Industry Track; arXiv:2503.10460v4.

- **Bài toán:** Cung cấp công thức giáo trình huấn luyện mở, có thể tái lập Long-CoT từ checkpoint short-CoT và xử lý rò rỉ dữ liệu kiểm chuẩn mở.
- **Phương pháp:** Quy trình gồm 3 giai đoạn huấn luyện (SFT-1 với 76k bài toán đã lọc và độ dài tối đa 20k tokens, SFT-2 với 3k bài thi đấu, DPO bán on-policy) kết hợp Model Merging trên checkpoint Qwen2.5-32B-Instruct; kèm kiểm định khử nhiễm benchmark nghiêm ngặt.
- **Kết quả tác giả báo cáo:** Light-R1-32B tăng tiến AIME24 qua các giai đoạn (Base 16.6% -> SFT-1 69.0% -> SFT-2 73.0% -> DPO 75.8% -> Merging 76.6%), trong khi GPQA biến động (64.3% ở SFT-1 -> 60.6% ở SFT-2 -> 61.8% ở mô hình cuối); phát hiện rò rỉ đề thi trong nhiều tập dữ liệu mở trước đó.
- **Đóng góp:** Công bố công thức giáo trình đào tạo Long-CoT mở có khả năng tái lập; định lượng vai trò của 3k mẫu chất lượng cao; cung cấp bộ kiểm tra rò rỉ benchmark.
- **Giới hạn:** Khởi tạo từ checkpoint instruct mạnh đã qua căn chỉnh; phụ thuộc vào dữ liệu thi đấu chất lượng cao ở Stage 2.
- **Vị trí nguồn:** arXiv:2503.10460v4, §3.1.2, §3.2, Table 2, Table 7

- **Đọc phương pháp:** Phân tích pipeline theo từng bước SFT-1, SFT-2, DPO và merging; chữ from scratch ở đây không phải huấn luyện từ trọng số ngẫu nhiên. Kiểm tra decontamination là một phần của bằng chứng về chất lượng dữ liệu.
- **Nhận xét đối chiếu của nhóm:** Dùng để thảo luận curriculum và trade-off giữa toán với miền khác: AIME tăng qua các stage nhưng GPQA không tăng đơn điệu. Không quy toàn bộ gain cho một stage nếu không kiểm soát thay đổi dữ liệu, budget và checkpoint.

Khóa BibTeX: `rra1_light_r1` trong [references.bib](../overleaf/references.bib).

### rra1-efficient-rl

**[Training Language Models to Reason Efficiently](https://arxiv.org/abs/2502.04463v4)** — Daman Arora; Andrea Zanette (2025).

Vai trò chính: **A1**; phụ: A2, A3; nhóm nhỏ: **A1.4**; phạm vi: **Long-CoT trực tiếp**.

- **Bài toán:** Học phân bổ compute theo độ khó.
- **Phương pháp:** RL với reward kết hợp độ đúng và phạt độ dài, điều chỉnh bằng hệ số alpha.
- **Kết quả:** Với DeepSeek-R1-Distill-Qwen-7B, alpha=0.2 giảm token 83% trên GSM8K nhưng 27% trên AIME24; đây là hai mức tiết kiệm theo tác vụ, không phải cùng độ chính xác.
- **Đóng góp:** Học đường đánh đổi accuracy–compute thay vì chỉ cắt chuỗi.
- **Giới hạn:** Nén có thể giảm accuracy và faithfulness; bảo đảm lý thuyết cần các giả định lý tưởng.
- **Nguồn:** v4, §4, §5.3.1–5.3.2, Figure 3; khóa `rra1_efficient_rl`.

- **Đọc phương pháp:** Length penalty thay đổi mục tiêu tối ưu của policy, không chỉ đặt max_tokens khi decode. Cùng một alpha có thể tạo mức nén khác nhau giữa tác vụ dễ và khó.
- **Nhận xét đối chiếu của nhóm:** Dùng làm đại diện learned compute allocation. Cần báo accuracy–cost frontier và faithfulness cùng nhau; mệnh đề tối ưu ở population level không bảo đảm một lần huấn luyện hữu hạn giữ nguyên độ đúng.

## A2 Inference/Control

| Nhóm nhỏ đề xuất | Paper đại diện |
| --- | --- |
| A2.1 — Adaptive reasoning và early stopping | [When Is Thinking Enough? Early Exit via Sufficiency Assessment for Efficient Reasoning](#rra2-dtsr); [Stop When Enough: Adaptive Early-Stopping for Chain-of-Thought Reasoning](#rra2-refrain) |
| A2.2 — Search, branching và phục hồi trajectory | [Thinking Traps in Long Chain-of-Thought: A Measurable Study and Trap-Aware Adaptive Restart](#rra2-taar); [Accessing GPT-4 level Mathematical Olympiad Solutions via Monte Carlo Tree Self-refine with LLaMa-3 8B](#rra2-mctsr) |
| A2.3 — Cô lập context và quản lý state | [Recursive Models for Long-Horizon Reasoning](#rra2-recursive-models) |
| A2.4 — Test-time compute và điều khiển độ sâu | Dẫn chéo [s1 / budget forcing](#rra1-s1), [Underthinking / TIP](#rra3-underthinking) và [FSF / branch pruning](#rra3-effective-reasoning); các paper giữ primary role gốc |

### rra2-taar

**[Thinking Traps in Long Chain-of-Thought: A Measurable Study and Trap-Aware Adaptive Restart](https://arxiv.org/abs/2601.11940v1)**

Tác giả: Kang Chen; Fan Yu; Junjie Nian; Shihan Zhao; Zhuoka Feng; Zijun Yao; Heng Wang; Minshen Yu; Yixin Cao.
Vai trò chính: **A2**; vai trò phụ: A3; nhóm nhỏ: A2.2: Search, branching và phục hồi trajectory; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v1](https://arxiv.org/abs/2601.11940v1); Author-reported Findings of ACL 2026; arXiv:2601.11940v1.

- **Bài toán:** Hiện tượng bẫy tư duy (thinking traps) do cam kết sai sớm ở đoạn đầu chuỗi tự củng cố, khiến nỗ lực tự sửa muộn ở cuối chuỗi thất bại.
- **Phương pháp:** Khung TAAR gồm policy chẩn đoán nhẹ pi_phi dự đoán vị trí bẫy t_hat và xác suất thoát lỗi p_hat; bộ điều khiển thực hiện Cut@Trap cắt bỏ phân đoạn bẫy và tái khởi động suy luận với nhiệt độ thích ứng.
- **Kết quả tác giả báo cáo:** Với cùng ngân sách đường đi báo cáo K=4, trên DeepSeek-R1-Distill-Qwen-8B, độ chính xác trung bình trên 5 benchmark đạt 69.1% (tăng +4.6 pp so với Avg@4 64.5% và +3.1 pp so với PRM@4 66.0%); Cut@Trap đạt escape rate 16.5% (8B); trên GPT-OSS-120B đạt 79.2% (thấp hơn Avg@4 80.6%).
- **Đóng góp:** Định lượng hiện tượng bẫy tư duy tập trung ở đoạn đầu chuỗi (44.4% xuất hiện trước vị trí 0.2); đề xuất cơ chế Cut@Trap can thiệp thích ứng lúc suy luận dựa trên chẩn đoán bẫy.
- **Giới hạn:** Không đo trực tiếp cơ chế chú ý (attention mechanism); trên mô hình biên giới rất lớn (120B) có thể cắt nhầm đường dẫn gần đúng làm giảm độ chính xác.
- **Vị trí nguồn:** arXiv:2601.11940v1, §3.1, Figure 4, §5.2, Table 2

- **Đọc phương pháp:** Đơn vị can thiệp là prefix được chẩn đoán mắc bẫy: cắt trước đoạn lỗi rồi sinh lại. Khác với tự phản tư chỉ nối thêm token vào cùng prefix sai, nhưng cần policy chẩn đoán đã huấn luyện.
- **Nhận xét đối chiếu của nhóm:** Dùng để nối phân tích lỗi A3 với recovery A2. Cùng K=4 chưa đồng nghĩa cùng tổng token hoặc thời gian; phải tính phần prefix bị bỏ, lượt chẩn đoán và rollout sinh lại. Kết quả trên 120B cho thấy restart không luôn có lợi.

Khóa BibTeX: `rra2_taar` trong [references.bib](../overleaf/references.bib).

### rra2-dtsr

**[When Is Thinking Enough? Early Exit via Sufficiency Assessment for Efficient Reasoning](https://arxiv.org/abs/2604.06787v1)**

Tác giả: Yang Xiang; Yixin Ji; Ruotao Xu; Dan Qiao; Zheming Yang; Juntao Li; Min Zhang.
Vai trò chính: **A2**; vai trò phụ: A3; nhóm nhỏ: A2.1: Adaptive reasoning và early stopping; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v1](https://arxiv.org/abs/2604.06787v1); Author-reported ACL 2026 Main Conference; arXiv:2604.06787v1.

- **Bài toán:** Hiện tượng overthinking khi mô hình tiếp tục kéo dài vết suy luận dù đã tích lũy đủ thông tin để kết luận đúng, làm tăng token và độ trễ.
- **Phương pháp:** Cơ chế DTSR không cần huấn luyện, giám sát từ khóa phản tư ("Wait", "Alternative") để xác định điểm kiểm tra, sau đó dùng prompt tự đánh giá độ đủ suy luận (thought sufficiency); nếu vượt ngưỡng tau thì ép dừng `</think>`.
- **Kết quả tác giả báo cáo:** Trên Qwen3-14B, độ chính xác đạt 84.8% (+0.4 pp so với baseline 84.4%) trong khi giảm 34.9% token; trên Qwen3-8B, token giảm 32.0% nhưng độ chính xác giảm nhẹ 0.9 pp (81.0% vs 81.9%).
- **Đóng góp:** Đề xuất phương pháp metacognitive sufficiency check không cần huấn luyện giúp tiết kiệm đáng kể chi phí token lúc suy luận.
- **Giới hạn:** Hiệu năng tự đánh giá độ đủ suy luận phụ thuộc vào quy mô mô hình; mô hình nhỏ hơn có thể dừng sớm khi chưa giải quyết trọn vẹn bài toán.
- **Vị trí nguồn:** arXiv:2604.06787v1, §2.2, §3.2, Table 1

- **Đọc phương pháp:** Tách thời điểm kiểm tra khỏi tiêu chuẩn dừng: tín hiệu phản tư/chu kỳ kiểm tra quyết định khi nào hỏi, sufficiency assessment quyết định có đủ để kết luận hay chưa.
- **Nhận xét đối chiếu của nhóm:** Dùng để so với fixed-budget truncation và confidence stopping. Accuracy trung bình gần nhau chưa chứng minh từng bài đều được giữ đúng; cần phân tích correct→wrong khi dừng sớm và đo latency gồm các lần sufficiency check.

Khóa BibTeX: `rra2_dtsr` trong [references.bib](../overleaf/references.bib).

### rra2-refrain

**[Stop When Enough: Adaptive Early-Stopping for Chain-of-Thought Reasoning](https://arxiv.org/abs/2510.10103v1)**

Tác giả: Renliang Sun; Wei Cheng; Dawei Li; Haifeng Chen; Wei Wang.
Vai trò chính: **A2**; vai trò phụ: A3; nhóm nhỏ: A2.1: Adaptive reasoning và early stopping; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v1](https://arxiv.org/abs/2510.10103v1); Preprint (arXiv:2510.10103v1).

- **Bài toán:** Chuỗi suy luận dài lặp lại các bước giải thích hoặc tính toán lại đáp án đã có, dẫn đến dư thừa phản tư và nguy cơ trôi dạt ngữ nghĩa.
- **Phương pháp:** REFRAIN kiểm tra đồng thời giả thuyết đáp án, token phản tư và độ dư thừa ngữ nghĩa cosine similarity giữa embedding câu hiện tại và quá khứ; dùng thuật toán Sliding-Window UCB bandit để tự điều chỉnh ngưỡng dừng tau.
- **Kết quả tác giả báo cáo:** Trên gpt-oss-20B, tăng Pass@1 trên toàn bộ benchmark thử nghiệm (+2.73 pp GSM8K, +3.40 pp MATH-500, +7.07 pp GPQA Diamond) và giảm 33.3% đến 44.7% token; trên Qwen3-8B tiết kiệm 21.5% đến 54.2% token.
- **Đóng góp:** Thiết lập chỉ số đo lường độ dư thừa phản tư dựa trên embedding câu; ứng dụng thuật toán bandit trực tuyến để điều tiết ngưỡng dừng tự thích ứng.
- **Giới hạn:** Dư thừa phản tư dựa trên embedding ngữ nghĩa không đồng nhất hoàn toàn với độ đủ logic hình thức; phụ thuộc vào chất lượng mô hình embedding câu.
- **Vị trí nguồn:** arXiv:2510.10103v1, §3.2, §3.4, §5.1, Table 1

- **Đọc phương pháp:** REFRAIN kết hợp đáp án hiện có, trigger phản tư và similarity; SW-UCB cập nhật ngưỡng từ reward gồm answer-only likelihood và phạt độ dài. Tín hiệu quality này là proxy không cần ground-truth test.
- **Nhận xét đối chiếu của nhóm:** Dùng để phân biệt online adaptation của controller với cập nhật trọng số LLM. Similarity có thể nhầm phép kiểm tra hữu ích với lặp thừa; likelihood cao cũng không bảo đảm correctness. Xem §3.3–3.6 cho cơ chế reward.

Khóa BibTeX: `rra2_refrain` trong [references.bib](../overleaf/references.bib).

### rra2-recursive-models

**[Recursive Models for Long-Horizon Reasoning](https://arxiv.org/abs/2603.02112v2)**

Tác giả: Chenxiao Yang; Nathan Srebro; Zhiyuan Li.
Vai trò chính: **A2**; vai trò phụ: A1; nhóm nhỏ: A2.3: Cô lập context và quản lý state; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v2](https://arxiv.org/abs/2603.02112v2); Author-reported ICML 2026; arXiv:2603.02112v2.

- **Bài toán:** Mô hình tự hồi quy phẳng (flat context) chịu chi phí chú ý bậc hai và hiện tượng phân tâm ngữ cảnh khi vết suy luận kéo dài hàng chục nghìn tokens.
- **Phương pháp:** Mô hình đệ quy (f^rm) phân rã bài toán thành các stack frame độc lập qua thẻ `<call>` và `<return>`; khi bài toán con hoàn thành chỉ trả về kết quả ngắn gọn b cho ngữ cảnh cha và giải phóng trace trung gian.
- **Kết quả tác giả báo cáo:** Fine-tune Qwen2.5-3B-Instruct đệ quy trên SAT solving đạt 98% (Easy), 95% (Medium), 64% (Hard OOD), vượt GPT-4o phẳng (48.8% Hard); trên 4x4 Go (Length-OOD) đạt 38.5% trace accuracy trong khi CoT phẳng sụt giảm xuống 1.0%.
- **Đóng góp:** Đặt cơ sở lý thuyết chứng minh mô hình đệ quy với ngữ cảnh giới hạn tương đương không gian tính toán Turing SPACE(S(n)); cô lập ngữ cảnh giúp cải thiện tổng quát hóa ngoài phân phối độ dài.
- **Giới hạn:** Đòi hỏi định dạng bài toán có thể phân rã cấu trúc đệ quy rõ ràng; chi phí quản lý stack và chuyển ngữ cảnh ngoài bộ nhớ.
- **Vị trí nguồn:** arXiv:2603.02112v2, §3, §5.1, Table 1, Table 2

- **Đọc phương pháp:** Mô hình đệ quy thay đổi cách mang trạng thái: mỗi call có local context, chỉ return kết quả cho parent. Rút gọn context hoạt động khác với việc toàn bộ quá trình dùng ít token hơn.
- **Nhận xét đối chiếu của nhóm:** Dùng để mở rộng A2 từ stopping sang memory/state management. So sánh cần cả tổng token, peak context và chi phí stack; bài toán phải có decomposition hợp lệ. Không đồng nhất framework đã fine-tune với prompting đệ quy cho model bất kỳ.

Khóa BibTeX: `rra2_recursive_models` trong [references.bib](../overleaf/references.bib).

### rra2-mctsr

**[Accessing GPT-4 level Mathematical Olympiad Solutions via Monte Carlo Tree Self-refine with LLaMa-3 8B](https://arxiv.org/abs/2406.07394v2)**

Tác giả: Di Zhang; Xiaoshui Huang; Dongzhan Zhou; Yuqiang Li; Wanli Ouyang.
Vai trò chính: **A2**; vai trò phụ: A3; nhóm nhỏ: A2.2: Search, branching và phục hồi trajectory; phạm vi: **Nghiên cứu suy luận liên quan**.
Nguồn đã dùng: [v2](https://arxiv.org/abs/2406.07394v2); Preprint (arXiv:2406.07394v2).

- **Bài toán:** Mô hình ngôn ngữ vừa và nhỏ gặp khó khăn trong toán thi đấu Olympic do lỗi logic và thiếu cơ chế tìm kiếm - sửa sai có hệ thống lúc suy luận.
- **Phương pháp:** Thuật toán MCTSr kết hợp tìm kiếm cây Monte Carlo với self-refine văn bản: mỗi nút là một lời giải hoàn chỉnh, mở rộng bằng critique và viết lại cải tiến, tự chấm điểm (-100 đến 100) và lan truyền ngược cập nhật giá trị.
- **Kết quả tác giả báo cáo:** Trên LLaMA-3-8B không fine-tune, MATH accuracy tăng từ 24.36% (zero-shot) lên 58.24% (8-rollouts); Math Odyssey đạt 49.36% (ngang ngửa GPT-4 Turbo 49.1%).
- **Đóng góp:** Đề xuất phương pháp kết hợp tìm kiếm cây MCTS với khả năng phản biện văn bản ở cấp độ lời giải hoàn chỉnh; minh họa khả năng thu hẹp khoảng cách hiệu năng qua test-time search.
- **Giới hạn:** Tìm kiếm ở cấp độ cả lời giải (coarse granularity) tiêu tốn nhiều lượt sinh văn bản hoàn chỉnh; điểm số tự đánh giá có thể thiếu tin cậy ở bài toán quá khó. Scope thuộc adjacent_reasoning.
- **Vị trí nguồn:** arXiv:2406.07394v2, §3, §4.3, Table 2, §4.4, Table 3

- **Đọc phương pháp:** Nút search là một lời giải hoàn chỉnh được refine; số rollout đếm các lần mở rộng/tinh chỉnh chứ không phải độ dài một chain. Self-evaluation là nguồn tín hiệu chọn nhánh.
- **Nhận xét đối chiếu của nhóm:** Dùng làm đối chiếu search bên ngoài cho Long-CoT nội sinh. Gain trên LLaMA-3-8B không chứng minh cùng mức tiết kiệm với early exit; cần cộng token cho critique, rewrite, evaluation và mọi nhánh search.

Khóa BibTeX: `rra2_mctsr` trong [references.bib](../overleaf/references.bib).

## A3 Analysis

| Nhóm nhỏ đề xuất | Paper đại diện |
| --- | --- |
| A3.1 — Cấu trúc diễn ngôn và interpretability/faithfulness | [ReasoningFlow: Discourse Structures for Understanding LLM Reasoning Traces](#rra3-reasoningflow); [Measuring Faithfulness in Chain-of-Thought Reasoning](#rra3-lanham-faithfulness) |
| A3.2 — Redundant steps và cấu trúc graph | [CoT2Graph](#rra3-cot2graph); [What Characterizes Effective Reasoning? / FSF](#rra3-effective-reasoning) |
| A3.3 — Complexity, error propagation và giới hạn horizon | [ZebraLogic](#rra3-zebralogic) |
| A3.4 — Reasoning behavior: overthinking/underthinking | [Do NOT Think That Much for 2+3=?](#rra3-chen-overthinking); [Thoughts Are All Over the Place](#rra3-underthinking); [Self-Doubt](#rra3-overthinking) |

### rra3-reasoningflow

**[ReasoningFlow: Discourse Structures for Understanding LLM Reasoning Traces](https://arxiv.org/abs/2606.05402v2)**

Tác giả: Jinu Lee; Shivam Agarwal; Amruta Parulekar; Siddarth Madala; Dilek Hakkani-Tür; Julia Hockenmaier.
Vai trò chính: **A3**; vai trò phụ: A4; nhóm nhỏ: A3.1: Cấu trúc diễn ngôn và interpretability/faithfulness; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v2](https://arxiv.org/abs/2606.05402v2); Author-reported EMNLP 2026 Oral; arXiv:2606.05402v2.

- **Bài toán:** Vết suy luận Long-CoT phi tuyến tính thiếu schema diễn ngôn chuẩn hóa để mô tả quan hệ giữa các bước và chưa kiểm chứng mối liên hệ giữa cấu trúc bề mặt và cơ chế tính toán nội tại.
- **Phương pháp:** Đề xuất ReasoningFlow biểu diễn vết suy luận thành DAG với các nhãn quan hệ diễn ngôn (support, attack, verify, assumption); thực hiện can thiệp Thought Anchors (attention masking) để đo điểm phụ thuộc nhân quả thực nghiệm qua log KL-divergence.
- **Kết quả tác giả báo cáo:** Trên QwQ và AIME, điểm phụ thuộc Thought Anchors khi dự đoán cạnh ReasoningFlow không vượt trội so với baseline heuristic chọn nút gần nhất theo khoảng cách token; trên quan sát vết giải, bước kiểm tra cục bộ có sửa lỗi ghi nhận tỷ lệ bước đúng là 84% (so với 64%) và tỷ lệ dẫn đến đáp án đúng cuối là 20% (so với 5%).
- **Đóng góp:** Cung cấp schema diễn ngôn hình thức phân tích cấu trúc vết suy luận; báo cáo quan sát thực nghiệm rằng mức độ thẳng hàng giữa đồ thị diễn ngôn bề mặt và điểm số dựa trên can thiệp nội tại là hạn chế trong thiết lập thử nghiệm QwQ và AIME.
- **Giới hạn:** Tỷ lệ đúng của bước sửa lỗi là quan sát tương quan hành vi trên tập vết giải, không phải can thiệp nhân quả có đối chứng độc lập; chú ý Thought Anchors chỉ kiểm tra trên mô hình và tác vụ cụ thể.
- **Vị trí nguồn:** arXiv:2606.05402v2, §3, §6.1, Figure 5, §8, Finding 4

- **Đọc phương pháp:** Schema discourse mô tả quan hệ giữa các bước ở mức văn bản. Thí nghiệm Thought Anchors kiểm tra một câu hỏi khác: thao tác attention có thay đổi phân phối dự đoán bước sau hay không.
- **Nhận xét đối chiếu của nhóm:** Dùng để phân biệt representation và mechanism. Cạnh diễn ngôn, điểm can thiệp và tỷ lệ sửa đúng là ba loại bằng chứng khác nhau; alignment yếu trong một setup không phủ nhận mọi phương pháp mechanistic analysis.

Khóa BibTeX: `rra3_reasoningflow` trong [references.bib](../overleaf/references.bib).

### rra3-cot2graph

**[Understanding Failures in LLM Reasoning by Learning Structured Representations of Chain-of-Thought](https://openreview.net/forum?id=wFTJZ8fvns)**

Tác giả: Tommaso Felice Banfi; Mubashara Akhtar; Jingwei Ni; Mrinmaya Sachan.
Vai trò chính: **A3**; vai trò phụ: không gán; nhóm nhỏ: A3.2: Redundant steps và cấu trúc graph; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [OpenReview](https://openreview.net/forum?id=wFTJZ8fvns); Author-reported Findings of EMNLP 2026; OpenReview forum:wFTJZ8fvns.

- **Bài toán:** Đánh giá CoT hiện tập trung vào tín hiệu cấp bước độc lập, bỏ qua cấu trúc tô-pô tổng thể của vết suy luận và các mẫu hình cấu trúc phân biệt thành công/thất bại.
- **Phương pháp:** Chuyển đổi vết CoT thành đồ thị phụ thuộc định kiểu nắm bắt phân nhánh và gộp bài toán con; huấn luyện Graph Neural Networks (GNN) kết hợp GNNExplainer để trích xuất đặc trưng cấu trúc liên quan đến độ đúng đắn và dư thừa.
- **Kết quả tác giả báo cáo:** Trên GPQA với vết suy luận DS-Qw14B, độ chính xác dự đoán đúng/sai của đáp án cuối đạt 65.4%, tăng +7.8 điểm phần trăm (pp) so với baseline Logistic Regression theo độ dài (57.6%) và +2.5 pp so với baseline cây LCoT2Tree (62.9%); trên 600 bài MMLU-Pro (N=5), CoT2Graph đạt 54.5% và graph+entropy đạt 56.1%, so với ORM-Best (50.8%), ORM+uncertainty (51.6%) và mean (43.2%); phân tích GNNExplainer giải thích bộ dự đoán GNN chứ không phải cơ chế nhân quả nội tại của LLM.
- **Đóng góp:** Minh họa rằng cấu trúc liên kết đồ thị của vết suy luận mang tín hiệu dự đoán hữu ích cho tính đúng đắn và độ dư thừa; đề xuất phương pháp phân tích vết giải dưới dạng đồ thị.
- **Giới hạn:** Cấu trúc đồ thị phản ánh tốt tính dư thừa và kế hoạch nhưng ít mang tín hiệu về lỗi hallucination nội bộ bước; phụ thuộc vào parser trích xuất đồ thị phụ thuộc.
- **Vị trí nguồn:** OpenReview forum:wFTJZ8fvns, §4.2, Table 1, §5.6, Figure 7

- **Đọc phương pháp:** GNN nhận đồ thị được trích từ trace rồi dự đoán tính đúng/sai; GNNExplainer phân tích bộ dự đoán đó. Best-of-N selection là ứng dụng riêng của tín hiệu cấu trúc.
- **Nhận xét đối chiếu của nhóm:** Dùng để đánh giá lợi ích của topology so với length-only features. Phải phân biệt accuracy của correctness predictor với accuracy giải bài sau selection; chi phí parser/GNN/judge và khả năng đổi model/domain là phần cần kiểm tra.

Khóa BibTeX: `rra3_cot2graph` trong [references.bib](../overleaf/references.bib).

### rra3-zebralogic

**[ZebraLogic: On the Scaling Limits of LLMs for Logical Reasoning](https://arxiv.org/abs/2502.01100v2)**

Tác giả: Bill Yuchen Lin; Ronan Le Bras; Kyle Richardson; Ashish Sabharwal; Radha Poovendran; Peter Clark; Yejin Choi.
Vai trò chính: **A3**; vai trò phụ: A4; nhóm nhỏ: A3.3: Complexity, error propagation và giới hạn horizon; phạm vi: **Nghiên cứu suy luận liên quan**.
Nguồn đã dùng: [v2](https://arxiv.org/abs/2502.01100v2); Author-reported ICML 2025; arXiv:2502.01100v2.

- **Bài toán:** Khảo sát ranh giới mở rộng (scaling limits) của LLMs và reasoning models trong bài toán suy luận logic thỏa mãn ràng buộc khi không gian tìm kiếm tăng theo cấp số nhân.
- **Phương pháp:** Thiết kế khuôn khổ câu đố lưới logic ZebraLogic dựa trên bài toán CSP với không gian tìm kiếm định lượng chính xác (<10^3 đến >10^9 ứng viên); đánh giá tác động của scaling tham số và scaling tính toán suy luận (Best-of-N, Self-Refinement).
- **Kết quả tác giả báo cáo:** Ghi nhận hiện tượng Lời nguyền phức tạp (Curse of Complexity): độ chính xác giảm sút nghiêm trọng khi không gian tìm kiếm vượt 10^6; Llama-3.1-405B đạt 32.6% tổng thể nhưng giảm về 1.5% ở mức Large và 0.0% ở X-Large; reasoning models (o1-full 42.5%, DeepSeek-R1 28.5% ở X-Large) cũng suy giảm mạnh; scaling test-time chỉ cải thiện cận biên trên các mô hình được thử nghiệm.
- **Đóng góp:** Định lượng ranh giới suy luận logic hình thức có không gian tìm kiếm tổ hợp lớn; chỉ ra điểm nghẽn của scaling tham số và suy luận trước độ phức tạp cấp số nhân.
- **Giới hạn:** Khảo sát trên dạng bài toán câu đố lưới CSP cụ thể; không trực tiếp nghiên cứu vết suy luận mở rộng dạng tự do (scope adjacent_reasoning, primary A3, secondary A4).
- **Vị trí nguồn:** arXiv:2502.01100v2, §3.1, Table 1, §3.2, §5, Figure 6

- **Đọc phương pháp:** Độ phức tạp được thao tác qua câu đố CSP, giúp khảo sát scaling thay vì chỉ nhóm câu hỏi theo độ dài output. Kích thước search space và độ dài vết giải không phải cùng đại lượng.
- **Nhận xét đối chiếu của nhóm:** Dùng làm adjacent evidence cho scaling limits, không là bằng chứng riêng rằng Long-CoT vô hiệu. Kết luận nên gắn với puzzle family và mô hình đã thử; cần tách combinatorial difficulty khỏi tải ghi nhớ trạng thái.

Khóa BibTeX: `rra3_zebralogic` trong [references.bib](../overleaf/references.bib).

### rra3-overthinking

**[Revisiting Overthinking in Long Chain-of-Thought from the Perspective of Self-Doubt](https://arxiv.org/abs/2505.23480v1)**

Tác giả: Keqin Peng; Liang Ding; Yuanxin Ouyang; Meng Fang; Dacheng Tao.
Vai trò chính: **A3**; vai trò phụ: A2; nhóm nhỏ: A3.4: Reasoning behavior: overthinking/underthinking; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v1](https://arxiv.org/abs/2505.23480v1); Preprint (arXiv:2505.23480v1).

- **Bài toán:** Hiện tượng các mô hình reasoning tiêu tốn lượng token khổng lồ cho các bước suy luận thừa thãi mà không làm tăng độ chính xác; cần định lượng cơ chế hành vi cụ thể.
- **Phương pháp:** Phân tích hành vi suy luận dưới góc nhìn tự nghi ngờ (self-doubt) — xu hướng kiểm tra lại liên tục các kết luận trung gian đã đúng; khảo sát trên 4 mô hình với GSM8K, MATH-500 và bộ đề thiếu tiền đề (Missing Premise); đề xuất prompt can thiệp kiểm tra tiền đề.
- **Kết quả tác giả báo cáo:** Self-doubt chiếm tỷ lệ lớn trong các bước overthinking thừa thãi; prompt can thiệp kiểm tra tiền đề giúp giảm 35%–45% số token trong khi bảo toàn hoặc tăng nhẹ độ chính xác trên mô hình thử nghiệm; trên bài thiếu tiền đề, tỷ lệ từ chối giải đúng tăng từ 30-50% lên 75-97%.
- **Đóng góp:** Đưa ra phân tích hành vi chỉ ra self-doubt là nhân tố dẫn đến overthinking; đề xuất giải pháp can thiệp tiền đề đơn giản giúp tiết kiệm token.
- **Giới hạn:** Can thiệp dựa trên prompt mang tính heuristic; chưa giải quyết triệt để overthinking bắt nguồn từ cơ chế tối ưu hóa RL nội tại.
- **Vị trí nguồn:** arXiv:2505.23480v1, §2, Figure 1, §5, Table 1, Table 3, §6

- **Đọc phương pháp:** Self-doubt được xem ở mức hành vi: kiểm lại kết luận đã có. Bộ đề thiếu tiền đề đặt thêm câu hỏi liệu mô hình có nhận ra bài không đủ điều kiện để giải.
- **Nhận xét đối chiếu của nhóm:** Dùng để tách unnecessary verification khỏi productive reflection. Prompt kiểm tra tiền đề có thể đổi chiến lược trả lời hoặc từ chối; tiết kiệm token trên dạng đề này chưa phải cải thiện chung cho mọi bài toán có đáp án.

Khóa BibTeX: `rra3_overthinking` trong [references.bib](../overleaf/references.bib).

### rra3-lanham-faithfulness

**[Measuring Faithfulness in Chain-of-Thought Reasoning](https://arxiv.org/abs/2307.13702v1)**

Tác giả: Tamera Lanham; Anna Chen; Ansh Radhakrishnan; Benoit Steiner; Carson Denison; Danny Hernandez; Dustin Li; Esin Durmus; Evan Hubinger; Jackson Kernion; Kamilė Lukošiūtė; Karina Nguyen; Newton Cheng; Nicholas Joseph; Nicholas Schiefer; Oliver Rausch; Robin Larson; Sam McCandlish; Sandipan Kundu; Saurav Kadavath; Shannon Yang; Thomas Henighan; Timothy Maxwell; Timothy Telleen-Lawton; Tristan Hume; Zac Hatfield-Dodds; Jared Kaplan; Jan Brauner; Samuel R. Bowman; Ethan Perez.
Vai trò chính: **A3**; vai trò phụ: không gán; nhóm nhỏ: A3.1: Cấu trúc diễn ngôn và interpretability/faithfulness; phạm vi: **Công trình nền tảng**.
Nguồn đã dùng: [v1](https://arxiv.org/abs/2307.13702v1); Preprint (arXiv:2307.13702v1).

- **Bài toán:** Khảo sát xem chuỗi suy luận từng bước có thực sự phản ánh tiến trình tính toán nội tại (tính trung thực) hay chỉ là sự hợp lý hóa sau khi đã có định kiến đáp án.
- **Phương pháp:** Thực hiện các can thiệp phản thực nghiệm (counterfactual perturbations) trên chuỗi CoT của các mô hình lên tới 175B tham số: trả lời sớm, chèn lỗi bước trung gian, diễn đạt lại, và thay thế CoT bằng filler tokens " ...".
- **Kết quả tác giả báo cáo:** Với các filler tokens, mô hình thử nghiệm không cải thiện độ chính xác so với direct answer; tác giả nêu giả thuyết hiệu ứng lệch phân phối (OOD) như một khả năng giải thích hiệu năng giảm, không phải nguyên nhân đã đo đạc độc lập.
- **Đóng góp:** Đặt nền tảng phương pháp luận cho việc kiểm tra tính trung thực của CoT bằng can thiệp phản thực nghiệm; ghi nhận trong các thiết lập thử nghiệm này, filler tokens không cải thiện độ chính xác.
- **Giới hạn:** Kết quả thực hiện trên các mô hình pre-o1 và prompt-based CoT; không tự động khái quát thành quy luật phủ định cho mọi nghiên cứu filler-token hay latent reasoning sau này. Scope foundational.
- **Vị trí nguồn:** arXiv:2307.13702v1, §2.1, §2.3, §2.5.1, Figure 5, Table 2

- **Đọc phương pháp:** Các phép truncation, chèn lỗi và filler tạo can thiệp trên vết suy luận. Chúng kiểm tra mức phụ thuộc của đáp án vào trace, không chỉ độ thuyết phục mà người đọc cảm nhận.
- **Nhận xét đối chiếu của nhóm:** Dùng làm nền tảng thiết kế thí nghiệm faithfulness. Can thiệp có thể đưa model ra ngoài phân phối; cần matched controls. Kết quả ở model pre-o1 không thay thế kiểm chứng trên reasoning model và kiến trúc latent sau này.

Khóa BibTeX: `rra3_lanham_faithfulness` trong [references.bib](../overleaf/references.bib).

### rra3-chen-overthinking

**[Do NOT Think That Much for 2+3=? On the Overthinking of o1-Like LLMs](https://arxiv.org/abs/2412.21187v2)** — Xingyu Chen et al. (2024; v2: 2025).

Vai trò chính: **A3**; phụ: A1, A4; nhóm nhỏ: **A3.4**; phạm vi: **Long-CoT trực tiếp**.

- **Bài toán:** Định lượng tính toán thừa sau khi đã có lời giải.
- **Phương pháp:** Chỉ số outcome/process efficiency; self-training với preference cho lời giải ngắn và giữ phản tư.
- **Kết quả:** QwQ-32B-Preview, MATH500: SimPO FCS+Reflection giảm 2407.9 xuống 1330.7 token; accuracy 93.0% xuống 92.8%.
- **Đóng góp:** Liên kết chẩn đoán overthinking với dữ liệu huấn luyện tiết kiệm.
- **Giới hạn:** Giảm token vẫn có thể mất accuracy, nhất là bài khó.
- **Nguồn:** v2, §2–3, Table 4; khóa `rra3_chen_overthinking`.

- **Đọc phương pháp:** Phân biệt efficiency theo outcome với phần tiến trình thực sự đóng góp; self-training chọn trace ngắn rồi vẫn giữ reflection để tránh loại cả suy nghĩ hữu ích.
- **Nhận xét đối chiếu của nhóm:** Dùng để giải thích vì sao shorter không tự động better. MATH500 tiết kiệm token lớn nhưng accuracy giảm nhẹ; chưa thể gọi là tương đương thống kê nếu thiếu uncertainty. First-correct solution trong construction dùng đáp án đúng, không phải oracle sẵn có lúc triển khai.

### rra3-underthinking

**[Thoughts Are All Over the Place: On the Underthinking of o1-Like LLMs](https://arxiv.org/abs/2501.18585v2)** — Yue Wang et al. (2025).

Vai trò chính: **A3**; phụ: A2, A4; nhóm nhỏ: **A3.4**; phạm vi: **Long-CoT trực tiếp**.

- **Bài toán:** Chuỗi dài nhưng đổi hướng quá sớm.
- **Phương pháp:** Underthinking score và TIP: phạt logits chuyển hướng trong một cửa sổ giải mã.
- **Kết quả:** QwQ-32B-Preview, AIME24: Pass@1 tăng 38.3% lên 44.1%, ước lượng từ 32 mẫu/bài; alpha=3, beta=600, chọn trên AIME22–23.
- **Đóng góp:** Phân biệt độ dài tổng với độ sâu khám phá từng hướng.
- **Giới hạn:** Phụ thuộc token chuyển hướng và siêu tham số; không mặc nhiên tiết kiệm compute.
- **Nguồn:** v2, §2–3, Tables 2–3; khóa `rra3_underthinking`.

- **Đọc phương pháp:** Underthinking nói về thiếu độ sâu trên một hướng, không nhất thiết tổng trace ngắn. TIP chỉ điều chỉnh xác suất chuyển hướng trong một cửa sổ, không có verifier xác nhận hướng hiện tại đúng.
- **Nhận xét đối chiếu của nhóm:** Dùng làm phản biện việc luôn khuyến khích suy nghĩ ngắn hơn. Kiểm tra cùng sampling và budget; penalty quá mạnh có thể giữ model trong nhánh sai. Không so trực tiếp số greedy ở bảng khác với Pass@1 ước lượng từ nhiều mẫu.

### rra3-effective-reasoning

**[What Characterizes Effective Reasoning? Revisiting Length, Review, and Structure of CoT](https://arxiv.org/abs/2509.19284v1)** — Yunzhen Feng et al. (2025).

Vai trò chính: **A3**; phụ: A2, A4; nhóm nhỏ: **A3.2**; phạm vi: **Long-CoT trực tiếp**.

- **Bài toán:** Cấu trúc nào dự đoán suy luận hiệu quả?
- **Phương pháp:** Trích đồ thị, đo Failed-Step Fraction (FSF), chọn ứng viên và can thiệp loại nhánh bỏ dở.
- **Kết quả:** Trên 10 LRM, FSF dự đoán correctness nhất quán hơn length/review; thử bỏ nhánh trên các trace HARP sai của R1 và GPT-oss-120B cải thiện khả năng tiếp tục giải đúng.
- **Đóng góp:** Đưa cấu trúc nhánh vào phân tích và điều khiển.
- **Giới hạn:** FSF phụ thuộc judge; nhánh bỏ dở không đồng nghĩa bước sai logic.
- **Nguồn:** v1, §3.2, §4–5, Table 1; khóa `rra3_effective_reasoning`.

- **Đọc phương pháp:** FSF là tỷ lệ nút thuộc các nhánh bị bỏ dở trong graph do judge trích. Selection trên tập ứng viên cố định và continuation sau branch editing là hai thí nghiệm khác nhau.
- **Nhận xét đối chiếu của nhóm:** Dùng để nối phân tích cấu trúc với kiểm soát context. Cần tính chi phí sinh ứng viên và graph judge; bỏ nhánh thành công trong thiết lập này không chứng minh mọi exploration thất bại đều vô ích đối với học hoặc kiểm chứng.

## A4 Evaluation/Benchmark

| Nhóm nhỏ đề xuất | Paper đại diện |
| --- | --- |
| A4.1 — Benchmark long-horizon và planning | [LongCoT: Benchmarking Long-Horizon Chain-of-Thought Reasoning](#rra4-longcot); [SPaRC: A Spatial Pathfinding Reasoning Challenge](#rra4-sparc) |
| A4.2 — Metric chất lượng, độ dài và redundancy | [CoTJudger: A Graph-Driven Framework for Automatic Evaluation of Chain-of-Thought Efficiency and Redundancy in LRMs](#rra4-cotjudger) |
| A4.3 — Process/outcome evaluation và verifier | [ProcessBench: Identifying Process Errors in Mathematical Reasoning](#rra4-processbench); [CriticBench: Benchmarking LLMs for Critique-Correct Reasoning](#rra4-criticbench) |

### rra4-longcot

**[LongCoT: Benchmarking Long-Horizon Chain-of-Thought Reasoning](https://arxiv.org/abs/2604.14140v1)**

Tác giả: Sumeet Ramesh Motwani; Daniel Nichols; Charles London; Peggy Li; Fabio Pizzati; Acer Blake; Hasan Hammoud; Tavish McDonald; Akshat Naik; Alesia Ivanova; Vignesh Baskaran; Ivan Laptev; Ruben Glatt; Tal Ben-Nun; Philip Torr; Natasha Jaques; Ameya Prabhu; Brian Bartoldson; Bhavya Kailkhura; Christian Schroeder de Witt.
Vai trò chính: **A4**; vai trò phụ: A3; nhóm nhỏ: A4.1: Benchmark long-horizon và planning; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v1](https://arxiv.org/abs/2604.14140v1); Author-reported ICML 2026; arXiv:2604.14140v1.

- **Bài toán:** Các benchmark hiện tại chủ yếu đo suy luận ngắn hoặc bão hòa; thiếu chuẩn đo lường năng lực duy trì trạng thái qua chuỗi phụ thuộc dài hạn với độ dài biến thiên (10k đến hơn 100k tokens).
- **Phương pháp:** Xây dựng benchmark LongCoT gồm 2,500 bài toán dựa trên template tham số hóa do chuyên gia thiết kế trên 5 miền (Toán, Hóa, CS, Cờ vua, Logic); tiến hành phân tích riêng rẽ thực nghiệm DAG phụ thuộc tuần tự (1 đến 35 nút từ Omni-Math) và bộ benchmark tổng hợp; đánh giá frontier models và scaffolding RLM.
- **Kết quả tác giả báo cáo:** Trên 2,000 bài vừa và khó, các frontier models được thử nghiệm đạt độ chính xác khiêm tốn (GPT 5.2 đạt 9.83%, Gemini 3 Pro 6.08%, Grok 4.1 2.04%); trong thực nghiệm DAG phụ thuộc, độ chính xác sụt giảm nhanh hơn đường cơ sở lỗi độc lập lý thuyết (p^N), đặc biệt sau 15 nút; scaffolding RLM thuần suy luận không cải thiện hiệu năng.
- **Đóng góp:** Cung cấp benchmark chuyên biệt đánh giá chuỗi suy luận dài hạn với cấu trúc phụ thuộc kiểm soát được; ghi nhận hiện tượng suy giảm hiệu năng khi chuỗi phụ thuộc kéo dài.
- **Giới hạn:** Hiện tượng suy giảm được tác giả giải thích như giả thuyết về mất mát trạng thái ngữ cảnh, chưa phải can thiệp nhân quả đo đạc trực tiếp cơ chế attention nội tại.
- **Vị trí nguồn:** arXiv:2604.14140v1, §3, §4.1, Figure 4, §4.2, Figure 6

- **Đọc phương pháp:** Tách bộ benchmark template đa miền khỏi thí nghiệm DAG tăng số dependency. Độ dài solution của benchmark và số nút DAG là hai cách thao tác horizon khác nhau.
- **Nhận xét đối chiếu của nhóm:** Dùng để stress-test state carrying. Accuracy thấp trên bộ vừa/khó không đại diện cho mọi reasoning task; đường p^N chỉ là baseline độc lập giản lược, chưa định danh duy nhất nguyên nhân suy giảm là attention hay memory loss.

Khóa BibTeX: `rra4_longcot` trong [references.bib](../overleaf/references.bib).

### rra4-cotjudger

**[CoTJudger: A Graph-Driven Framework for Automatic Evaluation of Chain-of-Thought Efficiency and Redundancy in LRMs](https://arxiv.org/abs/2603.07078v1)**

Tác giả: Siyi Li; Jiajun Shi; Shiwen Ni; Ge Zhang; Shuaimin Li; Shijian Wang; Zhoufutu Wen; Yizhi Li; Hamid Alinejad-Rokny; Jiaheng Liu; Min Yang; Wenhao Huang.
Vai trò chính: **A4**; vai trò phụ: A3; nhóm nhỏ: A4.2: Metric chất lượng, độ dài và redundancy; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v1](https://arxiv.org/abs/2603.07078v1); Author-reported ACL 2026 Main Conference; arXiv:2603.07078v1.

- **Bài toán:** Đánh giá CoT truyền thống phụ thuộc vào so khớp đáp án cuối hoặc gán nhãn thủ công từng bước tốn kém; thiếu khung tự động để đo lường độ dư thừa và hiệu quả logic.
- **Phương pháp:** Khung CoTJudger phân đoạn vết giải, phân loại nút nguyên tử, xây dựng CoT Graph, và trích xuất Shortest Effective Path (SEP) bằng DFS forward kết hợp kiểm tra tính nhất quán qua LLM; định nghĩa Redundancy Ratio R=(|V|-L_eff)/|V|.
- **Kết quả tác giả báo cáo:** Đánh giá trên 21 reasoning models ghi nhận tỷ lệ đáng kể các nút/bước suy luận nằm ngoài đường dẫn hiệu quả ngắn nhất SEP; phần lớn bước nằm ngoài SEP tập trung ở các vòng lặp tự kiểm tra sau khi đã đạt trạng thái có thể kết luận; mô hình chưng cất thể hiện mối tương quan về độ dài vết giải tương tự giáo viên nhưng mật độ nút hiệu quả trên bước suy luận thấp hơn.
- **Đóng góp:** Đề xuất khung đánh giá tự động dựa trên đồ thị cho phép đo lường chuẩn hóa tỷ lệ nút/bước suy luận nằm ngoài SEP của vết CoT mà không cần nhãn người cấp bước.
- **Giới hạn:** SEP là một structural proxy phụ thuộc vào mô hình thẩm định (judge-dependent) chứ không chứng minh mọi bước bị loại bỏ đều không cần thiết về mặt ngữ nghĩa; quan hệ giáo viên - học sinh là tương quan quan sát được, không phải bằng chứng nhân quả về sự kế thừa.
- **Vị trí nguồn:** arXiv:2603.07078v1, §4.1–4.6, Figure 2, §5, Figure 3

- **Đọc phương pháp:** Đơn vị của redundancy ratio là nút/step sau segmentation, không phải token. SEP được tìm trên graph đã trích và có kiểm tra nhất quán; preprocessing thay đổi có thể thay đổi mẫu số lẫn đường hiệu quả.
- **Nhận xét đối chiếu của nhóm:** Dùng làm structural efficiency metric, bổ sung cho accuracy và cost. Một bước ngoài SEP có thể là exploratory work cần thiết để phát hiện lời giải; muốn khẳng định có thể bỏ an toàn cần ablation tiếp tục sinh hoặc đánh giá lại đáp án.

Khóa BibTeX: `rra4_cotjudger` trong [references.bib](../overleaf/references.bib).

### rra4-sparc

**[SPaRC: A Spatial Pathfinding Reasoning Challenge](https://arxiv.org/abs/2505.16686v2)**

Tác giả: Lars Benedikt Kaesberg; Jan Philip Wahle; Terry Ruas; Bela Gipp.
Vai trò chính: **A4**; vai trò phụ: A3; nhóm nhỏ: A4.1: Benchmark long-horizon và planning; phạm vi: **Long-CoT trực tiếp**.
Nguồn đã dùng: [v2](https://arxiv.org/abs/2505.16686v2); Author-reported EMNLP 2025 Main Conference; arXiv:2505.16686v2.

- **Bài toán:** Thiếu chuẩn đánh giá năng lực lập kế hoạch không gian nhiều bước trong không gian tìm kiếm mở và khả năng thích ứng phân bổ compute theo độ khó bài toán.
- **Phương pháp:** Giới thiệu SPaRC gồm 1,000 bài toán tìm đường lưới 2D chia theo 5 cấp độ khó; đánh giá 3 mô hình instruct, 4 reasoning models (o4-mini, o3-mini, QwQ-32B, R1-Distill-70B) và 6 người giải.
- **Kết quả tác giả báo cáo:** Người giải đạt 98.0% tổng thể và 94.5% ở Level 5; mô hình reasoning cao nhất (o4-mini) đạt 15.8% tổng thể và 1.1% ở Level 5 (trên 50% đường đi vi phạm luật); trong khi người giải tăng thời gian suy nghĩ theo độ khó, mô hình thử nghiệm (như QwQ-32B) phát ra lượng token tương đương giữa các mức khó (14,433 tokens mức 1 vs 13,114 tokens mức 5).
- **Đóng góp:** Cung cấp benchmark tìm đường không gian có thể kiểm tra tự động và định lượng độ khó; chỉ ra sự chênh lệch lớn giữa người và mô hình reasoning cùng việc thiếu khả năng phân bổ compute thích ứng theo độ khó bài toán.
- **Giới hạn:** Giới hạn trong miền tìm đường lưới 2D biểu diễn bằng văn bản; kết luận về phân bổ compute áp dụng cho các mô hình và cấu hình prompt được khảo sát.
- **Vị trí nguồn:** arXiv:2505.16686v2, §3, Figure 2, Table 1, Table 2

- **Đọc phương pháp:** Bài toán tìm đường cho phép kiểm tra tính hợp lệ của từng move, không chỉ chuỗi mô tả nghe hợp lý. Phân tầng độ khó hỗ trợ phân tích compute adaptation.
- **Nhận xét đối chiếu của nhóm:** Dùng để bổ sung planning/state constraints ngoài toán. Phải giữ cách mã hóa grid, luật di chuyển và prompt; số token gần như không đổi là quan sát về allocation, chưa đủ để giải thích vì sao mô hình thất bại.

Khóa BibTeX: `rra4_sparc` trong [references.bib](../overleaf/references.bib).

### rra4-processbench

**[ProcessBench: Identifying Process Errors in Mathematical Reasoning](https://arxiv.org/abs/2412.06559v4)**

Tác giả: Chujie Zheng; Zhenru Zhang; Beichen Zhang; Runji Lin; Keming Lu; Bowen Yu; Dayiheng Liu; Jingren Zhou; Junyang Lin.
Vai trò chính: **A4**; vai trò phụ: không gán; nhóm nhỏ: A4.3: Process/outcome evaluation và verifier; phạm vi: **Nghiên cứu suy luận liên quan**.
Nguồn đã dùng: [v4](https://arxiv.org/abs/2412.06559v4); Author-reported ACL 2025 Main Conference; arXiv:2412.06559v4.

- **Bài toán:** Giám sát quá trình đóng vai trò quan trọng trong suy luận nhiều bước, nhưng thiếu chuẩn đo lường có nhãn chuyên gia cấp bước trên các tập bài toán toán học đa dạng để định vị bước lỗi đầu tiên.
- **Phương pháp:** Xây dựng ProcessBench gồm 3,400 trường hợp kiểm thử (test cases) kèm lời giải từng bước từ 4 tập dữ liệu toán (GSM8K, MATH, OlympiadBench, Omni-MATH); chuyên gia gán nhãn xác định bước lỗi sớm nhất; đánh giá PRMs và LLM Critics qua điểm F1 trung bình trên 4 tập con.
- **Kết quả tác giả báo cáo:** Skywork-PRM-7B đạt điểm F1 trung bình 42.1% trên 4 tập con; các reasoning models đóng vai trò critic đạt F1 trung bình: QwQ-32B-Preview đạt 71.5%, GPT-4o đạt 61.9%, và o1-mini đạt 87.9%.
- **Đóng góp:** Cung cấp benchmark gán nhãn chuyên gia cấp bước chuẩn hóa để đánh giá khả năng phát hiện lỗi suy luận toán học; đóng vai trò làm dữ liệu đối chứng cho giám sát quá trình.
- **Giới hạn:** Giới hạn trong suy luận toán học với độ khó hỗn hợp; bài toán định vị bước lỗi đầu tiên chưa mô tả toàn bộ cấu trúc lỗi của vết giải nhiều nhánh. Phạm vi adjacent_reasoning.
- **Vị trí nguồn:** arXiv:2412.06559v4, §3.1, §4.2, Table 2, Table 3

- **Đọc phương pháp:** Nhiệm vụ là xác định bước lỗi sớm nhất hoặc nhận ra lời giải không lỗi, không phải viết lời giải mới. F1 ở đây là harmonic mean giữa accuracy trên mẫu có lỗi và mẫu đúng (§4.1).
- **Nhận xét đối chiếu của nhóm:** Dùng để kiểm định verifier/critic trước khi dùng cho A1/A2. Điểm trung bình qua bốn subset không phải một accuracy gộp; cần báo riêng miền khó và quy tắc chọn threshold. Phát hiện lỗi đúng chưa bảo đảm sửa được lỗi.

Khóa BibTeX: `rra4_processbench` trong [references.bib](../overleaf/references.bib).

### rra4-criticbench

**[CriticBench: Benchmarking LLMs for Critique-Correct Reasoning](https://arxiv.org/abs/2402.14809v4)**

Tác giả: Zicheng Lin; Zhibin Gou; Tian Liang; Ruilin Luo; Haowei Liu; Yujiu Yang.
Vai trò chính: **A4**; vai trò phụ: A3; nhóm nhỏ: A4.3: Process/outcome evaluation và verifier; phạm vi: **Nghiên cứu suy luận liên quan**.
Nguồn đã dùng: [v4](https://arxiv.org/abs/2402.14809v4); Author-reported Findings of ACL 2024; arXiv:2402.14809v4.

- **Bài toán:** Năng lực phê phán và tự sửa lỗi là cốt lõi của suy luận nhiều lượt nhưng thường bị đánh giá tách rời; thiếu chuẩn đo lường có hệ thống về toàn bộ chu trình Sinh - Phê phán - Sửa sai (GQC) qua nhiều miền.
- **Phương pháp:** CriticBench bao phủ 5 miền suy luận (Toán, Code, Thuật toán, Logic đời thường, Suy luận ký hiệu) tích hợp từ 15 datasets; đánh giá 17 LLMs qua 3 giai đoạn: tự sinh (G), phê phán (Q), và sửa sai dựa trên critique (C).
- **Kết quả tác giả báo cáo:** Ghi nhận mối tương quan giữa độ chính xác phê phán và tỷ lệ sửa sai thành công; các bài toán lập trình và thuật toán có tỷ lệ sửa sai cao hơn nhờ phản hồi rõ ràng; các mô hình nhỏ khi tự phê phán có xu hướng bảo thủ nếu thiếu verifier ngoài.
- **Đóng góp:** Đề xuất benchmark toàn diện đánh giá chu trình GQC tương hỗ trong suy luận nhiều bước; khảo sát trên diện rộng 17 mô hình ngôn ngữ.
- **Giới hạn:** Đánh giá trên các prompt-based LLMs thế hệ trước; chưa chuyên biệt hóa cho các vết Long-CoT hàng vạn token của reasoning models mới (scope adjacent_reasoning).
- **Vị trí nguồn:** arXiv:2402.14809v4, §3, §4.1, Table 1, Figure 6

- **Đọc phương pháp:** Thiết kế Generation–Critique–Correction tách năng lực giải ban đầu, nhận xét và sửa sau phản hồi. Đây là đối chiếu cho self-correction, không phải benchmark chuyên cho horizon rất dài.
- **Nhận xét đối chiếu của nhóm:** Dùng để đánh giá chất lượng phản hồi thay vì chỉ đếm reflection tokens. Tương quan critique–correction không cô lập tác động nhân quả; cần giữ cùng lời giải đầu vào, feedback source và compute khi so critic.

Khóa BibTeX: `rra4_criticbench` trong [references.bib](../overleaf/references.bib).
