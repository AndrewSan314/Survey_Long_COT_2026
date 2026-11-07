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

## Đọc sâu từng survey

### S1 — Đặc trưng của Long-CoT

**Đơn vị tổ chức:** Các năng lực deep reasoning, feasible reflection và extensive exploration, không phải nhãn đóng góp của một paper. Nhánh feedback/refinement giúp tách phát hiện lỗi khỏi thực hiện sửa lỗi; format/learning giúp tách biểu diễn trace khỏi cách học.

**Cách dùng:** Dùng S1 để giới thiệu Long-CoT và giải thích vì sao reflection/exploration đáng được xem riêng. Sau đó dẫn cùng một phương pháp sang role thích hợp: phương pháp học phản tư thuộc A1, điều khiển phản tư thuộc A2, phân tích phản tư thuộc A3.

**Ranh giới đối chiếu của nhóm:** Khung năng lực và khung research role trả lời hai câu hỏi khác nhau. Không nói S1 “thiếu A3/A4” chỉ vì tên nhánh chính không trùng taxonomy của nhóm. Nguồn: S1 v5, Figures 2–3, §4–6.

### S2 — Chuyển từ System 1 sang System 2

**Đơn vị tổ chức:** Features mô tả hành vi; methods tổ chức thuật toán; evolution mô tả tiến trình phát triển. Structure search, reward modeling, self-improvement, macro action và RFT cùng xuất hiện trong một bối cảnh reasoning LLM rộng.

**Cách dùng:** Dùng để giải thích nguồn gốc thuật toán và liên hệ giữa search với training. Một reward model có thể nằm trong training A1 hoặc làm evaluator/controller ở A2/A4; macro action liên quan cả học abstraction và thực thi subproblem.

**Ranh giới:** System 1–2 là khung tổ chức/diễn giải ở mức survey, không tự chứng minh LLM có cơ chế nhận thức giống người. Không đồng nhất mọi System-2 method với trace ngôn ngữ dài. Nguồn: S2 v6, Figure 2, §3.1–3.3.

### S3 — Bốn câu hỏi về test-time scaling

**Đơn vị tổ chức:** What là dạng compute được mở rộng; How là phương pháp thực hiện; Where là miền tác vụ; How Well là tiêu chí đo kết quả. Một paper có thể nhận một giá trị ở mỗi trục, thay vì được đặt vào một ô duy nhất.

**Cách dùng:** Dùng để chuẩn hóa so sánh sequential Long-CoT, parallel sampling và hybrid search. A1/A2 phân biệt vị trí thay đổi training/inference; bốn W tiếp tục mô tả compute và miền đánh giá bên trong hai role đó.

**Ranh giới:** Test-time scaling bao gồm cả tăng số ứng viên mà mỗi trace không dài hơn. Số sample, độ dài mỗi sample và chi phí selection cần báo riêng. Nguồn: S3 v3, Figure 2, §2–5, §8.2.

### S4 — Inference-as-search

**Đơn vị tổ chức:** Representation/granularity của node, evaluation function, và các phép selection/expansion/simulation/backpropagation. Node là trace, state–action hay terminal solution làm thay đổi ý nghĩa của depth và rollout.

**Cách dùng:** Dùng cho A2.2 và đánh giá verifier trong search. Ví dụ MCTSr refine lời giải hoàn chỉnh nên không thể diễn giải một tầng cây như một bước lập luận nguyên tử của mọi phương pháp khác.

**Ranh giới:** Search bên ngoài và deliberation nội sinh đều có thể tiêu nhiều compute nhưng không có cùng đơn vị đo. Giá trị hữu ích của survey là làm rõ cơ chế search; không dùng tên taxonomy để giả định search tốt hơn flat Long-CoT. Nguồn: S4 v1, §3.2–3.4.

### S5 — Đánh giá reasoning trace

**Đơn vị tổ chức:** Tiêu chí *cần đánh giá* (factuality, validity, coherence, utility) tách khỏi *cách đánh giá* (rule-based matching, intrinsic metrics, external evaluators). Hai chiều này không ánh xạ một-một: cùng utility có thể được xấp xỉ bằng nhiều evaluator.

**Cách dùng:** Nguồn thuật ngữ cho A4 và phương pháp đọc A3. Khi paper báo correctness hay redundancy, cần chỉ rõ nó đang kiểm tra tiêu chí nào và bỏ ngỏ tiêu chí nào.

**Ranh giới:** Hữu ích về mặt diễn ngôn không đồng nghĩa faithful với tính toán nội tại. Dùng một LLM judge cũng tạo nhu cầu meta-evaluation và kiểm tra sai số judge; không biến output của judge thành ground truth tuyệt đối. Nguồn: S5 v3, §3 và §5.

### S0 — Compute ở lúc test, phạm vi rộng

