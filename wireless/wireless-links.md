---
title: Wireless Links
parent: Wireless
nav_order: 1
layout: page-with-toc
---

# Kết nối Không dây (Wireless Links)

## Giới thiệu về Công nghệ Không dây (Wireless Technologies)

Các công nghệ truyền thông không dây thực tế đã xuất hiện trước cả Internet. Vào những năm 1880, thiết bị **photophone** (Bell và Tainter) đã thử nghiệm gửi dữ liệu không dây bằng cách sử dụng chùm ánh sáng. Vào những năm 1890, **wireless telegraph** (Marconi) đã thử nghiệm gửi dữ liệu bằng sóng vô tuyến (radio waves). Cũng trong những năm 1890, đã có các thí nghiệm với **millimeter waves** (sóng milimet) của Bose, và ngày nay, sóng milimet đang trở thành một lĩnh vực nghiên cứu sôi động trở lại.

Về mặt khái niệm, bạn có thể hình dung rằng truyền thông không dây bao gồm các hạt vô hình di chuyển dọc theo một liên kết tưởng tượng từ điểm A đến điểm B, nhưng thực tế thì không hoàn toàn chính xác như vậy. Thực tế, truyền thông không dây giống như những gợn sóng trên mặt hồ. Khi bạn truyền dữ liệu không dây, bạn tạo ra các gợn sóng lan tỏa ra ngoài và yếu dần theo khoảng cách. Nếu những người khác cũng đang truyền dữ liệu, các gợn sóng này có thể giao thoa cộng hưởng hoặc triệt tiêu lẫn nhau. Các gợn sóng cũng có thể phản xạ hoặc khúc xạ khi gặp các vật thể như thuyền trên hồ hoặc bờ hồ.

<img width="500px" src="/assets/wireless/8-001-wireless-intro.png">

Trong phần này, chúng ta sẽ xem xét bốn điểm khác biệt chính giữa truyền thông có dây và không dây. Các khác biệt này chủ yếu ảnh hưởng đến **Layer 1 (Physical)** và **Layer 2 (Link)**, với một vài ngoại lệ mà chúng ta sẽ tìm hiểu sau (đáng chú ý là việc phá vỡ **End-to-end Principle** (Nguyên tắc đầu-cuối) và triển khai cơ chế đảm bảo độ tin cậy ở Layer 2 để cải thiện hiệu năng).

**Khác biệt 1:** Kết nối không dây về bản chất là môi trường dùng chung. Kết nối có dây thì không.

**Khác biệt 2:** Tín hiệu không dây yếu dần khi khoảng cách tăng. Tín hiệu có dây thì không.

**Khác biệt 3:** Môi trường không dây có thể thay đổi nhanh chóng. Môi trường có dây thì không.

**Khác biệt 4:** Việc phát hiện va chạm gói tin (packet collisions) trong hệ thống không dây khó hơn nhiều.


## Khác biệt: Không dây là môi trường dùng chung (Shared Medium)

**Khác biệt 1:** Kết nối không dây về bản chất là môi trường dùng chung. Kết nối có dây thì không.

Các kết nối có dây mặc định là kết nối riêng (point-to-point). Trực quan mà nói, một sợi dây kết nối hai thiết bị. Việc tạo ra một **multi-point bus** (bus đa điểm), nơi một sợi dây được kết nối với nhiều thiết bị, đòi hỏi thêm công đoạn. Tín hiệu bên ngoài khó có thể gây nhiễu cho tín hiệu trên dây (ví dụ: chúng ta có thể bọc lớp chắn quanh dây). Trên dây, chúng ta sử dụng tín hiệu điện để truyền dữ liệu (ví dụ: điện áp cao biểu thị 1, điện áp thấp biểu thị 0).

Kết nối không dây có đặc tính ngược lại. Mặc định, kết nối không dây là môi trường dùng chung. Trực quan mà nói, nếu bạn truyền một tín hiệu, tín hiệu đó sẽ lan tỏa ra mọi hướng. Việc tạo ra một kết nối riêng point-to-point giữa hai máy chủ đòi hỏi thêm công đoạn. Khó có thể che chắn tín hiệu khỏi nhiễu bên ngoài. Thay vì tín hiệu điện, chúng ta mã hóa các bit bằng sóng vô tuyến (radio waves) để truyền dữ liệu.


## Mã hóa dữ liệu qua kết nối không dây (Encoding Data over Wireless Link)

Làm thế nào để chúng ta mã hóa dữ liệu vào sóng điện từ ở **Layer 1**? Chúng ta có thể lấy chuỗi 1 và 0 và vẽ nó thành dạng sóng, nhưng dạng sóng thu được thường có tần số thấp, và tín hiệu tần số thấp thì yếu và khó truyền.

<img width="500px" src="/assets/wireless/8-002-modulation1.png">

Thay vào đó, chúng ta phải sử dụng **modulation** (điều chế) để truyền dữ liệu. Chúng ta bắt đầu với **carrier signal** (tín hiệu sóng mang), vốn là một sóng có tần số cố định (ví dụ: sóng sin). Sóng này không mang thông tin, nhưng có tần số cao nên dễ truyền hơn. Sau đó, chúng ta chồng tín hiệu dữ liệu (còn gọi là **modulation signal** – tín hiệu điều chế) lên trên sóng mang. Dạng sóng thu được vừa có tần số cao (dễ truyền), vừa chứa dữ liệu cần gửi. Lưu ý rằng phía thu sẽ cần tách dạng sóng đã điều chế để khôi phục lại chuỗi 1 và 0.

Có nhiều chiến lược điều chế tín hiệu dữ liệu lên sóng mang. Trong **amplitude modulation (AM)** (điều chế biên độ), chúng ta thay đổi độ cao của sóng mang dựa trên tín hiệu đầu vào. Để truyền bit 1, làm sóng sin cao; để truyền bit 0, làm sóng sin thấp. Trong **frequency modulation (FM)** (điều chế tần số), chúng ta thay đổi tần số (độ rộng) của sóng mang dựa trên tín hiệu đầu vào. Để truyền bit 1, làm sóng sin hẹp (tần số cao hơn); để truyền bit 0, làm sóng sin rộng (tần số thấp hơn). Ngoài ra còn có các chiến lược điều chế phức tạp hơn, như **phase modulation** (điều chế pha), hoặc kết hợp giữa điều chế biên độ và điều chế pha.

<img width="900px" src="/assets/wireless/8-003-modulation2.png">


## Nhiễu và can nhiễu (Noise and Interference)

Vì kết nối không dây là môi trường dùng chung, chúng ta cần xử lý **noise** (nhiễu) và **interference** (can nhiễu), những yếu tố có thể làm hỏng tín hiệu nhận được. Nhiễu luôn tồn tại, ngay cả khi không có ai khác gần đó đang truyền dữ liệu. (Ví dụ: ngay cả khi không ai xung quanh bạn nói chuyện, vẫn có tiếng ồn môi trường từ thiên nhiên.) Nhiễu nền này được gọi là **noise floor** (mức nhiễu nền). Ngược lại, can nhiễu đề cập đến việc các bộ phát khác cố tình gửi tín hiệu gây nhiễu cho tín hiệu của chúng ta.

