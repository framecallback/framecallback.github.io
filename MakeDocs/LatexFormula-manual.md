# Latex公式手册

## 参考

* https://www.zybuluo.com/codeep/note/163962 Cmd Markdown 公式指导手册
* https://www.cnblogs.com/1024th/p/11623258.html LaTex公式手册

## 工具

* https://webdemo.myscript.com/views/math/index.html 鼠标写公式自动识别
* http://www.hostmath.com/ 在线Latex公式编辑器, 简洁
* https://www.codecogs.com/latex/eqneditor.php 在线Latex公式编辑器, 可以生成图片
* https://math.edrawsoft.cn/index.html 在线像MathType一样编辑公式再复制Latex
* https://mathpix.com/ 根据图片识别公式生成Latex(linux下安装不了, 网页版也不好用)

## 如何插入公式

* 行内插入: `$xxx$`
    哈哈$x=2y$哈哈
* 行间插入(`$$xxx$$`): 
```
$$
xxxxxxx
$$
```
$$
x=2y
$$

## 公式行标
* 在每个公式末尾前使用`\tag{行标}`来实现行标。
```latex
y=3x \tag{行标3-1}
```
$$
y=3x \tag{行标3-1}
$$

## 函数、符号及特殊字符

### 上下标
* `^`表示上标，`_`表示下标, 如果上下标的内容多于一个字符，需要用 {} 将这些内容括成一个整体。上下标可以嵌套，也可以同时使用。
`x^{y^z}=(1+{\rm e}^x)^{-2xy^w}`:$x^{y^z}=(1+{\rm e}^x)^{-2xy^w}$
* 左右两边都有上下标，可以用 \sideset 命令:
`\sideset{^1_2}{^3_4}\bigotimes`:$\sideset{^1_2}{^3_4}\bigotimes$

### 括号，分隔符
* ()、[] 和 | 表示符号本身，使用 \{\} 来表示 {} 。
`(), [], |`:$(), [], |$
* 使用`\left`和`\right`来创建自动匹配高度的 (圆括号)，[方括号] 和 {花括号} 。
`\left(, \right), \left\{, \right\}`:$\left(, \right), \left\{, \right\}$
* 有时候要用 \left. 或 \right. 进行匹配而不显示本身:
`\left. \frac{{\rm d}u}{{\rm d}x} \right. | _{x=0}`:$\left. \frac{{\rm d}u}{{\rm d}x} \right. | _{x=0}$
* 公式中间需要使用大分隔符，可以用`\middle`:
```latex
\left\langle  
  q
\middle\|
  \frac{\frac{x}{y}}{\frac{u}{v}}
\middle| 
   p 
\right\rangle
```
$$
\left\langle  
  q
\middle\|
  \frac{\frac{x}{y}}{\frac{u}{v}}
\middle| 
   p 
\right\rangle
$$

### 文字注释
* 公式中使用`\text{文字}`来插入注释。在`\text {文字}`中仍可以使用`$公式$`插入其它公式，docsify要使用`\$公式\$`。
```latex
f(n)= \begin{cases}
n/2, & \text {if $n$ is even} \\
3n+1, & \text{if $n$ is odd}
\end{cases}
```
$$
f(n)= \begin{cases}
n/2, & \text {if \$n\$ is even} \\
3n+1, & \text{if \$n\$ is odd}
\end{cases}
$$

### 空格
* 在字符间加入空格，有四种宽度的空格可以使用： `\,`、`\;`、`\quad` 和 `\qquad`。
```latex
a \, b \mid a \; b \mid a \quad b \mid a \qquad b
```
$$
a \, b \mid a \; b \mid a \quad b \mid a \qquad b
$$
* 使用`\text {n个空格}`也可以达到同样效果。

### 删除线
* 使用删除线功能必须声明 $$ 符号。
* 在公式内使用 \require{cancel} 来允许 片段删除线 的显示。
* 声明片段删除线后，使用 \cancel{字符}、\bcancel{字符}、\xcancel{字符} 和 \cancelto{字符} 来实现各种片段删除线效果。
```latex
\require{cancel}\begin{array}{rl}
\verb|y+\cancel{x}| & y+\cancel{x}\\
\verb|\cancel{y+x}| & \cancel{y+x}\\
\verb|y+\bcancel{x}| & y+\bcancel{x}\\
\verb|y+\xcancel{x}| & y+\xcancel{x}\\
\verb|y+\cancelto{0}{x}| & y+\cancelto{0}{x}\\
\verb+\frac{1\cancel9}{\cancel95} = \frac15+& \frac{1\cancel9}{\cancel95} = \frac15 \\
\end{array}
```
$$
\require{cancel}\begin{array}{rl}
\verb|y+\cancel{x}| & y+\cancel{x}\\
\verb|\cancel{y+x}| & \cancel{y+x}\\
\verb|y+\bcancel{x}| & y+\bcancel{x}\\
\verb|y+\xcancel{x}| & y+\xcancel{x}\\
\verb|y+\cancelto{0}{x}| & y+\cancelto{0}{x}\\
\verb+\frac{1\cancel9}{\cancel95} = \frac15+& \frac{1\cancel9}{\cancel95} = \frac15 \\
\end{array}
$$

* 使用`\require{enclose}`来允许 整段删除线 的显示。
* 声明整段删除线后，使用`\enclose{删除线效果}{字符}`来实现各种整段删除线效果。
* 删除线效果有 horizontalstrike、verticalstrike、updiagonalstrike 和 downdiagonalstrike，可叠加使用。
* 此外，`\enclose`命令还可以产生包围的边框和圆等，参见 MathML Menclose Documentation 以查看更多效果。
```latex
\require{enclose}\begin{array}{rl}
\verb|\enclose{horizontalstrike}{x+y}| & \enclose{horizontalstrike}{x+y}\\
\verb|\enclose{verticalstrike}{\frac xy}| & \enclose{verticalstrike}{\frac xy}\\
\verb|\enclose{updiagonalstrike}{x+y}| & \enclose{updiagonalstrike}{x+y}\\
\verb|\enclose{downdiagonalstrike}{x+y}| & \enclose{downdiagonalstrike}{x+y}\\
\verb|\enclose{horizontalstrike,updiagonalstrike}{x+y}| & \enclose{horizontalstrike,updiagonalstrike}{x+y}\\
\end{array}
```
$$
\require{enclose}\begin{array}{rl}
\verb|\enclose{horizontalstrike}{x+y}| & \enclose{horizontalstrike}{x+y}\\
\verb|\enclose{verticalstrike}{\frac xy}| & \enclose{verticalstrike}{\frac xy}\\
\verb|\enclose{updiagonalstrike}{x+y}| & \enclose{updiagonalstrike}{x+y}\\
\verb|\enclose{downdiagonalstrike}{x+y}| & \enclose{downdiagonalstrike}{x+y}\\
\verb|\enclose{horizontalstrike,updiagonalstrike}{x+y}| & \enclose{horizontalstrike,updiagonalstrike}{x+y}\\
\end{array}
$$

