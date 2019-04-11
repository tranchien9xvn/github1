Các khái niệm quan trọng của ROS
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

 Một source package  xác định kho trong trang Wiki. Kho là một địa chỉ URL trên web nơi mà các package được lưu. 
 Kho quản lý các vấn đề, phát triển, tải về, và các tính năng khác sử dụng hệ thống kiểm soát phiên bản như svn, hg và git. 
 Nhiều người dùng ROS hiện có đang sử dụng GitHub như kho cho source code. Để xem nội dung của các source code cho từng package, kiểm tra Repository tương ứng.
 
Graph
-----

 Mối quan hệ giữa các node, các topic, publisher, và subscriber giới thiệu ở trên có thể được hình dung như một đồ thị. 
 Các đại diện đồ họa của messages không bao gồm các service như nó chỉ xảy ra một lần. 
 Đồ thị có thể được hiển thị bằng cách chạy nút 'rqt_graph' trong gói 'rqt_graph'. 
 Có hai lệnh thực hiện, 'rqt_graph' và 'rosrun rqt_graph rqt_graph'.
 
Name
----

 Node, parameter, topic và service đều có tên . Những tên đã được đăng ký trên master và tìm kiếm theo tên 
 để chuyển thông điệp khi sử dụng các thông số, chủ đề và các dịch vụ của mỗi nút. Tên rất linh hoạt vì họ có 
 thể được thay đổi khi được thực thi, và tên gọi khác nhau có thể được gán khi thực hiện các nút giống hệt nhau, 
 các thông số, chủ đề và các dịch vụ nhiều lần. Sử dụng tên làm cho ROS phù hợp cho các dự án quy mô lớn và hệ thống phức tạp.
 
Client Library
--------------
 
 ROS cung cấp môi trường phát triển cho các ngôn ngữ khác nhau bằng cách sử dụng thư viện khách hàng 
 để giảm sự phụ thuộc vào ngôn ngữ sử dụng. Các client library chính là C ++, Python, Lisp, và 
 ngôn ngữ khác như Java, Lua, NET, EusLisp, và R cũng được hỗ trợ. Với mục đích này, các thư viện client như 
 roscpp, rospy, roslisp, rosjava, roslua, roscs, roseus, Pharos, và rosR đã được phát triển.
 
URI
---
 
 Một URI (Uniform Resource Identifier) là một địa chỉ duy nhất đại diện cho một nguồn tài nguyên trên Internet. 
 URI là một trong những thành phần cơ bản cho phép tương tác với Internet và được sử dụng như một định danh trong giao thức Internet.
 
MD5
---
 
 MD5 (Message-Digest thuật toán 5) là mã hóa hàm băm 128 bit. Nó được sử dụng chủ yếu để xác minh tính toàn vẹn dữ liệu, 
 chẳng hạn như kiểm tra với các chương trình hoặc các tập tin ở dạng ban đầu chưa sửa đổi của nó. 
 Tính toàn vẹn của thông điệp truyền và nhận trong ROS được xác minh với MD5.
 
RPC
---
 
 RPC (Remote Procedure Call)  là viết tắt của chức năng gọi một thủ tục con trên một máy tính từ xa từ một máy tính khác trong mạng. 
 RPC sử dụng các giao thức như TCP / IP và IPX, và cho phép thực hiện các chức năng hoặc các thủ tục mà không cần phải lập trình viên 
 viết một chương trình cho phép điều khiển từ xa.
 
XML
---
 
 XML (Extensible Markup Language) là một ngôn ngữ đánh dấu mở rộng và linh hoạt mà W3C 
 khuyến cáo cho việc tạo ra ngôn ngữ đánh dấu mục đích đặc biệt khác. XML sử dụng thẻ để mô tả cấu trúc của dữ liệu. 
 Trong ROS, nó được sử dụng trong nhiều thành phần như * .launch, * .urdf, và package.xml.
 
XMLRPC
------
 
 XmlRpc (XML-Remote Procedure Call) là một loại giao thức RPC sử dụng XML như là định dạng mã hóa và sử dụng theo yêu cầu và đáp ứng phương pháp của giao thức HTTP mà 
 không duy trì cũng không kiểm tra kết nối. XmlRpc là một giao thức rất đơn giản, chỉ được sử dụng để xác định kiểu dữ liệu nhỏ hoặc lệnh. Kết quả là, 
 XmlRpc là rất nhẹ và hỗ trợ nhiều ngôn ngữ lập trình, làm cho nó rất thích hợp cho ROS, mà hỗ trợ một loạt các phần cứng và ngôn ngữ
 
TCP/IP
------
 
 TCP là viết tắt của Transmission Control Protocol. Nó thường được gọi là TCP / IP. TCP là viết tắt của Transmission Control Protocol. 
 Nó đảm bảo việc truyền tải và nhận dữ liệu liên tục trong truyền tải lớp giao thức internet.
 
 TCPROS là một định dạng thông điệp dựa trên giao thức TCP / IP và UDPROS là một định dạng thông điệp dựa trên UDP. TCPROS được dùng thường hơn trong ROS.
 
CMakeLists.txt
--------------
 
 Catkin xây dựng hệ thống của ROS, sử dụng CMake theo mặc định. Môi trường xây dựng được quy định trong 'CMakeLists.txt'  nằm trong mỗi file package.


 
package.xml
-----------

 Chứa thông tin mô tả tên gói, tác giả, giấy phép, và các gói phụ thuộc.
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 