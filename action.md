# .action动作

***实质上action是由service和topic组成的***

1.几个命令：ros2 action ->list :展示当前所有的动作指令

                        info：展示动作的相关信息,后面接具体的动作名称

                        send_goal：发出动作，后面接数据名称，数据类型，数据的结构 

                        // --feedback：可以提供周期反馈
---
2.
.引入接口->引入节点->引入客户端->引入自定义的运动接口

..执行都是在这个main里面，初始化接口，定义一个节点，spin监听循环，销毁节点，销毁接口

...需要补充的就是如何去书写这个node了，所以我们需要再定义一个node，这个node里面还存放了***动作服务器（含有回调函数）***，用来接收client不断输出的指令

....然后就是如何去书写这个***回调函数***

## **action_move_server**

'''python
import rclpy
from  rclpy.node  import Node
from  rclpy.action import  ActionClient
from learning_interface.action import MoveCircle(自定义的运动接口)

class MoveCircleActionSever(Node):
      def __init__(self,name):
          super().__init__(name)
          self._action_server=ActionServer(
              self,
              MoveCircle,
              'move_circle'，
              self.execute_callback)//接口类型，动作名，回调函数

def execute_callback(self,goal_handle):
     self.get_logger().info('Moving circle...')
     feedback_msg.state=MoveCircle.Feedback()

     for i in range(0,360,30):
         feedback_msg.state =i
         self.get_logger().info('Publishing feedback: %d'%feedback_msg.state)
         time.sleep(0.5)

    goal_handle.succeed()
    result=MoveCircle.Result()
    result.finish=True
    return result



def main(args=None):
    rclpy.init(args=args)
    node=MoveCircleActionSever("action_move_server")
    rclpy.spin(node)//不断循环监听，就是说程序一直停在这里运行，不断去server去要数据
    node.destroy_node()
    rclpy.shutdown()
'''

## **action_move_client**

含有很多个callback来进行回调

***主要是这个文件怎么去书写去定义，包括之前的都需要仔细去书写***

最终展现：
ros2 run learning_action action_move_client
ros2 run learning_action action_move_server



接口interface：目标--+--反馈+--结果
cmakelist.txt只有c++文件才能自定义接口包，python文件有setup文件，但是不能自定义接口包
