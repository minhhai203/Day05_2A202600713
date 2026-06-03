# V-App / V-AI teardown note

## 1. Product promise

Product chọn: **V-App - V-AI**

Nguồn marketing / app store:

- VnExpress viết V-App gom các dịch vụ trong hệ sinh thái Vingroup vào một ứng dụng duy nhất, gồm Vinhomes, VinFast, Xanh SM, Vinpearl, Vinmec, Vinschool, mua sắm và chi tiêu hằng ngày. Bài cũng nói AI dùng truy xuất thông tin, đối chiếu ngữ cảnh, nguồn chính thống và dữ liệu hệ sinh thái để giảm thao tác cho nhu cầu thường ngày.  
  Source: https://vnexpress.net/vingroup-ra-mat-sieu-ung-dung-v-app-5011472.html
- App Store mô tả V-App có AI gợi ý nội dung, dịch vụ và tiện ích phù hợp; cá nhân hóa trải nghiệm; kết nối nhiều dịch vụ số trong một nền tảng để không phải chuyển qua nhiều app.  
  Source: https://apps.apple.com/vn/app/v-app/id6755132024?l=vi
- Trang mini-app Cư dân Vinhomes trên V-App nêu các tác vụ cụ thể như đặt tiện ích, thanh toán hóa đơn, gửi yêu cầu hỗ trợ, liên hệ ban quản lý, tra cứu dịch vụ nội khu.  
  Source: https://v-app.vn/mini/vhr.v-app.vn

Promise rút ra:

> V-AI không chỉ là chatbot trả lời chung chung, mà nên là trợ lý hiểu ngữ cảnh người dùng trong hệ sinh thái Vingroup/V-App, biết gợi ý dịch vụ đúng, dẫn user tới tiện ích đúng, và chỉ dùng nguồn đáng tin cậy.

User được hứa sẽ được giúp:

- Người dùng V-App đang cần tìm đúng dịch vụ/tiện ích trong hệ sinh thái.
- Sinh viên hoặc người dùng có ngữ cảnh giáo dục, lịch học, giấy tờ, hỗ trợ campus.
- Người dùng mới không biết phải mở mục nào hoặc liên hệ ai.

Task kỳ vọng AI làm được:

> Khi user hỏi một thủ tục hoặc nhu cầu cụ thể, V-AI phải nhận ra intent, kiểm tra ngữ cảnh V-App/VinUni nếu có, và đưa ra next step đúng trong app hoặc nói rõ là chưa có dữ liệu.

## 2. Evidence đã thử

Screenshot nằm trong folder `screen-shot/`.

### Prompt 1 - lịch học/sự kiện hôm nay

Input:

```text
Hôm nay tôi có lịch học, sự kiện hoặc việc cần làm nào trong V app không? Hãy liệt kê thời gian, địa điểm, và nhắc tôi lịch cần chuẩn bị
```

Observation:

- V-AI gọi đúng tên user và ngày 03/06/2026.
- V-AI nói hệ thống chưa ghi nhận dữ liệu cụ thể về lịch học/sự kiện/to-do cá nhân.
- V-AI gợi ý kiểm tra Thông báo, Lịch trình/Tiện ích, chuẩn bị QR định danh/CCCD.
- Có card hành động **Xem lịch học VinUni** và các link như đồng bộ Google Calendar, kiểm tra lịch hẹn Vinmec, tìm sự kiện Vinhomes.

Đánh giá:

- Đây là happy path một phần: AI không bịa lịch cụ thể khi không có dữ liệu.
- Nhưng câu trả lời vẫn dài và hơi generic; nếu có card VinUni thì nên đưa card này lên sớm hơn, kèm trạng thái "chưa có quyền/chưa có dữ liệu lịch".

### Prompt 2 - mất thẻ sinh viên, cần vào thư viện hôm nay

Input:

```text
Tôi bị mất thẻ sinh viên và cần vào thư viện hôm nay. Tôi nên làm gì trong V-app, liên hệ ai, và có bước nào cần hoàn thành trước không?
```

Observation:

- V-AI nói đã xem xét 10 nguồn.
- Phần đầu có nói V-App hỗ trợ quản lý/cập nhật một số thông tin cá nhân cơ bản.
- Sau đó câu trả lời đưa thông tin không khớp ngữ cảnh VinUni: Quầy Giải đáp Thông tin tầng 1 thư viện, số điện thoại 043-854-8121, nguồn Hanu/HCMUSSH/Hutech.
- V-AI đưa ra lệ phí, ảnh 3x4, mẫu đơn, thời gian cấp lại thẻ, nhưng không xác nhận đây có phải quy trình của VinUni hay trong V-App không.

Đánh giá:

- Đây là failure path rõ nhất.
- AI trả lời tự tin nhưng bị lệch ngữ cảnh trường. User có thể làm sai quy trình hoặc liên hệ sai nơi.
- Lỗi nằm ở data/tool grounding và UX recovery: khi thiếu nguồn VinUni/V-App, hệ thống không hỏi lại hoặc không nói "chưa có dữ liệu chính thức".

### Prompt 3 - giấy xác nhận sinh viên để nộp visa

Input:

```text
Tôi muốn xin giấy xác nhận sinh viên để nộp visa. Hãy chỉ đúng mục trong V-app hoặc quy trình cần làm, đừng trả lời chung chung
```

Observation:

