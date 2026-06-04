# Synthesis & Decide — Vinpearl.com (Track B: Travel & Hospitality)

Dùng sau khi nhóm đã có evidence. Mục tiêu là chốt một build slice đủ nhỏ cho Day 06.

---

## 1. Gom evidence thành cụm

Gom theo **workflow/pain**, không gom theo tên feature.

| Cụm pain | Evidence dẫn đến | Mức độ |
|---|---|---|
| **"Không biết chọn khu nào"** | Vinpearl Nha Trang 6 khu — câu hỏi phổ biến nhất theo nhiều bài hướng dẫn; website không có tool hỗ trợ | Cao |
| **"Không biết gói nào bao gồm gì"** | Combo (phòng + VinWonders + vé máy bay) nằm tách biệt; user tự ghép tay và dễ chọn sai | Cao |
| **"Bị bất ngờ bởi chi phí ẩn"** | Review: nước suối trả phí, add-on giải trí không rõ giá, food restriction gây phát sinh | Cao |
| **"Không tin kênh đặt phòng nào"** | Báo Tuổi Trẻ: fanpage giả mạo lừa tiền; nhiều kênh (OTA, đại lý, trực tiếp) gây confusion | Trung bình |
| **"Không huỷ được khi cần"** | TripAdvisor: policy hoàn tiền không rõ, không có cancellation online | Trung bình |

---

## 2. Viết insight

```text
User lần đầu đặt Vinpearl không chỉ cần danh sách resort và giá phòng.
Họ thật ra cần hỗ trợ ra quyết định: khu nào đúng với trip của mình,
và tổng chi phí thực tế là bao nhiêu (không bị bất ngờ khi check-in),
vì Vinpearl có 20+ resort trải đều các điểm du lịch, mỗi khu có tiện ích và restriction khác nhau,
trong khi website hiện tại chỉ liệt kê — không hướng dẫn chọn.
```

---

## 3. Viết opportunity

```text
Cơ hội là dùng AI để augment bước ra quyết định của user:
nhận 3-4 câu hỏi ngắn về trip profile (đi với ai, bao lâu, ưu tiên gì, ngân sách),
gợi ý 2-3 khu resort phù hợp nhất kèm lý do ngắn gọn,
và tóm tắt các chi phí ẩn + restriction hay gặp cho từng khu —
giúp user set đúng kỳ vọng và tự tin đặt phòng,
trong khi vẫn để user tự quyết định cuối (augmentation, không automation).
```

---

## 4. Chọn build slice

**Build slice đề xuất:**  
> AI resort selector cho vinpearl.com — nhận profile trip ngắn → gợi ý top khu phù hợp + cảnh báo chi phí ẩn

Kiểm tra 5 câu hỏi:

| Câu hỏi | Đánh giá |
|---|---|
| User cụ thể chưa? | ✅ Gia đình/cặp đôi/nhóm bạn lần đầu đặt Vinpearl, không biết chọn khu nào |
| Task đủ hẹp chưa? | ✅ Chỉ xử lý bước "chọn khu" và "set kỳ vọng" — không bao gồm booking thực tế |
| AI decision rõ chưa? | ✅ AI rank + giải thích 2-3 khu phù hợp dựa trên input 4 câu hỏi |
| Failure path rõ chưa? | ✅ User input mâu thuẫn (budget thấp + muốn villa riêng) → AI hỏi lại / trade-off |
| Có evidence không? | ✅ 7+ reviews/observations từ TripAdvisor, Booking.com, review blogs |

---

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Đánh giá với Vinpearl | Quyết định |
|---|---|---|
| Evidence yếu, user mơ hồ | Evidence mạnh và cụ thể | Giữ |
| Ý tưởng quá rộng | Đã cắt xuống "chọn khu + cảnh báo chi phí ẩn" | Giữ scope này |
| AI không cần thiết | Rule-based thuần không đủ: cần rank theo combo nhiều tiêu chí | AI cần thiết |
| Rủi ro cao | Gợi ý sai → user đặt nhầm khu → tốn tiền. Chọn augmentation | Augmentation |
| Không demo được trong 1 ngày | Quiz 4 câu + output gợi ý = demo được trong 3-5 phút | Giữ |

---

## 6. Câu chốt cuối

```text
Dựa trên 7+ reviews từ TripAdvisor/Booking.com và phân tích website vinpearl.com,
nhóm sẽ build prototype AI Resort Selector cho vinpearl.com,
cho user là người đặt Vinpearl lần đầu (gia đình / cặp đôi / nhóm bạn),
để giải quyết pain "decision paralysis khi chọn khu" + "bị bất ngờ bởi chi phí ẩn",
bằng cách AI augment bước chọn khu: nhận 4 câu hỏi về trip profile → gợi ý top 2-3 khu + tóm tắt restriction/chi phí hay gặp,
và sẽ test failure path: user nhập budget thấp nhưng muốn villa riêng + WinWonders → AI phải hỏi lại hoặc đề xuất trade-off thay vì trả lời tự tin sai.
```

---

## 7. Backlog

Những thứ **không build trong Day 06**:

- Tích hợp booking thực tế (gọi API Vinpearl)
- So sánh giá realtime với OTA (Booking.com, Agoda, Traveloka)
- Chatbot hỗ trợ sau đặt phòng (hủy phòng, thay đổi ngày)
- Review aggregator từ nhiều nguồn
- Chức năng nhận diện fanpage giả mạo / cảnh báo lừa đảo
- Gợi ý lịch trình / itinerary tại điểm đến