### 分数
* 通常使用`\frac {分子} {分母}`命令产生一个分数，分数可嵌套: `\frac{a-1}{a+1}`生成$\frac{a-1}{a+1}$
* 便捷情况可直接输入 `\frac ab` 来快速生成一个$\frac ab$
* 如果分式很复杂，亦可使用`分子 \over 分母`命令，此时分数仅有一层: `{a-1 \over a+1}`生成${a-1 \over a+1}$

### 矢量
* 使用`\vec{矢量}`来自动产生一个矢量: `\vec{a} \cdot \vec{b}=0`生成
$$
\vec{a} \cdot \vec{b}=0
$$
* 也可以使用`\overrightarrow`等命令自定义字母上方的符号。`\overleftarrow{xy} \quad and \quad \overleftrightarrow{xy} \quad and \quad \overrightarrow{xy}`生成
$$
\overleftarrow{xy} \quad and \quad \overleftrightarrow{xy} \quad and \quad \overrightarrow{xy}
$$

### 积分
* `\int_积分下限^积分上限 {被积表达式}`来输入一个积分。`\int_0^1 {x^2} \,{\rm d}x`生成$\int_0^1 {x^2} \,{\rm d}x$

### 极限
* 使用`\lim_{变量 \to 表达式} 表达式`来输入一个极限。如有需求，可以更改`\to`符号至任意符号。
`\lim_{n \to +\infty} \frac{1}{n(n+1)} \quad and \quad \lim_{x\leftarrow{示例}} \frac{1}{n(n+1)}`生成
$$
\lim_{n \to +\infty} \frac{1}{n(n+1)} \quad and \quad \lim_{x\leftarrow{示例}} \frac{1}{n(n+1)}
$$

### 累加、累乘、并集和交集
* 使用`\sum_{下标表达式}^{上标表达式} {累加表达式}`来输入一个累加。`\sum_{i=1}^n \frac{1}{i^2}`生成$\sum_{i=1}^n \frac{1}{i^2}$
* 使用 \prod \bigcup \bigcap 来分别输入累乘、并集和交集。

### 希腊字母
* 输入`\小写希腊字母英文全称`和`\首字母大写希腊字母英文全称`来分别输入小写和大写希腊字母。对于大写希腊字母与英文字母相同的，直接输入大写英文字母即可。
| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| \alpha | $\alpha$ | A | $A$ | \beta | $\beta$ | B | $B$ |
| \gamma | $\gamma$ | \Gamma | $\Gamma$ | \delta | $\delta$ | \Delta | $\Delta$ |
| \epsilon | $\epsilon$ | E | $E$ | \zeta | $\zeta$ | Z | $Z$ |
| \eta | $\eta$ | H | $H$ | \theta | $\theta$ | \Theta | $\Theta$ |
| \iota | $\iota$ | I | $I$ | \kappa | $\kappa$ | K | $K$ |
| \lambda | $\lambda$ | \Lambda | $\Lambda$ | \mu | $\mu$ | M | $M$ |
| \nu | $\nu$ | N | $N$ | \xi | $\xi$ | \Xi | $\Xi$ |
| o | $o$ | O | $O$ | \pi | $\pi$ | \Pi | $\Pi$ |
| \rho | $\rho$ | P | $P$ | \sigma | $\sigma$ | \Sigma | $\Sigma$ |
| \tau | $\tau$ | T | $T$ | \upsilon | $\upsilon$ | \Upsilon | $\Upsilon$ |
| \phi | $\phi$ | \Phi | $\Phi$ | \chi | $\chi$ | X | $X$ |
| \psi | $\psi$ | \Psi | $\Psi$ | \omega | $\omega$ | \Omega | $\Omega$ |
部分字母有变量专用形式，以 \var- 开头。
| 小写形式|大写形式|变量形式|显示|
| :---: | :---: | :---: | :---: |
| \epsilon | E | \varepsilon | $\epsilon | E | \varepsilon$ |
| \theta | \Theta | \vartheta | $ \theta | \Theta | \vartheta $ |
| \rho | P | \varrho | $\rho | P | \varrho $ |
| \sigma | \Sigma | \varsigma | $ \sigma | \Sigma | \varsigma $ |
| \phi | \Phi | \varphi | $ \phi | \Phi | \varphi $ |

### 指数与对数
* `\exp_a b = a^b, \exp b = e^b, 10^m`: $\exp_a b = a^b, \exp b = e^b, 10^m$
* `\ln c, \lg d = \log e, \log_{10} f`: $\ln c, \lg d = \log e, \log_{10} f$

### 三角函数

* `\sin a, \cos b, \tan c, \cot d, \sec e, \csc f`: $\sin a, \cos b, \tan c, \cot d, \sec e, \csc f$
* `\arcsin a, \arccos b, \arctan c`: $\arcsin a, \arccos b, \arctan c$
* `\arccot d, \arcsec e, \arccsc f`: $\arccot d, \arcsec e, \arccsc f$（这行不行就看下一行用`\operatorname{xxx}a`
* `\arccot d, \arcsec e, \arccsc f`: $\operatorname{arccot}d, \operatorname{arcsec}e, \operatorname{arccsc}f$
* `\sinh a, \cosh b, \tanh c, \coth d`: $\sinh a, \cosh b, \tanh c, \coth d$
* `\operatorname{sh}k, \operatorname{ch}l, \operatorname{th}m, \operatorname{coth}n`: $\operatorname{sh}k, \operatorname{ch}l, \operatorname{th}m, \operatorname{coth}n$
* `\operatorname{argsh}o, \operatorname{argch}p, \operatorname{argth}q`: $\operatorname{argsh}o, \operatorname{argch}p, \operatorname{argth}q$

### 符号与绝对值

* `\sgn r, \operatorname{sgn}s`:  $\sgn r, \operatorname{sgn}s$

* `|t|, \left\vert u \right\vert`: $|t|, \left\vert u \right\vert$

### 极值，界限，极限

* `\min(x,y), \max(x,y)`: $\min(x,y), \max(x,y)$

* `\min x, \max y, \inf s, \sup t`: $\min x, \max y, \inf s, \sup t$
* `\lim u, \liminf v, \limsup w`: $\lim u, \liminf v, \limsup w$
* `\lim_{x \to \infty} \frac{1}{n(n+1)}`: $\lim_{x \to \infty} \frac{1}{n(n+1)}$ (这个Typora渲染好像有问题)
* `\dim p, \deg q, \det m, \ker\phi`: $\dim p, \deg q, \det m, \ker\phi$

### 投射

* `\Pr j, \hom l, \lVert z \rVert, \arg z`: $\Pr j, \hom l, \lVert z \rVert, \arg z$

### 微分及导数

* `dt, \mathrm{d}t, \partial t, \nabla\psi`: $dt, \mathrm{d}t, \partial t, \nabla\psi$

