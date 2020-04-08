# Robomaster ICRA 2019 人工智能挑战赛
本项目是参加 [RM ICRA AI 大赛](https://www.robomaster.com/zh-CN/robo/icra) 时完成的。在比赛中，4台全自动机器人在场地中进行射击对抗。我们的机器人头尾各装了一个摄像头，并搭载一台A2激光雷达。

软件包概述：
* Localization：使用 AMCL 算法；此外，机器人在场地中特定区域补充弹药时，我们使用尾部摄像头辅助得到更高精度的定位效果。
* planning：使用 Lazy Theta* 用于全局路径规划；使用 TEB 用于局部路径规划。
* detection：通过光学特征识别敌对机器人的装甲板。
* decision：使用 Behavior Tree 算法 实现机器人的自主决策。
* 环境：Ros-kinetic & C++

## 日志
### 2019.5.28
赛后最终版本

Bug list：
1. leonard_decision 第一分钟只能补充一次弹药
好像是由于在5s准备期间，主车的嵌入式程序默认增加了40颗弹，导致blackboard认为加了一次弹药，或是别的原因
2. robots_detection 识别红色装甲时，会受到黄色日光影响，打空气
3. apriltags2_ros 识别apriltag具有局限性，二维码必须得有白边才能保证识别率，而比赛时补给站的二维码没有白边，如果明年还是apriltag，建议自己写识别程序；最后今年决策模块采用planning来对准补给站（还好弹仓大）

未来方向：
1. 搭建模拟器，并开始强化学习方面的探索

    华科开源模拟器：https://github.com/LoveThinkinghard/RoboMaster-AI-Challenge-Simulator-2D

2. 开始探索多机规划或者多机协作方面，两车相撞的问题很大
3. 买一个好的、功率大的路由器，今年的经验是：官方路由器容易换IP，且延迟大；自家的路由器干脆就链接不上（比赛时，场地是封闭的，路由器必须放在外面）

### 5.4
完成leonard_decision包
roborts_base包:
*TurnAngle Action 完成,用于机器人迅速旋转至指定角度(规划旋转较慢)
*test_refree_node 节点完成,用于模拟裁判系统服务器(模拟补给站,Buff区等发布的指令)
roborts_localization包:
*SupplyPid Action 完成,用于机器人通过AprilTag包发布的变换矩阵Pid调整位姿

