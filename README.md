# poisson_freefem

ここではPoisson方程式をfreefemを使って解きます。

# メッシュ生成

方程式を考える領域は

![poisson_boundary](https://user-images.githubusercontent.com/1296728/222933369-2fc3b7a6-62c3-474f-97f4-89d783ac4d40.png)
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

<img width="583" alt="mesh_freefem" src="https://user-images.githubusercontent.com/1296728/222933424-e811270d-1d0d-4c02-a780-f883d43c41d1.png">

ここでnnは各部分境界の分割数です。境界の分割数を指定することによりメッシュの細かさを調整します。

このコードを少し直すと、メッシュ生成のコードになります

<img width="481" alt="mesh_freefem" src="https://user-images.githubusercontent.com/1296728/222933468-e03bf551-a070-4c9b-b558-defaefe93f86.png">

結果は

![poisson_mesh](https://user-images.githubusercontent.com/1296728/222933531-0d1f2ea1-4e5f-436c-aac8-8e025c19a44e.png)

# freefemによるPoisson方程式の数値解の計算

上で設定した領域でPoison方程式の近似解を求めます。以下の方程式を考えます。

$$
-\Delta u = f
$$

境界条件は

$$
\frac{\partial}{\partial n}u=0 \quad {\rm on }  \Gamma_1 \cup \Gamma_2 \cup \Gamma_3 \cup \Gamma_4
$$

方程式に関数を掛けて積分して弱形式にします。

$$
-\int_\Omega \Delta u v dx = \int_\Omega f v dx
$$

左辺を部分積分します

$$
-\int_\Omega \Delta u(x) v(x) dx=-\int_{\partial \Omega}\frac{\partial u}{\partial n}(x)v(x)d\sigma+\int_\Omega \nabla u\cdot \nabla v dx
$$

$\partial\Omega$ では法線方向微分は $0$ なので

$$
-\int_\Omega \Delta u(x) v(x) dx = \int_\Omega \nabla u\cdot \nabla v dx
$$

これを使って方程式を書き直すと

$$
\int_\Omega \nabla u\cdot \nabla v dx  - \int_\Omega f v dx = 0
$$

これを参考にしてfreefemのコードを書きます

<img width="470" alt="Poisson-solver-freefem" src="https://user-images.githubusercontent.com/1296728/222936413-e237f212-9915-4b96-bbfe-e762f73c711c.png">

１６行目ではメッシュ=Th上に区分1時の有限要素空間をつくります。次の行でその中の関数u,vを定義します。f=x*yは関数ｆの定義です。

２１行目は弱形式の方程式のfreefemの記法による記述です。solveはこの式を元にして数値計算を行う命令です。

結果は以下のとおりです

<img width="470" alt="Poisson-solver-freefem" src="https://user-images.githubusercontent.com/1296728/222937161-98d84c4f-5f77-4d5f-a254-9c5633fd4c00.png">