**SINR (Signal to Interference and Noise Ratio)** là một chỉ số dùng để đo chất lượng kết nối không dây tại phía thu. Đúng như tên gọi, SINR là công suất của tín hiệu chia cho tổng công suất của can nhiễu và nhiễu.

$$\text{SINR} = \frac{P_\text{signal}}{P_\text{interference} + P_\text{noise}}$$

SINR là một đại lượng không thứ nguyên, vì nó là tỷ số của hai giá trị. Nó cũng có thể được biểu diễn theo đơn vị **decibel (dB)**, là cách đo tỷ số theo thang logarit. Ở mức 0 dB, tỷ số là 1, và khi SINR tăng thêm 10 dB, tỷ số thực tế lớn hơn gấp 10 lần (ví dụ: tín hiệu mạnh hơn gấp 10 lần, hoặc nhiễu/can nhiễu yếu hơn gấp 10 lần).

<img width="400px" src="/assets/wireless/8-004-decibels.png">

$$\text{SINR}_\text{dB} = 10 \cdot \log_{10}\left(\frac{P_\text{signal}}{P_\text{interference} + P_\text{noise}}\right)$$

Phương trình này cho chúng ta biết rằng nếu có nhiều nhiễu hơn, chúng ta phải truyền tín hiệu với công suất lớn hơn. Ngoài ra, có thể áp dụng **coding gain** (lợi ích từ mã hóa – ví dụ: mã sửa lỗi), để ngay cả khi tín hiệu yếu và bị trộn lẫn với nhiễu và can nhiễu, chúng ta vẫn gửi tín hiệu với đủ dữ liệu dự phòng để phía thu có thể khôi phục lại tín hiệu.

**Dung lượng Shannon** (**Shannon capacity**) đưa ra giới hạn lý thuyết về lượng dữ liệu tối đa có thể truyền qua một kênh trong một đơn vị thời gian, với mức nhiễu (**noise**) và can nhiễu (**interference**) nhất định trên kênh đó. Công thức này áp dụng không chỉ cho các kết nối không dây (**wireless links**), mà còn cho các loại kết nối khác (ví dụ: kết nối có dây).

$$C = B \cdot \log_2(1 + \text{SINR})$$

Trong phương trình này, $$B$$ là **bandwidth** (băng thông) của kênh. $$\text{SINR}$$ là **signal-to-interference-and-noise ratio** (tỷ số tín hiệu trên nhiễu và can nhiễu). $$C$$ là giới hạn lý thuyết về lượng dữ liệu tối đa có thể truyền qua kênh trong một đơn vị thời gian, được đo bằng **bits per second** (bit trên giây). Lưu ý rằng trong phương trình này, băng thông được đo bằng hiệu giữa tần số cao nhất và tần số thấp nhất mà bộ thu có thể hiểu.

Phương trình này cho chúng ta biết rằng khi băng thông tăng, chúng ta có thể truyền nhiều dữ liệu hơn trong một đơn vị thời gian. Nó cũng cho thấy rằng khi SINR tăng (tín hiệu mạnh hơn hoặc ít nhiễu hơn), chúng ta có thể truyền nhiều dữ liệu hơn. Nếu chúng ta cần một kết nối với dung lượng mục tiêu cụ thể (ví dụ: 1 Mbps), chúng ta có thể thay các thông số vật lý của kết nối vào phương trình này để kiểm tra xem kết nối có đáp ứng được dung lượng mong muốn hay không.

Ví dụ, hãy xét hệ thống điện thoại cố định truyền thống (**plain old telephone system**). Hệ thống này có băng thông 3 kHz, nghĩa là điện thoại có thể xử lý các tần số từ 300 Hz đến 3300 Hz. Ngoài ra, hệ thống này có SINR xấp xỉ 20 dB, tương đương tỷ số 100 (0 dB = 1x, 10 dB = 10x, 20 dB = 100x, 30 dB = 1000x, v.v.). Thay các giá trị này vào phương trình, ta có:

$$C = 4000 \cdot \log_2(1 + 100) \approx 20000$$

Điều này cho thấy hệ thống điện thoại có thể truyền khoảng 20 kbps (**kilobits per second** – kilobit trên giây).

---

## Khác biệt: **Attenuation** (Suy hao tín hiệu)

Tín hiệu không dây (**wireless signals**) yếu đi đáng kể khi khoảng cách tăng. Ngược lại, tín hiệu có dây (**wired signals**) cũng yếu đi theo khoảng cách, nhưng mức độ nhỏ hơn nhiều. Trong các hệ thống không dây, thiết kế phải tính đến hiện tượng suy hao tín hiệu, trong khi ở hệ thống có dây, suy hao thường không phải là yếu tố thiết kế chính.

Điều này tạo ra một sự đánh đổi cơ bản khi thiết kế hệ thống không dây: chúng ta muốn tối đa hóa hiệu năng bằng cách làm cho kết nối chính xác, nhanh và có tầm xa; nhưng đồng thời muốn giảm thiểu việc sử dụng tài nguyên bằng cách tiết kiệm năng lượng (ví dụ: pin laptop) và sử dụng ít phổ tần (**frequency spectrum**) hơn (việc cấp phép phổ tần có thể tốn kém). Tuy nhiên, để có tín hiệu tốt hơn, cần nhiều công suất hơn hoặc băng thông tần số lớn hơn.

---

## **Free Space Model** (Mô hình không gian tự do)

Một cách đơn giản để mô hình hóa suy hao tín hiệu là **free-space model** (mô hình không gian tự do, còn gọi là **line-of-sight model** – mô hình đường thẳng tầm nhìn), trong đó giả định rằng bộ phát (**transmitter**) và bộ thu (**receiver**) tồn tại trong một môi trường hoàn toàn trống rỗng. Tín hiệu lan tỏa ra mọi hướng, không có vật cản (ngay cả bề mặt Trái Đất).

Trong mô hình này, công suất tín hiệu tỉ lệ nghịch với bình phương khoảng cách giữa bộ phát và bộ thu, theo **inverse-square law** (định luật nghịch đảo bình phương):

$$P_r \propto \frac{P_t}{d^2}$$

Trong phương trình này, $$P_r$$ là công suất tại bộ thu, $$P_t$$ là công suất tại bộ phát, và $$d$$ là khoảng cách giữa bộ phát và bộ thu. Nếu khoảng cách tăng gấp đôi, tín hiệu tại bộ thu sẽ yếu đi còn $$1/4$$. Nếu khoảng cách tăng gấp 10 lần, tín hiệu tại bộ thu sẽ yếu đi còn $$1/100$$.

<img width="200px" src="/assets/wireless/8-005-freespace1.png">