* `dy/dx, \mathrm{d}y/\mathrm{d}x, \frac{dy}{dx}, \frac{\mathrm{d}y}{\mathrm{d}x}, \frac{\partial^2}{\partial x_1\partial x_2}y`: $dy/dx, \mathrm{d}y/\mathrm{d}x, \frac{dy}{dx}, \frac{\mathrm{d}y}{\mathrm{d}x}, \frac{\partial^2}{\partial x_1\partial x_2}y$
* `\prime, \backprime, f^\prime, f', f'', f^{(3)}, \dot y, \ddot y`: $\prime, \backprime, f^\prime, f', f'', f^{(3)}, \dot y, \ddot y$

### 类字母符号及常数

* `\infty, \aleph, \complement, \backepsilon, \eth, \Finv, \hbar`:$\infty, \aleph, \complement, \backepsilon, \eth, \Finv, \hbar$
* `\Im, \imath, \jmath, \Bbbk, \ell, \mho, \wp, \Re, \circledS`:$\Im, \imath, \jmath, \Bbbk, \ell, \mho, \wp, \Re, \circledS$

### 模运算

* `s_k \equiv 0 \pmod{m}`: $s_k \equiv 0 \pmod{m}$
* `a \bmod b`: $a \bmod b$
* `\gcd(m, n), \operatorname{lcm}(m, n)`: $\gcd(m, n), \operatorname{lcm}(m, n)$
* `\mid, \nmid, \shortmid, \nshortmid`: $\mid, \nmid, \shortmid, \nshortmid$

### 运算符

* `\surd, \sqrt{2}, \sqrt[n]{}, \sqrt[3]{\frac{x^3+y^3}{2}}`: $\surd, \sqrt{2}, \sqrt[n]{}, \sqrt[3]{\frac{x^3+y^3}{2}}$
* `+, -, \pm, \mp, \dotplus`: $+, -, \pm, \mp, \dotplus$
* `\times, \div, \divideontimes, /, \backslash`: $\times, \div, \divideontimes, /, \backslash$
* `\cdot, * \ast, \star, \circ, \bullet`: $\cdot, * \ast, \star, \circ, \bullet$
* `\boxplus, \boxminus, \boxtimes, \boxdot`: $\boxplus, \boxminus, \boxtimes, \boxdot$
* `\oplus, \ominus, \otimes, \oslash, \odot`: $\oplus, \ominus, \otimes, \oslash, \odot$
* `\circleddash, \circledcirc, \circledast`: $\circleddash, \circledcirc, \circledast$
* `\bigoplus, \bigotimes, \bigodot`: $\bigoplus, \bigotimes, \bigodot$

### 集合

* `\{ \}, \emptyset, \varnothing`: $\{ \}, \emptyset, \varnothing$
* `\in, \notin, \not\in, \ni, \not\ni`: $\in, \notin, \not\in, \ni, \not\ni$
* `\cap, \Cap, \sqcap, \bigcap`: $\cap, \Cap, \sqcap, \bigcap$
* `\cup, \Cup, \sqcup, \bigcup, \bigsqcup, \uplus, \biguplus`: $\cup, \Cup, \sqcup, \bigcup, \bigsqcup, \uplus, \biguplus$
* `\setminus, \smallsetminus, \times`: $\setminus, \smallsetminus, \times$
* `\subset, \Subset, \sqsubset`: $\subset, \Subset, \sqsubset$
* `\supset, \Supset, \sqsupset`: $\supset, \Supset, \sqsupset$
* `\subseteq, \nsubseteq, \subsetneq, \varsubsetneq, \sqsubseteq`: $\subseteq, \nsubseteq, \subsetneq, \varsubsetneq, \sqsubseteq$
* `\supseteq, \nsupseteq, \supsetneq, \varsupsetneq, \sqsupseteq`: $\supseteq, \nsupseteq, \supsetneq, \varsupsetneq, \sqsupseteq$
* `\subseteqq, \nsubseteqq, \subsetneqq, \varsubsetneqq`: $\subseteqq, \nsubseteqq, \subsetneqq, \varsubsetneqq$
* `\supseteqq, \nsupseteqq, \supsetneqq, \varsupsetneqq`: $\supseteqq, \nsupseteqq, \supsetneqq, \varsupsetneqq$

### 关系运算符

* `=, \ne, \neq, \equiv, \not\equiv`: $=, \ne, \neq, \equiv, \not\equiv$
* `\doteq, \doteqdot, \overset{\underset{\mathrm{def}}{}}{=}, :=`: $\doteq, \doteqdot, \overset{\underset{\mathrm{def}}{}}{=}, :=$
* `\eqcirc \circeq \triangleq \bumpeq \Bumpeq \doteqdot \risingdotseq \fallingdotseq`:$\eqcirc \circeq \triangleq \bumpeq \Bumpeq \doteqdot \risingdotseq \fallingdotseq$
* `\sim, \nsim, \backsim, \thicksim, \simeq, \backsimeq, \eqsim, \cong, \ncong`: $\sim, \nsim, \backsim, \thicksim, \simeq, \backsimeq, \eqsim, \cong, \ncong$
* `\approx, \thickapprox, \approxeq, \asymp, \propto, \varpropto`: $\approx, \thickapprox, \approxeq, \asymp, \propto, \varpropto$
* `<, \nless, \ll, \not\ll, \lll, \not\lll, \lessdot`: $<, \nless, \ll, \not\ll, \lll, \not\lll, \lessdot$
* `>, \ngtr, \gg, \not\gg, \ggg, \not\ggg, \gtrdot`: $>, \ngtr, \gg, \not\gg, \ggg, \not\ggg, \gtrdot$
* `\le, \leq, \lneq, \leqq, \nleq, \nleqq, \lneqq, \lvertneqq`: $\le, \leq, \lneq, \leqq, \nleq, \nleqq, \lneqq, \lvertneqq$
* `\ge, \geq, \gneq, \geqq, \ngeq, \ngeqq, \gneqq, \gvertneqq`: $\ge, \geq, \gneq, \geqq, \ngeq, \ngeqq, \gneqq, \gvertneqq$
* `\lessgtr, \lesseqgtr, \lesseqqgtr, \gtrless, \gtreqless, \gtreqqless`: $\lessgtr, \lesseqgtr, \lesseqqgtr, \gtrless, \gtreqless, \gtreqqless$
* `\leqslant, \nleqslant, \eqslantless, \geqslant, \ngeqslant, \eqslantgtr`: $\leqslant, \nleqslant, \eqslantless, \geqslant, \ngeqslant, \eqslantgtr$
* `\lesssim, \lnsim, \lessapprox, \lnapprox, \gtrsim, \gnsim, \gtrapprox, \gnapprox`: $\lesssim, \lnsim, \lessapprox, \lnapprox, \gtrsim, \gnsim, \gtrapprox, \gnapprox$
* `\prec, \nprec, \preceq, \npreceq, \precneqq`: $\prec, \nprec, \preceq, \npreceq, \precneqq$
* `\preccurlyeq, \curlyeqprec, \succcurlyeq, \curlyeqsucc`: $\preccurlyeq, \curlyeqprec, \succcurlyeq, \curlyeqsucc$
* `\precsim, \precnsim, \precapprox, \precnapprox`: $\precsim, \precnsim, \precapprox, \precnapprox$
* `\succsim, \succnsim, \succapprox, \succnapprox`: $\succsim, \succnsim, \succapprox, \succnapprox$

