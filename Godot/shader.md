
# Shader Overview 
Shaders are a special type of program that runs on the GPU. They are used to render 3D graphics.

Graphics cards can run thousands of instructions in parallel, which makes them very fast.

Because of their parallel nature, Shader code runs on each vertex or pixel in isolation. You cannot store data between frames either

# Shader in Godot
In Godot, shaders are made up of main functions called "processor functions". Processor functions are the entry point for your shader into the program. There are seven different processor functions.

vertex() -> fragment() -> light()

vertex() runs once for each vertex in the mesh. It is used to transform the vertex position and other attributes.

fragment() runs once for each pixel in the screen. It is used to calculate the color of the pixel.

light() runs once for each light in the scene. It is used to calculate the color of the light on the pixel.

## 渲染流水线
应用阶段 -》 几何阶段 -》 光栅化阶段 -》 片段阶段 -》 合并阶段
几何阶段：
1、顶点着色器：对每个顶点进行变换，包括位置变换、法线变换、纹理坐标变换等。（可编程）
变换顶点位置和计算变换后的顶点属性（如法线、纹理坐标等、颜色）。
2、几何着色器：可选阶段，用于生成新的几何 primitive（如点、线、三角形）。（可选）
3、裁剪阶段：根据视锥体剔除不在视野内的 primitive。（可选，指定）
4、屏幕空间变换：将裁剪空间坐标转换为屏幕空间坐标。（固定的）

光栅化阶段：
1、将 primitive 转换为片段（fragment）。
2、进行深度测试和深度写入。

片段阶段：
1、对每个片段进行颜色计算。
2、应用光照模型（如 Phong 光照、Blinn-Phong 光照等）。
3、应用透明混合（如 alpha 混合、深度写入等）。

合并阶段：
1、将所有片段的颜色合并到最终的颜色缓冲区中。
2、应用后处理效果（如抗锯齿、颜色校正等）。

## 光照模型
光照模型是用来计算像素颜色的数学公式。不同的光照模型有不同的效果。
光照模型有很多种，常用的光照模型：Phong 光照模型和 Blinn-Phong 光照模型。

* 要想学会 Shader 必须要理解光照模型的原理
  理解涉及到的各种概念是关键

 Material 材质属性
 材质属性包括反射系数、高光指数、颜色等。
 这些属性决定了物体在不同光照条件下的外观


# 学 Shader 最重要的是 思考实现效果的思路

## 2D图形描边
1、描边的实现思路是在原始图形的基础上，绘制一个比原始图形大（一个单位）的图形，图形的颜色是描边的颜色。
2、如何计算边缘是关键（如何判断一个像素是否在原始图形的边缘）

## 3D效果
3D 效果核心是模拟真实世界的材质属性和光影交互，注重物理准确性和视觉真实感。
