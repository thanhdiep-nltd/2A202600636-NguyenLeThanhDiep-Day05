# Evidence Pack - AI hỗ trợ phân tích đánh giá khách hàng cho chuỗi nhà hàng

## 1. Nhóm và track

**Tên nhóm:** Group_A2_E402

**Track:** Food & Local Delivery

**Product/app đã chọn:** Workflow quản lý review từ Google Maps, Facebook, Shoppee

**Build slice đang nghĩ:** AI đọc review tiêu cực trong tuần của một chi nhánh, phân loại theo FOOD / SERVICE / AMBIENCE / PRICE / OTHER, gom thành 3 vấn đề vận hành nổi bật nhất và tạo báo cáo có quote gốc để quản lý kiểm tra.


## 2. User / review / social evidence

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| Quản lý chuỗi nhà hàng cần thấu hiểu khách hàng, đảm bảo chất lượng đồ ăn đồng đều, xây dựng đội ngũ phục vụ chuyên nghiệp và đồng bộ không gian trải nghiệm. | Kendesign - https://thicongnhahang.vn/5-nguyen-tac-quan-ly-chuoi-nha-hang-hieu-qua-chuyen-nghiep.html | Chủ/quản lý chuỗi nhà hàng | Pain không chỉ là đọc feedback, mà là phát hiện chi nhánh nào đang lệch chuẩn vận hành. |
| ReviewTrackers ghi nhận phần lớn rating trên Yelp là 4-5 sao, khách dùng rating filter khi tìm nhà hàng, và hành vi để lại review xảy ra cả sau trải nghiệm tích cực lẫn tiêu cực. | ReviewTrackers - https://www.reviewtrackers.com/blog/restaurant-star-rating/ | Nhà hàng/chuỗi nhà hàng quan tâm online reputation | Star rating là tín hiệu thô; nếu chỉ nhìn điểm sao thì dễ bỏ sót nguyên nhân cụ thể trong review text. |
| Con người tự đọc review rồi tạo báo cáo cho chủ chuỗi mất thời gian. | Self-use trong `explore.md` | Quản lý vận hành | Information overload; cần tổng hợp theo theme và mức rủi ro. |
| Review có thể thiếu ngữ cảnh, dùng từ lóng, hoặc khen/chê lẫn lộn. | Suy luận từ workshop four paths và review text thực tế thường gặp | Quản lý vận hành | AI có thể gom nhóm sai hoặc tự tin quá mức nếu không show source. |

Ghi chú kiểm chứng:

```text
Nhóm chưa có phỏng vấn trực tiếp chủ chuỗi/quản lý vận hành.
Trước checkpoint M1 Day 06, nhóm sẽ kiểm bằng 5-10 review thật từ Google Maps/Facebook của 2-3 chi nhánh cùng thương hiệu hoặc một bộ review mẫu có gắn nhãn thủ công.
```

## 3. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| ReviewTrackers / reputation management tools | Gom review từ nhiều nguồn, theo dõi rating, hỗ trợ phân tích trải nghiệm khách hàng. | Review cần được quản lý như dữ liệu vận hành, không chỉ là comment rời rạc. | Có, nhưng chỉ mô phỏng bằng CSV/JSON review mẫu thay vì tích hợp API thật. |
| BI dashboard vận hành chuỗi | Hiển thị KPI theo chi nhánh, thời gian, nhóm vấn đề. | Quản lý cần nhìn nhanh chi nhánh nào xấu đi và vấn đề nào lặp lại. | Có, tạo dashboard đơn giản với bảng nhóm lỗi và báo cáo Markdown. |
| Ticket triage / customer support AI | AI phân loại nội dung, gắn nhãn, ưu tiên case rủi ro, cho người dùng sửa nhãn. | AI nên augment việc phân loại; correction log giúp giảm lỗi lần sau. | Có, build manual relabel và correction log ở mức prototype. |

## 4. Evidence -> Insight

```text
Evidence nổi bật nhất:
Quản lý chuỗi cần kiểm soát chất lượng đồng đều giữa các chi nhánh, trong khi star rating không đủ nói rõ nguyên nhân vận hành.

Insight:
User không chỉ cần đọc review nhanh hơn.
Thật ra họ cần hỗ trợ ra quyết định vận hành: chi nhánh nào đang có rủi ro, vấn đề nào lặp lại, và bằng chứng review gốc nào chứng minh.

Opportunity:
AI có thể giúp bằng cách augment việc phân loại, gom nhóm và tóm tắt review thành báo cáo có quote gốc, trong khi vẫn để quản lý kiểm tra và sửa nhãn khi AI không chắc hoặc sai.
```

## 5. Evidence đổi SPEC như thế nào?

- [ ] Đổi user chính.
- [x] Đổi pain statement.
- [x] Đổi build slice.
- [x] Đổi Auto/Aug decision.
- [x] Đổi 4 paths.
- [x] Đổi failure mode.
- [x] Đổi owner/test plan.


```text
Trước evidence, nhóm định build dashboard + chatbot AI rộng cho mọi query về review.
Sau evidence, nhóm đổi thành báo cáo cuối tuần cho một chi nhánh/cụm chi nhánh, tập trung vào 3 vấn đề nổi bật nhất.
Lý do: Day 06 chỉ có thời gian build prototype nhỏ; user pain chính là quá tải review và thiếu insight vận hành, không phải thiếu chatbot tổng quát.

Trước evidence, nhóm có thể dùng star rating như tín hiệu chính.
Sau evidence, nhóm dùng review text + theme + quote gốc làm bằng chứng chính.
Lý do: Star rating giúp lọc nhanh nhưng không giải thích vì sao trải nghiệm khách hàng xấu đi.
```