### 几何符号

* `\parallel, \nparallel, \shortparallel, \nshortparallel`: $\parallel, \nparallel, \shortparallel, \nshortparallel$
* `\perp, \angle, \sphericalangle, \measuredangle, 45^\circ`: $\perp, \angle, \sphericalangle, \measuredangle, 45^\circ$
* `\Box, \blacksquare, \diamond, \Diamond \lozenge, \blacklozenge, \bigstar`: $\Box, \blacksquare, \diamond, \Diamond \lozenge, \blacklozenge, \bigstar$
* `\bigcirc, \triangle, \bigtriangleup, \bigtriangledown`: $\bigcirc, \triangle, \bigtriangleup, \bigtriangledown$
* `\vartriangle, \triangledown`: $\vartriangle, \triangledown$
* `\blacktriangle, \blacktriangledown, \blacktriangleleft, \blacktriangleright`: $\blacktriangle, \blacktriangledown, \blacktriangleleft, \blacktriangleright$

### 逻辑符号

* `\forall, \exists, \nexists`: $\forall, \exists, \nexists$
* `\therefore, \because, \And`: $\therefore, \because, \And$
* `\or \lor \vee, \curlyvee, \bigvee`: $\or \lor \vee, \curlyvee, \bigvee$
* `\and \land \wedge, \curlywedge, \bigwedge`: $\and \land \wedge, \curlywedge, \bigwedge$
* `\bar{q}, \bar{abc}, \overline{q}, \overline{abc}`: $\bar{q}, \bar{abc}, \overline{q}, \overline{abc}$
* `\lnot \neg, \not\operatorname{R}, \bot, \top`: $\lnot \neg, \not\operatorname{R}, \bot, \top$
* `\vdash \dashv, \vDash, \Vdash, \models`: $\vdash \dashv, \vDash, \Vdash, \models$
* `\Vvdash \nvdash \nVdash \nvDash \nVDash`: $\Vvdash \nvdash \nVdash \nvDash \nVDash$
* `\ulcorner \urcorner \llcorner \lrcorner`: $\ulcorner \urcorner \llcorner \lrcorner$

### 箭头

* `\Rrightarrow, \Lleftarrow`: $\Rrightarrow, \Lleftarrow$
* `\Rightarrow, \nRightarrow, \Longrightarrow \implies`: $\Rightarrow, \nRightarrow, \Longrightarrow \implies$
* `\Leftarrow, \nLeftarrow, \Longleftarrow`: $\Leftarrow, \nLeftarrow, \Longleftarrow$
* `\Leftrightarrow, \nLeftrightarrow, \Longleftrightarrow \iff`: $\Leftrightarrow, \nLeftrightarrow, \Longleftrightarrow \iff$
* `\Uparrow, \Downarrow, \Updownarrow`: $\Uparrow, \Downarrow, \Updownarrow$
* `\rightarrow \to, \nrightarrow, \longrightarrow`: $\rightarrow \to, \nrightarrow, \longrightarrow$
* `\leftarrow \gets, \nleftarrow, \longleftarrow`: $\leftarrow \gets, \nleftarrow, \longleftarrow$
* `\leftrightarrow, \nleftrightarrow, \longleftrightarrow`: $\leftrightarrow, \nleftrightarrow, \longleftrightarrow$
* `\uparrow, \downarrow, \updownarrow`: $\uparrow, \downarrow, \updownarrow$
* `\nearrow, \swarrow, \nwarrow, \searrow`: $\nearrow, \swarrow, \nwarrow, \searrow$
* `\mapsto, \longmapsto`: $\mapsto, \longmapsto$
* `\rightharpoonup, \rightharpoondown, \leftharpoonup, \leftharpoondown, \upharpoonleft, \upharpoonright, \downharpoonleft, \downharpoonright, \rightleftharpoons, \leftrightharpoons`: $\rightharpoonup, \rightharpoondown, \leftharpoonup, \leftharpoondown, \upharpoonleft, \upharpoonright, \downharpoonleft, \downharpoonright, \rightleftharpoons, \leftrightharpoons$
* `\curvearrowleft, \circlearrowleft, \Lsh, \upuparrows, \rightrightarrows, \rightleftarrows, \rightarrowtail, \looparrowright`: $\curvearrowleft, \circlearrowleft, \Lsh, \upuparrows, \rightrightarrows, \rightleftarrows, \rightarrowtail, \looparrowright$
* `\curvearrowright, \circlearrowright, \Rsh, \downdownarrows, \leftleftarrows, \leftrightarrows, \leftarrowtail, \looparrowleft`: $\curvearrowright, \circlearrowright, \Rsh, \downdownarrows, \leftleftarrows, \leftrightarrows, \leftarrowtail, \looparrowleft$
* `\hookrightarrow, \hookleftarrow, \multimap, \leftrightsquigarrow, \rightsquigarrow, \twoheadrightarrow, \twoheadleftarrow`: $\hookrightarrow, \hookleftarrow, \multimap, \leftrightsquigarrow, \rightsquigarrow, \twoheadrightarrow, \twoheadleftarrow$

### 省略号

* `\ldots, \cdots`: $\ldots, \cdots$
* `\cdots, \ddots, \vdots`: $\cdots, \ddots, \vdots$

### 其它符号

* `\amalg \% \dagger \ddagger`: $\amalg \% \dagger \ddagger$
* `\smile \frown \wr \triangleleft \triangleright`: $\smile \frown \wr \triangleleft \triangleright$
* `\diamondsuit, \heartsuit, \clubsuit, \spadesuit, \Game, \flat, \natural, \sharp`: $\diamondsuit, \heartsuit, \clubsuit, \spadesuit, \Game, \flat, \natural, \sharp$
* `\diagup \diagdown \centerdot \ltimes \rtimes \leftthreetimes \rightthreetimes`: $\diagup \diagdown \centerdot \ltimes \rtimes \leftthreetimes \rightthreetimes$
* `\intercal \barwedge \veebar \doublebarwedge \between \pitchfork`: $\intercal \barwedge \veebar \doublebarwedge \between \pitchfork$
* `\vartriangleleft \ntriangleleft \vartriangleright \ntriangleright`: $\vartriangleleft \ntriangleleft \vartriangleright \ntriangleright$
* `\trianglelefteq \ntrianglelefteq \trianglerighteq \ntrianglerighteq`: $\trianglelefteq \ntrianglelefteq \trianglerighteq \ntrianglerighteq$

### 声调、变音符号

