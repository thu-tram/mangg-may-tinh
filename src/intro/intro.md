# **Giới thiệu về Internet** (Introduction to the Internet)

## **Internet là gì?** (What is the Internet?)

Internet hiện diện ở khắp nơi như một công cụ để truyền dữ liệu giữa các thiết bị trên toàn thế giới. Trong khóa học này, chúng ta sẽ tập trung vào **hạ tầng** (bao gồm cả phần cứng và phần mềm) hỗ trợ cho hoạt động này.

Internet và **World Wide Web** không phải là cùng một thứ. Bạn có thể hình dung **web** là các ứng dụng được xây dựng trên nền tảng Internet (ví dụ: Facebook, Twitter) mà bạn có thể truy cập thông qua **web browser** (trình duyệt web) như Firefox, Chrome. Ngoài web, nhiều ứng dụng khác cũng sử dụng hạ tầng Internet. Ví dụ: các ứng dụng không thuộc web như Zoom, trò chơi trực tuyến, hoặc thậm chí các thiết bị **Internet of Things (IoT)** như cảm biến trong tủ lạnh hoặc ô tô của bạn.



## **Tại sao Internet thú vị?** (Why is the Internet Interesting?)

Internet không phải là một loại công nghệ mạng mới (ví dụ: dây điện đã tồn tại từ trước), mà là giải pháp cho một vấn đề hoàn toàn mới: **kết nối các mạng khác nhau đã tồn tại**. Giải quyết vấn đề này đòi hỏi một **mô hình thiết kế** mới, có ảnh hưởng đến nhiều lĩnh vực khác của khoa học máy tính.

**Networking** (mạng máy tính) là một lĩnh vực tương đối mới trong khoa học máy tính. Internet đã đưa ra nhiều thách thức mới, khác biệt so với các lĩnh vực truyền thống. Ví dụ: khác với các lĩnh vực lý thuyết, chúng ta không có mô hình hình thức cho Internet; khác với các lĩnh vực phần cứng, chúng ta không có thước đo hiệu năng cố định.

Khác với các môn học trước đây bạn từng học, giờ đây chỉ viết mã chạy được là chưa đủ. Mã bạn viết phải **scale** (mở rộng) tới hàng tỷ người dùng. Mã bạn viết cũng phải phù hợp với các mối quan hệ kinh doanh giữa các nhà vận hành (nếu không, họ có thể không đồng ý chạy mã của bạn).

Mã chạy tốt cho một ứng dụng nhẹ (ví dụ: máy tính cá nhân) có thể không hoạt động trên một **server** (máy chủ) chịu tải nặng. Mã chạy tốt hôm nay có thể không chạy được ngày mai, khi các máy tính khác tham gia hoặc rời khỏi mạng.

Thiết kế của Internet đã ảnh hưởng đến cách chúng ta kiến trúc các hệ thống hiện đại (ví dụ: cân nhắc mục tiêu, ràng buộc và đánh đổi trong thiết kế). **Network architecture** (kiến trúc mạng) thiên về tư duy thiết kế hơn là chứng minh định lý hoặc viết mã. Nó thiên về cân nhắc đánh đổi hơn là đạt các chỉ số cụ thể. Nó thiên về thiết kế hệ thống thực tiễn hơn là tìm kiếm thiết kế tối ưu. Internet không phải là tối ưu, nhưng đã cân bằng thành công nhiều mục tiêu khác nhau.



## **Internet là hệ thống liên kết liên bang** (The Internet is Federated)

Internet là một hệ thống **federated** (liên kết liên bang) và yêu cầu khả năng **interoperability** (tương tác) giữa các nhà vận hành. Nói cách khác, mỗi nhà vận hành (**ISP**) hoạt động độc lập, nhưng tất cả phải hợp tác để kết nối toàn thế giới. Tất cả các ISP trên thế giới cần thống nhất về một số **protocol** (giao thức) chung để đạt được khả năng kết nối toàn cầu.

Mô hình liên kết liên bang mang đến nhiều thách thức. Các thực thể cạnh tranh (ví dụ: các công ty đối thủ) buộc phải hợp tác, dù họ có thể không muốn chia sẻ thông tin mật. Khi thiết kế giao thức, chúng ta phải cân nhắc cả yếu tố kinh doanh thực tế bên cạnh yếu tố kỹ thuật.

Liên kết liên bang cũng làm phức tạp hóa đổi mới. Trong các lĩnh vực khác, công ty có thể đổi mới bằng cách phát triển tính năng mà không ai có. Nhưng trên Internet, nếu bạn có tính năng mà không ai khác có, bạn sẽ không thể sử dụng nó. Mọi người phải nói cùng một “ngôn ngữ” (protocol), vì vậy mọi nâng cấp Internet phải được thực hiện với khả năng tương tác trong tâm trí.