**Đơn vị tổ chức:** Test-time adaptation cho System 1 và deliberate reasoning cho System 2. Nhánh reasoning gồm feedback modeling, test-time strategies và improvement training; nhánh adaptation còn bao gồm những thay đổi ngoài explicit CoT.

**Cách dùng:** Dùng ở đoạn mở rộng bối cảnh: Long-CoT là một cách sử dụng test-time compute, cùng tồn tại với adaptation và search. Khung feedback → strategy → training giúp nối A4, A2, A1.

**Ranh giới:** Không lấy toàn bộ literature test-time compute làm corpus Long-CoT trực tiếp. Paper nền/adjacent cần có nhãn phạm vi, như repo đang làm. Nguồn: S0 v3, §3–4, §7.

### S6 — Efficiency theo lifecycle

**Đơn vị tổ chức:** Inference, SFT, RL, pretraining. Trong inference có length budgeting, system switch, model switch, parallel search; các phần training theo cơ chế nén hoặc học phân bổ.

**Cách dùng:** Dùng để so sánh efficiency đã học trong A1 với efficiency do controller ở A2, đồng thời đưa architectural cost vào thảo luận phạm vi.

**Ranh giới:** Ít token và ít compute không luôn đồng nghĩa, nhất là khi đổi model hoặc thêm routing/judge. Mở rộng về multimodal và ứng dụng phải phân biệt nội dung tổng hợp phương pháp với future directions. Nguồn: S6 v2, Figure 3, §2–6, §7.

### S7 — Efficiency theo nơi can thiệp

**Đơn vị tổ chức:** Model-based, reasoning-output-based, input-prompts-based; bổ sung data efficiency, model compression và evaluation. Đây là câu hỏi *can thiệp vào đâu*.

**Cách dùng:** Phân biệt tối ưu trọng số, sửa output/decoding và điều chỉnh prompt/routing. Cùng early stopping có thể nằm gần nhánh output; huấn luyện length reward gần nhánh model.

**Ranh giới:** Một pipeline có thể thay nhiều nơi cùng lúc nên cần multi-label khi đối chiếu. Không suy ra survey không có evaluation chỉ vì evaluation nằm ngoài ba nhánh phương pháp chính. Nguồn: S7 v4, §3–7.

### S8 — Concise/adaptive theo nhu cầu training

**Đơn vị tổ chức:** Training-free gồm prompt, pipeline, decoding manipulation, merging; training-based gồm fine-tuning và RL. Đồng thời quan tâm lúc nào dùng fast/slow thinking.

**Cách dùng:** Nguồn gần trực tiếp cho A1.4 và A2.1/A2.4. Chi phí chuẩn bị của phương pháp và chi phí thực thi cần được đọc riêng.

**Ranh giới:** Training-free không đồng nghĩa không thêm module, không có calibration hay không tốn compute. Survey nêu loại trừ general compression, architectural optimization và multimodal efficiency; đó là lựa chọn phạm vi của tác giả, không phải thiếu sót được nhóm phát hiện. Nguồn: S8 v1, §1, §3–4.

## Crosswalk: giữ nhiều trục thay vì ép taxonomy trùng nhau

| Survey | Trục phân loại trung tâm | Câu hỏi bổ sung khi đưa vào A1–A4 |
| --- | --- | --- |
| S1 | Năng lực/đặc trưng Long-CoT | Paper học, điều khiển, giải thích hay đo năng lực đó? |
| S2 | Features / methods / evolution | Đóng góp trung tâm là algorithm, behavior hay evidence? |
| S3 | What / How / Where / How Well | Tăng loại compute nào, ở đâu, với budget và metric nào? |
| S4 | Node / evaluator / search dynamics | Đơn vị search và nơi feedback ảnh hưởng policy là gì? |
| S5 | Tiêu chí và loại evaluator | Metric đo tiêu chí nào, có meta-evaluation không? |
| S0 | Adaptation / deliberate reasoning | Long-CoT trực tiếp hay chỉ là bối cảnh compute? |
| S6 | Lifecycle stage | Chi phí được chuyển từ inference sang training hay giảm toàn hệ thống? |
| S7 | Đích can thiệp | Input, model, output hay nhiều thành phần cùng thay đổi? |
| S8 | Training requirement | Thành phần nào học trước, thành phần nào thích ứng online? |

**Ví dụ mã hóa một paper:** s1 có primary A1 và secondary A2; theo S1 liên quan deep reasoning/exploration; theo S3 có tuning-based và sequential scaling; theo S8 có cả training-based và decoding control. Đây là crosswalk do nhóm đề xuất, không phải khẳng định từng survey đã gán s1 đúng các nhãn này.

## Luận điểm để viết Related Work

