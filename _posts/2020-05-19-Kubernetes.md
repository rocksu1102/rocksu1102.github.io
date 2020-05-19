---
title: "Tổng quang về Kubernetes"
excerpt_separator: "<!--more-->"
categories:
  - Kubernetes
tags:
  - Kubernetes
  
---

<h4>Kubernetes là gì?</h4>

Kubernestes hay còn gọi là k8s, nó được biết đến như một công cụ quản lý, điều phối container hiệu quả nhất. Một số khả năng của k8s:

* Quản lý các container cluster.
* Cung cấp các công cụ để triển khai ứng dụng.
* Mở rộng các ứng dụng khi cần.
* Quản lý các thay đổi đối với các ứng dụng được container hoá hiện có.
* Tối ưu hoá việc sử dụng phần cứng cơ bản bên dưới container.
* Cho phép thành phần ứng dụng khởi động lại và di chuyển trên toàn hệ thống khi cần thiết.

Cách thức hoạt động của kiến trúc Kubernetes:

<p><img style="display: block; margin-left: auto; margin-right: auto;" src="https://cloudfun.vn/attachments/kubernetes-architecture-png.1437/" alt="" width="640" height="352" /></p>

Kiến trúc k8s và các thành phần của nó:

    * K8s Master:
    Đây là đơn vị điều khiển chính quản lý wrokloads và liên lạc trên toàn hệ thống.

        * Etcd storage: Lưu trữ dữ liệu cấu hình của cluster để thể hiện trạng thái chung của cluster bất cứ lúc nào.
        * API-Server: Quản lý trung tâm nhận các REST requests, đóng vai trò là front-end để điều khiển cluster. Đây là thứ duy nhất giao tiếp với cluster etcd.
        * Scheduler: Lên lịch các pod trên các node khác nhau dựa trên việc sử dụng tài nguyên và quyết định nơi nào triển khai dịch vụ nào.
        * Controller Manager: Nó chạy một số quy trình điều khiển riêng biệt trong nền để điều chỉnh trạng thái chia sẻ của cluster và thực hiện một tác vụ theo quy luật. Khi có bất kỳ thay đổi nào trong dịch vụ, bộ điều khiển sẽ phát hiện ra sự thay đổi và bắt đầu làm việc theo trạng thái mong muốn mới.
        * Worker Node: Còn được gọi là Kubernetes hoặc Minion node, nó chứa thông tin để quản lý kết nối mạng giữa các container như Docker và liên lạc giữa master node khi gán tài nguyên cho các container theo lịch trình.
        * Kubelet: Đảm bảo rằng tất cả các container trong node đang chạy và ở trạng thái healthy. Kubelet theo dõi trạng thái của một pod nếu nó không ở trạng thái mong muốn. Nếu một node thất bại, bộ điều khiển sao chép sẽ quan sát sự thay đổi này và khởi chạy các pod trên một pod healthy khác.
        * Container: Container là mức thấp nhất của microservice, được đặt bên trong pod và cần địa chỉ IP bên ngoài để xem xét quy trình bên ngoài.
        * Kube Proxy: Nó hoạt động như một proxy mạng và bộ cân bằng tải. Ngoài ra, nó chuyển tiếp yêu cầu tới các pod chính xác trên các mạng bị cô lập trong một cluster.
        * cAdvisor: Hoạt động như một trợ lý chịu trách nhiệm theo dõi và thu thập dữ liệu về việc sử dụng tài nguyên và số liệu hiệu suất trên mỗi node.

