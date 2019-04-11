CÁC KHÁI NIỆM QUAN TRỌNG CỦA ROS
================================

MASTER
------
 
  **Master** đóng vai trò như một máy chủ cho các kết nối **node-to-node** và truyền thông tin. 
  Các lệnh roscore được sử dụng để chạy các master. Bạn có thể đăng ký tên của mỗi node và nhận được thông tin khi cần thiết khi đăng kí với master. 
  Sự kết nối giữa các node và việc truyền thông tin như các **topic** và **service** sẽ thất bại nếu không có master.
  Các master giao tiếp với các node thông qua XmlRpc (XML-Remote Procedure Call), đó là một giao thức dựa trên HTTP mà không duy trì kết nối. 
  Nói cách khác, các node chỉ có thể truy cập khi nó cần phải đăng ký thông tin của mình hoặc yêu cầu thông tin của các node khác. 
  Trạng thái kết nối với nhau không được kiểm tra thường xuyên. 
  Do tính năng này, ROS có thể được sử dụng trong môi trường rất lớn và phức tạp. 
  **XmlRpc** là rất nhẹ và hỗ trợ nhiều ngôn ngữ lập trình, làm cho nó rất thích hợp cho ROS, mà hỗ trợ nhiều phần cứng và lập trình ngôn ngữ.
  Khi bạn thực hiện ROS, **master** sẽ được cấu hình với địa chỉ **URI** và cổng được cấu hình trong **ROS_MASTER_URI**. Theo mặc định, địa chỉ URI sử dụng địa chỉ IP của máy tính địa phương, và số cổng 11311, trừ trường hợp sửa đổi.



 
NODE
----
 
  Node là đơn vị nhỏ nhất của bộ xử lý chạy trong ROS. 
  Hãy nghĩ về nó như là một chương trình thực thi. 
  ROS khuyên bạn tạo một node duy nhất cho từng mục đích, và nó được khuyến khích phát triển để dễ dàng tái sử dụng. 
  Ví dụ trong trường hợp của robot di động, chương trình hoạt động của robot được chia thành nhiều các chức năng chuyên biệt như đọc tín hiệu từ cảm biến, 
  chuyển đổi dữ liệu cảm biến, nhận dạng chướng ngại vật, kết nối điều khiển động cở, đọc tín hiệu encoder, định vị, dẫn đường.
  
  Sau khi khởi động, một node đăng ký thông tin như tên, loại messages, địa chỉ URI và số cổng của node đó cho master. 
  Node đăng ký có thể hoạt động như một publisher, subscriber, service server hoặc service client dựa trên các thông tin đã đăng ký. 
  Các node có thể trao đổi messages sử dụng các topic và service.
  
  Nút sử dụng XMLRPC để liên lạc với master và sử dụng XMLRPC hoặc TCPROS5 của các giao thức TCP / IP khi giao tiếp giữa các node. 
  Yêu cầu kết nối và phản hồi giữa các node sử dụng XmlRpc, truyền thông tin sử dụng TCPROS 
  vì nó là một thông tin liên lạc trực tiếp giữa các node độc lập với master. 
  Đối với các địa chỉ URI và số cổng, có một biến gọi là ROS_HOSTNAME được lưu trữ trên máy tính nơi mà các node đang chạy. 
  Địa chỉ URI, và sô cổng được thiết lập là một giá trị duy nhất tùy ý.

 