Trực quan mà nói, định luật nghịch đảo bình phương áp dụng ở đây vì tín hiệu lan tỏa ra mọi hướng. Tại một thời điểm, tín hiệu đã lan ra thành một hình cầu bao quanh bộ phát, và hình cầu này lớn dần khi tín hiệu lan xa hơn. Diện tích bề mặt của hình cầu bán kính $$r$$ là $$4\pi r^2$$, vì vậy khi tín hiệu lan ra, nó được phân bố trên một diện tích tăng theo bình phương khoảng cách. Ví dụ, khi khoảng cách tăng gấp đôi, diện tích bề mặt hình cầu tăng gấp 4 lần, do đó tín hiệu yếu đi còn $$1/4$$.

<img width="300px" src="/assets/wireless/8-006-freespace2.png">

Ngoài khoảng cách, chúng ta cũng cần xem xét loại **antenna** (ăng-ten) được sử dụng ở bộ phát và bộ thu. Điều này dẫn đến **Friis equation** (phương trình Friis) để đo cường độ tín hiệu theo khoảng cách:

$$\begin{align*}
    P_r &= P_t \cdot G_t \cdot G_r \cdot \left(\frac{\lambda^2}{4\pi}\right) \left(\frac{1}{4\pi d^2}\right) \\
    &= P_t \cdot G_t \cdot G_r \cdot \left(\frac{\lambda}{4\pi d}\right)^2 \\
\end{align*}$$

Trong phương trình này, $$P_r$$ là công suất tại bộ thu, $$P_t$$ là công suất tại bộ phát. $$G_t$$ là **gain** (độ lợi) của bộ phát, $$G_r$$ là độ lợi của bộ thu. $$\lambda$$ là **wavelength** (bước sóng), được dùng để biểu diễn diện tích hiệu dụng của ăng-ten. $$d$$ là khoảng cách giữa các ăng-ten.

Ý nghĩa của phương trình: để tính công suất tín hiệu tại bộ thu, bắt đầu từ công suất tại bộ phát $$P_t$$, nhân với độ lợi của hai ăng-ten $$G_t$$ và $$G_r$$. Độ lợi cao hơn nghĩa là ăng-ten tốt hơn trong việc phát hoặc thu tín hiệu.

Như đã thấy, khoảng cách ảnh hưởng đến cường độ tín hiệu theo định luật nghịch đảo bình phương, giải thích cho thành phần $$\frac{1}{4\pi d^2}$$.

Thành phần $$\frac{\lambda^2}{4\pi}$$ liên quan đến **aperture** (diện tích hiệu dụng) của ăng-ten thu. Trực quan, nếu bạn chiếu ánh sáng vào một tờ giấy, ánh sáng sẽ chiếu vào tờ giấy đó; nếu tờ giấy lớn hơn, nhiều ánh sáng hơn sẽ chiếu vào. Diện tích hiệu dụng của ăng-ten có thể tính bằng $$\frac{\lambda^2}{4\pi}$$. Lưu ý rằng $$(4\pi)^2$$ trong phương trình xuất phát từ hai yếu tố $$4\pi$$: một từ định luật nghịch đảo bình phương và một từ công thức diện tích hiệu dụng.

Chúng ta cũng có thể viết lại phương trình Friis bằng cách chia cả hai vế cho $$P_t$$:

$$\frac{P_r}{P_t} = G_t \cdot G_r \cdot \left(\frac{\lambda}{4\pi d}\right)^2$$

Phương trình này cho thấy tỷ lệ công suất tín hiệu tại bộ thu so với bộ phát (ví dụ: bằng một nửa, hoặc $$1/100$$ so với công suất tại bộ phát) phụ thuộc vào độ lợi của ăng-ten, nghịch đảo bình phương khoảng cách, và diện tích hiệu dụng của ăng-ten.

Một cách khác để viết phương trình Friis là lấy logarit hai vế, cho phép biểu diễn công suất và độ lợi theo đơn vị **decibel (dB)**:

$$P_r^\text{dB} = P_t^\text{dB} + G_t^\text{dB} + G_r^\text{dB} + 20 \log_{10} \left(\frac{\lambda}{4\pi d}\right)$$

Mô hình không gian trống là một mô hình lý thuyết hữu ích để đo lường cường độ tín hiệu lý tưởng tại bộ thu, tuy nhiên trên thực tế, các chướng ngại vật vật lý (ví dụ: bề mặt Trái Đất) ngăn cản chúng ta đạt được giá trị lý tưởng này.

Dưới đây là bản dịch tiếng Việt theo đúng quy tắc bạn yêu cầu, giữ nguyên thuật ngữ chuyên ngành kèm giải thích lần đầu xuất hiện và duy trì định dạng Markdown:

---

## **Link Budget** (Ngân sách liên kết)

Nếu tín hiệu yếu dần theo khoảng cách, làm thế nào để biết một liên kết có thực sự hoạt động hay không? Nói cách khác, làm thế nào để biết bộ thu (**receiver**) có thể phát hiện được một tín hiệu đủ rõ ràng để giải mã hay không?

Để đo lường khả năng hoạt động của một liên kết, chúng ta có thể tính **link budget** (ngân sách liên kết), bao gồm tất cả các **gains** (độ lợi) và **losses** (suy hao) trên đường truyền.

$$P_r^\text{dB} = P_t^\text{dB} + \sum \text{gains} - \sum \text{losses}$$

Trong phương trình này, $$P_r$$ là công suất tín hiệu tại bộ thu, và $$P_t$$ là công suất tín hiệu tại bộ phát (**sender**). Tất cả các độ lợi (ví dụ: độ lợi ăng-ten cao hơn) sẽ cộng vào ngân sách liên kết, và tất cả các suy hao (ví dụ: **path loss** – suy hao đường truyền do khoảng cách xa) sẽ trừ khỏi ngân sách liên kết.

Cộng tất cả độ lợi và trừ tất cả suy hao sẽ cho chúng ta biết cường độ tín hiệu tại bộ thu. Chúng ta có thể so sánh giá trị này với **receiver sensitivity** (độ nhạy của bộ thu) – tức là mức tín hiệu tối thiểu mà bộ thu cần để trích xuất thông tin hữu ích. So sánh này cho ra **link budget**. Nếu ngân sách tổng thể dương, liên kết khả thi và có thể hoạt động tốt. Nếu ngân sách âm, liên kết không khả thi.

Lưu ý rằng **link budget** được tính theo đơn vị **decibel (dB)**, là thang đo logarit. Điều này cho phép chúng ta sử dụng phép cộng và trừ thay vì nhân và chia. Ví dụ: độ lợi công suất gấp 1000 lần được biểu diễn bằng cách cộng 30 dB, và suy hao xuống còn 1% công suất được biểu diễn bằng cách trừ 20 dB.

<img width="900px" src="/assets/wireless/8-007-link-budget.png">

