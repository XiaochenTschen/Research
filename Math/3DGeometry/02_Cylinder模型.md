## 柱面模型基本概念

Cylinder（柱面）相机模型可以理解为：将空间射线投影到圆柱面，再把圆柱面展开成图像。

假设相机坐标系中 $X$ 向右、$Y$ 向下、$Z$ 向前，空间点为 $\mathbf P_c=(X,Y,Z)$。定义
$$
\theta=\operatorname{atan2}(X,Z),
\rho=\sqrt{X^2+Z^2}.
$$

## 投影公式推导

取一个半径为 $R$、轴线沿 $Y$ 方向的圆柱：
$
x^2+z^2=R^2.
$

从相机中心沿 $(X,Y,Z)$ 发出的射线与圆柱相交于
$$
\mathbf P_{\rm cyl}
=\frac{R}{\rho}(X,Y,Z).
$$

展开圆柱后，水平坐标是弧长 $R\theta$，垂直坐标是 $RY/\rho$。再乘以各方向的像素尺度 $s_x,s_y$，加上图像原点偏移：
$$
u=c_x+s_xR\theta,\qquad
v=c_y+s_yR\frac{Y}{\rho}.
$$

令 $f_x=s_xR,\ f_y=s_yR$，就得到投影公式
$$
u=c_x+f_x\theta,\qquad
v=c_y+f_y\frac{Y}{\rho}.
$$

## FOV

柱面模型的视角由内参和图像的有效范围共同决定。水平和垂直方向的计算方式不同。

由投影公式反解：
$$
\theta=\frac{u-c_x}{f_x},
\qquad
\frac{Y}{\rho}=\frac{v-c_y}{f_y},
\quad \rho=\sqrt{X^2+Z^2}.
$$

### 水平方向：像素位置与方位角成正比。

若图像左右边界为 $u_L,u_R$，则
$$
\theta_L=\frac{u_L-c_x}{f_x},\qquad
\theta_R=\frac{u_R-c_x}{f_x}.
$$
所以水平视场角为
$$
\boxed{\mathrm{HFOV}=\frac{u_R-u_L}{f_x}\approx\frac{W}{f_x}}
$$
结果单位是弧度。

### 垂直方向：像素位置与仰俯角的正切成正比

定义向下为正的仰俯角 $\alpha$，它是射线与水平面的夹角：
$$
\tan\alpha=\frac{Y}{\rho}.
$$
因此
$$
\alpha=\arctan\left(\frac{v-c_y}{f_y}\right).
$$
若上下边界为 \(v_T,v_B\)，则垂直视场角为
$$
\boxed{
\mathrm{VFOV}
=
\arctan\left(\frac{v_B-c_y}{f_y}\right)
-
\arctan\left(\frac{v_T-c_y}{f_y}\right)
}
$$
当主点位于图像中心时，可写成
$$
\boxed{\mathrm{VFOV}\approx2\arctan\left(\frac{H}{2f_y}\right)}.
$$