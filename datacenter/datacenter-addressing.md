---
title: Addressing
parent: Datacenters
nav_order: 4
layout: page-with-toc
---


# **Địa chỉ hóa trong Datacenter** (Datacenter Addressing)

## **Tại sao Datacenter lại khác biệt?** (Why are Datacenters Different?)

Trong phần trước, chúng ta đã thấy rằng có thể chỉnh sửa các giao thức định tuyến **distance-vector** (vectơ khoảng cách) và **link-state** (trạng thái liên kết) để tính toán tất cả các đường đi trong mạng **datacenter** (trung tâm dữ liệu).

Tuy nhiên, các giao thức này có thể **scale** (mở rộng) kém trong môi trường datacenter.  
- Trong giao thức distance-vector, chúng ta phải tạo thông báo cho **mỗi đích** (destination), nghĩa là phải quảng bá hơn 100.000 đích.  
- Trong giao thức link-state, chúng ta phải **flood** (phát tràn) các thông báo dọc theo mọi liên kết, điều này mở rộng kém trong các mạng **Clos** có số lượng liên kết khổng lồ.  

Ngoài ra, hãy nhớ rằng các **topology** (kiến trúc liên kết) của datacenter thường sử dụng các **commodity switch** (switch thương mại giá rẻ), vốn có tài nguyên bộ nhớ và CPU hạn chế (ví dụ: **forwarding table** – bảng chuyển tiếp – không thể quá lớn).

Trong các mạng đa dụng (general-purpose networks), chúng ta giải quyết các vấn đề mở rộng này bằng cách giới thiệu **hierarchical IP addressing** (địa chỉ IP phân cấp). Các tổ chức cấp cao hơn (ví dụ: cấp quốc gia) có thể phân bổ dải địa chỉ cho các tổ chức nhỏ hơn (ví dụ: trường đại học). Datacenter không có cấu trúc phân cấp địa lý hoặc tổ chức để áp dụng cách tổ chức địa chỉ này.

Tuy nhiên, trong datacenter, chúng ta có thể tận dụng việc **operator** (nhà vận hành) kiểm soát **physical topology** (topology vật lý) của mạng, và gán địa chỉ cho **server** dựa trên vị trí của chúng trong tòa nhà. Chúng ta cũng có thể tận dụng việc topology có cấu trúc đều đặn (ví dụ: thường sắp xếp server thành hàng, thay vì đặt ngẫu nhiên trong tòa nhà).

---

## **Địa chỉ hóa nhận thức topology** (Topology-Aware Addressing)

<img width="900px" src="../assets/datacenter/6-042-dc-addressing.png">

Trong topology cụ thể này, các **rack** (tủ máy) được tổ chức vật lý thành các **pod** riêng biệt trong tòa nhà. Một cách tiếp cận tự nhiên là phân bổ một dải địa chỉ cho mỗi pod. Sau đó, mỗi pod có thể phân bổ các **sub-range** (dải con) cho từng rack trong pod. Cuối cùng, mỗi rack có thể phân bổ một địa chỉ IP riêng cho từng server.

Nhà vận hành biết số lượng server trong mỗi rack và số lượng rack trong mỗi pod, vì vậy chúng ta có thể dùng thông tin này để phân bổ dải địa chỉ với kích thước phù hợp. Ví dụ: một rack có thể nhận một dải `/24`, cung cấp cho rack đó 256 địa chỉ cho các server của mình.

Cách phân bổ này cho phép **aggregate routes** (gộp tuyến) và lưu ít mục hơn trong bảng chuyển tiếp. Ví dụ: xét một **spine router** (router xương sống) ở phía trên cùng của sơ đồ. Router này không cần ghi nhớ đường đi đến từng server. Thay vào đó, bảng chuyển tiếp chỉ cần bốn mục, mỗi mục cho một pod. Khi một packet đến, router kiểm tra 16 bit đầu tiên để chuyển tiếp packet đến pod thích hợp.

**Route aggregation** (gộp tuyến) cũng mang lại sự ổn định cao hơn. Nếu một host được thêm hoặc gỡ bỏ trong một rack cụ thể, spine router không cần biết. Miễn là chúng ta duy trì cùng sơ đồ địa chỉ, bảng chuyển tiếp hiện tại vẫn đúng mà không cần thay đổi. Do đó, các bản cập nhật định tuyến thường chỉ xảy ra khi liên kết hoặc switch gặp sự cố, chứ không phải khi host gặp sự cố.

Việc gán địa chỉ dựa trên topology của datacenter rất tốt cho khả năng mở rộng, nhưng cũng có một số hạn chế. Đặc biệt, nếu chúng ta di chuyển một server sang vị trí khác, chúng ta sẽ phải thay đổi địa chỉ của nó.

---