PACKAGE
-------
 
  Một package là đơn vị cơ bản của ROS. Việc áp dụng ROS được phát triển trên cơ sở package. 
  Các package chứa một tập tin cấu hình để khởi động nó hoặc các node khác. Nó chứa tất cả các tệp cần thiết để chạy package, 
  bao gồm các thư viện phụ thuộc ROS để chạy các quy trình, bộ dữ liệu và các tệp cấu hình khác nhau. 
  
  Số liệu từ tháng 7 năm 2017 các package chính thức vào khoảng 2.500 cho ROS Indigo (http://repositories.ros.org/status_page/ ros_indigo_ default.html) 
  và khoảng 1.600 package cho ROS Kinetic (http://repositories.ros.org / status_page / ros_kinetic_default.html). 
  Bên cạnh đó, mặc dù có thể có một số dư thừa, có khoảng 4.600 gói phát triển và phát hành bởi người dùng (http://rosindex.github.io/stats/).
  
METAPACKAGE
-----------
 
  Tập hợp các package có cùng chung mục đích.
 
MESSAGE
-------
 
  Các node giao tiếp với nhau thông qua messages. Messages là các biến như int, floating point và boolean. Cấu trúc messages lồng nhau chứa các messages khác
  hoặc một mảng các messages có thể được sử dụng trong một messages
  TCPROS và UDPROS giao thức truyền thông được sử dụng cho truyền tin nhắn. 
  Topic được sử dụng trong gửi messages một chiều trong khi service được sử dụng trong gửi messages hai chiều có liên quan đến yêu cầu và phản hồi.

 
TOPIC
-----
 
  Topic giống như một chủ đề trong cuộc trò chuyện. 
  Đầu tiên node publisher đăng ký topic của nó với master và sau đó bắt đầu thông điệp publish về một topic. 
  Node Subscriber muốn nhận thông tin yêu cầu topic của nút piblisher tương ứng với tên của topic đăng ký trong master. 
  Dựa trên thông tin này, các node subscriber kết nối trực tiếp đến node publisher để trao đổi messages như một topic
 
PUBLISH AND PUBLISHER
---------------------
 
  Thuật ngữ ‘publish’ là viết tắt của hành động truyền messages tương ứng với topic. 
  Node publisher đăng ký thông tin và topic của riêng mình với master và gửi một message đến các node subscriber 
  được kết nối quan tâm đến cùng một topic. Publisher được khai báo trong node và có thể được khai báo nhiều lần trong một node
 
SUBSCRIBE AND SUBSCRIBER
------------------------
 
   Thuật ngữ 'subscribe' là viết tắt của hành động nhận messages tương ứng với topic. 
   Node subscriber đăng ký thông và topic của riêng mình với các master, 
   và nhận được thông tin publisher mà publish topic tương đối từ các master. 
   Dựa trên thông tin publisher nhận được, node subscriber trực tiếp yêu cầu kết nối đến node publisher và 
   nhận được tin nhắn từ node publisher đã được kết nối. Một publisher được khai báo trong node và có thể được khai báo nhiều lần trong một node
  
SERVICE
-------
 
   Topic yêu cầu phải kết nối liên tục và một chiều. Một cái luôn gửi và một cái luôn nhận. Nó thường được dùng cho cảm biến khi phải liên tục truyền dữ liệu.
   Service: một node truyền thông tin, node khác nhận thông tin, xử lý và truyền kết quả ngược lại cho node đầu. Sau khi hoàn tất chúng ngắt kết nối.
 
SERVICE SERVER
--------------
 
 Các 'service server' là một máy chủ trong truyền service mesage . 
 Service server nhận được yêu cầu như là một đầu vào và truyền một phản ứng như một đầu ra. 
 Cả hai yêu cầu và trả lời được truyền dưới dạng message. Khi yêu cầu service, server thực hiện các service thiết kế và
 cung cấp kết quả cho service client như một câu trả lời. Service server được thực hiện trong node tiếp nhận và thực hiện một yêu cầu nhất định.
 
SERVICE CLIENT
--------------
 
 Các 'service client' là một khách hàng. Gửi message yêu cầu service đến máy chủ và nhận được message kết quả. 
 Cả hai yêu cầu và đáp ứng được truyền dưới dạng message. Client  gửi một yêu cầu đến service sẻver và nhận được phản hồi. 
 Các service client được thực hiện trong node yêu cầu và nhận được kết quả.
 
ACTION
------
 
 Action là một phương pháp truyền thông tin sử dụng cho một giao tiếp hai chiều không đồng bộ. 
 Action được sử dụng mà nó đòi hỏi thời gian lâu hơn để đáp ứng sau khi nhận được yêu cầu và phản ứng 
 trung gian được yêu cầu cho đến khi kết quả được trả về. Cấu trúc của tập tin action cũng tương tự như của service. 
 uy nhiên, phần dữ liệu phản hồi cho phản ứng trung gian được bổ sung cùng với mục tiêu và kết quả phần dữ liệu được 
 thể hiện dưới dạng request và response trong dịch vụ tương ứng. Có action client đặt mục tiêu còn action server và hành động mà 
 thực hiện các hành động cụ thể của mục tiêu đó. Trả về thông tin phản hồi và kết quả cho action client.
 
ACTION SERVER
-------------
 
 Các 'action server' có trách nhiệm tiếp nhận mục tiêu từ các khách hàng và đáp ứng với những phản hồi và kết quả. 
 Một khi máy chủ nhận được mục tiêu từ các khách hàng, nó thực hiện quá trình xác định trước.
 
ACTION CLIENT
-------------

 Action client có nhiệm vụ truyền mục tiêu đến máy chủ và nhận kết quả hoặc
 dữ liệu phản hồi như đầu vào từ máy chủ action. client cung cấp mục tiêu cho máy chủ hành động,
 sau đó nhận kết quả hoặc phản hồi tương ứng. Chúng có thể truyền và theo dõi hướng dẫn hoặc hủy bỏ hướng dẫn.

 
PARAMETER
---------
 
 Tham số trong ROS đề cập đến các tham số được sử dụng trong node. 
 Giá trị mặc định được đặt trong tham số và có thể được đọc hoặc ghi nếu
 cần thiết. 
 Ví dụ: bạn có thể điều chỉnh các cài đặt như số cổng USB, thông số hiệu chỉnh máy ảnh, giá trị tối đa và tối thiểu của tốc độ động cơ thông qua parameter.

 
PARAMETER SERVER
----------------
 
 Khi các tham số được gọi trong package, chúng được đăng ký với parameter server được tải trong master.
  
CATKIN
------
 
 Catkin đề cập đến việc xây dựng hệ thống của ROS. Về cơ bản, hệ thống xây dựng sử dụng CMake (Tạo nền tảng chéo) và môi trường xây dựng được mô tả 
 trong tệp ‘CMakeLists.txt, trong thư mục gói. CMake đã được sửa đổi trong ROS để tạo ra một hệ thống xây dựng dành riêng cho ROS. 
 Catkin bắt đầu thử nghiệm alpha từ ROS Fuerte và các gói cốt lõi bắt đầu chuyển sang Catkin trong phiên bản ROS Groovy. 
 Catkin đã được áp dụng cho hầu hết các gói trong phiên bản ROS Hydro. Hệ thống xây dựng Catkin giúp dễ dàng sử dụng các bản dựng, 
 quản lý gói và phụ thuộc liên quan đến ROS giữa các gói. Nếu bạn định sử dụng ROS vào thời điểm này, bạn nên sử dụng Catkin thay vì xây dựng ROS (rosbuild).


 
ROS BUILD
---------
 
 The ROS build (rosbuild) là hệ thống build được sử dụng trước hệ thống Catkin build.
 Mặc dù có một số người dùng vẫn sử dụng nó, nhưng điều này được dành riêng cho khả năng tương thích của ROS, do đó,
 Nó chính thức không được khuyến khích sử dụng. Nếu một gói cũ chỉ hỗ trợ rosbuild phải được sử dụng, chúng tôi khuyên bạn nên sử dụng nó sau khi chuyển đổi rosbuild thành catkin.

 
roscore
-------
 
 roscore là lệnh chạy master ROS. Nếu nhiều máy tính nằm trong cùng mạng, 
 nó có thể được chạy từ một máy tính khác trong mạng. Tuy nhiên, ngoại trừ trường hợp đặc biệt hỗ trợ nhiều roscore, 
 chỉ nên chạy một roscore trong mạng. Khi ROS master đang chạy, địa chỉ URI và số cổng được gán cho các biến ROS_MASTER_URI 
 môi trường được sử dụng. Nếu người dùng chưa đặt biến môi trường, địa chỉ IP hiện tại được sử dụng làm địa chỉ URI và số cổng 11311 
 được sử dụng là số cổng mặc định cho master.
 
rosrun
------
 
 rosrun là lệnh thực hiện cơ bản của ROS. Nó được sử dụng để chạy một node duy nhất trong package. 
 Node sử dụng biến môi trường ROS_HOSTNAME được lưu trữ trong máy tính mà node đang chạy dưới dạng địa chỉ URI. 
 Các cổng được thiết lập một giá trị duy nhất tùy ý.
 
roslaunch
---------

 Trong khi rosrun là một lệnh để thực hiện chạy một node duy nhất thì roslaunch ngược lại thực hiện chạy nhiều node. 
 Đó là một lệnh ROS chuyên thực hiện chạy nút với chức năng bổ sung chẳng hạn như thay đổi các thông số gói hoặc tên nút, 
 cấu hình không gian tên của nút, thiết lập ROS_ ROOT và ROS_PACKAGE_PATH, và thay đổi biến môi trường 19 khi thực hiện chạy các node. 
 roslaunch sử dụng file '* .launch' để xác định mà node được thực thi. Các tập tin dựa trên XML (Extensible Markup Language) 
 và cung cấp một loạt các lựa chọn theo hình thức thẻ XML.
 
bag
---

 
 
ROS Wiki
--------
 
Repository
----------
 
Graph
-----
 
Name
----
 
Client Library
--------------
 
URI
---
 
MD5
---
 
RPC
---
 
XML
---
 
XMLRPC
------
 
TCP/IP
------
 
CMakeLists.txt
--------------
 
package.xml
-----------
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 