---
layout: post
title:  "Quaternion and Skinning Notes"
date:   2020-04-22 11:40:00
categories: Algorithm
permalink: /archivers/quaternion-skinning

---

This article introduces quaternion, dual-quaternion and their applications in skinning area.

<!--more-->

# 1. Quaternion

​	[wiki](https://en.wikipedia.org/wiki/Quaternion)

- Definition

  $$\begin{equation} Q=q_{0}+q_{1} \mathbf{i}+q_{2} \mathbf{j}+q_{3} \mathbf{k} \quad q_{i} \in \mathbb{R}, i=0, \ldots, 3 \end{equation}$$

  $\mathbf{i} \cdot \mathbf{i}=\mathbf{j} \cdot \mathbf{j}=\mathbf{k} \cdot \mathbf{k}=\mathbf{i} \cdot \mathbf{j} \cdot \mathbf{k}=-1$

  $\mathbf{i} \cdot \mathbf{j}=-\mathbf{j} \cdot \mathbf{i}=\mathbf{k} \quad \mathbf{j} \cdot \mathbf{k}=-\mathbf{k} \cdot \mathbf{j}=\mathbf{i} \quad \mathbf{k} \cdot \mathbf{i}=-\mathbf{i} \cdot \mathbf{k}=\mathbf{j}$

- Conjugate, Norm and Inverse

  $Q=\left(q_{0}, \vec{q}\right)$

  $Q^{\star}=\left(q_{0},-\vec{q}\right)$

  $\|Q\|^{2}=Q \cdot Q^{\star}=q_{0}^{2}+q_{1}^{2}+q_{2}^{2}+q_{3}^{2}$

  $Q^{-1} = Q^{\star} /\|Q\|^{2}$

- Multiplication

  $Q \cdot P=\left(q_{0} p_{0}-\vec{q} \cdot \vec{p}, q_{0} \vec{p}+p_{0} \vec{q}+\vec{q} \times \vec{p}\right)$

- The norm is *multiplicative*

  $\|PQ\| = \|P\|\|Q\|$

- Unit Quaternion

  Given a rotation matrix $R=\exp (\widehat{\omega} \theta)$, the associated unit quaternion is

  $Q=(\cos (\theta / 2), \omega \sin (\theta / 2))$

- Rotation between A and C is given by 

  $Q_{a c}=Q_{a b} \cdot Q_{b c}$


- A quaternion $\mathbf{t}:= (t_xi+t_yj+t_zk)=(0, t_x,t_y,t_z)$ corresponds to vector $(t_x, t_y, t_z)$

- to rotation matrix for $\mathbf{q}^{\prime}=w+x i+y j+z k$

  $$
  \left[
  \begin{matrix}
  x^{2}+w^{2}-y^{2}-z^{2} & 2 x y-2 w z & 2 x z+2 w y \\ 
  2 x y+2 w z & y^{2}+w^{2}-x^{2}-z^{2} & 2 y z-2 w x \\
  2 x z-2 w y & 2 y z+2 w x & z^{2}+w^{2}-x^{2}-y^{2}
  \end{matrix}
  \right]
  $$

- Rotation, for unit quaternion

  $\mathbf{v}^{\prime} = \mathbf{q} \mathbf{v}\mathbf{q}^{\star}$, where $\mathbf{v} = (0, \vec{v})$

  

# 2. Dual Quaternion

​	[wiki](https://en.wikipedia.org/wiki/Dual_quaternion)

​	[reference paper](https://wenku.baidu.com/view/e361f52f7fd5360cbb1adb1a.html)

- Definition

  $$\hat{\mathbf{q}}=\mathbf{q}_{0}+\epsilon \mathbf{q}_{\epsilon}$$  where $\epsilon^2=0$

  if $\hat{\mathbf{q}}$ isunit dual quaternion, the rotation is just a matrix representation of $\mathbf{q_0}$ and the translation is given by the vector part of $2\mathbf{q}_{\epsilon}\mathbf{q}_0^{\star}$

- Multiplication

  $\left(a_{0}+\epsilon a_{\epsilon}\right)\left(b_{0}+\epsilon b_{\epsilon}\right)=a_{0} b_{0}+\epsilon\left(a_{0} b_{\epsilon}+a_{\epsilon} b_{0}\right)$

- Conjugation of a dual quaternion

  $$ \hat{\mathbf{q}}^{\star}=\mathbf{q}_{0}^{\star} + \epsilon\mathbf{q}_{\epsilon}^{\star} $$

- Norm and Inverse

  $$ \|\hat{\mathbf{q}}\|=\sqrt{\hat{\mathbf{q}}^{\star} \hat{\mathbf{q}}}=\left\|\mathbf{q}_{0}\right\|+\epsilon \frac{\left\langle\mathbf{q}_{0}, \mathbf{q}_{\epsilon}\right\rangle}{\left\|\mathbf{q}_{0}\right\|} $$

  $$\hat{\mathbf{q}}^{-1}=\frac{\hat{\mathbf{q}}^{\star}}{\|\hat{\mathbf{q}}\|^{2}}$$

  Unit dual quaternions are those satisfying $\|\hat{\mathbf{q}} \| = 1$, a dual quaternion $\hat{\mathbf{q}}$ is unit if and only if $$ \|\mathbf{q}_0 \|=1 $$ and $$ \left\langle\mathbf{q}_{0}, \mathbf{q}_{\epsilon}\right\rangle=0 $$ 

  The norm is *multiplicative* $\|\hat{\mathbf{p}} \hat{\mathbf{q}}\|=\|\hat{\mathbf{p}}\|\|\hat{\mathbf{q}}\|$

  **Note that unit dual quaternions are always invertible (their inverse is just conjugation).** Just like ordinary quaternions, dual quaternions are also associative, distributive, but not commutative.

- convert a 3D vector $(v_1, v_2, v_3)$ to a unit dual quaternion

  $\hat{\mathbf{v}}=1+\epsilon(v_1i+v_2j+v_3k)$

- A unit dual quaternion $\hat{\mathbf{t}}:= 1 + \frac{\epsilon}{2}(t_xi+t_yj+t_zk)$ corresponds to translation by vector $(t_x, t_y, t_z)$

- Dual-Quaternion from Rotation and Translation

  - given a (dual) quaternion represents rotaion $\mathbf{q}_0$
  - and a quaternion represents translation $\mathbf{t}:= (t_xi+t_yj+t_zk)=(0, t_x,t_y,t_z)$
  - $$\hat{\mathbf{q}}=\hat{\mathbf{t}}\mathbf{q}_0=\left(1+\frac{\epsilon}{2}\left(t_{x} i+t_{y} j+t_{z} k\right)\right) \mathbf{q}_{0}=\mathbf{q}_{0}+\frac{\epsilon}{2}\left(t_{x} i+t_{y} j+t_{z} k\right) \mathbf{q}_{0}=\mathbf{q}_{0}+\frac{\epsilon}{2} \mathbf{t}\mathbf{q}_{0}$$
  
- Transformation

  $\hat{v}^{\prime}=\hat{\mathbf{q}} \cdot \hat{v} \cdot \bar{\hat{\mathbf{q}}^{\star}}$

  **pay attention that** $$\bar{\hat{\mathbf{q}}^{\star}}=\mathbf{q}_{0}^{\star} - \epsilon \mathbf{q}_{\epsilon}^{\star}$$

# 3. SBS

*Spherical blend skinning: A real-time deformation of articulated models*

- Center of Rotation $\mathbf{r}_c$

  it is possible to define the rotation center as the point whose transformations by associated matrices are as close as possible. This minimizes the drift and works even if the vertex is assigned to $n$ joints $j_1,\cdots, j_n$. We find the center of rotation $\mathbf{r}_c$ as the least-squares solution of the system of $\left(\begin{array}{l}n \\ 2\end{array}\right)$ linear vector equations.

    $$C_{a} \mathbf{r}_{c}=C_{b} \mathbf{r}_{c}, a<b, a, b \in\left\{j_{1}, \ldots, j_{n}\right\}$$

  $$
  C_{i}=\left[\begin{matrix}C_{i}^{r o t} & \mathbf{C}_{i}^{t r} \\ \mathbf{0}^{T} & 1\end{matrix}\right]
  $$

  $$
  \begin{aligned}
C_{a}^{r o t} \mathbf{r}_{c}+\mathbf{C}_{a}^{r} &=C_{b}^{r o t} \mathbf{r}_{c}+\mathbf{C}_{b}^{t r} \\\left(C_{a}^{r o t}-C_{b}^{r o t}\right) \mathbf{r}_{c} &=\mathbf{C}_{b}^{t r}-\mathbf{C}_{a}^{t r} \end{aligned}
  $$

  If we stack all these equations to one matrix $D$ and the right-hand sides to vector $\mathbf{e}$, we can write the whole system as $D \mathbf{r}_{c}=\mathbf{e}$, where $D$ is a $3\left(\begin{array}{l}n \\ 2\end{array}\right) \times 3$ matrix. Just solve this equation and get $\mathbf{r}_c$.

- **QLERP** is good enough though it is inferior than **SLERP**

  $$
  q\left(W ; C_{j_{1}}, \ldots, C_{j_{n}}\right)=\left[\begin{matrix}Q & \mathbf{m} \\ \mathbf{0}^{T} & 1\end{matrix}\right]
  $$

  the rotation submatrices $C_{j_i}^{rot}$ are converted to quaternions $\mathbf{q}_{j_i}$

  $$\mathbf{s}_{n}=\frac{\mathbf{s}}{\|\mathbf{s}\|}$$ , where $$\mathbf{s}=w_{1} \mathbf{q}_{j_{1}}+\ldots+w_{n} \mathbf{q}_{j_{n}}$$,  $$\mathbf{s}_{n}$$ is converted to the rotation matrix $$Q$$

  $$\mathbf{m}=\sum_{i=1}^{n} w_{i} \mathbf{C}_{j_{i}}^{t r}$$
  
  $$
  T=\left[\begin{matrix}I & \mathbf{r}_{c} \\ \mathbf{0}^{T} & 1\end{matrix}\right]
  $$
  
  $$
  \begin{aligned}\mathbf{v}^{\prime}=&T q\left(W ; T^{-1} C_{j_{1}} T, \ldots, T^{-1} C_{j_{n}} T\right) T^{-1} \mathbf{v}\\
  =&Q\left(\mathbf{v}-\mathbf{r}_{c}\right)+\sum_{i=1}^{n} w_{i} C_{j_{i}} \mathbf{r}_{c}
  \end{aligned}
  $$

# 4. DQS

  *Skinning with dual quaternions*

- Dual quaternion Linear Blending

  $$\begin{equation} D L B\left(\mathbf{w} ; \hat{\mathbf{q}}_{1}, \ldots, \hat{\mathbf{q}}_{n}\right)=\frac{w_{1} \hat{\mathbf{q}}_{1}+\ldots+w_{n} \hat{\mathbf{q}}_{n}}{\left\|w_{1} \hat{\mathbf{q}}_{1}+\ldots+w_{n} \hat{\mathbf{q}}_{n}\right\|} \end{equation}$$

- Algorithm

  **Input:** dual quaternions $\hat{\mathbf{q}}_{1}, \ldots, \hat{\mathbf{q}}_{p}$ (unifrom parameters)

  ​			vertex position $\mathbf{v}$ and normal $\mathbf{v}_n$

  ​			joints indices $j_{1}, \ldots, j_{n}$ and weights  $w_{1}, \ldots, w_{n}$

  **output:** transformed vertex position $\mathbf{v}^{\prime}$ and normal $\mathbf{v}_n^{\prime}$

  ​	$$\hat{\mathbf{b}}=w_{1} \hat{\mathbf{q}}_{j_{1}}+\ldots+w_{n} \hat{\mathbf{q}}_{j_{n}}$$

  ​	// denote the non-dual part of $\hat{\mathbf{b}}$ as $$\hat{\mathbf{b}}_0$$ and the dual one as $$\hat{\mathbf{b}}_{\epsilon}$$ 

  ​	$$\mathbf{c}_{0}=\mathbf{b}_{0} /\left\|\mathbf{b}_{0}\right\|$$
  
  ​	$$\mathbf{c}_{\epsilon}=\mathbf{b}_{\epsilon} /\left\|\mathbf{b}_{0}\right\|$$
  
  ​	// denote the components of $\mathbf{c}_0$ as $w_0, x_0, y_0, z_0$
  
  ​	// denote the components of $$\mathbf{c}_{\epsilon}$$ as $$w_{\epsilon}, x_{\epsilon}, y_{\epsilon}, z_{\epsilon}$$
  
    ​	$t_{0}=2\left(-w_{\epsilon} x_{0}+x_{\epsilon} w_{0}-y_{\epsilon} z_{0}+z_{\epsilon} y_{0}\right)$  
  
    ​	$t_{1}=2\left(-w_{\epsilon} y_{0}+x_{\epsilon} z_{0}+y_{\epsilon} w_{0}-z_{\epsilon} x_{0}\right)$  
  
    ​	$t_{2}=2\left(-w_{\epsilon} z_{0}-x_{\epsilon} y_{0}+y_{\epsilon} x_{0}+z_{\epsilon} w_{0}\right)$				

​			$$ M=\left[\begin{matrix}1-2 y_{0}^{2}-2 z_{0}^{2} & 2 x_{0} y_{0}-2 w_{0} z_{0} & 2 x_{0} z_{0}+2 w_{0} y_{0} & t_{0} \\ 2 x_{0} y_{0}+2 w_{0} z_{0} & 1-2 x_{0}^{2}-2 z_{0}^{2} & 2 y_{0} z_{0}-2 w_{0} x_{0} & t_{1} \\ 2 x_{0} z_{0}-2 w_{0} y_{0} & 2 y_{0} z_{0}+2 w_{0} x_{0} & 1-2 x_{0}^{2}-2 y_{0}^{2} & t_{2}\end{matrix}\right] $$

​			$\mathbf{v}^{\prime}=M \mathbf{v}$ where $\mathbf{v}$ has form $\mathbf{v} = (v_0, v_1, v_2, 1)$

​			$$\mathbf{v}_n^{\prime}=M \mathbf{v}_n$$ where $$\mathbf{v}$$ has form $$\mathbf{v}_n = (v_{n,0}, v_{n,1}, v_{n,2}, 1)$$

​			Note that the formulas for $t_0, t_1, t_2$ are simply the expanded forms of quaternion product $2\mathbf{c}_{\epsilon}\mathbf{c}_0^\star$