**Ví dụ:** Công suất tín hiệu tại bộ phát là 10 dB. Tín hiệu đi qua một đoạn cáp, một **lightning arrestor** (thiết bị chống sét – bạn không cần biết chi tiết), và một đoạn cáp khác, lần lượt mất 0,44 dB, 0,1 dB và 2,21 dB. Sau đó, tín hiệu được phát qua ăng-ten, tăng thêm 25 dB. Tín hiệu truyền qua 10 km không gian, mất 120 dB. Tín hiệu được thu bởi ăng-ten, tăng thêm 25 dB. Sau đó, tín hiệu đi qua thêm các đoạn cáp, mất 0,44 dB, 0,1 dB và 2,21 dB, trước khi đến bộ thu. Cộng tất cả độ lợi và trừ tất cả suy hao, ta tính được công suất tín hiệu tại bộ thu là -65,5 dB.

So sánh với độ nhạy bộ thu là -80 dB: bộ thu có thể nhận bất kỳ tín hiệu nào mạnh hơn -80 dB. Vì -65,5 dB > -80 dB, **link budget** là dương, và liên kết sẽ hoạt động.

**Link margin** (biên độ liên kết) là hiệu giữa công suất tín hiệu tại bộ thu và độ nhạy của bộ thu. Nếu nhận được tín hiệu 30 dB và độ nhạy cho phép phát hiện tín hiệu trên 10 dB, thì link margin là 20 dB. Trong ví dụ trên, link margin là 14,5 dB.

**Link margin** cho biết chất lượng của liên kết. Nếu link margin âm, liên kết sẽ không hoạt động và tín hiệu sẽ không được nhận. Link margin càng cao càng tốt, vì tín hiệu sẽ ổn định và ít bị ảnh hưởng bởi nhiễu hoặc các vấn đề khác.

---

## Khác biệt: **Environments Change** (Môi trường thay đổi)

Môi trường không dây (**wireless environment**) có thể thay đổi nhanh chóng. Các thiết bị có thể di chuyển. Môi trường có thể thay đổi (ví dụ: một vật cản xuất hiện giữa các thiết bị). Các kết nối khác có thể bắt đầu gây nhiễu cho liên lạc của chúng ta.

Trong **free-space model** (mô hình không gian tự do) đã đề cập trước đó, khoảng cách $$d$$ giữa các thiết bị được coi là hằng số. Nhưng nếu thiết bị di chuyển thì sao? Chúng ta cũng giả định không có vật cản và không có tín hiệu gây nhiễu. Vậy mô hình sẽ thay đổi thế nào khi có các yếu tố này?

Trong **free-space model**, giả sử ăng-ten không đổi (cùng độ lợi, cùng diện tích hiệu dụng), chúng ta có đồ thị mượt mà, trong đó cường độ tín hiệu giảm dần khi khoảng cách tăng. Khi tính đến môi trường thay đổi, đồ thị khoảng cách – cường độ tín hiệu trở nên dao động mạnh hơn.

<img width="900px" src="/assets/wireless/8-008-obstacle1.png">

Đồ thị này thực chất là tổng của ba đồ thị nhỏ hơn, mỗi đồ thị thể hiện một đặc tính môi trường ảnh hưởng đến cường độ tín hiệu theo khoảng cách. Một số đặc tính thay đổi chậm khi khoảng cách tăng, trong khi một số thay đổi nhanh và thất thường.

<img width="900px" src="/assets/wireless/8-009-obstacle2.png">

1. **Free-space path loss** – suy hao đường truyền trong không gian tự do: tín hiệu giảm chậm và đều theo khoảng cách, tuân theo **inverse-square law** (định luật nghịch đảo bình phương).
2. **Shadowing** – hiện tượng bóng che: xảy ra khi vật cản vật lý nằm giữa bộ phát và bộ thu chặn tín hiệu. Tín hiệu phải khúc xạ hoặc phản xạ để đi vòng qua vật cản, khiến tín hiệu đến bộ thu yếu hơn. Khi di chuyển, tín hiệu có thể yếu đi hoặc mạnh lên tùy vị trí vật cản.
3. **Multipath fading** – hiện tượng suy giảm đa đường: xảy ra khi sóng phản xạ và khúc xạ trên các vật cản, tạo ra các bản sao tín hiệu đến bộ thu với độ trễ khác nhau. Nếu các tín hiệu này lệch pha, chúng có thể gây giao thoa và làm suy yếu tín hiệu.

**Multipath fading** có thể gây ra biến đổi rất nhỏ nhưng rõ rệt trong cường độ tín hiệu – chỉ cần thay đổi khoảng cách một chút cũng có thể làm tín hiệu mạnh hơn hoặc yếu đi.

Khi xét cả ba yếu tố này cùng lúc, đồ thị tổng thể sẽ thể hiện sự biến thiên phức tạp của tín hiệu theo khoảng cách. Nếu thiết bị đứng yên, tín hiệu sẽ ở một điểm cố định trên đồ thị; nếu di chuyển, tín hiệu sẽ thay đổi theo đường cong này. Khi môi trường thay đổi (vật cản xuất hiện hoặc biến mất), bản thân đồ thị cũng thay đổi.

---

## **Approximating Path Loss** (Xấp xỉ suy hao đường truyền)

Việc xấp xỉ **path loss** (suy hao đường truyền) từ **free-space loss**, **shadowing** và **multipath fading** là rất khó, đặc biệt khi có vật cản khiến tín hiệu đi theo nhiều đường khác nhau và gây giao thoa lệch pha tại bộ thu.

Một mô hình đơn giản hơn để xấp xỉ suy hao là **two-ray model** (mô hình hai tia). Trong mô hình này, tín hiệu truyền theo hai đường: một đường thẳng **line-of-sight** (tầm nhìn thẳng) từ bộ phát đến bộ thu, và một đường phản xạ từ mặt đất (**ground-bounce**) đến bộ thu. Đây vẫn là một tín hiệu phát ra từ bộ phát, nhưng một phần sóng đến trực tiếp, phần khác phản xạ từ mặt đất.

<img width="900px" src="/assets/wireless/8-010-obstacle3.png">

Nếu khoảng cách đủ xa, hai sóng từ hai đường sẽ lệch pha 180°, gây giao thoa triệt tiêu (**destructive interference**) và làm tín hiệu tại bộ thu yếu đi đáng kể. Khi đó, cường độ tín hiệu không còn tỉ lệ với $$1/d^2$$ mà tỉ lệ với $$1/d^4$$ – tức là suy giảm nhanh hơn nhiều khi khoảng cách tăng.

Trong **free-space model**, không tính đến vật cản (kể cả bề mặt Trái Đất), nên tín hiệu tỉ lệ với $$1/d^2$$. Trong **two-ray model**, tính đến bề mặt Trái Đất khiến tín hiệu tỉ lệ với $$1/d^4$$.

<img width="900px" src="/assets/wireless/8-011-obstacle4.png">