Ưu điểm của k8s

    * <h4>Nguồn mở và di động</h4>
    Kubernetes có thể chạy các container trên một hoặc nhiều môi trường public cloud, máy ảo hoặc trên bare metal, điều đó có nghĩa là nó có thể được triển khai trên bất kỳ cơ sở hạ tầng nào. Hơn nữa, nó tương thích trên nhiều nền tảng, giúp cho chiến lược đa cloud trở nên linh hoạt và có thể sử dụng được.

    * <h4>Khả năng mở rộng workloads</h4>
        * <h4>Horizontal Infrastructure Scaling:</h4> Các thao tác được thực hiện ở cấp máy chủ riêng lẻ để thực hiện chia tỷ lệ theo chiều ngang. Máy chủ mới có thể được thêm hoặc gỡ bỏ dễ dàng.

        * <h4>Auto-Scaling :</h4> Dựa trên việc sử dụng tài nguyên CPU hoặc các số liệu ứng dụng khác, có thể sửa đổi số lượng container đang chạy.

        * <h4>Manual Scaling :</h4> Có thể thay đổi số lượng container đang chạy thông qua một lệnh hoặc giao diện.

        * <h4>Replication Controller :</h4> Bộ điều khiển sao chép đảm bảo rằng cluster có số lượng pod tương đương được chỉ định trong điều kiện đang chạy. Nếu có quá nhiều pod, bộ điều khiển sao chép có thể loại bỏ các pod bổ sung hoặc ngược lại.

    * <h4>Tính sẵn sàng cao</h4>

        * <h4>Health Checks:</h4> Kubernetes đảm bảo rằng ứng dụng không bị lỗi bằng cách liên tục kiểm tra tình trạng của các mode và container. Kubernetes cung cấp khả năng tự phục hồi và tự động thay thế nếu pod bị hỏng do lỗi.

        * <h4>Định tuyến lưu lượng và cân bằng tải:</h4> Bộ cân bằng tải Kubernetes phân phối tải trên nhiều tải, cho phép cân bằng tài nguyên nhanh chóng trong lưu lượng ngẫu nhiên hoặc xử lý hàng loạt.

    * <h4>Được thiết kế để triển khai</h4>
        * <h4>Tự động triển khai và khôi phục:</h4> Kubernetes xử lý phiên bản mới và cập nhật cho ứng dụng mà không có downtime, đồng thời theo dõi health trong quá trình triển khai. Nếu bất kỳ lỗi nào xảy ra trong quá trình, nó sẽ tự động khôi phục.

        * <h4>Triển khai Canary:</h4> Kubernetes kiểm tra song song việc sản xuất triển khai mới và phiên bản trước đó, trước khi tăng quy mô triển khai mới và đồng thời giảm quy mô triển khai trước đó.

        * <h4>Hỗ trợ Framework và ngôn ngữ lập trình:</h4> Kubernetes hỗ trợ hầu hết các ngôn ngữ và framework lập trình như Java, .NET, v.v. và cũng nhận được sự hỗ trợ lớn từ cộng đồng phát triển. Nếu một ứng dụng có khả năng chạy trong một container, nó cũng có thể chạy trong Kubernetes.

    * <h4>Và nhiều hơn nữa</h4>

    Kubernetes cung cấp quản lý DNS, giám sát tài nguyên, ghi nhật ký, sắp xếp lưu trữ và cũng giải quyết vấn đề bảo mật. Chẳng hạn, nó đảm bảo rằng thông tin như mật khẩu hoặc ssh keys được lưu trữ an toàn trong các Kubernetes secret. Các tính năng mới được phát hành liên tục và có thể có trên Kubernetes GitHub.

    * <h4>K8s và Container Stateful</h4>

    Kubernetes StatefulSets cung cấp các tài nguyên như khối lượng, id mạng ổn định và chỉ mục thứ tự từ 0 đến N, v.v để đối phó với các stateful container. Volume là một trong những tính năng quan trọng như vậy cho phép chạy ứng dụng stateful. Hai loại volume chính được hỗ trợ là:
        * <h4>Volume lưu trữ nhất thời:</h4> Lưu trữ dữ liệu nhất thời khác với Docker. Trong Kubernetes, volume được tính đến bất kỳ container nào chạy trong pod và dữ liệu được lưu trữ trên container. Nhưng, nếu các pod bị phá hoại, volume sẽ tự động bị loại bỏ.

        * <h4>Lưu trữ trọn đời:</h4> Dữ liệu sẽ được lưu trữ mãi mãi. Khi pod bị phá hoại hoặc được chuyển đến một node khác, dữ liệu đó sẽ vẫn còn cho đến khi nó bị xóa bởi người dùng. Do đó, dữ liệu được lưu trữ từ xa.

* <h4>Đặt nền móng để phát triển ứng dụng cloud</h4>

Một số công cụ quản lý và điều phối container như Apache Mesos với Marathon, Docker Swarm và AWS EC2 Container Service cung cấp các tính năng tuyệt vời nhưng nhẹ hơn Kubernetes.

<h4>Docker Swarm</h4> được gắn kết chặt chẽ với Docker runtime; do đó rất dễ dàng để chuyển từ Docker sang Swarm và ngược lại. 

<h4>Mesos</h4> với Marathon có thể triển khai bất kỳ loại ứng dụng nào và chỉ giới hạn ở các container. 

<h4>AWS ECS</h4> có thể dễ dàng truy cập bởi người dùng AWS hiện tại.

Các trường hợp sủ dụng thực tế của K8s
* Pokémon GO
* Pearson
* Pinterest

<h4>Kết luận</h4>

Trong một khoảng thời gian ngắn, Kubernetes đã lớn mạnh và phát triển thành một hệ thống cực kỳ mạnh mẽ. Vì nó mang lại nhiều lợi ích khác nhau, nhiều công ty thuộc mọi quy mô tìm cách phát triển sản phẩm và dịch vụ để đáp ứng nhu cầu ngày càng tăng. Kubernetes có khả năng hoạt động trên cả public và private cloud và đã biến nó thành một trong những công cụ yêu thích cho các doanh nghiệp hoạt động với các hybrid cloud. Nếu điều này tiếp tục, thậm chí có thể thấy nhiều công ty đầu tư vào Kubernetes và hệ thống quản lý container.

Nguồn: https://cloudfun.vn/threads/huong-dan-day-du-ve-kubernetes-chi-trong-10-phut.411/


