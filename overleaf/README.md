# Bản thảo Research Role & Related Work — build local

Đây là bản nháp tiếng Anh để nhóm biên tập, gồm hai phần và thư mục tài liệu tham khảo:

- `research-role.tex`: A1 Training/Data, A2 Inference/Control, A3 Analysis, A4 Evaluation/Benchmark.
- `research-synthesis.tex`: so sánh phương pháp, cấp bằng chứng, metric và 8 RQ đề xuất; được nhập ngay sau `research-role.tex` trong cùng section.
- `related-work.tex`: phạm vi và cách phân loại literature của chín survey.
- `references.bib`: BibTeX dùng chung.
- `draft-main.tex`: tài liệu độc lập để biên dịch và xem trước bằng `draft-main.pdf`.

## Build local

Từ thư mục `overleaf`, chạy lần lượt:

```powershell
pdflatex -interaction=nonstopmode -halt-on-error draft-main.tex
bibtex draft-main
pdflatex -interaction=nonstopmode -halt-on-error draft-main.tex
pdflatex -interaction=nonstopmode -halt-on-error draft-main.tex
```

PDF đầu ra là `draft-main.pdf`; không cần dịch vụ Overleaf. Bản ngày 07/11/2026 gồm 24 paper và 9 survey, dùng chung 33 entry BibTeX. Nếu đã có Perl, có thể thay chuỗi trên bằng `latexmk -pdf draft-main.tex`; MiKTeX trên máy hiện tại chưa có Perl nên dùng chuỗi lệnh trực tiếp.

## Tích hợp vào template LaTeX / Overleaf (nếu cần)

Với project mới, tải các tệp `.tex` và `.bib` trong thư mục này lên, chọn `draft-main.tex` làm Main document và dùng pdfLaTeX. Biên dịch cục bộ tương đương: `pdflatex draft-main`, `bibtex draft-main`, rồi chạy `pdflatex draft-main` hai lần.

Với project nhóm đã có template, nhập `\input{related-work}`, `\input{research-role}`, rồi `\input{research-synthesis}`, sau đó gộp các entry vào bibliography hiện có. Wrapper dùng `natbib`, `hyperref`, `booktabs`, `tabularx`, `amsmath`; điều chỉnh theo template trước khi gộp, tránh nạp trùng gói hoặc thay wrapper đang dùng của nhóm.

Các khóa `rra1_`–`rra4_` và `survey_` liên kết đến nguồn được dùng trong bản thảo. Giữ khóa duy nhất khi bổ sung hoặc hợp nhất BibTeX. Các nhóm nhỏ và primary/secondary role là đề xuất làm việc của nhóm, không phải taxonomy do từng paper công bố.

Chưa đồng bộ với một project Overleaf trực tuyến. Sửa danh mục Markdown hoặc GitHub không tự cập nhật nội dung Overleaf; cần tích hợp vào đúng project và kiểm tra lại template, trích dẫn, bảng và ngắt trang.