* `\dot{a}, \ddot{a}, \acute{a}, \grave{a}`: $\dot{a}, \ddot{a}, \acute{a}, \grave{a}$
* `\check{a}, \breve{a}, \tilde{a}, \bar{a}`: $\check{a}, \breve{a}, \tilde{a}, \bar{a}$
* `\hat{a}, \widehat{a}, \vec{a}`: $\hat{a}, \widehat{a}, \vec{a}$

## 矩阵
### 无框矩阵
* 在开头使用`\begin{matrix}`，在结尾使用`\end{matrix}`，在中间插入矩阵元素，每个元素之间插入`&` ，并在每行结尾处使用`\\`。使用矩阵时必须声明 `$` 或 `$$` 符号。
```latex
\begin{matrix}
1 & x & x^2 \\
1 & y & y^2 \\
1 & z & z^2 \\
\end{matrix}
```
$$
\begin{matrix}
1 & x & x^2 \\
1 & y & y^2 \\
1 & z & z^2 \\
\end{matrix}
$$

### 边框矩阵
* 在开头将`matrix`替换为`pmatrix` `bmatrix` `Bmatrix` `vmatrix` `Vmatrix` 。
```latex
$ \begin{matrix} 1 & 2 \\ 3 & 4 \\ \end{matrix} $
$ \begin{pmatrix} 1 & 2 \\ 3 & 4 \\ \end{pmatrix} $
$ \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ \end{bmatrix} $
$ \begin{Bmatrix} 1 & 2 \\ 3 & 4 \\ \end{Bmatrix} $
$ \begin{vmatrix} 1 & 2 \\ 3 & 4 \\ \end{vmatrix} $
$ \begin{Vmatrix} 1 & 2 \\ 3 & 4 \\ \end{Vmatrix} $
```

|matrix|pmatrix|bmatrix|Bmatrix|vmatrix|Vmatrix|
|:---:|:---:|:---:|:---:|:---:|:---:|
|$ \begin{matrix} 1 & 2 \\ 3 & 4 \\ \end{matrix} $|$ \begin{pmatrix} 1 & 2 \\ 3 & 4 \\ \end{pmatrix} $|$ \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ \end{bmatrix} $|$ \begin{Bmatrix} 1 & 2 \\ 3 & 4 \\ \end{Bmatrix} $|$ \begin{vmatrix} 1 & 2 \\ 3 & 4 \\ \end{vmatrix} $|$ \begin{Vmatrix} 1 & 2 \\ 3 & 4 \\ \end{Vmatrix} $|

### 带分隔符的矩阵
* 详见"数组使用参考"。
```latex
\left[
    \begin{array}{cc|c}
      1&2&3\\
      4&5&6
    \end{array}
\right]
```
$$
\left[
    \begin{array}{cc|c}
      1&2&3\\
      4&5&6
    \end{array}
\right]
$$
其中`cc|c`代表在一个三列矩阵中的第二和第三列之间插入分割线。

### 行内矩阵
* 使用`\bigl(\begin{smallmatrix} ... \end{smallmatrix}\bigr)`。
```latex
这是一个行中矩阵的示例 $\bigl( \begin{smallmatrix} a & b \\ c & d \end{smallmatrix} \bigr)$ 。
```
这是一个行中矩阵的示例 $\bigl( \begin{smallmatrix} a & b \\ c & d \end{smallmatrix} \bigr)$ 。

## 方程式
### 方程式序列
* 使用`\begin{align}…\end{align}`来创造一列方程式，其中在每行结尾处使用`\\`。
* 使用方程式序列无需声明公式符号`$`或`$$`。
* 请注意 {align} 语句是**自动编号**的，使用 {align*} 声明(头尾两处)停止自动编号。
* 可以使用`\tag{}`语句编号，优先级高于自动编号。
```latex
\begin{align}
v + w & = 0  &\text{Given} \tag 1\\
-w & = -w + 0 & \text{additive identity} \tag 2\\
-w + 0 & = -w + (v + w) & \text{equations $(1)$ and $(2)$}
\end{align}
```
$$
\begin{align}
v + w & = 0  &\text{Given} \tag 1\\
-w & = -w + 0 & \text{additive identity} \tag 2\\
-w + 0 & = -w + (v + w) & \text{equations \$(1)\$ and \$(2)\$}
\end{align}
$$

## 条件表达式
### 常规条件表达式
* 使用`begin{cases}`来创造一组条件表达式，在每一行条件中插入`&`来指定需要对齐的内容，并在每一行结尾处使用 `\\`，以`end{cases}`结束。条件表达式无需声明`$`或`$$`符号。
```latex
f(n) = \begin{cases}
        n/2,  & \text{if $n$ is even} \\
        3n+1, & \text{if $n$ is odd}
        \end{cases}
```
$$
f(n) = \begin{cases}
        n/2,  & \text{if \$n\$ is even} \\
        3n+1, & \text{if \$n\$ is odd}
        \end{cases}
$$

### 文字左侧对齐
```latex
\left.
\begin{array}{l}
    \text{if $n$ is even:}&n/2\\
    \text{if $n$ is odd:}&3n+1
\end{array}
\right \}=f(n)
```
$$
\left.
\begin{array}{l}
    \text{if \$n\$ is even:}&n/2\\
    \text{if \$n\$ is odd:}&3n+1
\end{array}
\right \}=f(n)
$$

### 适配行高
* 条件表达式中某些行的行高为非标准高度，此时使用`\\[2ex]`语句代替该行末尾的`\\`来让编辑器适配。
* 一个`[ex]`指一个 "X-Height"，即x字母高度。可以根据情况指定多个`[ex]`，如`[3ex]`、`[4ex]`等。
其实可以在任何地方使用`\\[2ex]`语句，只要你觉得合适。
```latex
不适配 f(n) = 
\begin{cases}
\frac{n}{2},  & \text{if $n$ is even} \\
3n+1, & \text{if $n$ is odd}
\end{cases}
```
$$
适配 f(n) = 
\begin{cases}
\frac{n}{2},  & \text{if \$n\$ is even} \\[2ex]
3n+1, & \text{if \$n\$ is odd}
\end{cases}
$$

## 数组和表格
### 单个数组
* 数组和表格均以`begin{array}`开头，并在其后定义列数及每一列的文本对齐属性，`c` `l` `r` 分别代表居中、左对齐及右对齐。若需要插入垂直分割线，在定义式中插入 `|`，若要插入水平分割线，在下一行输入前插入`\hline`。与矩阵相似，每行元素间均须要插入`&`，每行元素以`\\` 结尾，最后以`end{array}`结束数组。使用单个数组或表格时无需声明 $ 或 $$ 符号。
```latex
\begin{array}{c|lcr}
n & \text{左对齐} & \text{居中对齐} & \text{右对齐} \\
\hline
1 & 0.24 & 1 & 125 \\
2 & -1 & 189 & -8 \\
3 & -20 & 2000 & 1+10i
\end{array}
```
$$
\begin{array}{c|lcr}
n & \text{左对齐} & \text{居中对齐} & \text{右对齐} \\
\hline
1 & 0.24 & 1 & 125 \\
2 & -1 & 189 & -8 \\
3 & -20 & 2000 & 1+10i
\end{array}
$$

