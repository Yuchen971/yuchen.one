alias:: 行列式

- 矩阵对应的线性变换前后有向面积(体积)的比例 (可以为负)
- 如果矩阵的列线性相关, 行列式等于0
- $$
  \operatorname{det}\left(\left[\begin{array}{ll}
  a & b \\
  c & d
  \end{array}\right]\right)=a d-b c
  $$
- $$
  \begin{aligned}
  \operatorname{det}\left(\left[\begin{array}{lll}
  a & b & c \\
  d & e & f \\
  g & h & i
  \end{array}\right]\right) &=a \operatorname{det}\left(\left[\begin{array}{ll}
  e & f \\
  h & i
  \end{array}\right]\right) \\
  &-b \operatorname{det}\left(\left[\begin{array}{ll}
  d & f \\
  g & i
  \end{array}\right]\right) \\
  &+c \operatorname{det}\left(\left[\begin{array}{ll}
  d & e \\
  g & h
  \end{array}\right]\right)
  \end{aligned}
  $$