# Evidence Pack — Vinpearl.com (Track B: Travel & Hospitality)

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:** Nhóm Track B  
**Track:** B — Travel & Hospitality  
**Product/app đã chọn:** vinpearl.com — website đặt phòng resort & combo du lịch chính thức của Vinpearl  
**Build slice đang nghĩ:** AI assistant giúp user chọn đúng khu resort Vinpearl phù hợp với nhu cầu (gia đình, ngân sách, loại kỳ nghỉ) và tóm tắt các điểm khác nhau giữa các gói  

---

## 2. Self-use evidence

Nhóm tự dùng vinpearl.com và ghi lại điểm gãy.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Trang `/hotels` liệt kê 20+ resort trải khắp VN (Phú Quốc, Nha Trang, Hạ Long, Đà Nẵng…) nhưng không có bộ lọc theo "loại kỳ nghỉ" hay "phù hợp với…" | booking.vinpearl.com | Failure | User phải đọc thủ công từng trang resort để so sánh |
| Riêng Nha Trang đã có 6 khu Vinpearl khác nhau; không có công cụ so sánh side-by-side ngay trên trang | vinpearlresortvietnam.com (quan sát từ bài hướng dẫn) | Low-confidence | Câu hỏi "ở khu nào?" là câu hỏi phổ biến nhất theo bài review — website chưa giải quyết |
| Combo (phòng + VinWonders + vé máy bay) và gói phòng đơn thuần nằm ở các tab riêng; user dễ bỏ sót gói tiết kiệm hơn | booking.vinpearl.com | Low-confidence | Navigation phân mảnh gây mất cơ hội cross-sell |
| Thông tin "nước suối chỉ cấp 2 chai/ngày", "không được mang đồ ăn từ đất liền" không hiển thị ở trang đặt phòng | TripAdvisor reviews | Failure | Expectation gap → review tiêu cực sau khi check-in |
| Không có chức năng hủy phòng linh hoạt trực tuyến; policy hoàn tiền không rõ ràng trên trang | TripAdvisor (r925399432) | Failure | User bị bất ngờ khi cần hủy; mất niềm tin vào thương hiệu |

---

## 3. User / review / social evidence

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| "Ở Vinpearl Nha Trang nên ở khu nào?" — được ghi nhận là câu hỏi phổ biến nhất trong bài hướng dẫn chọn khu, có 6 lựa chọn khác biệt | vinpearlresortvietnam.com | Du khách lần đầu đặt Vinpearl | Decision paralysis: quá nhiều lựa chọn, không biết khu nào phù hợp với mình |
| "Absence of the ability to cancel your booking. It's not their obligation to do so and have full right not to return money" | TripAdvisor r925399432 – Vinpearl Resort & Spa Nha Trang Bay | Khách quốc tế | Chính sách hoàn tiền không rõ ràng tại bước đặt phòng → cảm giác bị lừa |
| "Hotel water only gives 2 bottles if you still have to buy from the hotel and she is very expensive 50000 debts" | TripAdvisor – Vinpearl Resort Nha Trang | Khách lưu trú ngắn ngày | Chi phí ẩn không được công bố khi booking → bất ngờ tiêu cực |
| "we would have to pay VND 650,000 per person (4 hours)" cho công viên giải trí tối — giá add-on không được trình bày rõ lúc đặt phòng | TripAdvisor – Vinpearl Resort Nha Trang | Gia đình có con nhỏ | Khó ước tính tổng chi phí chuyến đi khi chỉ nhìn giá phòng |
| "Disappointed and dirty", "pool bar staff were rude", "communication options with staff was poor" | Booking.com – 1461 verified reviews | Nhiều phân khúc khách | Kỳ vọng 5-sao không được set đúng ở bước tìm hiểu online |
| Website Vinpearl có nhiều nguồn đặt phòng: vinpearl.com, booking.vinpearl.com, Traveloka, Booking.com, đại lý — dễ gặp tình trạng giả mạo fanpage | Tuổi Trẻ 2026-05-23: "Giả mạo fanpage Vinpearl Nha Trang lừa tiền du khách" | Du khách tìm kiếm khuyến mãi qua mạng xã hội | Trust issue: không biết kênh nào chính thống → sợ bị lừa tiền |
| "You sign a paper on entry saying you can't bring anything from the mainland to the hotel" — không có thông tin này lúc book | TripAdvisor – Vinpearl Resort Nha Trang | Gia đình có trẻ nhỏ / người cao tuổi | Restriction không được communicate → mang đồ dư, bị confiscate |