### 嵌套数组
* 多个数组/表格可**互相嵌套**并组成一组数组/一组表格。使用嵌套前必须声明`$$`符号。
```latex
% outer vertical array of arrays 外层垂直表格
\begin{array}{c}
    % inner horizontal array of arrays 内层水平表格
    \begin{array}{cc}
        % inner array of minimum values 内层"最小值"数组
        \begin{array}{c|cccc}
        \text{min} & 0 & 1 & 2 & 3\\
        \hline
        0 & 0 & 0 & 0 & 0\\
        1 & 0 & 1 & 1 & 1\\
        2 & 0 & 1 & 2 & 2\\
        3 & 0 & 1 & 2 & 3
        \end{array}
    &
        % inner array of maximum values 内层"最大值"数组
        \begin{array}{c|cccc}
        \text{max}&0&1&2&3\\
        \hline
        0 & 0 & 1 & 2 & 3\\
        1 & 1 & 1 & 2 & 3\\
        2 & 2 & 2 & 2 & 3\\
        3 & 3 & 3 & 3 & 3
        \end{array}
    \end{array}
    % 内层第一行表格组结束
    \\
    % inner array of delta values 内层第二行Delta值数组
        \begin{array}{c|cccc}
        \Delta&0&1&2&3\\
        \hline
        0 & 0 & 1 & 2 & 3\\
        1 & 1 & 0 & 1 & 2\\
        2 & 2 & 1 & 0 & 1\\
        3 & 3 & 2 & 1 & 0
        \end{array}
        % 内层第二行表格组结束
\end{array}
```
$$
% outer vertical array of arrays 外层垂直表格
\begin{array}{c}
    % inner horizontal array of arrays 内层水平表格
    \begin{array}{cc}
        % inner array of minimum values 内层"最小值"数组
        \begin{array}{c|cccc}
        \text{min} & 0 & 1 & 2 & 3\\
        \hline
        0 & 0 & 0 & 0 & 0\\
        1 & 0 & 1 & 1 & 1\\
        2 & 0 & 1 & 2 & 2\\
        3 & 0 & 1 & 2 & 3
        \end{array}
    &
        % inner array of maximum values 内层"最大值"数组
        \begin{array}{c|cccc}
        \text{max}&0&1&2&3\\
        \hline
        0 & 0 & 1 & 2 & 3\\
        1 & 1 & 1 & 2 & 3\\
        2 & 2 & 2 & 2 & 3\\
        3 & 3 & 3 & 3 & 3
        \end{array}
    \end{array}
    % 内层第一行表格组结束
    \\
    % inner array of delta values 内层第二行Delta值数组
        \begin{array}{c|cccc}
        \Delta&0&1&2&3\\
        \hline
        0 & 0 & 1 & 2 & 3\\
        1 & 1 & 0 & 1 & 2\\
        2 & 2 & 1 & 0 & 1\\
        3 & 3 & 2 & 1 & 0
        \end{array}
        % 内层第二行表格组结束
\end{array}
$$

