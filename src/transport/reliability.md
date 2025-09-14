# Nguyên lý của Tầng Vận chuyển (*Transport Layer Principles*)

## Trừu tượng hóa và Mục tiêu của Độ tin cậy (*Reliability Abstraction and Goals*)

Nhiều ứng dụng yêu cầu độ tin cậy (*reliability*). Ví dụ, khi gửi một tệp qua Internet, chúng ta muốn bên nhận nhận được đúng các byte theo đúng thứ tự mà bên gửi đã gửi.

Tuy nhiên, *Layer 3* (tầng 3) chỉ cung cấp dịch vụ truyền gói tin (*packet*) không đáng tin cậy, theo cơ chế *best-effort* (nỗ lực tối đa nhưng không đảm bảo). Gói tin có thể bị mất (*dropped*), bị hỏng (*corrupted*), và bị thay đổi thứ tự (thứ tự gói tin gửi không khớp với thứ tự gói tin nhận). Gói tin cũng có thể bị trễ (ví dụ: bị kẹt trong hàng đợi chờ qua một liên kết).

Trong một số trường hợp hiếm, gói tin thậm chí có thể bị nhân bản (*duplicated*), khi bên gửi chỉ gửi một gói tin nhưng bên nhận lại nhận được nhiều bản sao của gói đó. Điều này thường xảy ra nếu một *router* trên đường truyền gặp lỗi nào đó. Trên thực tế, lỗi này rất hiếm.

Thông tin thú vị: Vern Paxson, giảng viên tại UC Berkeley, là một trong những người đầu tiên phát hiện và báo cáo hiện tượng gói tin bị nhân bản ở tầng liên kết (*link layer*).

Chúng ta sẽ sử dụng *Layer 4* (tầng vận chuyển – *transport layer*) để lấp đầy khoảng trống này bằng cách phát triển các giao thức dựa trên trừu tượng hóa truyền gói tin *best-effort* do mạng cung cấp, và cung cấp một trừu tượng hóa đáng tin cậy mà lập trình viên ứng dụng có thể sử dụng.

Vì lý do thực tiễn (được thảo luận ở phần khác), độ tin cậy được triển khai tại các *end host* (máy đầu cuối), không phải tại các *router* trung gian. Ngoài ra, độ tin cậy được triển khai trong hệ điều hành (*operating system*) để thuận tiện, giúp các ứng dụng không phải tự triển khai lại cơ chế này.

<img width="900px" src="/assets/transport/3-007-reliability-at-end-hosts.png">

Chúng ta sẽ chính thức hóa khái niệm độ tin cậy bằng cách định nghĩa **at-least-once delivery** (giao hàng ít nhất một lần). Trong mô hình này, đích đến phải nhận được mọi gói tin, không bị hỏng, ít nhất một lần, nhưng có thể nhận nhiều bản sao của cùng một gói. *Transport layer* sẽ sử dụng truyền *best-effort* để cung cấp *at-least-once delivery*. Sau đó, dựa trên *at-least-once delivery*, giao thức của chúng ta có thể loại bỏ các bản sao và cung cấp *exactly-once delivery* (giao hàng chính xác một lần) cho ứng dụng.

Lưu ý rằng truyền tin đáng tin cậy không đảm bảo rằng gói tin sẽ được gửi đi. Một máy tính không kết nối mạng thì không thể gửi dữ liệu đến đích, bất kể chúng ta dùng giao thức độ tin cậy nào. Các giao thức độ tin cậy được phép từ bỏ và không gửi một gói tin, nhưng lỗi này phải được báo cho ứng dụng. Giao thức không được phép báo sai rằng đã gửi thành công một gói tin.

Giao thức của chúng ta cũng cần hiệu quả. Cụ thể hơn, giao thức nên truyền dữ liệu nhanh nhất có thể, đồng thời giảm thiểu việc sử dụng *bandwidth* (băng thông) và tránh gửi gói tin không cần thiết. Ví dụ, chúng ta có thể đảm bảo gói tin đến nơi bằng cách gửi lại mỗi gói hàng trăm lần, nhưng điều này sẽ vi phạm yêu cầu sử dụng *bandwidth* hiệu quả.

## Mục tiêu của Tầng Vận chuyển (*Transport Layer Goals*)

Tại *transport layer*, mục tiêu của chúng ta là cung cấp cho ứng dụng một trừu tượng hóa tiện lợi, giúp lập trình viên dễ dàng hơn. *Transport layer* cho phép lập trình viên nghĩ theo khái niệm kết nối (*connection*), thay vì từng gói tin riêng lẻ được gửi qua mạng. Lý tưởng nhất, lập trình viên không cần quan tâm đến các chi tiết mạng cấp thấp như chia nhỏ dữ liệu dài thành gói tin, gửi lại gói tin bị mất, *timeout* (hết thời gian chờ), v.v.

