# poisson_freefem

ここではPoisson方程式をfreefemを使って解きます。

方程式を考える領域は

![poisson_boundary](https://user-images.githubusercontent.com/1296728/222932461-ba32a528-fe21-48fd-96c1-81fe190bf448.png)
のようにとります。

式で書くと

$$
\begin{eqnarray*}
\begin{array}{l}
\Gamma_1: x=t,y=0,\quad R_1 \le t \le R_2 \\
\Gamma_2: x=R_2 \cos t, y=R_2 \sin t, \quad 0 \le t \le \pi \\
\Gamma_3: x=t,y=0,\quad -R_2 \le t \le -R_1 \\
\Gamma_4: x=R_1 \cos t,y=R_1 \sin t,\quad -\pi \le t \le 0
\end{array}
\end{eqnarray*}
$$

freefemのコードに直すと

<img width="596" alt="boundary-freefem-code" src="https://user-images.githubusercontent.com/1296728/222932596-659617e2-38dc-4944-8e31-a1937d17cb68.png">

ここでnnは各部分境界の分割数です。境界の分割数を指定することによりメッシュの細かさを調整します。

このコードを少し直すと、メッシュ生成のコードになります

<img width="467" alt="mesh_freefem" src="https://user-images.githubusercontent.com/1296728/222932851-f5b3c612-4c59-4155-ae6f-ac50a8aeaaaf.png">

結果は

<img width="467" alt="mesh_freefem" src="https://user-images.githubusercontent.com/1296728/222932927-6885f8c9-6ea9-4093-9518-20d4ca90e574.png">