## **Internet có khả năng mở rộng** (The Internet is Scalable)

Liên kết liên bang cho phép Internet đạt quy mô khổng lồ. Thay vì một nhà vận hành duy nhất quản lý hàng tỷ người dùng và hàng nghìn tỷ dịch vụ, chúng ta chỉ cần tập trung vào việc kết nối các nhà vận hành khác nhau. Liên kết liên bang cũng cho phép xây dựng Internet từ nhiều công nghệ đa dạng (ví dụ: **wireless**, **optical**) với nhiều mức năng lực khác nhau (ví dụ: đường truyền gia đình dung lượng nhỏ, hoặc cáp quang biển dung lượng cực lớn). Các công nghệ này liên tục phát triển, nghĩa là chúng ta không thể đặt ra một mục tiêu cố định (ví dụ: dung lượng và nhu cầu liên tục tăng theo cấp số nhân).

Quy mô khổng lồ của Internet cũng đồng nghĩa với việc bất kỳ hệ thống nào chúng ta thiết kế phải hỗ trợ phạm vi rộng lớn người dùng và ứng dụng (ví dụ: một số cần nhiều băng thông hơn, một số có thể có hành vi độc hại).

Quy mô toàn cầu của Internet yêu cầu hệ thống và giao thức hoạt động **asynchronously** (bất đồng bộ). Dữ liệu không thể di chuyển nhanh hơn tốc độ ánh sáng (và thường chậm hơn nhiều). Giả sử bạn gửi một thông điệp tới một server ở phía bên kia thế giới. Khi thông điệp đến nơi, CPU của bạn có thể đã thực hiện hàng triệu lệnh khác, và thông điệp bạn gửi có thể đã lỗi thời.

Quy mô Internet cũng có nghĩa là ngay cả việc gửi một thông điệp đơn lẻ cũng có thể cần tương tác với nhiều thành phần (ví dụ: phần mềm, switch, liên kết). Bất kỳ thành phần nào cũng có thể hỏng, và chúng ta có thể không biết. Nếu có sự cố, có thể mất nhiều thời gian để nhận thông tin xấu. Internet là hệ thống đầu tiên được thiết kế để chịu lỗi ở quy mô lớn. Nhiều ý tưởng này sau đó đã được áp dụng trong các lĩnh vực khác.



## **Giao thức** (Protocols)

Trong khóa học này, chúng ta sẽ tập trung nhiều vào **protocol** – các quy tắc xác định cách các thực thể trao đổi thông tin. Giao thức quy định **định dạng** của thông điệp và **cách phản hồi** với các thông điệp đó.

Ví dụ: bạn viết một ứng dụng cần gửi và nhận dữ liệu qua Internet. Mã ở máy gửi và mã ở máy nhận phải thống nhất về cách định dạng dữ liệu và cách xử lý các thông điệp khác nhau.

Ví dụ về một giao thức: Alice và Bob cùng chào nhau, sau đó Alice yêu cầu một tệp, và Bob gửi lại tệp. Để định nghĩa giao thức này, chúng ta cần xác định **syntax** (cú pháp – ví dụ: cách viết “hãy gửi tôi tệp này” bằng bit 0 và 1) và **semantics** (ngữ nghĩa – ví dụ: Alice phải nhận lời chào từ Bob trước khi yêu cầu tệp).

Các giao thức khác nhau được thiết kế cho các nhu cầu khác nhau. Ví dụ: nếu Alice cần nhận tệp càng nhanh càng tốt, ta có thể thiết kế giao thức bỏ qua bước chào ban đầu. Thiết kế một giao thức tốt có thể khó hơn tưởng tượng! Chúng ta cũng cần tính đến các trường hợp ngoại lệ, lỗi và hành vi độc hại. Ví dụ: nếu Alice yêu cầu tệp, nhưng Bob lại trả lời bằng lời chào, Alice nên phản ứng thế nào?

Trong khóa học này, chúng ta sẽ thấy nhiều giao thức đã được **standardize** (tiêu chuẩn hóa) trên toàn Internet. Bạn sẽ đôi khi thấy từ viết tắt **RFC** (Request For Comments) khi nhắc đến một giao thức. Nhiều tiêu chuẩn được công bố dưới dạng tài liệu RFC và sau đó được chấp nhận rộng rãi, mặc dù không phải tất cả RFC đều được áp dụng. Các tài liệu RFC được đánh số, và đôi khi giao thức được gọi theo số RFC. Ví dụ: “RFC 1918 addresses” đề cập đến các địa chỉ được định nghĩa trong tài liệu đó.

Có nhiều tổ chức tiêu chuẩn khác nhau chịu trách nhiệm tiêu chuẩn hóa giao thức. **IEEE** tập trung vào các tầng thấp hơn liên quan đến kỹ thuật điện tử. **IETF** tập trung vào Internet và chịu trách nhiệm về các RFC.

