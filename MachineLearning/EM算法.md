# EM算法

## 背景

​		EM算法主要应用于具有隐变量的混合模型的参数估计，对于简单的问题，可以直接使用MLE算法求出解析解。但是对于混合模型来讲，直接求解析解是非常困难的，比如在GMM中很难求解。因此需要引入EM算法来解决这些问题。

​		也就是说对于传统的最大似然分布来说，如果不知道x的分布很难对其进行求解，**但是如果我们通过引入隐变量z，假设x服从某个分布，并在迭代中不断逼近该分布（$p_z$）以及该分布的参数（$\mu,\Sigma$），从而实现对参数的估计。**

## 公式及其推导

EM算法公式：

![image-20230222231424167](C:\Users\Go\AppData\Roaming\Typora\typora-user-images\image-20230222231424167.png)

推导：

​		根据贝叶斯公式得到下列等式，并引入分布q(z):

![image-20230222234256152](C:\Users\Go\AppData\Roaming\Typora\typora-user-images\image-20230222234256152.png)

![image-20230222234310350](C:\Users\Go\AppData\Roaming\Typora\typora-user-images\image-20230222234310350.png)

​		由于相对熵KL$\ge0$,当p和q分布相同时取等号，所以我们在这里令$q(z)=P(z|x,\theta)$,所以$logP(x|\theta)\ge ELBO$.

​		因此我们可以对其进行最大似然估计：

![image-20230222234953828](C:\Users\Go\AppData\Roaming\Typora\typora-user-images\image-20230222234953828.png)

​		因此EM算法的过程实际上就是先给定一个初始参数$\theta_0,\theta=(p_z,\mu,\Sigma)$,求出期望ELBO，然后在这个期望上进行滑动，找到下一个$\theta_1$使得期望最大，之后用$\theta_1$代替原参数求期望，循环往复，直到找到使$logP(x|\theta)$最大的参数。

​		如果我们比较一下EM算法的公式以及最大似然估计的公式，我们就会发现EM算法实际上就是多引入了一个隐变量z，使得数据x的未知复杂分布可以通过调整隐变量z的概率分布来逼近。

## 广义EM及其变种





