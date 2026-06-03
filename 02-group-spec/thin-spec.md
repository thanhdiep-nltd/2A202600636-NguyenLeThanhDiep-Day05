# Thin SPEC cuối Day 05 - AI hỗ trợ phân tích đánh giá khách hàng cho chuỗi nhà hàng

Thin SPEC này là bản cam kết đủ rõ để sáng Day 06 nhóm build prototype ngay. Ý tưởng gốc nằm trong `explore.md`.

## 1. Track, product/app và user

**Track:** Food & Local Delivery

**Product/app thật:** Workflow quản lý review từ Google Maps, Facebook, Shoppee Food hoặc file review nội bộ; prototype mô phỏng dashboard/báo cáo nội bộ cho chủ/quản lý chuỗi nhà hàng.

**User cụ thể:** Quản lý vận hành hoặc chủ chuỗi nhà hàng có nhiều chi nhánh, cần theo dõi chất lượng đồ ăn, dịch vụ, không gian và giá cả từ review khách hàng.


## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Quản lý chuỗi nhà hàng cần thấu hiểu khách hàng, giữ chất lượng đồ ăn đồng đều, chuẩn hóa phục vụ và đồng bộ không gian trải nghiệm. | Kendesign - https://thicongnhahang.vn/5-nguyen-tac-quan-ly-chuoi-nha-hang-hieu-qua-chuyen-nghiep.html | Vấn đề không chỉ là đọc review, mà là phát hiện chi nhánh nào đang lệch chuẩn vận hành. | Phân loại review theo nhóm vận hành: FOOD, SERVICE, AMBIENCE, PRICE, OTHER. |
| Yelp có tỷ lệ lớn review 4-5 sao; khách dùng rating filter khi tìm nhà hàng; khách để lại review sau cả trải nghiệm tích cực và tiêu cực. | ReviewTrackers - https://www.reviewtrackers.com/blog/restaurant-star-rating/ | Điểm sao là tín hiệu nhanh nhưng không đủ tin cậy để biết vấn đề vận hành cụ thể. | Không lấy star rating làm kết luận chính; AI phải trích theme lặp lại và quote gốc. |

## 3. Pain statement

```text
User là quản lý vận hành chuỗi nhà hàng đang gặp khó ở bước kiểm tra chất lượng từng chi nhánh từ review khách hàng,
vì review nằm rải rác, số lượng lớn, điểm sao không chỉ ra lỗi vận hành cụ thể, và việc tự đọc rồi viết báo cáo mất nhiều thời gian,
dẫn tới chủ chuỗi chậm phát hiện chi nhánh đang xuống chất lượng hoặc phát hiện nhưng không biết vấn đề chính là đồ ăn, dịch vụ, không gian hay giá cả.
Bằng chứng chính là nguồn về quản lý chuỗi nhà hàng cần kiểm soát chất lượng đồng đều và nguồn ReviewTrackers cho thấy rating chỉ là tín hiệu thô, không đủ thay thế phân tích nội dung review.
```

## 4. Build slice

```text
Cho quản lý vận hành chuỗi nhà hàng đang đọc review tiêu cực trong tuần của một chi nhánh,
prototype sẽ dùng AI để phân loại review theo FOOD / SERVICE / AMBIENCE / PRICE / OTHER và gom thành 3 vấn đề nổi cộm nhất,
tạo ra một báo cáo Markdown gồm tên vấn đề, tỷ lệ/lượt nhắc, mức rủi ro, chi nhánh liên quan và 2-3 quote gốc của khách,
và xử lý failure mode phân loại/gom nhóm sai bằng cách hiển thị quote gốc, đánh dấu low-confidence và cho quản lý gắn nhãn thủ công.
```

## 5. Auto/Aug decision

- [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Review khách hàng có ngữ cảnh, cảm xúc, tiếng lóng và khả năng mỉa mai. Nếu AI tự động kết luận hoặc gửi cảnh báo cho store manager, rủi ro false alarm cao. Prototype nên để AI giảm thời gian đọc và tổng hợp, nhưng con người vẫn kiểm tra trước khi hành động.

**Human role:** Reviewer, decider, trainer. Quản lý kiểm tra quote gốc, quyết định có điều tra chi nhánh hay không, và sửa nhãn khi AI phân loại sai.

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| Happy | Nhiều review cùng nhắc "đợi món lâu", "nhân viên chậm", "phục vụ thiếu chủ động" -> AI gom thành nhóm SERVICE: thời gian phục vụ chậm, hiển thị số lượt nhắc, chi nhánh, mức rủi ro và quote gốc. |
| Low-confidence | Review quá ngắn như "Tệ", "Không quay lại", hoặc câu có nhiều nghĩa -> AI không ép vào nhóm chắc chắn; đưa vào mục "Chưa đủ dữ liệu", show review thô và yêu cầu người quản lý xem lại. |
| Failure | AI gom sai ngữ cảnh, ví dụ review khen "nhân viên nhiệt tình như người nhà" và review chê "nhân viên nói chuyện việc nhà quá to" vào cùng nhóm "nhân viên thiếu chuyên nghiệp". |
| Correction | Quản lý bấm "Gắn nhãn thủ công" hoặc "Tách khỏi nhóm này", chọn FOOD / SERVICE / AMBIENCE / PRICE / OTHER, rồi prototype lưu correction vào log để dùng cho lần chạy sau. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu user nhận báo cáo tổng hợp cuối tuần và chỉ nhìn headline,
AI có thể gom nhóm sai ngữ cảnh hoặc tạo false correlation giữa các review không cùng nguyên nhân,
hậu quả là quản lý hiểu sai vấn đề vận hành, kiểm tra nhầm chi nhánh/bộ phận, hoặc gây áp lực sai cho store manager.
Prototype sẽ xử lý bằng show source: dưới mỗi nhóm lỗi bắt buộc có quote gốc, confidence label, số review liên quan, và nút manual relabel/tách nhóm.
Owner kiểm thử path này là [TBD - thành viên phụ trách test/failure path].
```

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| Đỗ Minh Phúc - 2A202600585 | Research / evidence | Link nguồn Kendesign, ReviewTrackers, bộ review mẫu hoặc screenshot workflow mô phỏng. |
| Nguyen Van Minh - 2A202600904 | Data setup | Customer review analysis by LLM |
| Thanh Điệp - 2A202600636 | Prototype | Demo dashboard/chatbot nhận file review mẫu, phân loại review và tạo báo cáo Markdown. |
| Lê Thanh Minh-2A202600872 | Tool design | Design tool, function for AI Agent |
| Phí Đình Mạnh - 2A202600826 | Demo script / repo | Script demo 3-5 phút: input review -> AI report -> kiểm quote -> sửa nhãn -> xem report cập nhật. |
