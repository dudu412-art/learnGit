# param

## ros2 param 指令：

                 1. list 查看某个具体节点的所有参数
                 
                 2. describe 描述某个节点参数的相关内容
                 
                 3. get 获取参数的具体值
                 
                 4. set 临时赋值，下一次的时候值消失
                 
                 5. dump 将所有的参数保存到yaml文件里面
                 
                  ```python
                 # 导出到 params.yaml
                 ros2 param dump /move_server --file params.yaml
                 # 简写
                 ros2 param dump /move_server > params.yaml
                 ```
                 
                 6. load 从yaml里面加载参数到节点里面
                 
                  ros2 param load <节点名称> <yaml文件路径>
                 
                  //  --no-override这个添加上去是把yaml里面节点没有的参数添加进去，已经有的保持不变


```python
import rclpy
from rclpy.node import Node

class  ParameterNode(Node):
       def __init__(self,name):
            super().__init__(name)
            self.timer=self.creat_timer(2,self.name_callback)
            self.declare_parameter('robot_name','mbot')



        def timer_callback(self):
             robot_name_param=self.get_parameter('robot_name').get_parameter_value().string_value
             self.get_logger().info('Hello %s !'%robot_name_param)
             new_name_param=rclpy.parameter.Parameter('robot_name',rclpy.Parameter.Type.STRING,'mbot')
             all_new_parameters=[all_new_parameters]
              self.set_parameters(all_new_parameters)

def main(args=None):
     rclpy.init(args=args)
     node=ParameterNode("param_declare")
     rclpy.spin(node)
     node.destroy_node()
     rclpy.shutdown()
```









                 
