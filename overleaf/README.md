# Bản thảo Research Role & Related Work — build local

Đây là bản thảo tiếng Việt để nhóm biên tập, gồm hai phần và thư mục tài liệu tham khảo. Terminology, tên paper/model, tên dataset, prompt và các ký hiệu kỹ thuật được giữ nguyên khi cần để đối chiếu nguồn.

- `research-role.tex`: phần chính có bốn nhóm A1–A4, 16 hướng nhỏ và 24 paper; từng paper có bài toán, phương pháp, thiết lập/metric, kết quả, đóng góp, hạn chế, nhận xét và vị trí nguồn. Mỗi subgroup có phân tích cơ chế/ranh giới, cuối từng nhóm có bảng đối chiếu.
- `research-synthesis.tex`: phân tích mở rộng và 8 RQ của bản trước, được giữ làm tài liệu bổ sung; **không được nhập vào PDF chính**.
- `related-work.tex`: chín survey được đối chiếu theo phạm vi, taxonomy, đơn vị phân loại, cách sử dụng và giới hạn; có vị trí nguồn và bảng crosswalk.
- `references.bib`: BibTeX dùng chung.
- `draft-main.tex`: bản độc lập, nhập `research-role.tex` trước và `related-work.tex` sau; biên dịch thành `draft-main.pdf`.

## Build local

Từ thư mục `overleaf`, chạy lần lượt:

```powershell
pdflatex -interaction=nonstopmode -halt-on-error draft-main.tex
bibtex draft-main
pdflatex -interaction=nonstopmode -halt-on-error draft-main.tex
pdflatex -interaction=nonstopmode -halt-on-error draft-main.tex
```

PDF đầu ra là `draft-main.pdf`; không cần dịch vụ Overleaf. Bản tiếng Việt ngày 08/11/2026 gồm 24 paper và 9 survey, dùng chung 33 entry BibTeX. Lần chuyển ngôn ngữ giữ nguyên phạm vi tài liệu và số liệu của bản ngày 07/11/2026. Nếu đã có Perl, có thể thay chuỗi trên bằng `latexmk -pdf draft-main.tex`; MiKTeX trên máy hiện tại chưa có Perl nên dùng chuỗi lệnh trực tiếp.

Wrapper dùng UTF-8, font encoding `T5` và `babel` với tùy chọn `vietnamese`; các gói hỗ trợ tiếng Việt đã có sẵn trên máy. Khi nhập vào template khác, bảo đảm template hỗ trợ dấu tiếng Việt; không nạp trùng hoặc để `T1` ghi đè `T5` đang dùng cho phần nội dung.

## Tích hợp vào template LaTeX / Overleaf (nếu cần)

Với project mới, tải các tệp `.tex` và `.bib` trong thư mục này lên, chọn `draft-main.tex` làm Main document và dùng pdfLaTeX. Biên dịch cục bộ tương đương: `pdflatex draft-main`, `bibtex draft-main`, rồi chạy `pdflatex draft-main` hai lần.

Với project nhóm đã có template, nhập `\input{research-role}` và `\input{related-work}` tại vị trí thích hợp, rồi gộp các entry vào bibliography hiện có. Nếu Literature Review là mục 4 trong template nhóm như ảnh phân công, bộ đếm section của template sẽ tự tạo 4.1–4.4; không đặt cứng số mục trong hai tệp nội dung. Wrapper dùng `natbib`, `hyperref`, `booktabs`, `tabularx`, `amsmath`; điều chỉnh theo template trước khi gộp, tránh nạp trùng gói.

Phần mở rộng `research-synthesis.tex` chỉ nhập riêng khi nhóm cần thảo luận metric hoặc RQ; không trộn vào phần tổng hợp literature theo phân công. [Bản Markdown tóm tắt](../papers/literature-review.md) tương ứng trực tiếp với Literature Review trong PDF; [hồ sơ đầy đủ](../papers/research-role.md) giữ vị trí nguồn và các số liệu bổ sung.

Các khóa `rra1_`–`rra4_` và `survey_` liên kết đến nguồn được dùng trong bản thảo. Giữ khóa duy nhất khi bổ sung hoặc hợp nhất BibTeX. Các nhóm nhỏ và primary/secondary role là đề xuất làm việc của nhóm, không phải taxonomy do từng paper công bố.

Chưa đồng bộ với một project Overleaf trực tuyến. Sửa danh mục Markdown hoặc GitHub không tự cập nhật nội dung Overleaf; cần tích hợp vào đúng project và kiểm tra lại template, trích dẫn, bảng và ngắt trang.
