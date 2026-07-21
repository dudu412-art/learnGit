# 机器人的神经网络

DDS 数据分发服务：data destribution service

DDS主要由domain组成，每个domain相当于一个小组，小组内成员才可以互相沟通交流。有Qos策略，通过这个Qos来约束小组内沟通交流方式

## ros2 topic pub /chatter std_msgs/msg/Int32 "data:31"  

发布话题：ros2 topic pub 话题名称 消息类型 消息内容 qos通讯方式
---
***qos通讯方式：***
                                             
            **--qos-depth**（可缓存的最大消息量，只有与history一起用才成效，默认为10，可调节）
                                                          
            **--qos-durability**（可持久化策略，新订阅能否收到历史消息，后面接***volatile不持久***或者是***transient_local本地持久***）
                                                          
            **--qos-history**（消息缓存策略，后面接**keep_last只保留最后的n条消息，需要和depth配合使用**或者**keep_all保留所有消息**）
                                                          
            **--qos-profile**（一次性匹配所有qos属性，采用key：value这样的形式）

           Eg: ros2 topic pub -r 1 /chatter std_msgs/msg/Int32 "{data:31}"  --qos-profile history:=keep_last depth:=10 reliability:=reliable durability:=volatile
                                                          
            **--qos-reliability**（消息可靠传输，后面接**reliable可靠传输，丢包再重传，best_effort尽力传输，丢包不重传,system_default由底层决定使用哪种可靠性**）
---
***订阅话题：ros2 topic echo /chatter --qos***这里的qos要保证和话题的发布者qos一致，才可以订阅接受内容。
 
 ros2 topic info /chatter --verbose(加入--verbose会显示所有具体内容)

 
