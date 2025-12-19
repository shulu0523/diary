# 工作流
Mixamo 下载动画文件 fbx 
导入 Blender 编辑 到处 glb

Direct kinematics and inverse kinematics.

Support for animating any property with customizable interpolation.

Support for calling methods in animation tracks.

Support for playing sounds in animation tracks.

Support for Bézier curves in animation.

# Direct kinematics and inverse kinematics.

## Direct kinematics（DK）
从 “关节” 到 “末端” 的正向计算
场景 1：机械臂定位
已知机械臂的 3 个关节角度：腰部旋转 30°、大臂抬起 60°、小臂弯曲 45°。通过 DK 计算，可直接得出手部的精确位置（如基座前方 50cm、高度 80cm），无需猜测。

## Inverse kinematics （IK）
从 “末端” 到 “关节” 的逆向计算

逆运动学是更贴近 “实际需求” 的逻辑 —— 我们通常关心 “末端要到达哪里”，而非 “关节要转多少度”。但由于反向映射的非线性，IK 存在多解性（多个关节组合可实现同一末端目标）或无解性（末端目标超出机器人工作范围）。
场景 1：机器人抓取物体
目标是 “机械臂手部到达桌子上的水杯位置（X=100cm,Y=0,Z=50cm）并保持水平姿态”。通过 IK 可反推出：腰部需旋转 10°、大臂抬起 70°、小臂弯曲 30°，才能让手部精准触达水杯。

正运动学：“我动了关节，所以末端到了这里”—— 用于从驱动端推导结果；
逆运动学：“我要末端到那里，所以关节该这么动”—— 用于从目标端反推驱动

# 如何更好的利用运动学知识制作动画

