# Phân tích hướng nghiên cứu Long-CoT theo A1–A4

Bản phân tích mở rộng, ngày **07/11/2026**. Đọc cùng [24 hồ sơ paper](research-role.md) và [9 survey đối chiếu](related-work.md). Các so sánh, ranh giới nhóm và câu hỏi nghiên cứu dưới đây là **tổng hợp/đề xuất của nhóm**, không phải kết quả thực nghiệm mới.

## 1. Đơn vị phân loại và các khái niệm phải tách

Taxonomy A1–A4 trả lời **paper đóng góp điều gì**, còn subgroup mô tả **họ phương pháp**. Không dùng tên model để quyết định role. Một benchmark có phần phân tích mạnh có thể được gán A3 chính, A4 phụ; một paper SFT có inference control vẫn giữ một bản ghi chính.

| Khái niệm | Câu hỏi được trả lời | Không thể thay thế bằng |
| --- | --- | --- |
| Long-CoT | Có quá trình deliberation mở rộng, khám phá, kiểm chứng? | Chỉ số token đầu vào dài |
| Độ dài trace | Model sinh bao nhiêu nội dung? | Độ sâu logic hay số trạng thái phụ thuộc |
| Độ sâu khám phá | Một hướng được theo đến đâu trước khi đổi hướng? | Tổng số hướng hoặc tổng token |
| Correctness | Đáp án hay bước có đúng theo tiêu chuẩn tác vụ? | Likelihood/confidence cao |
| Utility | Bước có giúp tìm hoặc kiểm tra lời giải? | Chỉ việc bước xuất hiện trên một đường suy luận rút gọn |
| Faithfulness | Trace có phản ánh các yếu tố thực sự ảnh hưởng đáp án? | Trace mạch lạc hoặc đáp án đúng |

## 2. A1 — Cách hình thành và điều chỉnh năng lực

### A1.1 RL-Driven Emergence and Scale

