# Báo cáo QC — Nhóm mã 101–104

## 1. Mục đích, dữ liệu và phiên bản

- Mục đích và giới hạn sử dụng: Đặc tả và QC nhãn bounding box 2D cho bài thực hành Day 07; 40 ảnh tuyển chọn, không đại diện cho dữ liệu vận hành.
- Nguồn và phép sử dụng dữ liệu: Nguồn và giấy phép được liệt kê trong `data/ATTRIBUTION.csv`; cần giữ ghi công và điều kiện giấy phép khi chia sẻ.
- Manifest và checksum nhãn cuối: Chưa có `batch_manifest.json` hoặc checksum nhãn cuối vì chưa có nhãn calibration được xác nhận.
- Guideline và taxonomy khi gán / khi bàn giao: Gán độc lập theo guideline/taxonomy v1.0. v1.1 hiện là bản nháp editorial, chưa được nhóm chốt; taxonomy không đổi.

## 2. Phân công và đồng thuận trước calibration

- Lượt hoàn thành / được giao: 80/80 lượt; 40 ảnh, 4 thành viên, mỗi ảnh có 2 annotator theo `assignment.csv`.
- Số cặp box ghép, IoU TB, đồng thuận lớp và mẫu số: 295 cặp ghép; IoU TB 0.969/295; cùng lớp 289/295 = 98.0%. IAA tổng đạt ngưỡng script; cặp 101|102 chưa đạt ngưỡng lớp (38/41 = 92.7%).
- Box chưa ghép, loại do ignore, bất đồng vùng ignore: 102/37 box chưa ghép theo hai phía ghép; 1 box được loại do cả hai vùng ignore; 27 ca bất đồng ignore. Đây là số liệu so sánh, chưa phải số lỗi đã xác nhận.
- Ca hai người có thể cùng sai sau khi đối chiếu tham chiếu: Chưa có bộ tham chiếu được nhóm/coach xác nhận trong hồ sơ này; cần reviewer đối chiếu ảnh gốc, đặc biệt các ảnh đông và các ca tượng/ảnh in/đối tượng chở trên xe.

## 3. Calibration và kiểm lại

- Ca đã xử lý, rule ID, bản sửa và người xác nhận: 0/230 ca được nhóm chốt. `calibration_candidates.csv` có 230 ca trên 32 ảnh; `calibration_decisions.csv` ghi từng ca đang chờ review thủ công, chưa có người chốt.
- Hỗ trợ triage: `calibration_proposals.csv` có 230/230 ca, nối bbox candidate với annotation COCO nguồn (kèm ID, thuộc tính, IoU đối chiếu và quy tắc cần xem); 230 crop theo mã ca được tạo dưới `work/calibration_review/cases/`. Đây là gợi ý AI/chứng cứ định vị, chưa phải review ảnh đầy đủ hay quyết định nhóm; ảnh/nhãn nguồn không bị sửa.
- Tác động v1.1 lên nhãn và ảnh: Chưa áp dụng. Bản v1.1 chỉ là dự thảo quy trình, không đổi taxonomy hay quy tắc gán nhãn; chưa xác nhận sửa ảnh/annotation nào trên CVAT.
- Tham chiếu bằng chứng khi Rework: Chưa có vòng Rework hoặc export sửa. Cần giữ COCO, quyết định và ảnh đối chiếu của vòng trước khi mở vòng mới.

## 4. Kết quả duyệt

- Vòng QC: Chưa mở vòng 1; `qc_sample.py` cần nhãn cuối và manifest hợp lệ trước khi tạo vòng.
- Người review và ngày: Chưa có reviewer QC hoặc ngày review được xác nhận.
- Đã duyệt / cả lô: 0/40 ảnh có bằng chứng QC chính thức; đây không phải kết quả 0 lỗi.
- Ảnh lỗi / ảnh đã duyệt: N/A (chưa có ảnh được duyệt).
- Annotation đối tượng hiện có bị lỗi / annotation đối tượng đã duyệt: N/A (chưa có annotation được duyệt).
- Vật bỏ sót, ảnh và vùng: Chưa được xác nhận bởi QC thủ công; xem các dòng `bo_sot_thua` trong `calibration_candidates.csv` như ca cần điều tra, không coi là lỗi đã chốt.
- Ca khó / phần còn lại, lỗi lặp và ví dụ: 230 ca IAA chưa chốt. Validator cấu trúc cảnh báo `img_031.jpg` annotation #109 (`person`, bbox 16×19 px), cần đối chiếu ngưỡng tối thiểu 20 px bằng reviewer; chưa tự sửa nhãn.
- Một lỗi máy chặn được và một lỗi cần người đọc ảnh: Máy phát hiện được annotation dưới ngưỡng kích thước tại `img_031.jpg` #109; mắt người cần xác định box có khớp người thật và ranh giới nhìn thấy hay không.

## 5. Quyết định bàn giao

- Quyết định: Hold
- Lý do, người nhận và phạm vi sử dụng: Chưa có calibration được chốt, bản COCO cuối/manifest và bằng chứng QC thủ công. Đây chỉ là hồ sơ làm việc, chưa phát hành nhãn cho huấn luyện hoặc đánh giá.
- Nếu còn việc: Nhóm chốt 230 ca trong `calibration_decisions.csv`; người được nhóm giao sửa thực hiện các sửa cần thiết trên CVAT; reviewer độc lập kiểm export, sau đó chạy `build_final.py`, `qc_sample.py --round 1`, điền phiếu thực tế và chạy `qc_report.py`.
- Kiểm ngược từ báo cáo tới ảnh, rule và nhãn: IAA và các ca truy ngược qua `iaa_summary.json`, `calibration_candidates.csv`, `flagged_images.txt`, ảnh gốc `data/images/` và lớp phủ tạm trong `work/viz/`. Chưa có nhãn calibrated để đối chiếu.
