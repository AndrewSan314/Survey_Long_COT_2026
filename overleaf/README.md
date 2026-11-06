# Bản thảo Research Role & Related Work

Đây là bản nháp tiếng Anh để nhóm biên tập, gồm hai phần và thư mục tài liệu tham khảo:

- `research-role.tex`: A1 Training/Data, A2 Inference/Control, A3 Analysis, A4 Evaluation/Benchmark.
- `related-work.tex`: phạm vi và cách phân loại literature của sáu survey.
- `references.bib`: BibTeX dùng chung.
- `draft-main.tex`: tài liệu độc lập để biên dịch và xem trước bằng `draft-main.pdf`.

## Nhập vào Overleaf

Với project mới, tải các tệp `.tex` và `.bib` trong thư mục này lên, chọn `draft-main.tex` làm Main document và dùng pdfLaTeX. Biên dịch cục bộ tương đương: `pdflatex draft-main`, `bibtex draft-main`, rồi chạy `pdflatex draft-main` hai lần.

Với project nhóm đã có template, nhập hai section bằng `\input{related-work}` và `\input{research-role}`, rồi gộp các entry vào bibliography hiện có. Wrapper dùng `natbib`, `hyperref`, `booktabs`, `tabularx`, `amsmath`; điều chỉnh theo template trước khi gộp, tránh nạp trùng gói hoặc thay wrapper đang dùng của nhóm.

Các khóa `rra1_`–`rra4_` và `survey_` liên kết đến nguồn được dùng trong bản thảo. Giữ khóa duy nhất khi bổ sung hoặc hợp nhất BibTeX. Các nhóm nhỏ và primary/secondary role là đề xuất làm việc của nhóm, không phải taxonomy do từng paper công bố.

Chưa đồng bộ với một project Overleaf trực tuyến. Sửa danh mục Markdown hoặc GitHub không tự cập nhật nội dung Overleaf; cần tích hợp vào đúng project và kiểm tra lại template, trích dẫn, bảng và ngắt trang.