**Câu hỏi:** Có thể học hành vi khám phá, kiểm tra và sửa sai từ reward đáp án đến mức nào? [DeepSeek-R1](research-role.md#rra1-deepseek-r1) và [Kimi k1.5](research-role.md#rra1-kimi-k15) là hai đại diện. Trọng tâm là objective, rollout, verifier và độ ổn định của quá trình tối ưu; không chỉ là chuỗi cuối cùng dài bao nhiêu.

**Ranh giới:** Reward ở cuối vẫn có thể khuyến khích một policy sinh nhiều bước, nhưng không chứng minh mọi bước đúng hoặc cần thiết. Phải tách năng lực base, dữ liệu/prompt RL và điều kiện verifier khỏi đóng góp riêng của thuật toán.

### A1.2 Minimalist Data-Centric SFT

**Câu hỏi:** Một tập trace nhỏ, được chọn tốt, có đủ để khai thác năng lực của checkpoint mạnh? [s1](research-role.md#rra1-s1) và [LIMO](research-role.md#rra1-limo) đặt dữ liệu ở trung tâm: độ khó, độ đa dạng, khả năng giải được và hành vi có trong trace.

**Ranh giới:** Ít mẫu SFT không đồng nghĩa ít tổng compute. Năng lực teacher, chi phí sinh/lọc và tri thức base vẫn tham gia. So sánh s1 với LIMO cần giữ base, decoding và ngân sách đánh giá; không xếp hạng bằng số AIME lấy từ các setup khác nhau.

### A1.3 Curriculum and Hybrid Recipes

**Câu hỏi:** Thứ tự các stage và loại dữ liệu giúp ổn định Long-CoT ra sao? [Light-R1](research-role.md#rra1-light-r1) kết hợp curriculum SFT, preference optimization và merging. Đơn vị phân tích là **thay đổi qua stage**.

**Ranh giới:** Một stage tăng toán nhưng giảm GPQA cho thấy cần xem chuyển giao đa miền. Ablation đáng tin cần kiểm soát lượng dữ liệu và training budget; đường cong checkpoint đơn thuần chưa cô lập nguyên nhân.

### A1.4 Efficiency-Aware RL and Learned Allocation

**Câu hỏi:** Có thể học cách dùng ít compute cho bài dễ nhưng giữ deliberation cho bài khó? [Arora & Zanette](research-role.md#rra1-efficient-rl) dùng length-aware objective; Long2short của Kimi và self-training của Chen cung cấp các cơ chế chuyển giao liên quan.

**Ranh giới:** Học efficiency khác cắt max_tokens khi inference. Cần so cả accuracy–cost frontier và faithfulness, vì nén trace có thể bỏ cả bước thừa lẫn nội dung giải thích hữu ích.

| Họ phương pháp | Thành phần thay đổi | Điều kiện cần ghi | Đối chứng quan trọng |
| --- | --- | --- | --- |
| R1/Kimi | Policy qua RL; reward/rollout recipe | Base, verifier, rollout budget | SFT/RL từ cùng checkpoint |
| s1/LIMO | Dữ liệu và trọng số SFT | Teacher, cách lọc, số mẫu, decoding | Random/equal-size data selection |
| Light-R1 | Thứ tự stage, preference và merging | Data từng stage, decontamination | Bỏ/đổi thứ tự stage cùng compute |
| Efficient RL | Objective và policy allocation | Length weight, task difficulty | Cutoff/SFT/DPO ở mức cost tương ứng |

**Kết luận tổng hợp A1:** Hai trục phụ có ích là *học capability hay học efficiency* và *phụ thuộc dữ liệu teacher hay feedback khi rollout*. Đây là trục mô tả bổ sung; không tăng số primary role.

## 3. A2 — Điều khiển tiến trình lúc suy luận

### A2.1 Early Stopping and Sufficiency

[DTSR](research-role.md#rra2-dtsr) hỏi đã đủ thông tin để kết luận chưa; [REFRAIN](research-role.md#rra2-refrain) tìm phản tư dư thừa và thích ứng ngưỡng. Cần tách **trigger kiểm tra**, **tín hiệu quyết định**, **action dừng**. Cùng trigger “Wait” không có nghĩa hai phương pháp dùng cùng tiêu chuẩn.

### A2.2 Recovery and External Search

[TAAR](research-role.md#rra2-taar) cắt prefix mắc bẫy và restart; [MCTSr](research-role.md#rra2-mctsr) tìm kiếm qua các bản lời giải được refine. Chia nhỏ hướng này thành **sửa prefix có điều kiện** và **phân bổ nhiều ứng viên** giúp tránh gộp mọi phương pháp có restart vào cùng cơ chế.

### A2.3 Context Isolation and State Management

[Recursive Models](research-role.md#rra2-recursive-models) tổ chức subproblem bằng stack frame và return value. Mục tiêu là kiểm soát nội dung đang hoạt động và đường truyền trạng thái. Một thuật toán có thể dùng nhiều tổng token nhưng ít peak context hơn; vì vậy không đánh giá chỉ bằng output length.

### A2.4 Budget and Exploration-Depth Control

Budget forcing của [s1](research-role.md#rra1-s1) điều tiết thời lượng; [TIP](research-role.md#rra3-underthinking) điều tiết chuyển hướng; [FSF](research-role.md#rra3-effective-reasoning) hỗ trợ selection/pruning theo cấu trúc. Đây là dẫn chéo, không thêm ba paper mới vào số lượng A2.

| Điều khiển | Quan sát/tín hiệu | Hành động | Kiểu sai cần đo |
| --- | --- | --- | --- |
| DTSR | Sufficiency assessment | Kết thúc thinking | Dừng khi vẫn thiếu bước |
| REFRAIN | Redundancy + likelihood proxy + bandit | Đổi ngưỡng/dừng | Nhầm kiểm chứng hữu ích với lặp |
| TAAR | Vị trí bẫy và khả năng thoát dự đoán | Cắt prefix, restart | Cắt nhầm prefix gần đúng |
| MCTSr | Self-evaluation/value của ứng viên | Chọn và refine nút search | Reward/judge thiên lệch chọn nhánh |
| Recursive | Call/return và local context | Tách subproblem, trả state | Return làm mất điều kiện cần |
| s1/TIP/FSF | Budget, chuyển hướng, graph | Kéo dài, trì hoãn đổi hướng, chọn/cắt nhánh | Overthinking hoặc cố bám nhánh sai |

**Kết luận tổng hợp A2:** Có thể mô tả mỗi controller bằng bộ *(quan sát, quyết định, hành động, chi phí phụ)*. Cách này giúp so sánh controller có huấn luyện phụ với controller training-free mà không nhầm training-free là cost-free.

## 4. A3 — Giải thích hành vi và giới hạn

### A3.1 Discourse and Faithfulness

[ReasoningFlow](research-role.md#rra3-reasoningflow) mô tả quan hệ diễn ngôn; [Lanham et al.](research-role.md#rra3-lanham-faithfulness) dùng can thiệp trên trace để kiểm tra sự phụ thuộc của đáp án. Cấu trúc đọc được và cấu trúc tính toán nội tại là hai đối tượng khác nhau.

### A3.2 Structural Diagnosis

[CoT2Graph](research-role.md#rra3-cot2graph) khai thác topology để dự đoán correctness và chọn ứng viên. [Feng et al.](research-role.md#rra3-effective-reasoning) phân tích nhánh bị bỏ dở bằng FSF. Cả hai tạo động lực nghiên cứu graph quality, khả năng đổi judge và mức chuyển giao giữa model/domain.

### A3.3 Scaling Limits

[ZebraLogic](research-role.md#rra3-zebralogic) kiểm soát độ khó tổ hợp. Liên hệ với [LongCoT](research-role.md#rra4-longcot) cho phép đặt hai câu hỏi riêng: search space tăng có làm thất bại, và dependency horizon tăng có làm thất bại? Thiết kế nghiên cứu nên thao tác độc lập hai yếu tố.

### A3.4 Overthinking, Underthinking, Self-Doubt

[Chen](research-role.md#rra3-chen-overthinking), [Wang](research-role.md#rra3-underthinking) và [Peng](research-role.md#rra3-overthinking) mô tả các dạng allocation thất bại khác nhau. Một trace có thể vừa dài, vừa đổi hướng nhiều, vừa chưa phát triển đủ một hướng tốt; ba nhãn không phải các lớp loại trừ nhau.

| Loại bằng chứng | Ví dụ | Có thể kết luận | Chưa đủ để kết luận |
| --- | --- | --- | --- |
| Quan sát trace | Length, self-doubt, switching | Có mẫu hành vi trong dữ liệu đã xét | Mẫu đó là nguyên nhân duy nhất |
| Dự đoán | GNN correctness, FSF selector | Feature hữu ích cho dự đoán/selection | Feature là mechanism nội tại |
| Can thiệp trace | Chèn lỗi, cắt nhánh, continuation | Model phản ứng với thao tác cụ thể | Hiệu quả khái quát mọi model/task |
| Can thiệp nội tại | Attention masking/Thought Anchors | Dependency theo phép can thiệp đã chọn | Toàn bộ graph diễn ngôn tương ứng cơ chế |

**Kết luận tổng hợp A3:** Kết quả “longer hurts” và “more thinking helps” chỉ đối lập nếu cùng task, model, budget và loại can thiệp. Cần hỏi *nội dung nào được thêm, ở đâu, và với tác động nào*.

## 5. A4 — Đo cái gì và đo bằng cách nào

### A4.1 Long-Horizon Stress Tests

[LongCoT](research-role.md#rra4-longcot) kiểm tra chuỗi phụ thuộc đa miền; [SPaRC](research-role.md#rra4-sparc) kiểm tra planning và tính hợp lệ của trạng thái/di chuyển. Điểm mạnh là tạo failure analysis ngoài đáp án cuối. Tuy nhiên, mỗi benchmark vẫn có thiên lệch theo cách sinh đề và biểu diễn.

### A4.2 Structural Efficiency

[CoTJudger](research-role.md#rra4-cotjudger) đo phần graph nằm ngoài SEP. Cần giữ riêng **step redundancy**, **token cost**, **latency** và **utility nhân quả**. Một step dài và mười step ngắn có thể tạo tỷ lệ node rất khác dù tiêu tốn token tương tự.

### A4.3 Error Localization and Critique–Correction

[ProcessBench](research-role.md#rra4-processbench) hỏi bước lỗi đầu tiên nằm đâu; [CriticBench](research-role.md#rra4-criticbench) tách generation, critique và correction. Đánh giá critic tốt là điều kiện hữu ích cho hệ thống dùng feedback, nhưng không bảo đảm critic đó chọn đúng action dừng hoặc sửa trong mọi Long-CoT.

| Artifact | Đơn vị đánh giá | Tín hiệu chính | Vai trò trong survey |
| --- | --- | --- | --- |
| LongCoT | Bài toán / dependency chain | Đáp án và suy giảm theo horizon | Đánh giá state carrying |
| SPaRC | Bài tìm đường / move | Solution validity, difficulty tiers | Đánh giá planning và allocation |
| CoTJudger | Graph node / SEP | Step redundancy ratio | Đánh giá cấu trúc efficiency |
| ProcessBench | Lời giải gán nhãn bước | Earliest error hoặc no-error | Đánh giá verifier/critic |
| CriticBench | Generation–critique–correction | Kết quả từng năng lực | Tách phát hiện lỗi khỏi sửa lỗi |

## 6. Quy tắc đọc số liệu và so sánh

**Accuracy và sampling.** Pass@1 ước lượng bằng nhiều lần lấy mẫu vẫn đo một lần thử kỳ vọng; khác với xác suất có ít nhất một đáp án đúng trong k lần thử. Khi paper báo Pass@k, ghi estimator của paper. Đối với lấy mẫu không hoàn lại từ n output, công thức thường dùng là `1 − C(n−c,k)/C(n,k)` với c output đúng. Không đổi “average accuracy over k samples” thành Pass@k.

**ProcessBench F1.** Với `a_err` là accuracy xác định đúng lỗi đầu tiên ở mẫu có lỗi và `a_ok` là accuracy nhận diện lời giải đúng, score là `2*a_err*a_ok/(a_err+a_ok)` theo giao thức paper. Báo rõ aggregation theo subset; không gọi đây là token-level hay step-level binary F1 thông thường.

**Compute.** Ngân sách đường đi K, output tokens và FLOPs không hoán đổi được. Với mục tiêu so hệ thống đầy đủ, cần ghi chi phí policy generation, judge/verifier, kiểm tra dừng, parsing, nhánh bị bỏ và restart; cả training/setup cost nếu câu hỏi là tổng chi phí triển khai. Đây là yêu cầu đo được đề xuất cho nhóm, không phải một số liệu đã có ở mọi paper.

**Uncertainty và leakage.** Một chênh lệch 0.2–0.4 pp không tự chứng minh ưu thế hay equivalence. Cần số lần chạy/samples và khoảng bất định phù hợp; test set nhỏ như AIME đặc biệt nhạy. Ghim checkpoint, phiên bản dataset, ngày model API, prompt và cách kiểm tra contamination.

## 7. Tám câu hỏi nghiên cứu có thể phát triển

Các RQ sau là **đề xuất thực nghiệm**, chưa được thực hiện trong repo này.

| RQ | Động lực từ literature | Thiết kế tối thiểu đề xuất | Chỉ số cần báo |
| --- | --- | --- | --- |
| **RQ1: Học capability hay elicitation?** | R1 so với s1/LIMO | Giữ base và train-token budget; thay dữ liệu/recipe, đánh giá held-out difficulty | Accuracy, generalization, total data-generation cost |
| **RQ2: Learned efficiency có hợp với stopping?** | Efficient RL + DTSR/REFRAIN | Thiết kế 2×2: có/không efficiency training × có/không controller | Accuracy–cost frontier; correct→wrong; overhead |
| **RQ3: Khi nào phản tư hữu ích?** | Chen/Peng so với TIP | Trên cùng prefix, tiếp tục bình thường, suppress, hoặc encourage reflection với budget tương ứng | Repair gain, wrong-turn rate, chi phí |
| **RQ4: Đồ thị có ổn định qua judge?** | CoT2Graph, FSF, CoTJudger | Trích cùng trace bằng nhiều judge và một tập gán nhãn người | Agreement, metric ranking, selector accuracy, judge cost |
| **RQ5: Lỗi do horizon hay combinatorics?** | LongCoT và ZebraLogic | Thay độc lập dependency depth và branching/search difficulty | Accuracy theo hai trục; state validity |
| **RQ6: Khi nào nên restart?** | TAAR và branch editing | Cùng tập prefix và tổng budget; so continue/restart/prune | Escape rate, discarded-correct-prefix rate, net accuracy |
| **RQ7: Nén có làm mất faithfulness?** | Efficient RL và Lanham | Matched hints/perturbations trước và sau nén, có OOD controls | Accuracy, faithfulness proxy, human-readable trace quality |
| **RQ8: Verifier có chuyển sang dài hơn được?** | ProcessBench và long-horizon tests | Giữ loại lỗi, tăng số bước/độ trễ đến lỗi; không tune threshold trên test | Localization, no-error accuracy, calibration, latency |

## 8. Tổ chức đọc và bổ sung paper trong nhóm

Đọc trước R1, s1, Chen-overthinking, Wang-underthinking và ProcessBench để thống nhất khái niệm; tiếp theo đọc các paper thuộc subgroup đang phụ trách. Mỗi bản ghi mới cần primary/secondary role, phạm vi direct/adjacent/foundational, source version, đơn vị đánh giá và claim có vị trí nguồn.

Khi thêm paper, ưu tiên ghi nó **thay đổi hoặc phản biện kết luận nào của subgroup**. Một phương pháp mới có cùng tên gọi “efficient reasoning” nhưng đổi action hoặc yêu cầu verifier khác có thể cần subgroup mới; đổi model/benchmark đơn thuần thường chỉ cần bổ sung bằng chứng trong subgroup hiện có. Quy trình đóng góp nằm ở [CONTRIBUTING](../CONTRIBUTING.md).
