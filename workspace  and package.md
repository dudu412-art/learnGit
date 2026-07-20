# **workspace工作空间，就是存放项目相关的文件**

1.包含四个空间，src代码空间，install安装空间，build编译空间，log日志空间

2.***创建工作空间:***
              mkdir -p ~/dev_ws/src   
              
              cd ~/dev_ws/src
              
              git clone https://gitee.com/guyuehome/ros2_21_tutorials.git
              
  ***自动安装依赖：***      
              sudo apt install -y python3-pip(-y默认同意之后所有请求)
              
              sudo pip3 install rosdepc
              
              sudo rosdepc init && rosdepc update  （rosdepc的初始化和更新）  
              
              rosdepc install -r --from-path src -i --rosdistro jazzy -y
              
              // （-r是扫描所有src以下的子文件夹，-i是在安装系统依赖的所有库，而不去管我们自己书写的库，rosdistro 这个是用来控制ros2的版本）
              
  ***编译工作空间：***           
              sudo apt install python3-colcon-ros（安装colcon）//colcon 是用来编译我们的文件的
              
              cd ~/dev_wc/
              
              colcon build(进行编译操作)
              
 ***设置环境变量：***
             source install/local_setup.sh(生效环境变量)
             
             //为了不让我们一直每次都要书写这句话，我们可以直接在bashrc文件里面输入这两句话来自动开启终端时可以生效环境变量。或者是通过命令行写入：
             
             echo "source ~/dev_ws/install/local_setup.sh">>~/.bashrc
             
             //  >>追加写入，>清空写入
             
             在bashrc里面写入 source /opt/ros/jazzy/setup.bash   &&source ~/dev_ws/install/local_setup.sh


#package

1.***package 是放置很多小配件比如节点的整体的一个大工具箱，而节点就是放置单独的一个小运作***

2.***创建功能包：***
                 cd ~/dev_ws/src
                 ros2 pkg creat --build-type ament__python learning_pkg_python
 3.***编译功能包***
                 cd ~dev_ws/src
                 colcon build
                 source install/local_setup.bash



//-p一键创建完整目录（前一目录如果没有就会直接创建）

//mkdir创建文件夹

//git clone  是git的常用方法，直接克隆其他人的文件

//alt+ctrl+t 快捷键打开终端，alt+ctrl 释放鼠标，可展示出鼠标光标

//sudo apt install  安装

//rosdepc 自动安装工具，输入rosdepc install  可以自动匹配查看你所需要的所有包，而不需要一一单独下载

//ctrl+h显示隐藏文件