Nếu tồn tại các vật cản khác ngoài bề mặt Trái Đất, **two-ray model** (mô hình hai tia) sẽ không tính đến chúng. Trong các môi trường phức tạp hơn, chúng ta có thể xây dựng **general ray tracing models** (mô hình dò tia tổng quát), mô phỏng việc tín hiệu bị phản xạ (**reflected**), tán xạ (**scattered**) và nhiễu xạ (**diffracted**). Các mô hình này yêu cầu thông tin chi tiết về môi trường (ví dụ: vị trí các vật cản) và có thể được xây dựng bằng mô phỏng máy tính. Trong các mô hình này, các phiên bản tín hiệu bị phản xạ thường chiếm ưu thế so với tín hiệu truyền thẳng không bị cản (**unobstructed line-of-sight**).

<img width="900px" src="/assets/wireless/8-012-obstacle5.png">

Từ các mô hình này, chúng ta có thể rút ra một mô hình suy hao đường truyền (**path loss model**) đơn giản hơn, liên hệ giữa khoảng cách và cường độ tín hiệu:

$$P_r = P_t K d^\gamma$$

Trong phương trình này, như trước, $$P_r$$ và $$P_t$$ lần lượt là công suất tín hiệu tại bộ thu (**receiver signal power**) và công suất tín hiệu tại bộ phát (**transmitter signal power**), $$d$$ là khoảng cách.

$$K$$ và $$\gamma$$ là các hằng số được xác định thực nghiệm, dựa trên môi trường và mô hình. Ví dụ, nếu có nhiều vật cản đặt ở vị trí bất lợi, $$K$$ có thể rất nhỏ, khiến tín hiệu tại bộ thu yếu.

Trong thực tế, $$\gamma$$ nằm trong khoảng từ 2 đến 8. Trong trường hợp tốt nhất, cường độ tín hiệu tỉ lệ với $$1/d^2$$, tương tự **free-space model** (mô hình không gian tự do). Trong trường hợp xấu nhất, cường độ tín hiệu tỉ lệ với $$1/d^8$$, và tín hiệu yếu đi nhanh hơn nhiều khi khoảng cách tăng.

---

## Khác biệt: **Detecting Collisions** (Phát hiện va chạm)

Trong kết nối có dây (**wired**), việc phát hiện va chạm (**collision**) thường dễ dàng. Trên một kết nối **point-to-point** (điểm-điểm), va chạm có thể không xảy ra. Chúng ta thường có thể phát hiện va chạm chỉ bằng cách cảm nhận tín hiệu trên dây. Có thể tồn tại vấn đề về **propagation delay** (độ trễ lan truyền), nhưng về cơ bản, chỉ có một tín hiệu trên dây cần được cảm nhận.

Ngược lại, trong kết nối không dây (**wireless**), việc phát hiện va chạm khó hơn nhiều, vì va chạm còn phụ thuộc vào yếu tố không gian. Sóng có thể va chạm ở một vị trí nhưng không va chạm ở vị trí khác.

<img width="500px" src="/assets/wireless/8-013-collision1.png">

Thiết kế cơ chế phát hiện và tránh va chạm (**collision detection** và **collision avoidance**) trong hệ thống không dây phức tạp hơn, nhưng vẫn cần thiết để nhiều thiết bị có thể truyền trên cùng một môi trường dùng chung (**shared medium**). Có nhiều phương pháp **multiple access** (truy nhập đa điểm), bao gồm phân bổ tần số cố định (**fixed frequency allocation**) hoặc điều phối thời gian truyền. Phương pháp nào hiệu quả nhất phụ thuộc vào môi trường. Ví dụ, ở nơi hẻo lánh, có thể chấp nhận để va chạm xảy ra và xử lý sau. Trong phần này, chúng ta tập trung vào phương pháp **CSMA (Carrier Sense Multiple Access)** – cảm nhận sóng mang và không truyền nếu phát hiện có thiết bị khác đang truyền.

Để đơn giản, trong phần này, chúng ta bỏ qua vật cản, nghĩa là tín hiệu lan tỏa ra mọi hướng. Giả sử tín hiệu lan truyền đến một khoảng cách nhất định với cường độ tối đa, và không thể phát hiện được ngoài khoảng cách đó. Ngoài ra, trong các ví dụ minh họa, giả sử tất cả thiết bị được bố trí trên một đường thẳng, nên chỉ cần xét tín hiệu lan sang trái và phải. Trong thực tế, tín hiệu lan tỏa trong không gian ba chiều.

---

## Vấn đề với **CSMA**

Để kiểm tra xem có thiết bị khác đang truyền hay không, bộ thu phát (**radio**) sẽ cố gắng phát hiện năng lượng vượt quá một ngưỡng nhất định. Nếu phát hiện, kết luận rằng có thiết bị khác đang truyền.

Chiến lược này hoạt động tốt nếu hai cặp thiết bị ở xa nhau.

<img width="800px" src="/assets/wireless/8-014-collision2.png">

Ví dụ: A và B muốn liên lạc, C và D cũng muốn liên lạc. A không phát hiện tín hiệu nào và bắt đầu truyền cho B. Lưu ý rằng tín hiệu của A lan tỏa ra mọi hướng, không chỉ về phía B. Sau đó, C cũng không phát hiện tín hiệu (vì nằm ngoài phạm vi của A), nên bắt đầu truyền cho D.

Chiến lược này cũng hoạt động tốt nếu hai cặp thiết bị ở trong phạm vi của nhau.

<img width="600px" src="/assets/wireless/8-015-collision3.png">

Ví dụ: A và B muốn liên lạc, C và D cũng muốn liên lạc. A không phát hiện tín hiệu và bắt đầu truyền cho B. Sau đó, C phát hiện tín hiệu (vì A đang truyền và C nằm trong phạm vi), nên C sẽ chờ đến khi A kết thúc mới truyền cho D.

Tuy nhiên, đôi khi chiến lược này gây ra vấn đề.

<img width="700px" src="/assets/wireless/8-016-collision4.png">

Giả sử A và C đều muốn truyền cho B. A không phát hiện tín hiệu và bắt đầu truyền cho B. Sau đó, C cũng không phát hiện tín hiệu (vì nằm ngoài phạm vi của A), nên cũng bắt đầu truyền cho B. Kết quả là xảy ra va chạm tại B.

Trường hợp này gọi là **hidden terminal problem** (vấn đề nút ẩn). Hai bộ phát (A và C) nằm ngoài phạm vi của nhau, nên không thể phát hiện rằng đang có truyền dữ liệu.

---

Dưới đây là một trường hợp khác mà **CSMA (Carrier Sense Multiple Access)** gặp vấn đề:

<img width="600px" src="/assets/wireless/8-017-collision5.png">

Trong trường hợp này, giả sử B muốn truyền dữ liệu cho A, và C muốn truyền dữ liệu cho D. Đầu tiên, B không phát hiện tín hiệu nào và bắt đầu truyền cho A. Hãy nhớ rằng tín hiệu của B lan tỏa ra mọi hướng, bao gồm cả đến C. Lúc này, C muốn truyền cho D nhưng phát hiện tín hiệu của B nên giữ im lặng.

