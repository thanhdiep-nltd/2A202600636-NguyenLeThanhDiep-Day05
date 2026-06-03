# Synthesis & Decide - Từ evidence đến build slice

## 1. Gom evidence thành cụm

Gom theo workflow/pain, không gom theo tên feature.

| Cụm pain | Evidence liên quan | Ý nghĩa product |
|---|---|---|
| Quá tải review nhiều chi nhánh | nhiều chuỗi cửa hàng, nhiều đánh giá, con người tự đọc mất thời gian | Cần tổng hợp theo tuần/chi nhánh, không build màn hình đọc từng review là chính. |
| Star rating không đủ đáng tin | ReviewTrackers: phần lớn rating Yelp là 4-5 sao; khách dùng rating filter khi chọn nhà hàng | Không kết luận bằng điểm sao; phải đọc nội dung review và show quote gốc. |
| Cần kiểm soát chất lượng đồng đều | Kendesign: quản lý chuỗi cần thấu hiểu khách hàng, giữ chất lượng món ăn, phục vụ và không gian đồng bộ | Nhãn phân loại phải map với vận hành: FOOD, SERVICE, AMBIENCE, PRICE, OTHER. |
| AI có thể gom nhóm sai | Failure path: review ngắn, mỉa mai, từ lóng, khen/chê lẫn lộn | Cần low-confidence state, quote gốc và correction path. |

## 2. Insight

```text
Quản lý vận hành chuỗi nhà hàng không chỉ cần đọc review nhanh hơn.
Họ thật ra cần một bản đồ rủi ro vận hành theo chi nhánh,
vì review quá nhiều, star rating không giải thích nguyên nhân, và chất lượng chuỗi phải được giữ đồng đều ở đồ ăn, dịch vụ, không gian và giá cả.
```

## 3. Opportunity

```text
Cơ hội là dùng AI để augment việc phân loại và gom nhóm review tiêu cực,
giúp quản lý nhìn ra 3 vấn đề vận hành nổi bật nhất trong tuần,
trong khi vẫn kiểm soát rủi ro AI gom nhóm sai bằng quote gốc, confidence label và manual relabel.
```

## 4. Build slice

| Câu hỏi | Quyết định |
|---|---|
| User cụ thể chưa? | Có. Quản lý vận hành/chủ chuỗi nhà hàng có nhiều chi nhánh. |
| Task đủ hẹp chưa? | Có. Đọc review tiêu cực trong tuần của một chi nhánh/cụm chi nhánh và nhận báo cáo 3 vấn đề nổi bật. |
| AI decision rõ chưa? | Có. AI phân loại review vào FOOD / SERVICE / AMBIENCE / PRICE / OTHER, gom nhóm vấn đề, tạo summary có quote. |
| Failure path rõ chưa? | Có. AI gom nhóm sai ngữ cảnh hoặc không hiểu review ngắn/tiếng lóng/mỉa mai. |
| Có evidence không? | Có evidence public từ Kendesign, ReviewTrackers và self-use workflow trong; cần bổ sung review mẫu thật trước demo. |

Build slice cuối:

```text
Cho quản lý vận hành chuỗi nhà hàng đang đọc review tiêu cực trong tuần của một chi nhánh,
prototype dùng AI để phân loại và gom nhóm review thành 3 vấn đề vận hành nổi bật nhất,
tạo ra báo cáo Markdown có số lượt nhắc, mức rủi ro, chi nhánh và quote gốc,
đồng thời cho phép người quản lý sửa nhãn hoặc tách review khỏi nhóm sai.
```

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

**Quyết định:** Giữ domain F&B/customer review, nhưng giảm scope mạnh.

| Phần | Quyết định |
|---|---|
| User | Giữ: quản lý/chủ chuỗi nhà hàng. |
| Workflow | Giảm từ "dashboard + chatbot query database toàn diện" xuống "báo cáo review cuối tuần". |
| AI | Giữ một AI decision chính: phân loại + gom nhóm + tóm tắt có quote. |
| Data | Dùng CSV/JSON review mẫu; chưa tích hợp API Google/Facebook/Yelp. |
| UX recovery | Bắt buộc có low-confidence và manual relabel. |

Lý do:

```text
Ý tưởng ban đầu trong `explore.md` có dashboard, chatbot ReAct Agent, tool query database và tool dựng báo cáo động.
Scope này quá rộng cho Day 06.
Lát cắt hợp lý hơn là một input review mẫu -> một AI report -> một correction path.
```

## 6. Câu chốt cuối

```text
Dựa trên evidence rằng quản lý chuỗi cần giữ chất lượng đồng đều và star rating không đủ chỉ ra lỗi vận hành,
nhóm sẽ build prototype báo cáo review cuối tuần,
cho quản lý vận hành chuỗi nhà hàng,
để giải quyết pain quá tải review và chậm phát hiện chi nhánh đang xuống chất lượng,
bằng cách AI augment việc phân loại, gom nhóm và tóm tắt review thành 3 vấn đề nổi bật có quote chứng minh,
và sẽ test failure path AI gom nhóm sai ngữ cảnh bằng confidence label, quote gốc và manual relabel.
```

## 7. Backlog

Những thứ không build trong Day 06:

- Kết nối API thật với Google Maps, Facebook, Yelp, Tripadvisor.
- Chatbot ReAct Agent query database tự do.
- Tool dựng dashboard động cho mọi query.
- Gửi email/Telegram tự động cho chủ chuỗi hoặc store manager.
- Phân quyền owner / operation manager / store manager.
- Training model thật từ correction log.
- Dự báo doanh thu hoặc liên kết với dữ liệu POS.
