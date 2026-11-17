# Guideline gán nhãn — v1.1 — BẢN NHÁP CHỜ NHÓM CHỐT

> **Trạng thái: HOLD.** Đây là phần bổ sung quy trình để nhóm thảo luận, chưa phải guideline đã được phê duyệt và không được dùng làm căn cứ phát hành nhãn cuối. Các định nghĩa lớp, thuộc tính, quy tắc R-01 đến R-11 và ngưỡng giữ nguyên theo [guideline_v1.0_agreed.md](guideline_v1.0_agreed.md) và [`taxonomy.json`](../taxonomy.json). Không có thay đổi taxonomy trong bản nháp này.

## Căn cứ lập bản nháp

IAA trước calibration ghi nhận 295 cặp box ghép trên 40 ảnh, IoU trung bình 0.969 và đồng thuận lớp 98.0%. Tuy vậy có 230 ca bất thường trên 32 ảnh: 125 ca bỏ sót/thừa, 42 ca thuộc tính, 27 ca bất đồng vùng ignore, 24 ca IoU thấp, 6 ca sai lớp và 6 ca có cờ `can_review`. Các số này là dấu hiệu để điều tra, không phải quyết định rằng bên nào đúng.

`consensus_draft.json` là đầu ra gom box tự động để hỗ trợ xem xét. Không dùng nó làm nhãn cuối và không mặc định chọn box trung bình, lớp đa số hoặc thuộc tính đa số nếu chưa đối chiếu ảnh gốc và quy tắc.

## Bổ sung quy trình calibration — đề xuất editorial

1. Với từng `case_id`, mở ảnh gốc và lớp phủ nhãn của các annotator; kiểm tra box, lớp, thuộc tính, đối tượng bị bỏ sót và vùng `ignore_region` theo quy tắc v1.0.
2. Ghi rõ chứng cứ và quy tắc liên quan trong `calibration_decisions.csv`. Phân biệt quyết định đã được người trong nhóm chốt với ca còn chờ review; không điền người chốt, phiếu sửa hoặc kết quả kiểm lại nếu việc đó chưa xảy ra.
3. Ca chưa đủ chứng cứ phải ghi `CHỜ REVIEW THỦ CÔNG:` kèm nguyên nhân. Ca này chưa được tính là đã calibration và không được đi tiếp tới `build_final.py` hoặc QC phát hành.
4. Chỉ ghi đã sửa sau khi có bản COCO sửa từ người gán; chỉ ghi đã kiểm lại sau khi reviewer so sánh ảnh, quyết định và bản export tương ứng.
5. Đổi nghĩa quy tắc cần quyết định phạm vi toàn lô và kiểm lại cả 40 ảnh theo quy trình trong `GUIDE.md`. Không đổi taxonomy hoặc các ngưỡng `rules` nếu chưa có căn cứ và phiên bản taxonomy mới.

## Việc còn mở

- Nhóm cần xem và chốt từng ca trong `../qc/calibration_decisions.csv`; hiện các dòng còn trạng thái chờ review.
- Sau khi quyết định, người được giao sửa cần thực hiện trên CVAT, export đúng phạm vi và nhờ reviewer kiểm lại. Không có sửa CVAT nào được xác nhận trong bản nháp này.
- Chỉ sau khi hoàn tất các bước trên mới thay trạng thái bản nháp, tạo COCO final và mở vòng QC.
