# Thin SPEC — AI Resort Selector cho Vinpearl.com

Track B: Travel & Hospitality | vinpearl.com

---

## 1. Track, product/app và user

**Track:** B — Travel & Hospitality  
**Product/app thật:** vinpearl.com — website đặt phòng resort & combo du lịch chính thức  
**User cụ thể:** Người Việt (gia đình hoặc cặp đôi), lần đầu hoặc lần hiếm gặp đặt Vinpearl, đang ngồi lên kế hoạch chuyến đi 2–5 ngày, chưa biết chọn khu nào trong 20+ resort của Vinpearl.  
**Nhóm có phải user thật không?** Gần đúng — thành viên nhóm đã từng tìm hiểu Vinpearl nhưng chưa ai đặt trực tiếp trên vinpearl.com. Khác biệt chính: nhóm có thời gian nghiên cứu kỹ; user thật thường quyết định vội, dựa nhiều vào gợi ý của người quen hoặc tìm kiếm Google.

---

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Câu hỏi "ở khu nào?" là phổ biến nhất với Vinpearl Nha Trang (6 khu); website không có công cụ giúp chọn | vinpearlresortvietnam.com + review blogs | User bị decision paralysis trước 20+ resort của cả hệ thống | Build slice phải giải quyết "chọn khu" trước, không phải "đặt phòng" |
| "Absence of the ability to cancel your booking… full right not to return money" — TripAdvisor r925399432 | TripAdvisor | Policy ẩn → mất trust sau khi đặt | Prototype phải hiển thị cảnh báo policy quan trọng trước khi user quyết định |
| "Hotel water only gives 2 bottles… very expensive 50000 VND" — TripAdvisor Nha Trang | TripAdvisor | Chi phí ẩn gây shock sau check-in | Output của AI phải kèm "chi phí hay phát sinh" cho từng khu |
| Giả mạo fanpage Vinpearl lừa tiền khách — Tuổi Trẻ 23/5/2026 | Tuổi Trẻ | User không biết kênh nào chính thống | Prototype chạy trên vinpearl.com chính thức, không phải kênh ngoài |
| Club Med / Booking.com dùng quiz flow + guided filtering để giảm decision fatigue | Competitor analysis | Pattern đã được validate ở thị trường tương tự | Build quiz 4 câu thay vì search text tự do |

---

## 3. Pain statement

```text
User (gia đình / cặp đôi lần đầu đặt Vinpearl) đang gặp khó ở bước chọn khu resort,
vì vinpearl.com liệt kê 20+ resort không có bộ lọc theo nhu cầu cụ thể
và không hiển thị sự khác biệt thực sự giữa các khu (tiện ích, restriction, giá add-on),
dẫn tới: mất nhiều giờ đọc thủ công, chọn nhầm khu không phù hợp,
hoặc bị bất ngờ bởi chi phí ẩn / quy định sau khi đã đặt — dẫn đến trải nghiệm kém và review tiêu cực.
Bằng chứng chính là: review tiêu cực về chi phí ẩn trên TripAdvisor/Booking.com
và câu hỏi "ở khu nào?" xuất hiện lặp đi lặp lại trên các diễn đàn review.
```

---

## 4. Build slice

```text
Cho user (gia đình / cặp đôi) đang lên kế hoạch đặt resort Vinpearl,
prototype sẽ dùng AI để augment bước chọn khu:
  nhận input từ 4 câu hỏi ngắn (đi với ai, bao lâu, ưu tiên gì, ngân sách/đêm),
  → output: top 2-3 khu phù hợp kèm lý do ngắn + cảnh báo chi phí ẩn / restriction hay gặp tại từng khu,
tạo ra: so sánh cá nhân hóa thay vì danh sách toàn bộ,
và xử lý failure mode "input mâu thuẫn (budget thấp + villa riêng + WinWonders)"
bằng cách hỏi lại / đề xuất trade-off thay vì trả lời tự tin sai.
```

---

## 5. Auto/Aug decision

Chọn một:

- [x] **Augmentation:** AI gợi ý / so sánh / cảnh báo, user quyết định cuối (tự đặt phòng).
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Việc chọn khu resort ảnh hưởng đến tài chính (triệu đồng/đêm) và kỳ vọng cả chuyến đi — user cần tự quyết định cuối. Nếu AI tự đặt phòng mà gợi ý sai, hậu quả rất khó thu hồi. Augmentation giữ được trust và cho phép user override dễ dàng.  
**Human role:** decider (user tự bấm đặt phòng sau khi đọc gợi ý AI)

---

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| Happy | User nhập: "Gia đình 2 người lớn 2 trẻ em, 3 đêm Phú Quốc, muốn có bãi biển và công viên nước, ~3 triệu/đêm" → AI gợi ý đúng khu (VD: Vinpearl Resort & Spa Phú Quốc) kèm lý do rõ ràng và cảnh báo "gói WinWonders nên mua trước, rẻ hơn mua tại cổng" |
| Low-confidence | User nhập: "Đi 2 người, thích yên tĩnh, 2 đêm, không biết ngân sách bao nhiêu" → AI đề xuất 2 khu phù hợp nhưng nêu rõ "thiếu thông tin ngân sách nên chưa thể lọc chính xác — bạn có thể cho biết budget/đêm để tôi lọc thêm không?" |
| Failure | User nhập: "Budget 800k/đêm, muốn villa riêng hồ bơi" → AI không tự tin gợi ý khu nào trong hệ thống Vinpearl (giá thấp nhất ~2 triệu/đêm), phải thông báo rõ: "Không tìm được khu phù hợp trong ngân sách này — các villa hồ bơi của Vinpearl bắt đầu từ X triệu/đêm" |
| Correction | User nhận gợi ý khu nhưng nói: "Tôi đã ở khu đó rồi, muốn thử khu khác" → AI loại khu cũ và gợi ý lại top 2 từ danh sách còn lại |

---

## 7. Failure mode nguy hiểm nhất

```text
Nếu user nhập profile mơ hồ / mâu thuẫn (VD: budget thấp + yêu cầu premium),
AI có thể gợi ý tự tin một khu không phù hợp ngân sách hoặc không có tiện ích yêu cầu,
hậu quả là: user đặt nhầm khu, tốn vài triệu VND và trải nghiệm kém,
reinforcing đúng pattern review tiêu cực hiện tại của Vinpearl.
Prototype sẽ xử lý bằng: hỏi lại thay vì tự suy luận khi confidence thấp;
hiển thị rõ "Tôi không chắc với thông tin này — bạn có thể làm rõ X không?"
thay vì đưa ra gợi ý kèm disclaimer nhỏ dễ bỏ qua.
Owner kiểm thử path này là: [điền tên thành viên phụ trách test].
```

---

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| [TBD] | Research / evidence bổ sung: phỏng vấn nhanh 1-2 người từng đặt Vinpearl | File ghi chú phỏng vấn hoặc screenshot review thêm |
| [TBD] | SPEC: hoàn thiện thin SPEC + cập nhật sau feedback Day 06 | vinpearl-thin-spec.md cập nhật |
| [TBD] | Prototype: build quiz 4 câu + logic gợi ý khu + cảnh báo chi phí ẩn | Link demo hoặc video prototype |
| [TBD] | Test failure path: input mâu thuẫn (budget thấp + villa) + input không rõ ngân sách | Screenshot / recording test 2 failure cases |
| [TBD] | Demo script + repo: viết script 5 phút, chuẩn bị repo cho checkpoint M1 | Demo script .md + repo link |