Nếu quan sát kỹ, B và C thực ra có thể truyền đồng thời. Đúng là sẽ có va chạm (**collision**) ở vùng giữa B và C, nhưng các bộ thu (**receiver**) là A và D sẽ không phát hiện bất kỳ va chạm nào.

Trường hợp này được gọi là **exposed terminal problem** (vấn đề nút lộ). Trong tình huống này, hai phiên truyền hoàn toàn có thể diễn ra đồng thời, nhưng một phiên bị ngăn lại vì C phát hiện nhầm là có va chạm.

---

## **MACA for Collision Avoidance** (MACA để tránh va chạm)

Thay vì sử dụng CSMA, **MACA (Multiple Access with Collision Avoidance)** là một phương pháp truy nhập đa điểm (**multiple access**) giúp giải quyết **hidden terminal problem** (vấn đề nút ẩn).

Vấn đề chính của CSMA là bộ phát (**sender**) phát hiện va chạm ở phía phát, trong khi vấn đề thực sự là va chạm xảy ra ở phía thu (**receiver**). Để giải quyết, MACA cho phép bộ thu thông báo xem nó có phát hiện va chạm hay không.

Giả sử A muốn gửi dữ liệu cho B. Một phiên truyền dữ liệu thành công gồm 3 bước:

<img width="900px" src="/assets/wireless/8-018-maca1.png">

1. A gửi một gói **RTS (Request To Send)** kèm độ dài dữ liệu. Đây là cách A nói: “Tôi muốn gửi k bit cho B.”
2. B gửi lại một gói **CTS (Clear To Send)** kèm độ dài dữ liệu. Điều này báo cho A rằng có thể gửi dữ liệu an toàn và xác nhận rằng không có va chạm ở phía thu. Gói CTS cũng cảnh báo tất cả các thiết bị trong phạm vi của B: “Tôi là B, tôi sắp nhận k bit, vui lòng không truyền trong thời gian này.”
3. A truyền dữ liệu và B nhận dữ liệu. Cảnh báo CTS đảm bảo tất cả các thiết bị khác trong phạm vi của bộ thu giữ im lặng trong thời gian này.

Giao thức này giải quyết được **hidden terminal problem**. Hãy nhớ rằng, trong vấn đề nút ẩn, A và C đều cảm nhận kênh trống và bắt đầu truyền, gây va chạm tại B. Với giao thức này, nếu A gửi RTS, B sẽ gửi CTS, cảnh báo tất cả các thiết bị trong phạm vi của B (bao gồm C) giữ im lặng.

<img width="700px" src="/assets/wireless/8-019-maca2.png">

Nếu bạn nghe thấy một gói RTS, điều đó có nghĩa là bạn nằm trong phạm vi của bộ phát. Bộ phát sắp lắng nghe CTS. Do đó, bạn cần giữ im lặng và chờ một **time slot** (khoảng thời gian) đủ lâu để không làm nhiễu CTS tại bộ phát bằng dữ liệu của bạn. Nói cách khác, bạn cần giữ im lặng để bộ phát nhận được CTS.

Sau khi RTS được gửi, nếu bạn nghe thấy CTS, điều đó có nghĩa là bạn cũng nằm trong phạm vi của bộ thu, vì vậy bạn cũng phải giữ im lặng trong suốt quá trình truyền dữ liệu. Nếu bạn không nghe thấy CTS, điều đó có nghĩa là bạn nằm ngoài phạm vi của bộ thu và có thể tự do truyền dữ liệu.

Với một số giả định nhất định, giao thức này cũng giải quyết được **exposed terminal problem**. Hãy nhớ rằng, trong vấn đề nút lộ, B đang gửi cho A và C đang gửi cho D. Với CSMA, C phát hiện tín hiệu của B và giữ im lặng, mặc dù thực tế có thể truyền an toàn. Với giao thức này, nếu B gửi RTS, C sẽ trì hoãn một time slot (để tránh làm nhiễu CTS tại B). Sau đó, vì C không nghe thấy CTS, điều này có nghĩa là C nằm ngoài phạm vi của bộ thu (A), nên C có thể bắt đầu truyền cho D một cách an toàn.

<img width="900px" src="/assets/wireless/8-020-maca3.png">

Giả định để điều này hoạt động là C phải nghe được CTS từ D. Hãy nhớ rằng, ngay cả khi C là bộ phát, nó phải nhận được CTS trước khi bắt đầu truyền. Tuy nhiên, C thực tế cũng đang nghe dữ liệu từ B, nên có thể không nghe được CTS để bắt đầu truyền. Vấn đề chính ở đây là: Trong CSMA, bộ phát chỉ truyền. Nhưng trong MACA, bộ phát phải nhận được CTS trước khi truyền, và CTS này có thể bị nhiễu trong trường hợp **exposed terminal**.

<img width="900px" src="/assets/wireless/8-021-maca4.png">

Nếu chúng ta gửi RTS nhưng không nghe thấy CTS tương ứng, điều đó có nghĩa là chúng ta **không được phép truyền**. Có thể đang có va chạm ở phía thu, ví dụ: bộ thu đang nhận dữ liệu hoặc nhận hai yêu cầu cùng lúc. Nếu điều này xảy ra, chúng ta áp dụng **binary exponential backoff** (cơ chế lùi thời gian theo cấp số nhân nhị phân, tương tự CSMA/CD) và chờ lâu gấp đôi trước khi gửi lại RTS.

Trong MACA, mỗi thiết bị duy trì một giá trị **CW (Contention Window)**, cho biết sau một va chạm cần chờ bao lâu trước khi gửi lại yêu cầu. Nếu phát hiện va chạm (không nhận được CTS), thiết bị chọn ngẫu nhiên một số trong khoảng từ 0 đến CW và chờ thời gian tương ứng trước khi gửi lại. Giá trị tối thiểu là 2 time slots và tối đa là 64 time slots, trong đó một time slot là thời gian cần để truyền một gói RTS. Khi RTS/CTS thành công, CW được đặt lại về giá trị tối thiểu là 2. Khi RTS thất bại (không có CTS), CW được nhân đôi, nhưng không vượt quá giá trị tối đa 64.


## Tính năng MACAW: **ACK** (Để đảm bảo độ tin cậy)

**MACAW (Multiple Access Collision Avoidance for Wireless)** mang đến một số cải tiến so với giao thức **MACA**.

Cải tiến đầu tiên là bổ sung **acknowledgement** (gói xác nhận – ACK) để đảm bảo độ tin cậy. Như trước đây, bộ phát (**sender**) gửi một gói **RTS (Request To Send)**, bộ thu (**receiver**) gửi một gói **CTS (Clear To Send)**, và bộ phát truyền dữ liệu. Giờ đây, chúng ta thêm một bước nữa ở cuối, trong đó bộ thu gửi một gói ACK.

<img width="300px" src="/assets/wireless/8-022-macaw-acks.png">

Nếu dữ liệu bị mất, sẽ không có ACK, và bộ phát sẽ phải thử lại, bắt đầu lại với một RTS mới. Nếu dữ liệu được gửi chính xác nhưng ACK bị mất, bộ phát sẽ thử lại với một RTS mới, nhưng bộ thu có thể trả lời ngay bằng ACK thay vì CTS.