---

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| **Booking.com** – "Which property type is right for you?" quiz flow | Hỏi 3–4 câu về trip purpose (beach, city, family, romantic) rồi filter kết quả | Guided filtering giảm quyết định | Có — prototype quiz 3 câu |
| **Airbnb** – smart search với tag "Great for families", "Entire home" | Tag-based filtering kết hợp AI ranking theo preference | Personalized ranking từ ít input | Có — rule-based ranking trước, AI sau |
| **Agoda** – price transparency tooltip | Hiển thị breakdown tổng chi phí (thuế, phí dịch vụ, bữa sáng) ngay ở kết quả tìm kiếm | Transparent pricing giảm shock | Có — component tóm tắt chi phí ẩn |
| **Club Med** – resort selector chatbot | Bot hỏi "Bạn đi với ai? Bạn muốn làm gì?" → gợi ý resort phù hợp | Conversational decision support | Có — chatbot đơn giản với 4–5 câu hỏi |

---

## 5. Evidence → Insight

```text
Evidence nổi bật nhất:
- Vinpearl Nha Trang có 6 khu khác biệt; câu hỏi "ở khu nào?" là phổ biến nhất nhưng website không có công cụ hỗ trợ chọn.
- Review tiêu cực tập trung vào: chi phí ẩn (nước, add-on), policy không rõ (hủy phòng, quy định mang đồ), và kỳ vọng không được set đúng.
- Đối thủ (Booking.com, Club Med) đã dùng guided filtering / chatbot để giảm decision fatigue.

Insight:
User không chỉ gặp vấn đề tìm kiếm resort.
Thật ra họ cần được dẫn dắt ra quyết định: khu nào phù hợp với gia đình/cặp đôi/nhóm bạn,
gói nào bao gồm những gì, tổng chi phí thực sự là bao nhiêu,
vì họ thiếu điểm so sánh rõ ràng và sợ bị "bất ngờ" khi tới nơi.

Opportunity:
AI có thể giúp bằng cách tóm tắt sự khác biệt giữa các khu/gói dựa trên profile ngắn của user
(đi với ai, bao lâu, ưu tiên gì) và cảnh báo các chi phí/restriction hay gặp — ngay tại trang booking.
```

---

## 6. Evidence đổi SPEC như thế nào?

- [x] Đổi user chính.
- [x] Đổi pain statement.
- [x] Đổi build slice.
- [ ] Đổi Auto/Aug decision.
- [x] Đổi 4 paths.
- [x] Đổi failure mode.
- [ ] Đổi owner/test plan.

```text
Trước evidence, nhóm định build: chatbot tư vấn chung về du lịch Vinpearl.
Sau evidence, nhóm đổi thành: AI assistant hẹp hơn — nhận 3-4 câu input từ user (ai đi, bao lâu, ưu tiên gì)
  → so sánh 2-3 khu resort phù hợp nhất + cảnh báo chi phí ẩn phổ biến + tóm tắt restriction cần biết.
Lý do: evidence cho thấy pain cụ thể là decision paralysis (quá nhiều khu) và expectation gap (chi phí ẩn),
  không phải thiếu thông tin tổng quan — nên cần augmentation hẹp, không cần chatbot rộng.
```
