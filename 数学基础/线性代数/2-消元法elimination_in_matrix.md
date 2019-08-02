# 2.消元法（elimination in matrix）

1. ## 消元法：

   将矩阵A，通过逐行消元，最后形成上三角矩阵U

2. ## 矩阵乘法：

   预备知识：

   - Tips1:

     row exchange < —— > left matrix mulplification
     $$
     \begin{bmatrix}
     0 & 1 \\ 1 & 0
     \end{bmatrix}
     \begin{bmatrix}
     a & b \\ c & d
     \end{bmatrix} = 
     \begin{bmatrix}
     c & d \\ a & b
     \end{bmatrix}
     $$
     Column exchange < —— > right matrix mulplification
     $$
     \begin{bmatrix}a & b \\ c & d\end{bmatrix}\begin{bmatrix}0 & 1 \\ 1 & 0\end{bmatrix} = \begin{bmatrix}b & a \\ d & c\end{bmatrix}
     $$

   - Tips2:

     $$AB=C$$

     $$C_{i,j}=A.row_{i}B.col_{j}$$

     Or:

     $$AB=\sum{(col(A_{i})·row(B_{j}))}$$

     Or: by Block
     $$
     \begin{Bmatrix}
     A_{1} &|& A_{2} \\
     \hline
     A_{4}  &|& A_{4}
     \end{Bmatrix}·
     \begin{Bmatrix}
     B_{1} &|& B_{2} \\
     \hline
     B_{3}  &|& B_{4}
     \end{Bmatrix}=
     \begin{Bmatrix}
     A_{1}B_{1}+A_{2}B_{3} &|& ... \\
     \hline
     ...  &|& ...
     \end{Bmatrix}
     $$

