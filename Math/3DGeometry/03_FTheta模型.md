## 基本概念

F-theta 是一种 **等距投影** 模型，核心公式是：
$$
\boxed{r=f\theta}
$$
其中 $r$ 是像点到主点的距离，$f$ 是焦距，$\theta$ 是入射光线与光轴的夹角，单位为弧度。

## 投影公式

设三维点在相机坐标系中为 $P=(X,Y,Z)$，光轴沿 $Z$ 轴，定义：
$$
\rho=\sqrt{X^2+Y^2},\qquad
\theta=\operatorname{atan2}(\rho,Z)
$$
其中 $\theta$ 是光线与光轴的夹角。

① 从角度得到成像平面坐标
F-theta 模型规定径向像距为：
$$
r=f\theta
$$
假设镜头绕光轴旋转对称，投影保持光线的方位角 $\varphi$，因此：
$$
\cos\varphi=\frac{X}{\rho},\qquad
\sin\varphi=\frac{Y}{\rho}
$$
将径向像距 $r$ 分解到图像平面的两个轴上：
$$
x=r\cos\varphi=f\theta\frac{X}{\rho}
$$
$$
y=r\sin\varphi=f\theta\frac{Y}{\rho}
$$
这里 $x,y,f$ 使用相同的物理长度单位。

② 从成像平面坐标转换为像素坐标
设横、纵方向的像素尺寸分别是 $s_x,s_y$，主点为 $(c_x,c_y)$。假设图像坐标轴与相机的 $X,Y$ 方向一致，且没有轴倾斜：
$$
u=c_x+\frac{x}{s_x},\qquad
v=c_y+\frac{y}{s_y}
$$
定义以像素为单位的焦距：
$$
f_x=\frac{f}{s_x},\qquad f_y=\frac{f}{s_y}
$$
代入即可得到：
$$
\boxed{
\begin{aligned}
u&=c_x+f_x\frac{\theta}{\rho}X\\
v&=c_y+f_y\frac{\theta}{\rho}Y
\end{aligned}
}
\qquad
\begin{aligned}
\rho&=\sqrt{X^2+Y^2}\\
\theta&=\operatorname{atan2}(\rho,Z)
\end{aligned}
$$

际标定时，常加入角度多项式畸变：
$$
\theta_d=\theta\left(1+k_1\theta^2+k_2\theta^4+k_3\theta^6+k_4\theta^8\right)
$$