*Reliability* chỉ là một trong nhiều mục tiêu mà chúng ta muốn đạt được ở *transport layer*.

*Transport layer* triển khai **demultiplexing** (tách luồng) giữa các tiến trình khác nhau tại *end host*, bằng cách sử dụng số *port* (cổng) để liên kết mỗi luồng (*flow* hoặc *connection*) với một tiến trình khác nhau trên *end host*.

*Transport layer* cũng triển khai *flow control* (điều khiển luồng) và *congestion control* (điều khiển tắc nghẽn), giúp giới hạn tốc độ gửi gói tin để tránh làm quá tải bộ nhận và mạng.

## Tách luồng bằng *Port* (*Demultiplexing with Ports*)

Giả sử máy tính cá nhân của tôi có hai ứng dụng cùng kết nối đến một máy chủ. Khi các gói tin đến máy tính của tôi, chúng có cùng địa chỉ *IP* nguồn (máy chủ) và cùng địa chỉ *IP* đích (máy tính của tôi). Làm sao tôi biết gói tin nào dành cho ứng dụng nào?

<img width="900px" src="/assets/transport/3-001-demultiplex.png">

Để phân biệt, hay **demultiplex**, gói tin nào dành cho ứng dụng nào, *transport layer* thêm vào tiêu đề một **port number** (số cổng), dùng để xác định một ứng dụng cụ thể trên *end host*.

<img width="900px" src="/assets/transport/3-002-ports.png">

Khi *transport layer* nhận một gói tin, nó có thể dùng số *port* để quyết định ứng dụng tầng cao nào sẽ nhận phần dữ liệu (*payload*). Vì *transport layer* được triển khai trong *operating system*, các *port* (đôi khi gọi là **logical ports** – cổng logic) là điểm kết nối nơi ứng dụng liên kết với ngăn xếp mạng (*network stack*) của hệ điều hành. Ứng dụng biết số *port* của mình, và hệ điều hành biết số *port* của tất cả ứng dụng, nhờ đó dữ liệu được truyền chính xác giữa ứng dụng và hệ điều hành (không bị lẫn với dữ liệu của ứng dụng khác).

<img width="800px" src="/assets/transport/3-003-port-attachment.png">

Số *port* dài 16 bit. Internet hiện đại thường sử dụng mô hình *client-server* (máy khách – máy chủ), trong đó *client* truy cập dịch vụ và *server* cung cấp dịch vụ. *Server* thường lắng nghe yêu cầu trên các *well-known ports* (cổng nổi tiếng, số từ 0–1023). *Client* biết các cổng này và có thể truy cập để yêu cầu dịch vụ. Ví dụ, các giao thức tầng ứng dụng với cổng nổi tiếng gồm *HTTP* (cổng 80) và *SSH* (cổng 22).

Ngược lại, *client* có thể chọn số *port* ngẫu nhiên (thường từ 1024–65535). Các số *port* này có thể được chọn ngẫu nhiên vì *client* là bên khởi tạo kết nối, và không ai cần *client* có số *port* cố định (vì *client* không cung cấp dịch vụ). Số *port* của *client* là **ephemeral** (tạm thời), vì có thể bỏ sau khi kết nối kết thúc.

## Trừu tượng hóa luồng byte (*Bytestream Abstraction*)

Việc triển khai *reliability* (độ tin cậy) ở *transport layer* (tầng vận chuyển) có nghĩa là lập trình viên ứng dụng không còn phải nghĩ đến từng *packet* (gói tin) kích thước giới hạn được gửi qua mạng. Thay vào đó, lập trình viên có thể nghĩ theo khái niệm **reliable in-order bytestream** (luồng byte đáng tin cậy, đúng thứ tự).  

Phía gửi có một luồng byte không giới hạn độ dài và cung cấp luồng này cho *transport layer*. Sau đó, phía nhận sẽ nhận được chính xác cùng luồng byte đó, theo đúng thứ tự, không mất byte nào. Bạn có thể hình dung *bytestream* như một đường ống: phía gửi đưa từng byte vào một đầu ống, và các byte đó xuất hiện ở đầu kia của ống theo đúng thứ tự.  

Phía gửi và phía nhận không cần quan tâm đến việc gửi lại các *packet* bị mất hay xử lý *packet* đến sai thứ tự, vì giao thức *transport layer* sẽ đảm nhiệm điều đó cho lập trình viên.

<img width="900px" src="/assets/transport/3-004-bytestream.png">

## *UDP* và *Datagram*

