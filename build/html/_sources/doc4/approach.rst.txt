Kiến trúc của ROS
=================



.. image:: images4/anh21.png
   :width: 600px
   
1. **URDF**: Lập trình trên ngôn ngữ (xml) thiết kế cấu hình robot để điêu khiển trực quan trên RVIZ của bạn. RVIZ chỉ là một guide để điều khiển trực quan robot của bạn thôi nhé.
2. **GAZEBO**: Giả lập 3D có thể mô phỏng môi trường hoạt động thực tế. Lập trình trên ngôn ngữ xml. Gazebo cũng hỗ trợ các chức năng ROS-Control và plugin để điều khiển các cảm biến và robot khác nhau.
3. **MOVEIT**: Tích hợp các thư viện và công cụ mạnh mẽ dành cho người thao tác. Cung cấp các thư viện mở như: Kinematics and Dynamics Library (KDL), The Open Motion Planning Library (OMPL). 
               Giúp bạn xác định các chức năng khác nhau của trình thao tác, như tính toán va chạm, lập kế hoạch chuyển động và các bản demo Pick and Place.

