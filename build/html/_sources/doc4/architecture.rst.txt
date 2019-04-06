Kiến trúc của MoveIt
====================

.. image:: images4/anh22.png
   :width: 600px

Tổng quan cách tiếp cận học MoveIt! Tutorials
---------------------------------------------

Link: https://ros-planning.github.io/moveit_tutorials/ 

1. MoveIt Đã cung cấp sẵn robot 6DOF để học “panda robot”
2. Chạy example mẫu (Getting Started & Quick start in Rviz)
3. Dành cho beginers, cách dễ nhất là sử dụng “MoveGroup C++ interface”  đó là “MoveGroupInterface” class ta có thể
      * Giao tiếp qua ROS topics, services and action
      * Set góc khớp, tư thế mong muốn
      * Di chuyển robot, thêm đối tượng trong môi trường
	  
.. image:: images4/anh23.png
   :width: 300px

4. Cao thủ hơn, sử dụng trực tiếp các API C++ của MoveIt! Để build các ứng dụng phức tạp. Kết quả việc sử dụng các API C++ trực tiếp sẽ bỏ qua rất nhiều ROS service/action layers và ta có được hiệu năng nhanh hơn
5. Tích hợp vào robot mới
      * Kiểm tra robot của mình đã được setup chưa?
      * Nếu không, làm theo tutorials ở đây để tích hợp robot vào MoveIt!
6. Cấu hình
      * Cấu hình động học
      * …
	  
.. image:: images4/anh24.png
   :width: 300px
   
.. image:: images4/anh25.png
   :width: 300px
   
   
7. Các đặc tính khác
      * Điều khiển qua joystick
      * Benchmarking
      * ...
	  
	  


Move_group node
---------------

UI(C++/PYTHON/GUI)
------------------

ROS interface
-------------


Robot interface (JS,TF,CTRL...)
-------------------------------

Config (URDF,SRDF,Wizard)
-------------------------

Plugins(planning: OMPL, Conllision: FCL, Kinematics: KDL)
---------------------------------------------------------