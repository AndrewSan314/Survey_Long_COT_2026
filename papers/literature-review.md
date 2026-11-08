# Tổng hợp literature Long-CoT theo A1–A4

Danh mục chọn lọc gồm 24 paper (A1: 6, A2: 5, A3: 8, A4: 5), trong đó 19 nghiên cứu trực tiếp Long-CoT, bốn nghiên cứu liên quan và một công trình nền tảng. Mỗi paper có một primary role; dẫn chéo không tăng số lượng. Kết quả là tác giả báo cáo trong thiết lập được nêu, chưa được nhóm tái lập.

Bản này là đầu ra chính theo phân công. Xem [hồ sơ đầy đủ và vị trí nguồn](research-role.md), [Related Work](related-work.md) và [PDF](../overleaf/draft-main.pdf).

## A1 — Training/Data

Làm thế nào học và chuyển giao năng lực Long-CoT từ dữ liệu và feedback?

| Nhóm nhỏ | Hướng nghiên cứu | Paper tiêu biểu |
| --- | --- | --- |
| A1.1 | RL hình thành năng lực reasoning | DeepSeek-R1; Kimi k1.5 |
| A1.2 | SFT với dữ liệu được chọn lọc | s1; LIMO |
| A1.3 | Data synthesis/selection và curriculum | Light-R1; dẫn chéo s1, LIMO, R1 |
| A1.4 | RL hướng efficiency | Arora và Zanette |
| A1.5 | Distillation và Long2short | Dẫn chéo DeepSeek-R1, Kimi k1.5 |

### A1.1 — RL hình thành năng lực reasoning

Học policy từ reward độ đúng, mở rộng rollout/context và khuyến khích exploration, self-verification.

#### [DeepSeek-R1](https://arxiv.org/abs/2501.12948v2)

**Long-CoT trực tiếp.** Tên đầy đủ: DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning.

- **Bài toán:** Học năng lực Long-CoT qua RL và chuyển giao sang model nhỏ.
- **Phương pháp:** R1-Zero dùng GRPO với reward độ đúng/định dạng; R1 kết hợp cold-start SFT, RL, rejection sampling và distillation.
- **Kết quả:** R1 đạt 79.8% AIME24; Distill-Qwen-32B đạt 72.6% AIME24 trong thiết lập paper.
- **Đóng góp:** Cung cấp quy trình RL hình thành self-verification/exploration và chuyển giao reasoning qua SFT.
- **Hạn chế:** Phụ thuộc base mạnh và verifier; pure RL có thể trộn ngôn ngữ.