### 创建方程组
* 使用`\begin{array}…\end{array}`和`\left\{…\right.`来创建一个方程组。
```latex
\left\{ 
\begin{array}{c}
a_1x+b_1y+c_1z=d_1 \\ 
a_2x+b_2y+c_2z=d_2 \\ 
a_3x+b_3y+c_3z=d_3
\end{array}
\right.
```
$$
\left\{ 
\begin{array}{c}
a_1x+b_1y+c_1z=d_1 \\ 
a_2x+b_2y+c_2z=d_2 \\ 
a_3x+b_3y+c_3z=d_3
\end{array}
\right. 
$$
* 或者也可以使用条件表达式组`\begin{cases}…\end{cases}`来实现相同效果。
```latex
\begin{cases}
a_1x+b_1y+c_1z=d_1 \\ 
a_2x+b_2y+c_2z=d_2 \\ 
a_3x+b_3y+c_3z=d_3
\end{cases}
```
$$
\begin{cases}
a_1x+b_1y+c_1z=d_1 \\ 
a_2x+b_2y+c_2z=d_2 \\ 
a_3x+b_3y+c_3z=d_3
\end{cases}
$$

## 连分数
* 使用`\cfrac{}{}`保持字体大小，不要使用`\frac{}{}`，字体会越来越小非常难看。
$$
\begin{array}{c|c}
cfrac效果 & frac效果 \\
\hline \\
x = a_0 + \cfrac{1^2}{a_1
          + \cfrac{2^2}{a_2
          + \cfrac{3^2}{a_3 + \cfrac{4^4}{a_4 + \cdots}}}}
&
x = a_0 + \frac{1^2}{a_1
          + \frac{2^2}{a_2
          + \frac{3^2}{a_3 + \frac{4^4}{a_4 + \cdots}}}}
\end{array}
$$

## 二项式
* `\dbinom{n}{r}=\binom{n}{n-r}=\mathrm{C}_n^r=\mathrm{C}_n^{n-r}`
$\dbinom{n}{r}=\binom{n}{n-r}=\mathrm{C}_n^r=\mathrm{C}_n^{n-r}$
* 小型二项式系数`\tbinom{n}{r}=\tbinom{n}{n-r}=\mathrm{C}_n^r=\mathrm{C}_n^{n-r}`
$\tbinom{n}{r}=\tbinom{n}{n-r}=\mathrm{C}_n^r=\mathrm{C}_n^{n-r}$
* 大型二项式系数`\binom{n}{r}=\dbinom{n}{n-r}=\mathrm{C}_n^r=\mathrm{C}_n^{n-r}`
$\binom{n}{r}=\dbinom{n}{n-r}=\mathrm{C}_n^r=\mathrm{C}_n^{n-r}$


## 交换图表
* 使用一行`$\require{AMScd}$`语句来允许交换图表的显示。声明交换图表后，语法与矩阵相似，在开头使用 `begin{CD}`，在结尾使用`end{CD}`，在中间插入图表元素，每个元素之间插入`&`，并在每行结尾处使用`\\`。
```latex
$\require{AMScd}$
\begin{CD}
    A @>a>> B\\
    @V b V V\# @VV c V\\
    C @>>d> D
\end{CD}
```
$$
\require{AMScd}
\begin{CD}
    A @>a>> B\\
    @V b V V\# @VV c V\\
    C @>>d> D
\end{CD}
$$
其中，@>>> 代表右箭头、@<<< 代表左箭头、@VVV 代表下箭头、@AAA 代表上箭头、@= 代表水平双实线、@| 代表竖直双实线、@.代表没有箭头。
在 @>>> 的 >>> 之间任意插入文字即代表该箭头的注释文字。
$$
\begin{CD}
    A @>>> B @>{\text{very long label}}>> C \\
    @. @AAA @| \\
    D @= E @<<< F
\end{CD}
$$
在本例中， "very long label"自动延长了它所在箭头以及对应箭头的长度。

## 格式
### 文字颜色
* 使用`\color{颜色}{文字}`来更改特定的文字颜色。
* 更改文字颜色 需要浏览器支持 ，如果浏览器不知道你所需的颜色，那么文字将被渲染为黑色。
对于较旧的浏览器（HTML4与CSS2），以下颜色是被支持的：

| 输入 | 显示 | 输入 | 显示 |
| :---: | :---: | :---: | :---: |
| black | $\color{black}{text}$ | grey | $\color{grey}{text}$ |
| silver | $\color{silver}{text}$ | white | $\color{white}{text}$ |
| maroon | $\color{maroon}{text}$ | red | $\color{red}{text}$ |
| yellow | $\color{yellow}{text}$ | lime | $\color{lime}{text}$ |
| olive | $\color{olive}{text}$ | green | $\color{green}{text}$ |
| teal | $\color{teal}{text}$ | auqa | $\color{auqa}{text}$ |
| blue | $\color{blue}{text}$ | navy | $\color{navy}{text}$ |
| purple | $\color{purple}{text}$ | fuchsia | $\color{fuchsia}{text}$ |

对于较新的浏览器（HTML5与CSS3），额外的124种颜色将被支持：
$\color{Apricot}{Apricot}$
$\color{Aquamarine}{Aquamarine}$
$\color{Bittersweet}{Bittersweet}$
$\color{Black}{Black}$
$\color{Blue}{Blue}$
$\color{BlueGreen}{BlueGreen}$
$\color{BlueViolet}{BlueViolet}$
$\color{BrickRed}{BrickRed}$
$\color{Brown}{Brown}$
$\color{BurntOrange}{BurntOrange}$
$\color{CadetBlue}{CadetBlue}$
$\color{CarnationPink}{CarnationPink}$
$\color{Cerulean}{Cerulean}$
$\color{CornflowerBlue}{CornflowerBlue}$
$\color{Cyan}{Cyan}$
$\color{Dandelion}{Dandelion}$
$\color{DarkOrchid}{DarkOrchid}$
$\color{Emerald}{Emerald}$
$\color{ForestGreen}{ForestGreen}$
$\color{Goldenrod}{Goldenrod}$
$\color{Fuchsia}{Fuchsia}$
$\color{Gray}{Gray}$
$\color{Green}{Green}$
$\color{GreenYellow}{GreenYellow}$
$\color{JungleGreen}{JungleGreen}$
$\color{Lavender}{Lavender}$
$\color{LimeGreen}{LimeGreen}$
$\color{Magenta}{Magenta}$
$\color{Mahogany}{Mahogany}$
$\color{Maroon}{Maroon}$
$\color{Melon}{Melon}$
$\color{MidnightBlue}{MidnightBlue}$
$\color{Mulberry}{Mulberry}$
$\color{NavyBlue}{NavyBlue}$
$\color{OliveGreen}{OliveGreen}$
$\color{Orange}{Orange}$
$\color{OrangeRed}{OrangeRed}$
$\color{Orchid}{Orchid}$
$\color{Peach}{Peach}$
$\color{Periwinkle}{Periwinkle}$
$\color{PineGreen}{PineGreen}$
$\color{Plum}{Plum}$
$\color{ProcessBlue}{ProcessBlue}$
$\color{Purple}{Purple}$
$\color{RawSienna}{RawSienna}$
$\color{Red}{Red}$
$\color{RedOrange}{RedOrange}$
$\color{RedViolet}{RedViolet}$
$\color{Rhodamine}{Rhodamine}$
$\color{RoyalBlue}{RoyalBlue}$
$\color{RoyalPurple}{RoyalPurple}$
$\color{RubineRed}{RubineRed}$
$\color{Salmon}{Salmon}$
$\color{SeaGreen}{SeaGreen}$
$\color{Sepia}{Sepia}$
$\color{SkyBlue}{SkyBlue}$
$\color{SpringGreen}{SpringGreen}$
$\color{Tan}{Tan}$
$\color{TealBlue}{TealBlue}$
$\color{Thistle}{Thistle}$
$\color{Turquoise}{Turquoise}$
$\color{Violet}{Violet}$
$\color{VioletRed}{VioletRed}$
$\color{White}{White}$
$\color{WildStrawberry}{WildStrawberry}$
$\color{Yellow}{Yellow}$
$\color{YellowGreen}{YellowGreen}$
$\color{YellowOrange}{YellowOrange}$

* 输入`\color {#rgb} {text}`来自定义更多的颜色，其中`#rgb`的`r``g``b` 可输入`0-9`和`a-f`来表示红色、绿色和蓝色的纯度（饱和度）。
```latex
\begin{array}{|rrrrrrrr|}
\hline
\verb+#000+ & \color{#000}{text} & \verb+#005+ & \color{#005}{text} & \verb+#00A+ & \color{#00A}{text} & \verb+#00F+ & \color{#00F}{text}  \\
\verb+#500+ & \color{#500}{text} & \verb+#505+ & \color{#505}{text} & \verb+#50A+ & \color{#50A}{text} & \verb+#50F+ & \color{#50F}{text}  \\
\verb+#A00+ & \color{#A00}{text} & \verb+#A05+ & \color{#A05}{text} & \verb+#A0A+ & \color{#A0A}{text} & \verb+#A0F+ & \color{#A0F}{text}  \\
\verb+#F00+ & \color{#F00}{text} & \verb+#F05+ & \color{#F05}{text} & \verb+#F0A+ & \color{#F0A}{text} & \verb+#F0F+ & \color{#F0F}{text}  \\
\hline
\verb+#080+ & \color{#080}{text} & \verb+#085+ & \color{#085}{text} & \verb+#08A+ & \color{#08A}{text} & \verb+#08F+ & \color{#08F}{text}  \\
\verb+#580+ & \color{#580}{text} & \verb+#585+ & \color{#585}{text} & \verb+#58A+ & \color{#58A}{text} & \verb+#58F+ & \color{#58F}{text}  \\
\verb+#A80+ & \color{#A80}{text} & \verb+#A85+ & \color{#A85}{text} & \verb+#A8A+ & \color{#A8A}{text} & \verb+#A8F+ & \color{#A8F}{text}  \\
\verb+#F80+ & \color{#F80}{text} & \verb+#F85+ & \color{#F85}{text} & \verb+#F8A+ & \color{#F8A}{text} & \verb+#F8F+ & \color{#F8F}{text}  \\
\hline
\verb+#0F0+ & \color{#0F0}{text} & \verb+#0F5+ & \color{#0F5}{text} & \verb+#0FA+ & \color{#0FA}{text} & \verb+#0FF+ & \color{#0FF}{text}  \\
\verb+#5F0+ & \color{#5F0}{text} & \verb+#5F5+ & \color{#5F5}{text} & \verb+#5FA+ & \color{#5FA}{text} & \verb+#5FF+ & \color{#5FF}{text}  \\
\verb+#AF0+ & \color{#AF0}{text} & \verb+#AF5+ & \color{#AF5}{text} & \verb+#AFA+ & \color{#AFA}{text} & \verb+#AFF+ & \color{#AFF}{text}  \\
\verb+#FF0+ & \color{#FF0}{text} & \verb+#FF5+ & \color{#FF5}{text} & \verb+#FFA+ & \color{#FFA}{text} & \verb+#FFF+ & \color{#FFF}{text}  \\
\hline
\end{array}
```
$$
\begin{array}{|rrrrrrrr|}
\hline
\verb+#000+ & \color{#000}{text} & \verb+#005+ & \color{#005}{text} & \verb+#00A+ & \color{#00A}{text} & \verb+#00F+ & \color{#00F}{text}  \\
\verb+#500+ & \color{#500}{text} & \verb+#505+ & \color{#505}{text} & \verb+#50A+ & \color{#50A}{text} & \verb+#50F+ & \color{#50F}{text}  \\
\verb+#A00+ & \color{#A00}{text} & \verb+#A05+ & \color{#A05}{text} & \verb+#A0A+ & \color{#A0A}{text} & \verb+#A0F+ & \color{#A0F}{text}  \\
\verb+#F00+ & \color{#F00}{text} & \verb+#F05+ & \color{#F05}{text} & \verb+#F0A+ & \color{#F0A}{text} & \verb+#F0F+ & \color{#F0F}{text}  \\
\hline
\verb+#080+ & \color{#080}{text} & \verb+#085+ & \color{#085}{text} & \verb+#08A+ & \color{#08A}{text} & \verb+#08F+ & \color{#08F}{text}  \\
\verb+#580+ & \color{#580}{text} & \verb+#585+ & \color{#585}{text} & \verb+#58A+ & \color{#58A}{text} & \verb+#58F+ & \color{#58F}{text}  \\
\verb+#A80+ & \color{#A80}{text} & \verb+#A85+ & \color{#A85}{text} & \verb+#A8A+ & \color{#A8A}{text} & \verb+#A8F+ & \color{#A8F}{text}  \\
\verb+#F80+ & \color{#F80}{text} & \verb+#F85+ & \color{#F85}{text} & \verb+#F8A+ & \color{#F8A}{text} & \verb+#F8F+ & \color{#F8F}{text}  \\
\hline
\verb+#0F0+ & \color{#0F0}{text} & \verb+#0F5+ & \color{#0F5}{text} & \verb+#0FA+ & \color{#0FA}{text} & \verb+#0FF+ & \color{#0FF}{text}  \\
\verb+#5F0+ & \color{#5F0}{text} & \verb+#5F5+ & \color{#5F5}{text} & \verb+#5FA+ & \color{#5FA}{text} & \verb+#5FF+ & \color{#5FF}{text}  \\
\verb+#AF0+ & \color{#AF0}{text} & \verb+#AF5+ & \color{#AF5}{text} & \verb+#AFA+ & \color{#AFA}{text} & \verb+#AFF+ & \color{#AFF}{text}  \\
\verb+#FF0+ & \color{#FF0}{text} & \verb+#FF5+ & \color{#FF5}{text} & \verb+#FFA+ & \color{#FFA}{text} & \verb+#FFF+ & \color{#FFF}{text}  \\
\hline
\end{array}
$$

### 字号
* 若需要显示更大或更小的字符，在符号前插入`\large`或`\small`命令。

### 字体
* 若要对公式的某一部分字符进行字体转换，可以用`{\字体 {需转换的部分字符}}`命令，其中`\字体` 部分可以参照下表选择合适的字体。一般情况下，公式默认为意大利体$italic$。

| 输入 | 说明 | 显示 |
| :---: | :---: | :---: |
| \rm | 罗马体 | ${\rm Sample}$ |
| \it | 意大利体 | ${\it Sample}$ |
| \bf | 粗体 | ${\bf Sample}$ |
| \sf | 等线体 | ${\sf Sample}$ |
| \tt | 打字机体 | ${\tt Sample}$ |
| \frak | 旧德式字体 | ${\frak Sample}$ |
| \cal | 花体(仅大写) | ${\cal SAMPLE}$ |
| \Bbb | 黑板粗体(仅大写) | ${\Bbb SAMPLE}$ |
| \mit | 数学斜体(仅大写) | ${\mit SAMPLE}$ |
| \scr | 手写体(仅大写) | ${\scr SAMPLE}$ |

字体转换示例(使用`\operatorname`命令也可以达到相同的效果):
```latex
\begin{array}{cc}
\mathrm{Bad} & \mathrm{Better} \\
\hline \\
\int_0^1 x^2 dx & \int_0^1 x^2 \,{\rm d}x
\end{array}
```
$$
\begin{array}{cc}
\mathrm{Bad} & \mathrm{Better} \\
\hline \\
\int_0^1 x^2 dx & \int_0^1 x^2 \,{\rm d}x
\end{array}
$$

## 特殊注意事项

* 在以e为底的指数函数、极限和积分中尽量不要使用`\frac`符号：它会使整段函数看起来很怪，而且可能产生歧义。也正是因此它在专业数学排版中几乎从不出现。横着写这些分式，中间使用斜线间隔`/`（用斜线代替分数线）。
$$
\begin{array}{cc}
\mathrm{Bad} & \mathrm{Better} \\
\hline \\
e^{i\frac{\pi}2} \quad e^{\frac{i\pi}2}& e^{i\pi/2} \\
\int_{-\frac\pi2}^\frac\pi2 \sin x\,dx & \int_{-\pi/2}^{\pi/2}\sin x\,dx \\
\end{array}
$$
* `|`符号在被当作分隔符时会产生错误的间隔，因此在需要分隔时最好使用`\mid`来代替它。
$$
\begin{array}{cc}
\mathrm{Bad} & \mathrm{Better} \\
\hline \\
\{x|x^2\in\Bbb Z\} & \{x\mid x^2\in\Bbb Z\} \\
\end{array}
$$
* 使用多重积分符号时，不要多次使用`\int`来声明，直接使用`\iint`来表示二重积分，使用`\iiint`来表示三重积分 等。对于无限次积分，可以用`\int \cdots \int`表示。
$$
\begin{array}{cc}
\mathrm{Bad} & \mathrm{Better} \\
\hline \\
\int\int_S f(x)\,dy\,dx & \iint_S f(x)\,dy\,dx \\
\int\int\int_V f(x)\,dz\,dy\,dx & \iiint_V f(x)\,dz\,dy\,dx
\end{array}
$$
* 在微分符号前加入`\,`来插入一个小的间隔空隙；没有`\,`符号的话，Tex将会把不同的微分符号堆在一起，不好看。
$$
\begin{array}{cc}
\mathrm{Bad} & \mathrm{Better} \\
\hline \\
\iiint_V f(x){\rm d}z {\rm d}y {\rm d}x & \iiint_V f(x)\,{\rm d}z\,{\rm d}y\,{\rm d}x
\end{array}
$$