1. **Các survey đã có những trục phân loại khác nhau.** S1 mô tả đặc trưng Long-CoT; S2/S0 dùng khung System 1–2; S3 phân tích cách scale compute; S4 đi sâu search; S5 tập trung evaluation; S6–S8 tập trung efficiency/adaptivity.
2. **A1–A4 là cách tổ chức theo vai trò nghiên cứu.** Một paper có thể được đặt vào nhiều taxonomy trước: s1 vừa là SFT dữ liệu ít (A1), vừa có budget forcing (A2). Gán primary/secondary role giúp tránh đếm trùng và giữ rõ đóng góp trung tâm.
3. **Điểm nhấn đề xuất của bản thảo:** nối training/data → inference/control → phân tích hành vi/cơ chế → bằng chứng đánh giá. Đây là lựa chọn tổng hợp của nhóm, chưa phải tuyên bố novelty hay sự vượt trội đã được kiểm chứng.
4. **So sánh cần cùng điều kiện.** Ghi model, split, sampling và tổng chi phí; tách accuracy, process quality, efficiency, faithfulness. Token giảm không tự chứng minh latency/FLOPs giảm tương ứng.

### Phạm vi đóng góp nên phát biểu như thế nào?

Có thể viết: “Chúng tôi tổ chức literature theo vai trò đóng góp A1–A4 và dùng các trục capability, compute, intervention và evaluation của survey trước để đối chiếu. Cách tổ chức này giúp nối mục tiêu huấn luyện, hành động điều khiển, bằng chứng phân tích và giao thức đánh giá trong cùng bản ghi paper.”

Không nên viết “đây là survey đầu tiên có cả training, inference, analysis và benchmark” khi chưa kiểm kê toàn bộ survey. Cũng không nên tạo bảng tick/cross coi survey không dùng tên A3 là không nghiên cứu analysis. Một phát biểu novelty mạnh cần có corpus survey, tiêu chí coverage và quá trình đối chiếu riêng.

### Các khoảng trống dùng để dẫn sang Research Role

- **Đánh đổi giữa các mục tiêu:** Literature dùng nhiều cách tối ưu accuracy/cost; bản thảo sẽ hỏi phương pháp giữ được process quality và faithfulness ra sao, thay vì chỉ so token.
- **Tín hiệu và action chưa đồng nhất:** “Confidence”, “redundancy”, “sufficiency” là tín hiệu khác nhau; stop, switch, restart và prune là action khác nhau. A2 có thể làm rõ mapping này.
- **Cấp bằng chứng:** Correlation, correctness prediction, trace intervention và internal intervention không có cùng ý nghĩa. A3 nên ghi rõ mức bằng chứng và setup.
- **Đơn vị đánh giá:** Dataset long-horizon, error localization và graph redundancy kiểm tra các đối tượng khác nhau. A4 giải thích metric nào hỗ trợ được claim nào.

Đây là **góc tổng hợp được đề xuất**, không tuyên bố các survey trước bỏ qua toàn bộ bốn vấn đề này. Chi tiết subgroup, so sánh và RQ nằm ở [research-directions.md](research-directions.md).

## Quy trình cập nhật và mức kiểm chứng

- Tìm theo từ khóa Long-CoT / long chain-of-thought / reasoning efficiency / underthinking / test-time scaling; mở rộng từ survey và danh mục sẵn có. Ưu tiên nguồn tác giả, arXiv và proceedings.
- Chọn nghiên cứu đại diện cho một phương pháp hoặc hiện tượng; giữ công trình liên quan/nền tảng khi cần giải thích nguồn gốc phương pháp. Đây không phải corpus bao phủ mọi paper đến ngày cập nhật.
- Ngày 07/11 đã đọc các phần hỗ trợ nhận xét của **4 paper mới** và **3 survey mới**, ghim phiên bản; đối chiếu taxonomy của S0–S5 từ PDF sẵn có và spot-check R1 v2. Các bản ghi cũ được kế thừa, không tuyên bố đã tái kiểm toàn bộ số liệu trong lượt này.
- Bản mở rộng bổ sung đọc phương pháp/nhận xét đối chiếu cho cả 24 hồ sơ; kiểm tra sâu hơn reward online của REFRAIN (§3.3–3.6), overhead sufficiency check của DTSR (§4.2) và định nghĩa F1 của ProcessBench (§4.1). Các nhận xét so sánh và RQ là diễn giải/đề xuất của nhóm; không tạo thêm kết quả thực nghiệm hoặc thay thế việc tái kiểm toàn bộ bảng số liệu.
- Số liệu là tác giả báo cáo, chưa tái lập thí nghiệm. Không xem đồ thị trích bằng LLM là bằng chứng trực tiếp về cơ chế nhân quả nội tại.

Bản LaTeX tương ứng: [related-work.tex](../overleaf/related-work.tex). Nguồn S0–S5 có [PDF trong repo](surveys/); S6–S8 dùng link phiên bản, không cần commit thêm bản PDF.