[Nguồn và ghi chú chi tiết](research-role.md#rra1-deepseek-r1).

#### [Kimi k1.5](https://arxiv.org/abs/2501.12599v4)

**Long-CoT trực tiếp.** Tên đầy đủ: Kimi k1.5: Scaling Reinforcement Learning with LLMs.

- **Bài toán:** Mở rộng RL cho reasoning dài và giảm chi phí triển khai.
- **Phương pháp:** Long-context RL đến 128k token; policy không value head, CoT-RM và Long2short.
- **Kết quả:** Đạt 77.5% Pass@1 AIME24 và 96.2% MATH-500; có thực nghiệm chuyển từ long sang short reasoning.
- **Đóng góp:** Kết nối RL scaling, thiết kế reward và chuyển giao năng lực sang trace ngắn.
- **Hạn chế:** Chi phí training lớn; CoT-RM chấm đáp án cuối, không phải nhãn đúng/sai từng bước.

[Nguồn và ghi chú chi tiết](research-role.md#rra1-kimi-k15).

### A1.2 — SFT với dữ liệu được chọn lọc

Tuyển chọn demonstration chất lượng cao để khai thác năng lực reasoning của checkpoint mạnh.

#### [s1](https://arxiv.org/abs/2501.19393v3)

**Long-CoT trực tiếp.** Tên đầy đủ: s1: Simple test-time scaling.

- **Bài toán:** Kích hoạt reasoning và test-time scaling với ít dữ liệu SFT.
- **Phương pháp:** Chọn s1K gồm 1,000 bài/trace chất lượng; SFT Qwen2.5-32B-Instruct và budget forcing.
- **Kết quả:** AIME24 tăng từ 50.0% lên 56.7% khi bật budget forcing trên s1-32B.
- **Đóng góp:** Cho thấy hiệu quả dữ liệu chọn lọc và cơ chế điều khiển độ dài đơn giản.
- **Hạn chế:** Phải tách gain do SFT và inference control; vẫn cần base và teacher mạnh.

[Nguồn và ghi chú chi tiết](research-role.md#rra1-s1).

#### [LIMO](https://arxiv.org/abs/2502.03387v3)

**Long-CoT trực tiếp.** Tên đầy đủ: LIMO: Less is More for Reasoning.

- **Bài toán:** Giảm lượng demonstration cần để học reasoning toán khó.
- **Phương pháp:** Chọn 817 mẫu theo độ khó và chất lượng trace: lập luận, verification, exploration, adaptive granularity.
- **Kết quả:** LIMO-32B đạt 63.3% AIME24, 95.6% MATH-500; đổi sang base Qwen1.5-32B-Chat chỉ còn 9.2% AIME24.
- **Đóng góp:** Đề xuất cách chọn dữ liệu chất lượng và chỉ ra điều kiện phụ thuộc năng lực base.
- **Hạn chế:** Kết quả không chứng minh ít dữ liệu luôn đủ trên mọi checkpoint.

[Nguồn và ghi chú chi tiết](research-role.md#rra1-limo).

### A1.3 — Data synthesis/selection và curriculum

Sinh hoặc lọc trace, kiểm tra contamination và sắp xếp dữ liệu qua các stage training.

#### [Light-R1](https://arxiv.org/abs/2503.10460v4)

**Long-CoT trực tiếp.** Tên đầy đủ: Light-R1: Curriculum SFT, DPO and RL for Long COT from Scratch and Beyond.

- **Bài toán:** Xây quy trình dữ liệu và training Long-CoT mở, có kiểm tra contamination.
- **Phương pháp:** Lọc dữ liệu, curriculum SFT với 76k rồi 3,000 mẫu, DPO và model merging.
- **Kết quả:** Light-R1-32B đạt 76.6% AIME24 sau merging; GPQA biến động qua các stage.
- **Đóng góp:** Công bố pipeline nhiều stage và kiểm tra test-set leakage trong dữ liệu mở.
- **Hạn chế:** Khởi tạo từ instruct checkpoint; gain toán không đồng nghĩa gain đa miền.

[Nguồn và ghi chú chi tiết](research-role.md#rra1-light-r1).

### A1.4 — RL hướng efficiency

Học đánh đổi accuracy–length, phân bổ reasoning budget theo độ khó.

#### [Training Language Models to Reason Efficiently](https://arxiv.org/abs/2502.04463v4)

**Long-CoT trực tiếp.** Tên đầy đủ: Training Language Models to Reason Efficiently.

- **Bài toán:** Học phân bổ compute theo độ khó thay vì luôn sinh trace dài.
- **Phương pháp:** RL kết hợp correctness reward và length penalty điều chỉnh bằng alpha trên reasoning model đã có.
- **Kết quả:** Với DeepSeek-R1-Distill-Qwen-7B, alpha=0.2 giảm token 83% GSM8K và 27% AIME24.
- **Đóng góp:** Xây các điểm đánh đổi accuracy–cost bằng objective training.
- **Hạn chế:** Có thể mất accuracy hoặc faithfulness; không phải bảo đảm nén miễn phí.

[Nguồn và ghi chú chi tiết](research-role.md#rra1-efficient-rl).

### A1.5 — Distillation và Long2short

Chuyển năng lực từ teacher hoặc trace dài sang model nhỏ hay trace ngắn; không đếm lại paper.

**Tổng hợp hướng nghiên cứu.** Các công trình cho thấy có nhiều con đường đến Long-CoT: RL từ feedback, SFT dữ liệu chọn lọc, pipeline nhiều stage và distillation. Tuy nhiên, ít mẫu SFT không có nghĩa ít tổng chi phí; năng lực base, chi phí teacher và verifier vẫn quan trọng. Số điểm giữa các paper chỉ có ý nghĩa khi đối chiếu cùng model, task và budget.

**Liên hệ dependency khi có bằng chứng.** Với SFT/RL/distillation nói chung, ghi B=N/A nếu chưa có bằng chứng can thiệp trực tiếp vào reasoning dependency. Sinh trace dài hoặc đạt accuracy cao chưa đủ để gán chức năng formation/state carrying; liên hệ trên đây chủ yếu là vai trò training/data.

## A2 — Inference/Control

Làm thế nào phân bổ test-time compute và điều khiển trajectory khi model đã được training?

| Nhóm nhỏ | Hướng nghiên cứu | Paper tiêu biểu |
| --- | --- | --- |
| A2.1 | Adaptive reasoning và early stopping | DTSR; REFRAIN |
| A2.2 | Search, branching và phục hồi trajectory | MCTSr; TAAR |
| A2.3 | Cô lập context và quản lý state | Recursive Models |
| A2.4 | Test-time compute và điều khiển độ sâu | Dẫn chéo s1, TIP, FSF |

### A2.1 — Adaptive reasoning và early stopping

Chọn thời điểm kiểm tra và quyết định khi nào reasoning đã đủ hoặc đang lặp thừa.

#### [DTSR — When Is Thinking Enough?](https://arxiv.org/abs/2604.06787v1)

**Long-CoT trực tiếp.** Tên đầy đủ: When Is Thinking Enough? Early Exit via Sufficiency Assessment for Efficient Reasoning.

- **Bài toán:** Dừng reasoning khi đã đủ cơ sở kết luận.
- **Phương pháp:** Theo dõi reflection trigger, thực hiện sufficiency assessment và đóng thinking khi đạt điều kiện.
- **Kết quả:** Qwen3-14B giảm 34.9% token; accuracy 84.8% so với baseline 84.4%.
- **Đóng góp:** Đưa sufficiency vào early stopping training-free.
- **Hạn chế:** Qwen3-8B giảm 0.9 điểm phần trăm accuracy; phải tính overhead của các lần kiểm tra.

[Nguồn và ghi chú chi tiết](research-role.md#rra2-dtsr).

#### [REFRAIN — Stop When Enough](https://arxiv.org/abs/2510.10103v1)

**Long-CoT trực tiếp.** Tên đầy đủ: Stop When Enough: Adaptive Early-Stopping for Chain-of-Thought Reasoning.

- **Bài toán:** Giảm reflection lặp thừa và thích ứng ngưỡng dừng.
- **Phương pháp:** Kết hợp đáp án hiện có, reflection trigger, embedding similarity và SW-UCB cập nhật threshold.
- **Kết quả:** Trên gpt-oss-20B, giảm 33.3%–44.7% token và tăng Pass@1 trên các benchmark được thử.
- **Đóng góp:** Kết hợp redundancy detection với online stopping control.
- **Hạn chế:** Similarity và answer likelihood chỉ là proxy, không bảo đảm logical sufficiency.

[Nguồn và ghi chú chi tiết](research-role.md#rra2-refrain).

### A2.2 — Search, branching và phục hồi trajectory

Tạo/chọn nhánh bằng feedback hoặc self-evaluation; prune, backtrack hoặc restart khi phát hiện bế tắc.

#### [TAAR — Thinking Traps](https://arxiv.org/abs/2601.11940v1)

**Long-CoT trực tiếp.** Tên đầy đủ: Thinking Traps in Long Chain-of-Thought: A Measurable Study and Trap-Aware Adaptive Restart.

- **Bài toán:** Thoát prefix mắc bẫy thay vì tiếp tục tự sửa trên tiền đề sai.
- **Phương pháp:** Diagnostic policy dự đoán trap/escape probability; Cut@Trap cắt prefix và restart với temperature thích ứng.
- **Kết quả:** Cùng K=4 trên R1-Distill-Qwen-8B: accuracy trung bình 69.1%, so với Avg@4 64.5% và PRM@4 66.0%.
- **Đóng góp:** Nối chẩn đoán thinking trap với action phục hồi lúc inference.
- **Hạn chế:** Có thể cắt nhầm prefix gần đúng; K bằng nhau chưa đồng nghĩa tổng compute bằng nhau.

[Nguồn và ghi chú chi tiết](research-role.md#rra2-taar).

#### [MCTSr](https://arxiv.org/abs/2406.07394v2)

**Nghiên cứu suy luận liên quan.** Tên đầy đủ: Accessing GPT-4 level Mathematical Olympiad Solutions via Monte Carlo Tree Self-refine with LLaMa-3 8B.

- **Bài toán:** Tăng chất lượng reasoning toán bằng search và self-refinement.
- **Phương pháp:** MCTS với node là lời giải hoàn chỉnh; critique, rewrite, self-evaluation và cập nhật UCT/value.
- **Kết quả:** LLaMA-3-8B trên MATH tăng từ 24.36% zero-shot lên 58.24% với 8 rollout.
- **Đóng góp:** Cung cấp đối chiếu về branching/search và feedback-guided lựa chọn lời giải.
- **Hạn chế:** Là nghiên cứu liên quan; không phải Long-CoT trực tiếp. Cần tính mọi nhánh và evaluator call.

[Nguồn và ghi chú chi tiết](research-role.md#rra2-mctsr).

### A2.3 — Cô lập context và quản lý state

Dùng call/return và local context để tổ chức subproblem và chuyển intermediate result.

#### [Recursive Models](https://arxiv.org/abs/2603.02112v2)

**Long-CoT trực tiếp.** Tên đầy đủ: Recursive Models for Long-Horizon Reasoning.

- **Bài toán:** Quản lý state/context khi reasoning kéo dài.
- **Phương pháp:** Call/return qua stack frame độc lập; chỉ chuyển return value ngắn về parent.
- **Kết quả:** Model fine-tune từ Qwen2.5-3B-Instruct đạt 64% SAT Hard OOD; trace accuracy Go 4x4 length-OOD đạt 38.5%, flat CoT 1.0%.
- **Đóng góp:** Đề xuất thực thi đệ quy giúp cô lập context và giữ kết quả subproblem.
- **Hạn chế:** Cần decomposition phù hợp; active context ngắn chưa đồng nghĩa tổng token ít.

[Nguồn và ghi chú chi tiết](research-role.md#rra2-recursive-models).

### A2.4 — Test-time compute và điều khiển độ sâu

Điều tiết độ dài, thời điểm đổi hướng hoặc selection/pruning; giữ primary role của paper gốc.

**Tổng hợp hướng nghiên cứu.** Các phương pháp khác nhau ở tín hiệu quan sát và action: kéo dài, dừng, chọn nhánh, sửa prefix, restart hoặc tách context. Search/branching và feedback-guided selection được thể hiện ở MCTSr; TAAR so với PRM@4 và dùng chẩn đoán để restart. Đây là bằng chứng ở mức trajectory/solution, không tự đồng nghĩa verification-guided decoding ở từng token. So sánh cần tính cả evaluator call, nhánh bị bỏ và overhead kiểm tra.

**Liên hệ dependency khi có bằng chứng.** Có liên hệ theo chức năng khi thiết kế thể hiện rõ: Recursive Models mang state giữa các subproblem; TAAR sửa/reconfigure trajectory; DTSR đánh giá sufficiency để đóng reasoning. Budget forcing vì đạt giới hạn token chưa tự chứng minh closure của một reasoning obligation.

## A3 — Analysis

Long reasoning có những hành vi, failure mode và giới hạn nào; bằng chứng hỗ trợ đến đâu?

| Nhóm nhỏ | Hướng nghiên cứu | Paper tiêu biểu |
| --- | --- | --- |
| A3.1 | Cấu trúc diễn ngôn và interpretability/faithfulness | ReasoningFlow; Lanham và cộng sự |
| A3.2 | Redundant steps và cấu trúc graph | CoT2Graph; FSF |
| A3.3 | Complexity, error propagation và giới hạn horizon | ZebraLogic; dẫn chéo LongCoT |
| A3.4 | Reasoning behavior: overthinking/underthinking | Chen; Wang; Peng |

### A3.1 — Cấu trúc diễn ngôn và interpretability/faithfulness

Phân biệt trace nhìn thấy được với dependency của tính toán nội tại; kiểm tra bằng perturbation.

#### [ReasoningFlow](https://arxiv.org/abs/2606.05402v2)

**Long-CoT trực tiếp.** Tên đầy đủ: ReasoningFlow: Discourse Structures for Understanding LLM Reasoning Traces.

- **Bài toán:** Mô tả discourse dependency và kiểm tra liên hệ với tính toán nội tại.
- **Phương pháp:** Trích DAG với cạnh support/attack/verify/assumption; đối chiếu với can thiệp Thought Anchors.
- **Kết quả:** Trong setup QwQ/AIME, Thought Anchors dự đoán cạnh discourse không vượt rõ heuristic khoảng cách token.
- **Đóng góp:** Cung cấp schema trace và bằng chứng phân biệt discourse structure với mechanistic dependency.
- **Hạn chế:** Các thống kê sửa lỗi quan sát được không tự chứng minh quan hệ nhân quả.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-reasoningflow).

#### [Measuring Faithfulness in CoT Reasoning](https://arxiv.org/abs/2307.13702v1)

**Công trình nền tảng.** Tên đầy đủ: Measuring Faithfulness in Chain-of-Thought Reasoning.

- **Bài toán:** Kiểm tra đáp án có phụ thuộc thực chất vào CoT được viết ra hay không.
- **Phương pháp:** Early answering, chèn lỗi, paraphrase và thay reasoning bằng filler token.
- **Kết quả:** Filler token không cải thiện accuracy trong các model/tác vụ được thử.
- **Đóng góp:** Cung cấp phương pháp can thiệp nền tảng cho đánh giá faithfulness.
- **Hạn chế:** Công trình nền tảng pre-o1; không tự khái quát sang mọi reasoning model hoặc latent architecture.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-lanham-faithfulness).

### A3.2 — Redundant steps và cấu trúc graph

Trích topology, dự đoán correctness và phân tích nhánh bị bỏ dở hoặc dependency không được đáp ứng.

#### [CoT2Graph](https://openreview.net/forum?id=wFTJZ8fvns)

**Long-CoT trực tiếp.** Tên đầy đủ: Understanding Failures in LLM Reasoning by Learning Structured Representations of Chain-of-Thought.

- **Bài toán:** Phân tích failure mode mà feature độ dài tuyến tính bỏ sót.
- **Phương pháp:** Trích typed dependency graph, học GNN correctness predictor và phân tích bằng GNNExplainer.
- **Kết quả:** Trên GPQA/DS-Qw14B, correctness-prediction accuracy 65.4%, so với length-based Logistic Regression 57.6%.
- **Đóng góp:** Cho thấy topology mang tín hiệu dự đoán hữu ích và có thể hỗ trợ selection.
- **Hạn chế:** Giải thích GNN predictor không đồng nghĩa giải thích cơ chế nhân quả của LLM.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-cot2graph).

#### [What Characterizes Effective Reasoning?](https://arxiv.org/abs/2509.19284v1)

**Long-CoT trực tiếp.** Tên đầy đủ: What Characterizes Effective Reasoning? Revisiting Length, Review, and Structure of CoT.

- **Bài toán:** Xác định cấu trúc trace liên quan reasoning hiệu quả hơn length/review.
- **Phương pháp:** Dùng Failed-Step Fraction (FSF), chọn ứng viên và can thiệp loại nhánh bị bỏ dở.
- **Kết quả:** Trên 10 LRM, FSF dự đoán correctness nhất quán hơn length/review; branch editing cải thiện continuation ở setup được thử.
- **Đóng góp:** Nối phân tích cấu trúc với selection và context control.
- **Hạn chế:** Graph phụ thuộc judge; abandoned branch không đồng nghĩa bước sai logic.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-effective-reasoning).

### A3.3 — Complexity, error propagation và giới hạn horizon

Phân tích suy giảm theo độ khó hoặc chuỗi phụ thuộc; không đồng nhất complexity với horizon.

#### [ZebraLogic](https://arxiv.org/abs/2502.01100v2)

**Nghiên cứu suy luận liên quan.** Tên đầy đủ: ZebraLogic: On the Scaling Limits of LLMs for Logical Reasoning.

- **Bài toán:** Đo giới hạn reasoning khi độ phức tạp tổ hợp tăng.
- **Phương pháp:** Câu đố lưới CSP có search space kiểm soát; so parameter scaling và test-time strategies.
- **Kết quả:** Llama-3.1-405B đạt 32.6% tổng thể nhưng 1.5% ở Large và 0.0% ở X-Large.
- **Đóng góp:** Định lượng suy giảm theo complexity, bổ sung cho nghiên cứu long-horizon failure.
- **Hạn chế:** Là nghiên cứu liên quan; complexity scaling chưa cô lập cơ chế error propagation trong Long-CoT.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-zebralogic).

### A3.4 — Reasoning behavior: overthinking/underthinking

Khảo sát lặp thừa, đổi hướng sớm và self-doubt; phân biệt tổng độ dài với độ sâu exploration.

#### [Do NOT Think That Much for 2+3=?](https://arxiv.org/abs/2412.21187v2)

**Long-CoT trực tiếp.** Tên đầy đủ: Do NOT Think That Much for 2+3=? On the Overthinking of o1-Like LLMs.

- **Bài toán:** Định lượng compute thừa sau khi đã tìm được lời giải.
- **Phương pháp:** Outcome/process efficiency metric và self-training ưu tiên trace ngắn nhưng giữ reflection.
- **Kết quả:** QwQ-32B-Preview trên MATH500: 2407.9 xuống 1330.7 token, accuracy 93.0% xuống 92.8%.
- **Đóng góp:** Kết nối chẩn đoán overthinking với lựa chọn dữ liệu và preference training.
- **Hạn chế:** Token giảm có thể mất accuracy; first-correct construction dùng nhãn đáp án.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-chen-overthinking).

#### [Thoughts Are All Over the Place](https://arxiv.org/abs/2501.18585v2)

**Long-CoT trực tiếp.** Tên đầy đủ: Thoughts Are All Over the Place: On the Underthinking of o1-Like LLMs.

- **Bài toán:** Giải thích trace dài nhưng đổi hướng trước khi khám phá đủ sâu.
- **Phương pháp:** Underthinking score và TIP phạt transition-token logits trong một cửa sổ decoding.
- **Kết quả:** QwQ-32B-Preview trên AIME24: Pass@1 38.3% lên 44.1%, ước lượng từ 32 mẫu/bài.
- **Đóng góp:** Phân biệt độ dài tổng với độ sâu phát triển từng hướng suy luận.
- **Hạn chế:** Penalty quá mạnh có thể giữ nhánh sai; không mặc nhiên tiết kiệm compute.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-underthinking).

#### [Revisiting Overthinking from Self-Doubt](https://arxiv.org/abs/2505.23480v1)

**Long-CoT trực tiếp.** Tên đầy đủ: Revisiting Overthinking in Long Chain-of-Thought from the Perspective of Self-Doubt.

- **Bài toán:** Khảo sát verification lặp lại và hành vi cố giải đề thiếu tiền đề.
- **Phương pháp:** Phân tích self-doubt và can thiệp prompt kiểm tra tiền đề.
- **Kết quả:** Trên đề thiếu tiền đề, can thiệp giảm 35%–45% token, giữ hoặc tăng accuracy ở model được thử.
- **Đóng góp:** Làm rõ một dạng reasoning behavior gây lãng phí và cách can thiệp đơn giản.
- **Hạn chế:** Kết quả ở đề thiếu tiền đề chưa đại diện cho mọi bài toán có đáp án.

[Nguồn và ghi chú chi tiết](research-role.md#rra3-overthinking).

**Tổng hợp hướng nghiên cứu.** Nhiều token không bảo đảm exploration đủ sâu, và verification lặp lại không nhất thiết có ích. Các nghiên cứu graph bổ sung tín hiệu ngoài length, còn benchmark complexity/horizon cho thấy giới hạn của scaling. Cần tách mô tả tương quan, correctness prediction, trace intervention và internal intervention; một feature dự đoán tốt chưa phải cơ chế nhân quả được chứng minh.

**Liên hệ dependency khi có bằng chứng.** Discourse/structural graph có thể dùng để mô tả hoặc đánh giá dependency; chỉ ghi loại bằng chứng tương ứng. ReasoningFlow không cho phép suy từ cạnh discourse sang causal edge nội tại; ZebraLogic không cô lập riêng error propagation trong Long-CoT. B=N/A khi paper chỉ mô tả hành vi mà chưa đáp ứng tiêu chí chức năng dependency.

## A4 — Evaluation/Benchmark

Đo năng lực reasoning dài, process quality và hiệu quả compute bằng những bài toán và metric nào?

| Nhóm nhỏ | Hướng nghiên cứu | Paper tiêu biểu |
| --- | --- | --- |
| A4.1 | Benchmark long-horizon và planning | LongCoT; SPaRC |
| A4.2 | Metric chất lượng, độ dài và redundancy | CoTJudger; dẫn chéo FSF và metric overthinking |
| A4.3 | Process/outcome evaluation và verifier | ProcessBench; CriticBench |

### A4.1 — Benchmark long-horizon và planning

Tăng dependency horizon/độ khó và kiểm tra state hoặc ràng buộc của lời giải.

#### [LongCoT benchmark](https://arxiv.org/abs/2604.14140v1)

**Long-CoT trực tiếp.** Tên đầy đủ: LongCoT: Benchmarking Long-Horizon Chain-of-Thought Reasoning.

- **Bài toán:** Đánh giá reasoning qua nhiều dependency và horizon dài.
- **Phương pháp:** 2,500 bài template ở năm miền; thí nghiệm riêng tăng số dependency DAG.
- **Kết quả:** Trên 2,000 bài vừa/khó, GPT-5.2 đạt 9.83%; accuracy theo DAG suy giảm nhanh hơn baseline p^N.
- **Đóng góp:** Cung cấp stress test trực tiếp cho long-horizon reasoning và state carrying.
- **Hạn chế:** Không trộn benchmark tổng với thí nghiệm DAG; suy giảm chưa định danh duy nhất cơ chế gây lỗi.

[Nguồn và ghi chú chi tiết](research-role.md#rra4-longcot).

#### [SPaRC](https://arxiv.org/abs/2505.16686v2)

**Long-CoT trực tiếp.** Tên đầy đủ: SPaRC: A Spatial Pathfinding Reasoning Challenge.

- **Bài toán:** Đo planning nhiều bước, giữ ràng buộc và thích ứng compute theo độ khó.
- **Phương pháp:** Bài tìm đường lưới 2D, năm difficulty tier, kiểm tra tính hợp lệ đường đi.
- **Kết quả:** Người giải đạt 98.0% tổng thể; o4-mini đạt 15.8% tổng thể và 1.1% ở Level 5.
- **Đóng góp:** Bổ sung đánh giá planning/state constraints ngoài miền toán.
- **Hạn chế:** Phụ thuộc task representation; token không tăng theo độ khó chưa giải thích nguyên nhân thất bại.

[Nguồn và ghi chú chi tiết](research-role.md#rra4-sparc).

### A4.2 — Metric chất lượng, độ dài và redundancy

Bổ sung chỉ số ở cấp graph/step cho accuracy, token cost và latency.

#### [CoTJudger](https://arxiv.org/abs/2603.07078v1)

**Long-CoT trực tiếp.** Tên đầy đủ: CoTJudger: A Graph-Driven Framework for Automatic Evaluation of Chain-of-Thought Efficiency and Redundancy in LRMs.

- **Bài toán:** Đo redundancy cấu trúc thay vì chỉ đáp án hoặc tổng token.
- **Phương pháp:** Trích graph và Shortest Effective Path (SEP); tính tỷ lệ node nằm ngoài SEP.
- **Kết quả:** Đánh giá 21 reasoning model ghi nhận redundancy đáng kể, thường ở verification sau khi đã có thể kết luận.
- **Đóng góp:** Cung cấp metric tự động cho efficiency ở cấp node/step.
- **Hạn chế:** SEP là proxy phụ thuộc judge, không chứng minh mọi bước ngoài SEP đều bỏ được an toàn.

[Nguồn và ghi chú chi tiết](research-role.md#rra4-cotjudger).

### A4.3 — Process/outcome evaluation và verifier

Đo tìm lỗi, nhận diện lời giải đúng và tách generation, critique, correction.

#### [ProcessBench](https://arxiv.org/abs/2412.06559v4)

**Nghiên cứu suy luận liên quan.** Tên đầy đủ: ProcessBench: Identifying Process Errors in Mathematical Reasoning.

- **Bài toán:** Đánh giá khả năng tìm bước lỗi đầu tiên hoặc nhận ra lời giải không lỗi.
- **Phương pháp:** 3,400 mẫu với nhãn chuyên gia; so PRM và LLM critic qua bốn subset.
- **Kết quả:** F1 trung bình: Skywork-PRM-7B 42.1%, QwQ-32B-Preview 71.5%, o1-mini 87.9%.
- **Đóng góp:** Cung cấp benchmark process evaluation và kiểm tra generalization của verifier/critic.
- **Hạn chế:** F1 là harmonic mean accuracy trên mẫu lỗi/mẫu đúng; tìm lỗi đúng chưa bảo đảm sửa được.

[Nguồn và ghi chú chi tiết](research-role.md#rra4-processbench).

#### [CriticBench](https://arxiv.org/abs/2402.14809v4)

**Nghiên cứu suy luận liên quan.** Tên đầy đủ: CriticBench: Benchmarking LLMs for Critique-Correct Reasoning.

- **Bài toán:** Tách năng lực giải, critique và correction.
- **Phương pháp:** Giao thức Generation–Critique–Correction trên năm miền, đánh giá 17 LLM.
- **Kết quả:** Critique accuracy tương quan với correction success; model nhỏ có thể dè dặt khi self-critique.
- **Đóng góp:** Cung cấp đối chiếu process/outcome và hiệu quả feedback cho reasoning.
- **Hạn chế:** Là nghiên cứu liên quan; tương quan không phải chứng minh nhân quả và không chuyên đo horizon rất dài.

[Nguồn và ghi chú chi tiết](research-role.md#rra4-criticbench).

**Tổng hợp hướng nghiên cứu.** Outcome accuracy không thay thế process quality; error localization khác correction success; token count khác step redundancy. Dependency horizon cần được thao tác hoặc đo riêng thay vì suy từ output length. ProcessBench dùng F1 riêng theo harmonic mean accuracy trên mẫu lỗi/mẫu đúng; metric graph còn phụ thuộc segmentation và judge.

**Liên hệ dependency khi có bằng chứng.** LongCoT tạo task-defined dependency để đánh giá state carrying; CoTJudger và ProcessBench liên quan assessment ở mức cấu trúc hoặc bước. Benchmark/metric đo được failure chưa có nghĩa đã đề xuất phương pháp repair hay chứng minh mechanism nội tại.

## Related Work và tài liệu bổ sung

[Related Work](related-work.md) mô tả phạm vi và cách chín survey phân loại literature. [Phân tích mở rộng/RQ](research-directions.md) là tài liệu bổ sung, không thay thế phần tổng hợp trên.
