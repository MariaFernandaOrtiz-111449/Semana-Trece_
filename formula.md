$$
\begin{bmatrix} 
\hat{x}_1 \\ 
\hat{x}_2 \\ 
\vdots \\ 
\hat{x}_n \\ 
\hat{\xi} \\ 
\hat{\xi}^{(1)} \\ 
\vdots \\ 
\hat{\xi}^{(m-1)} 
\end{bmatrix} 
= 
\underbrace{
\begin{bmatrix} 
0_{n+m \times 1} & I_{n+m-1 \times n+m-1} \\ 
0 & 0_{1 \times n+m-1} 
\end{bmatrix}
}_{A_\xi} 
\begin{bmatrix} 
\hat{x}_1 \\ 
\hat{x}_2 \\ 
\vdots \\ 
\hat{x}_n \\ 
\hat{\xi} \\ 
\hat{\xi}^{(1)} \\ 
\vdots \\ 
\hat{\xi}^{(m-1)} 
\end{bmatrix} 
+ 
\underbrace{
\begin{bmatrix} 
0 \\ 
0 \\ 
\vdots \\ 
1 \\ 
0 \\ 
\vdots \\ 
0 
\end{bmatrix}
}_{B_\xi} 
u 
+ 
\underbrace{
\begin{bmatrix} 
\lambda_{n+m-1} \\ 
\lambda_{n+m-2} \\ 
\vdots \\ 
\lambda_{m+1} \\ 
\lambda_m \\ 
\lambda_{m-1} \\ 
\vdots \\ 
\lambda_0 
\end{bmatrix}
}_{\lambda_\xi} 
\tilde{e}_y(t)
$$

$$
\hat{y} = 
\begin{bmatrix} 
1 & 0 & 0 & \cdots & 0 
\end{bmatrix} 
\hat{x}_\xi
$$