Tại sao chúng ta thêm ACK? Hãy nhớ rằng **End-to-end Principle** (Nguyên tắc đầu-cuối) cho rằng độ tin cậy phải được triển khai tại các máy đầu cuối để đảm bảo tính đúng đắn. Tuy nhiên, trong trường hợp này, chúng ta triển khai độ tin cậy ngay trong mạng, trên một liên kết đơn lẻ, chỉ nhằm cải thiện hiệu năng. Nếu không triển khai độ tin cậy ở tầng liên kết, **TCP** vẫn đảm bảo tính đúng đắn, nhưng một gói tin bị mất sẽ khiến TCP giảm tốc độ đáng kể (nhớ rằng cửa sổ tắc nghẽn – **congestion window** – sẽ bị giảm một nửa). Ngược lại, bằng cách triển khai độ tin cậy ở tầng liên kết, chúng ta có thể khôi phục sau mất gói hiệu quả hơn.

---

## Tính năng MACAW: **Better Backoff** (Để đảm bảo công bằng)

Giao thức MACA thiếu công bằng khi hai nút va chạm cùng muốn gửi dữ liệu. Cụ thể, “người thắng” thường tiếp tục thắng, còn “người thua” tiếp tục thua.

Ví dụ về sự thiếu công bằng: Giả sử A và B đều có giá trị **CW (Contention Window)** là 2, và cả hai đồng thời cố gắng đặt chỗ kênh truyền. Giả sử A thắng, B thua. Khi đó, CW của A vẫn là 2, còn CW của B tăng gấp đôi thành 4. Điều này có nghĩa là A có khả năng đặt chỗ kênh sớm hơn và nhiều khả năng lại thắng. Khi B thử lại, A đã chiếm kênh, và CW của B lại tăng gấp đôi thành 8. Mẫu này tiếp diễn: A liên tục chiếm kênh nhanh chóng, còn B liên tục thất bại và phải chờ lâu hơn trước khi thử lại (và lại thất bại).

<img width="800px" src="/assets/wireless/8-023-maca-unfair.png">

Để giải quyết vấn đề này, thay vì mỗi thiết bị có CW riêng, tất cả sẽ dùng chung một CW. Phần tiêu đề gói tin (**packet header**) giờ đây có một trường chứa giá trị CW, và nếu bạn nhận được một gói tin, bạn sẽ đặt CW của mình bằng giá trị trong gói đó. Vì tất cả cùng có CW như nhau, cơ chế thử lại sẽ không thiên vị thiết bị nào. Mỗi thiết bị chọn ngẫu nhiên một giá trị từ 0 đến CW và chờ tương ứng. (Lưu ý: Chúng ta đang đơn giản hóa một chút, điều này đúng nếu tất cả thiết bị đều trong phạm vi của nhau.)

MACAW cũng thay đổi quy tắc cập nhật CW để “mềm” hơn. Như trước, giá trị tối thiểu là 2 và tối đa là 64. Khi RTS thất bại (không nhận được CTS), CW được nhân với 1,5 (thay vì gấp đôi), và vẫn giới hạn không vượt quá 64. Khi truyền thành công một chuỗi RTS/CTS/DATA/ACK, CW giảm đi 1 (thay vì đặt lại về 2). Lưu ý rằng khi RTS/CTS thành công nhưng ACK thất bại, CW không thay đổi. Cách tiếp cận này đôi khi được gọi là **Multiplicative Increase, Linear Decrease (MILD)**.

---

## Tính năng MACAW: **DS** (Để xử lý Exposed Terminals)

Hãy nhớ lại ví dụ **exposed terminal** (nút lộ) trước đó, khi B muốn liên lạc với A. B gửi RTS, A gửi CTS, và B bắt đầu truyền dữ liệu. Lúc này, C không nghe thấy CTS, nghĩa là C nằm ngoài phạm vi của bộ thu và có thể truyền dữ liệu an toàn. Tuy nhiên, để truyền, C phải nghe được CTS. Điều này có thể không xảy ra, vì C cũng đang nghe dữ liệu từ B, và có thể xảy ra va chạm giữa dữ liệu của B và CTS từ D.

MACAW kết luận rằng trong trường hợp **exposed terminal**, các cặp B–A và C–D thực tế không thể truyền dữ liệu đồng thời. Nói cách khác, cả MACAW lẫn CSMA đều không giải quyết được vấn đề nút lộ.

Điều này có nghĩa là nếu chúng ta nằm trong phạm vi của bộ phát khác, chúng ta không thể truyền dữ liệu (ngay cả khi không nằm trong phạm vi của bộ thu kia). Nguyên nhân là vì chúng ta sẽ nghe dữ liệu từ bộ phát kia, và do đó không thể nghe được CTS cần thiết để bắt đầu truyền.

Để giải quyết vấn đề này, MACAW thêm một gói **DS (Data Sending)** trước khi truyền dữ liệu. Đây là cách bộ phát cảnh báo mọi thiết bị: “Tôi sắp gửi k bit dữ liệu, vui lòng giữ im lặng trong thời gian này.”

<img width="900px" src="/assets/wireless/8-024-ds1.png">

Giao thức giờ đây có 5 bước:

1. Bộ phát gửi RTS, yêu cầu truyền k bit dữ liệu.
2. Bộ thu gửi CTS, thông báo cho mọi thiết bị trong phạm vi: Giữ im lặng, tôi đang nhận k bit dữ liệu.
3. Bộ phát gửi DS, thông báo cho mọi thiết bị trong phạm vi: Giữ im lặng, tôi đang gửi k bit dữ liệu. (Các thiết bị khác không thể gửi dữ liệu, vì dữ liệu của tôi sẽ làm nhiễu CTS mà bạn cần nhận cho phiên truyền của mình.)
4. Bộ phát truyền dữ liệu.
5. Bộ thu gửi ACK.

Lưu ý rằng RTS và DS không trùng lặp chức năng. RTS là yêu cầu có thể bị từ chối (ví dụ: không nhận được CTS). DS xác nhận rằng yêu cầu đã được chấp thuận và buộc mọi thiết bị trong phạm vi của bộ phát phải giữ im lặng.

## Tính năng MACAW: **DS** (Đồng bộ hóa – For Synchronization)

**DS** có một mục đích quan trọng thứ hai. Hãy xem lại ví dụ **exposed terminal** (nút lộ) trước đó, nhớ rằng **MACAW** chấp nhận “thất bại” và buộc hai phiên truyền phải diễn ra tách biệt.

Giả sử không có gói DS. Khi đó, như trước, B gửi một gói **RTS (Request To Send)**, A gửi một gói **CTS (Clear To Send)**, và B bắt đầu truyền dữ liệu. C nghe thấy RTS và trì hoãn một **time slot** (khoảng thời gian) để tránh làm gián đoạn B. Tuy nhiên, C không nghe thấy CTS. Lúc này, C sẽ gửi một RTS vô ích và sẽ không bao giờ nghe được CTS (vì CTS bị “chìm” trong dữ liệu từ B). C sẽ tiếp tục thử lại và gửi các yêu cầu RTS vô ích, nhưng không hề biết khi nào B sẽ ngừng truyền dữ liệu.

