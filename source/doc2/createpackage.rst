Tạo package
-----------

.. note:: Hãy chắc chắn rằng bạn đã cài các mục bắt buộc mà tôi đã hướng dẫn bên trên.

Bước 1. Mở terminal -> Tạo package::
 
  cd ~/catkin_ws/src 
  catkin_create_pkg my_first_ros_pkg std_msgs roscpp 
  
Bước 2. Sửa đổi file cấu hình package: “package.xml”
 
.. image:: images2/anh11.png
   :width: 300px
   
Mở folder “src” trong folder (ROS package) vua tao. Add source code (.cpp).
 
.. image:: images2/anh26.png
   :width: 300px
  
Bước 3. Sửa đổi file cấu hình build: “CMakeLists.txt”
          
 * find_package
 * add_executable
 * target_link_libraries

.. image:: images2/anh27.png
   :width: 300px
  

Bước 4. Tạo thư mục msg và file định nghĩa kiểu message

.. image:: images2/anh12.png
   :width: 600px
   
.. image:: images2/anh13.png
   :width: 600px
   
.. image:: images2/anh14.png
   :width: 300px

.. image:: images2/anh15.png
   :width: 300px
   
Bước 6. Coding publisher node \*.cpp\

.. image:: images2/anh16.png
   :width: 600px

Bước 7. Coding subscriber node \*.cpp\

.. image:: images2/anh17.png
   :width: 600px
   
Bước 8. Build hệ thống::

 cd ~/catkin_ws
 catkin_make



.. image:: images2/anh18.png
   :width: 600px
   
Bước 9. Run the publisher/ subscriber
 
.. image:: images2/anh19.png
   :width: 600px

.. image:: images2/anh20.png
   :width: 600px
   
Bước 10. Kiểm tra và chạy thử node đã build::

 rosrun my_movegroup_example my_program
 
 