- V-AI nhận đúng intent là xin giấy xác nhận sinh viên.
- V-AI nói V-App chưa hỗ trợ tính năng xin giấy xác nhận sinh viên trực tiếp.
- Tuy nhiên phần quy trình lại dùng nguồn ngoài và rộng: VnExpress, HIU, LuatVietnam, VFSGLOBAL, Vinschool.
- Câu trả lời không chỉ ra mục cụ thể trong V-App hoặc đường fallback chính thức cho VinUni.

Đánh giá:

- Đây là low-confidence/failure pha trộn.
- Điểm tốt: AI nói "V-App chưa hỗ trợ trực tiếp".
- Điểm gãy: sau khi nói không hỗ trợ, AI vẫn tiếp tục đưa quy trình chung từ nguồn ngoài thay vì chuyển sang fallback an toàn: hỏi trường/cơ sở, đưa Trung tâm trợ giúp, hoặc yêu cầu user xác nhận mình là VinUni student.

## 3. Four paths

| Path | Quan sát từ V-AI | Đánh giá |
|---|---|---|
| Happy | Prompt 1: không bịa lịch cụ thể, có card **Xem lịch học VinUni**. | Có dấu hiệu tốt, nhưng card/action nên xuất hiện sớm hơn và câu trả lời nên ngắn hơn. |
| Low-confidence | Prompt 3: nói V-App chưa hỗ trợ trực tiếp, nhưng vẫn đưa quy trình ngoài. | Low-confidence chưa tốt vì không hỏi lại và không giới hạn nguồn. |
| Failure | Prompt 2: trả lời quy trình mất thẻ bằng nguồn Hanu/HCMUSSH/Hutech, không phải VinUni/V-App. | Failure nghiêm trọng vì user cần hành động trong ngày. |
| Correction | Chưa có screenshot correction. Trong UI có thumbs up/down và copy, nhưng chưa thấy cơ chế hỏi lại, undo, hoặc log correction thành case. | Cần test thêm bằng follow-up: "Thông tin này không phải VinUni, hãy sửa lại theo VinUni/V-App". |

## 4. Finding thành product decision

Khi user hỏi một thủ tục campus có hậu quả hành động thật, ví dụ mất thẻ sinh viên để vào thư viện hoặc xin giấy xác nhận sinh viên,

V-AI có thể nhận đúng intent nhưng truy xuất nguồn ngoài không đúng ngữ cảnh VinUni/V-App và trả lời như một quy trình chính thức,

hậu quả là user có thể liên hệ sai nơi, chuẩn bị sai giấy tờ, mất thời gian trong tình huống cần xử lý ngay,

lỗi thuộc layer **data-tool grounding + UX recovery**,

nên sửa bằng requirement:

> Với các task thủ tục/campus, V-AI chỉ được trả lời quy trình chính thức khi có nguồn thuộc V-App/VinUni hoặc nguồn đã whitelist. Nếu thiếu nguồn, V-AI phải chuyển sang low-confidence path: nói rõ chưa có dữ liệu chính thức, hỏi user xác nhận trường/cơ sở, đưa 2-3 lựa chọn fallback an toàn như Trung tâm trợ giúp V-App, phòng/đơn vị phụ trách trong app, hoặc nút gửi yêu cầu hỗ trợ.

## 5. Sketch as-is / to-be

### As-is

```text
User hỏi thủ tục campus trong V-App
        |
        v
V-AI nhận intent: mất thẻ / xin giấy xác nhận
        |
        v
Search nhiều nguồn ngoài
        |
        v
Trả lời tự tin bằng nguồn lẫn lộn
Hanu / Hutech / HIU / VnExpress / LuatVietnam
        |
        v
User không biết phần nào là chính thức cho VinUni/V-App
        |
        v
Điểm gãy: không có hỏi lại, không có source filter, không có fallback rõ
```

### To-be

```text
User hỏi thủ tục campus trong V-App
        |
        v
V-AI nhận intent + phân loại risk:
"thủ tục hành chính / cần hành động thật"
        |
        v
Kiểm tra nguồn whitelist:
V-App / VinUni / help center / mini-app liên quan
        |
        +-----------------------------+
        | Có nguồn chính thức          | Không có hoặc confidence thấp
        v                             v
Trả lời ngắn, kèm bước cụ thể          Nói rõ chưa có dữ liệu chính thức
và nút mở đúng mục trong app            Hỏi lại trường/cơ sở hoặc mục đích
        |                             |
        v                             v
User làm tiếp trong app                 Đưa fallback an toàn:
                                      Trung tâm trợ giúp / gửi yêu cầu /
                                      liên hệ đơn vị phụ trách
```

## 6. Câu SPEC-change

Finding này sẽ đổi SPEC như sau:

> Prototype không build chatbot trả lời mọi câu hỏi campus. Prototype chỉ xử lý một slice hẹp: **AI hỗ trợ user tìm đúng thủ tục trong V-App/VinUni khi thiếu thẻ hoặc cần giấy xác nhận**, và bắt buộc có low-confidence path: nếu không có nguồn chính thức thì hỏi lại hoặc chuyển sang Trung tâm trợ giúp thay vì tự tổng hợp từ nguồn ngoài.

## 7. Self-check

- [x] Có screenshot/observation cụ thể: `screen-shot/prompt-1-1.PNG` đến `screen-shot/prompt-3-2.PNG`.
- [x] Có đủ 4 paths hoặc nói rõ path chưa có: correction chưa có screenshot, đã ghi rõ cần test thêm.
- [x] Finding viết thành product decision.
- [x] Sketch có as-is và to-be.
- [x] Có câu nói rõ finding này sẽ đổi gì trong SPEC.
