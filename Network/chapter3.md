# 第三章 交换网络

## 一、网桥与数据帧转发

#### 1.网桥

数据链路层扩展局域网，工作方式为基于转发表/转发数据库过滤转发帧。

网桥各个接口属于不同碰撞域。

#### 2.数据帧转发

根据转发表中mac地址到端口的映射进行转发：

1. 若存在对应端口号且与接收端口号一致则丢弃；
2. 若存在对应端口号且与接收端口号不一致则从该端口转发；
3. 若不存在对应端口号则将数据包从所有端口转发。

## 二、学习结点位置

**生成树协议**：去掉网络图中的一些边形成无环子树。

**算法**：

1. 选择一个网桥作为生成树的根(如序号最小的网桥)；
2. 其它结点计算到根节点的最短路径并记录下路径经过它的哪个端口，并将这个端口作为到根节点的优先路径；
3. 为每个局域网选纸牌指派网桥。

**消息格式**:(本网桥认定的根网桥标识符， 本网桥到本网桥的距离(跳数)，正在发送信息的网桥标识符)

**根节点选择**：

1. 初始时，每个结点认为自己是跟，并发出对应消息；

2. 当收到其他网桥消息时，若

   1. 根的标识符更小；
   2. 根相同，但有更小的距离；
   3. 根相同，跳数相同，发送者有更小的标识符

   则保留，跳数+1，转发；否则丢弃。

## 三、以太网交换机

本质上为多接口网桥，工作在数据链路层，也被称为二层交换机。