Đôi khi, ứng dụng không cần *reliability*. Ví dụ, hãy xem xét một cảm biến đo áp suất nước trong nhà bạn. Cảm biến này gửi một bản ghi (thông điệp nhỏ, kích thước cố định, gồm thời gian và áp suất nước) đến công ty cấp nước mỗi phút.  

Hệ thống này có thể không cần các *packet* đến đúng thứ tự (ví dụ: nếu bản ghi đã bao gồm dấu thời gian), và cũng có thể không cần khả năng chia nhỏ thông điệp dài thành nhiều *packet* (mỗi bản ghi vốn đã nhỏ). Hệ thống thậm chí có thể không cần *reliability*, miễn là phần lớn bản ghi đến được công ty cấp nước.  

Các ứng dụng không cần *reliability* có thể sử dụng **UDP** (*User Datagram Protocol* – Giao thức gói tin người dùng) thay vì *TCP* ở *transport layer*. *UDP* không cung cấp đảm bảo *reliability*. Nếu ứng dụng cần một *packet* đến nơi, ứng dụng phải tự xử lý việc gửi lại (vì *transport layer* sẽ không gửi lại).  

Thông điệp trong *UDP* bị giới hạn trong một *packet*. Nếu ứng dụng muốn gửi thông điệp lớn hơn, ứng dụng phải tự chia nhỏ và ghép lại. Lưu ý rằng *UDP* vẫn sử dụng khái niệm *port* để *demultiplexing* (tách luồng).

<img width="900px" src="/assets/transport/3-005-datagram.png">

Ở *transport layer*, bạn có thể chọn dùng *UDP* hoặc *TCP* tùy nhu cầu, nhưng không thể dùng cả hai cùng lúc. *UDP* và *TCP* là các giao thức *transport layer* tiêu chuẩn trên Internet hiện đại.

<img width="300px" src="/assets/transport/3-006-tcp-features.png">


## Các thiết kế *Reliability* khác (*Other Reliability Designs*)

*TCP* ban đầu được triển khai bởi Vint Cerf và Bob Kahn khi họ còn là sinh viên tại UCLA. Sau này, họ đã nhận Giải thưởng Turing, Huân chương Tự do của Tổng thống, v.v. cho công trình của mình.  

Điều đáng chú ý là thiết kế ban đầu của *TCP* khá giống với những gì đang được sử dụng trong thực tế ngày nay và đã đứng vững trước thử thách của thời gian. Các ý tưởng cốt lõi của *TCP* rất đơn giản, thiết kế thanh thoát (dù không hoàn hảo). Tuy nhiên, việc triển khai có thể phức tạp để làm đúng, và rủi ro cao vì gần như toàn bộ Internet hiện đại chạy trên *TCP*.  

Kể từ khi ra đời, nhiều thành phần riêng lẻ của *TCP* đã được cải tiến (ví dụ: thuật toán ước lượng bộ định thời tốt hơn, cơ chế *acknowledgement* thông minh hơn, lựa chọn *ISN* tốt hơn, *congestion control* thông minh hơn), nhưng các quyết định kiến trúc và trừu tượng hóa cốt lõi (luồng byte theo kết nối, cửa sổ truyền) vẫn giữ nguyên.

*TCP* là giao thức *reliability* tiêu chuẩn trên Internet, nhưng vẫn tồn tại các cách tiếp cận hoàn toàn khác.  

Ví dụ, phía gửi có thể tận dụng ý tưởng **redundancy** (dư thừa – như trong mã sửa lỗi (*error-correcting codes*) hoặc *RAID*) để gửi dữ liệu đáng tin cậy hơn. Thay vì gửi nguyên dữ liệu, phía gửi mã hóa dữ liệu thành nhiều *packet* hơn, với phần dư thừa được chèn vào mỗi *packet*.  

Ví dụ: người dùng có 10 *packet*, và một thuật toán có thể mã hóa dữ liệu đó thành 20 *packet*. Thuật toán có thể đảm bảo rằng chỉ cần nhận được bất kỳ 15 trong số 20 *packet*, dữ liệu gốc gồm 10 *packet* có thể được khôi phục.

Một cách mô tả chính xác hơn: thuật toán mã hóa nhận vào *k* *packet*, mã hóa thành *n* *packet* (với *n* > *k*), sao cho dữ liệu gốc có thể được khôi phục nếu nhận được bất kỳ *k'* *packet* nào (với *k'* > *k* nhưng *k'* < *n*).

Các sơ đồ mã hóa (*coding schemes*) là một chủ đề sâu rộng với nhiều thuật toán (ví dụ: *fountain codes*, *raptor codes*), dù ở đây chúng ta sẽ không đi sâu. Chúng có thể được ứng dụng thực tế trong các nền tảng truyền phát video (*video streaming*).