Ngược lại, B biết chính xác khi nào nó sẽ ngừng truyền dữ liệu. Điều này mang lại cho B lợi thế lớn trong vòng tranh chấp (**contention**) tiếp theo. Khi B truyền xong, nó có thể ngay lập tức gửi yêu cầu mới và nhiều khả năng sẽ thắng, tiếp tục giữ quyền truyền dữ liệu. Trong khi đó, C không biết khi nào B sẽ ngừng, nên phải đoán ngẫu nhiên thời điểm gửi yêu cầu mới. Khả năng cao là C sẽ đoán sai và gửi yêu cầu khi B vẫn đang truyền, dẫn đến thất bại và yêu cầu không được chấp nhận (va chạm).

<img width="900px" src="/assets/wireless/8-025-ds2.png">

Sự thiếu đồng bộ này dẫn đến mất công bằng. Nếu tôi thắng, tôi có khả năng sẽ thắng tiếp, vì tôi biết chính xác khi nào vòng tranh chấp tiếp theo diễn ra (ngay khi tôi truyền xong). Nếu bạn thua, bạn có khả năng sẽ tiếp tục thua, vì bạn không biết khi nào vòng tranh chấp tiếp theo diễn ra (bạn không biết khi nào tôi truyền xong). Thời gian tranh chấp thường rất ngắn, vì phần lớn thời gian được dùng để truyền dữ liệu. Tôi biết chính xác thời điểm đó, còn bạn thì không, nên tôi sẽ liên tục thắng.

Gói DS giải quyết vấn đề này, vì nó cho phép bộ phát thông báo cho mọi người khi nào vòng tranh chấp tiếp theo sẽ diễn ra. Giờ đây, B sử dụng gói DS để thông báo cho mọi người: “Tôi bắt đầu gửi k bit dữ liệu.” Nhờ đó, C không chỉ biết rằng mình không nên gửi các yêu cầu RTS vô ích, mà còn biết khi nào B sẽ truyền xong. Điều này giúp C có cơ hội công bằng hơn để thắng trong vòng tranh chấp tiếp theo.

<img width="900px" src="/assets/wireless/8-026-ds3.png">

---

## Tính năng MACAW: **RRTS** (Đồng bộ hóa – For Synchronization)

Có một trường hợp khác mà đồng bộ hóa là yếu tố then chốt để đảm bảo công bằng. Giả sử A muốn gửi dữ liệu cho B, và D muốn gửi dữ liệu cho C.

A truyền cho B (A gửi RTS, B gửi CTS, A gửi DS và truyền dữ liệu). C nghe thấy CTS và phải giữ im lặng trong khi dữ liệu được truyền. Lúc này, D hoàn toàn “mù thông tin” và thất thế. D sẽ gửi RTS, nhưng sẽ không nghe thấy CTS vì C đang giữ im lặng. D sẽ tiếp tục thử lại vào những thời điểm ngẫu nhiên và liên tục thất bại, vì không biết khi nào A sẽ ngừng truyền dữ liệu.

Ngược lại, A biết chính xác khi nào nó sẽ ngừng truyền dữ liệu. Giống như trước, điều này mang lại cho A lợi thế lớn trong vòng tranh chấp tiếp theo. A có thể ngay lập tức gửi yêu cầu mới và giành quyền truyền. Trong khi đó, D không biết khi nào nên gửi lại yêu cầu. Cách duy nhất để D thắng là cực kỳ may mắn, gửi yêu cầu ngay sau khi A truyền xong nhưng trước khi A gửi lại yêu cầu.

<img width="900px" src="/assets/wireless/8-027-rrts1.png">

Lưu ý rằng gói DS không giúp ích trong trường hợp này, vì hai bộ phát A và D nằm ngoài phạm vi của nhau. A sẽ gửi gói DS và thông báo khi nó đang truyền dữ liệu, nhưng D sẽ không nghe thấy, nên vẫn thất thế.

Để giải quyết vấn đề này, chúng ta sẽ để bộ thu tranh chấp thay cho bộ phát. D không biết khi nào nên gửi lại yêu cầu, nhưng C thì biết, vậy hãy để C gửi yêu cầu thay.

Khi D gửi RTS, C biết rằng D muốn liên lạc, nhưng C phải giữ im lặng cho đến vòng tranh chấp tiếp theo. Lưu ý rằng C biết khi nào vòng tranh chấp tiếp theo diễn ra, vì nó sẽ nghe thấy gói ACK từ B. Khi vòng tranh chấp tiếp theo bắt đầu, C gửi một gói mới gọi là **RRTS (Request-for-RTS)**. Gói này ngay lập tức báo cho D rằng vòng tranh chấp đã bắt đầu, cho phép D gửi RTS ngay lập tức. Điều này giúp D có cơ hội công bằng hơn để thắng vòng tranh chấp.

<img width="900px" src="/assets/wireless/8-028-rrts2.png">

Nếu bạn nghe thấy một gói RRTS, điều đó có nghĩa là có ai đó trong phạm vi của bạn đang cố gắng gửi yêu cầu, vì vậy bạn nên giữ im lặng trong 2 time slots để họ thực hiện trao đổi RTS/CTS.

Trong ví dụ, nếu C gửi RRTS, B sẽ nghe thấy và giữ im lặng trong 2 time slots, cho phép D gửi RTS và C gửi CTS. CTS sẽ yêu cầu B giữ im lặng, và cho phép phiên truyền D–C diễn ra.

Nói chung, bạn nên gửi RRTS nếu bạn nghe thấy RTS nhưng không được phép phản hồi, vì có ai đó đã yêu cầu bạn giữ im lặng.

DS và RRTS giúp đồng bộ hóa và đảm bảo các vòng tranh chấp công bằng hơn, nhưng chúng không giải quyết được mọi vấn đề. Xét trường hợp A gửi cho B và C gửi cho D. Giả sử C bắt đầu gửi cho D. Lúc này, nếu A gửi RTS, B sẽ không nghe thấy vì RTS bị “chìm” trong dữ liệu từ C. Cách duy nhất để RTS của A đến được B là trong khoảng trống rất ngắn giữa các lần truyền của C. Trong tình huống này, A chắc chắn sẽ thua, vì nó không biết khi nào C sẽ ngừng truyền, trong khi C biết chính xác thời điểm đó. Lưu ý rằng RRTS cũng không giúp được ở đây, vì RRTS chỉ được gửi nếu bạn nghe thấy RTS, nhưng B thậm chí không nghe thấy RTS. B sẽ không bao giờ biết rằng A muốn liên lạc, nên sẽ không gửi RRTS thay mặt A. Bài báo gốc về MACAW để lại vấn đề này chưa được giải quyết.

