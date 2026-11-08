# Bổ sung paper cho Long-CoT survey

Đầu ra chính theo phân công là [`papers/literature-review.md`](papers/literature-review.md); hồ sơ đầy đủ và vị trí nguồn nằm ở [`papers/research-role.md`](papers/research-role.md). Thêm hoặc sửa paper bằng pull request; nếu có quyền ghi, dùng nhánh riêng để thành viên cùng đối chiếu nguồn.

Survey và đối chiếu taxonomy nằm ở [`papers/related-work.md`](papers/related-work.md). Với thành viên chưa có quyền ghi, fork repo rồi gửi pull request; không cần được thêm collaborator để đề xuất paper.

Phân tích mở rộng và RQ nằm ở [`papers/research-directions.md`](papers/research-directions.md) và `overleaf/research-synthesis.tex`; phần này không nằm trong PDF chính. Khi thêm phương pháp, ghi nó bổ sung hoặc phản biện kết luận nào của subgroup.

Viết nội dung giải thích bằng tiếng Việt; giữ terminology và tên riêng kỹ thuật để tra cứu được nguồn. Không dịch lại tên paper, model, dataset, prompt literal hoặc khóa BibTeX. Wrapper LaTeX dùng UTF-8, encoding `T5` và `babel[vietnamese]`.

## Thông tin cần có

- Tên chính xác, tác giả, năm, phiên bản đã đọc và URL nguồn sơ cấp ổn định (arXiv, proceedings hoặc trang chính thức của paper).
- Vai trò chính: **A1 Training/Data**, **A2 Inference/Control**, **A3 Analysis**, hoặc **A4 Evaluation/Benchmark**. Có thể ghi vai trò phụ; chọn vai trò chính theo đóng góp trung tâm của paper.
- Phạm vi: trực tiếp nghiên cứu Long-CoT, nghiên cứu suy luận liên quan, hoặc công trình nền tảng. Nêu lý do nếu mối liên hệ với Long-CoT chỉ gián tiếp.
- Bốn ghi chú ngắn: **bài toán**, **phương pháp**, **kết quả**, **đóng góp**; thêm giới hạn quan trọng và vị trí nguồn (mục/bảng/hình/trang).
- Nếu có số liệu, giữ đúng model, dataset/split, metric, baseline và ngân sách thử nghiệm. Ghi rõ đó là kết quả tác giả báo cáo; phân biệt điểm phần trăm với phần trăm tương đối.
- Tách **đơn vị đánh giá** (bài, trace, bước, node, token), **nguồn nhãn/verifier**, **chi phí phụ** và **cấp bằng chứng** (quan sát, dự đoán, can thiệp trace, can thiệp nội tại). Nếu paper không báo một chi phí hay uncertainty cần thiết, ghi “chưa báo/không xác minh”, không điền suy đoán.
- Ghi nhận xét so sánh của nhóm riêng với claim tác giả. Một feature dự đoán correctness không mặc nhiên là nguyên nhân của correctness; một gain khi đổi controller không chứng minh cơ chế nhận thức tổng quát.

Đọc các phần toàn văn hỗ trợ nhận xét; không dùng riêng search snippet làm bằng chứng. Đánh dấu thông tin chưa xác minh, đặc biệt venue, phạm vi thực nghiệm và các diễn giải nhân quả. Những nhóm nhỏ dưới A1–A4 là đề xuất tổng hợp đang được điều chỉnh của nhóm.

## Trước khi gửi thay đổi

1. Kiểm tra paper đã có theo DOI/arXiv ID; paper liên quan nhiều nhóm dùng một bản ghi chính và dẫn chéo thay vì đếm thành nhiều paper.
2. Kèm link và vị trí nguồn cho nhận xét được thêm/sửa. Khi thay vai trò hoặc nhóm nhỏ, giải thích ngắn lý do trong pull request.
3. Cập nhật bản tóm tắt trong `papers/literature-review.md` và `overleaf/research-role.tex` với cùng bốn trường bắt buộc; giữ ghi chú nguồn chi tiết trong `papers/research-role.md`. Thêm entry vào [`overleaf/references.bib`](overleaf/references.bib) nếu chưa có; dùng khóa duy nhất. Các tệp được hiệu chỉnh thủ công, không tự đồng bộ lên dịch vụ Overleaf.
4. Khi thêm paper/survey, cập nhật số lượng và bảng tổng hợp ở README, phần mở đầu paper list và abstract trong `overleaf/draft-main.tex`. Nếu chỉ bổ sung phân tích, giữ số lượng và primary role hiện có. Build local bằng lệnh trong [`overleaf/README.md`](overleaf/README.md); kiểm tra citation và bảng sau khi biên dịch.

README dẫn đến danh mục paper và các tệp LaTeX. Giữ các tài liệu survey đã có khi bổ sung nghiên cứu mới.
