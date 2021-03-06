# 微分

### 0.2.1 微分とは

$$x$$が$$a \rightarrow b$$に変化したとき、$$f(x)$$ の$$a$$から$$b$$での平均変化率は  
$$\frac{f(b)-f(a)}{b-a}$$  
と表されます。$$b$$を$$a$$にどんどん近づけていくとこの変化率はある一定値に近づいていきます。その近づいていく先の値を$$x=a$$における$$f(x)$$ の微分係数と呼び、 $$f'(a)$$ と書きます。数式で表すと  
$$ f'(a) = \lim_{h \to 0} \frac{f(a+h)-f(a)}{h} $$  
となります。$$\lim _{h \to 0}$$ は「$$h$$をどんどん$$0$$に近づけていったときに近づいていく先の値」を表すイメージの記号です。本当にある一定値に近づいていくのかは疑問の余地があるところで、 $$\varepsilon-\delta$$論法を使って厳密に考える必要がありますが、ここでは極限値が存在する素直な関数のみを考えることにします。

微分係数は$$f(x)$$ と$$a$$を定めると一つに定まるのでこれも関数と考えることができます。$$f(x)$$ の微分係数を表す関数を$$f'(x)$$ や $$\frac{df}{dx}$$ などと書き$$f(x)$$ の**導関数**と呼びます。導関数を求める操作を**微分**と呼びます。

### 0.2.2 微分の計算

#### $$f(x) = x^n$$の微分

$$f'(x)=nx^{n-1}$$  
が成り立ちます。なお、これは$n$が自然数以外の場合でも成立します。$$n=0$$の場合は例外で、定数を微分すると0になります。

例: $$f(x) = x^5$$ の微分は$$f'(x)=5x^4$$となります。

例: $$f(x) = 3$$の微分は$$f'(x)=0$$となります。

#### $$a \cdot f(x)$$ の微分

$$(a \cdot f(x))' = a \cdot f'(x)$$  
 となります。関数を定数倍したものを微分すると、関数の微分を定数倍したものになるということです。

例: $$f(x) = 3x^5$$の微分は$$f'(x)=3 \cdot 5x^4 = 15x^4$$となります。

#### $$f(x) + g(x)$$ の微分

$$(f(x) + g(x))' = f'(x)+g'(x) $$  
が成り立ちます。関数の和の微分は関数の微分の和になるということです。

$$af(x)$$ の微分と合わせると  
$$(af(x)+bf(x))' = af'(x)+bg'(x)$$  
も成り立ちます。

例: $$f(x) = x^4 + x$$ のとき$$f'(x) = 4 \cdot x^3 + 1 \cdot x^0 = 4x^3+1$$

例: $$f(x) = 2x^3 + 5x^2 + 4x + 1$$ のとき$$f'(x) = 2 \cdot 3 \cdot x^2 + 5 \cdot 2 \cdot x^1 + 4 \cdot x^0 + 0 = 4x^3+10x+4$$

#### 積の微分

$$(f(x)g(x))' = f'(x)g(x)+f(x)g'(x)$$  
が成り立ちます。

例: $$f(x) = (2x^2+3)(x^3+4x^2)$$ のとき $$f'(x) = 4x \cdot (3x^2+8x) = 12x^3 + 32x^2$$

#### 商の微分

$$\left( \frac{g(x)}{f(x)} \right)' = \frac{f(x)g'(x)-f'(x)g(x)}{(f(x))^2}$$  
が成り立ちます。

例: $$f(x)=\frac{x+2}{x^2+3}$$ のとき $$f'(x) = \frac{(x^2+3) \cdot 1 - 2x \cdot (x+2)}{(x^2+3)^2} = \frac{-3x^2-4x+3}{(x^2+3)^2}$$

#### 合成関数の微分

$$(f(g(x))' = g'(x)f'(g(x)) $$  
が成り立ちます。少し分かりにくいので例をよく見てください。

例: $$h(x) = (x^2+3x+1)^5$$ のとき$$h'(x) = (x^2+3x+1)' \cdot 5 (x^2+3x+1)^4 = 5(2x+3)(x^2+3x+1)^4$$

これは$$h(x) = (x^2+3x+1)^5$$を$$f(x)=x^5$$と$$g(x)=x^2+3x+1$$の合成関数 $$f(g(x))$$ と考えて公式を当てはめた結果です。

#### 指数関数の微分

$$(a^x)'=\ln a \cdot a^x$$  
となります。まだ説明していない表記がいくつかあるので説明します。

指数関数の微分はある特殊な数$$e$$を用いて定義します。$$e$$は$$f(x)=e^x$$のとき$$f'(x)=e^x$$となる性質を持つ数でおよそ2.718です。$$e$$は「ネイピア数」や「自然対数の底」などと呼ばれています。

一般の $$f(x) = a^x$$のような関数に対しては、$$a^x = e^{x \cdot log_e a}$$ という式変形を行って、$$f'(x)=\log_e a \cdot e^{x \cdot \log_e a} = \log_e a \cdot a^x$$ のように計算します（分からない人は合成関数の微分と対数関数の公式を確認してください）。

$$e$$を底とする対数関数 $$\log_e x$$はよく使うので特別に自然対数と呼ばれていて、 $$\ln x$$のように書きます。（底を省略して単に $$\log x$$と書く場合もありますが、底を省略した場合の底は分野によってバラバラで、$$e$$や10や2などの可能性があります。混乱を避けるため私は自然対数を $$\ln$$と表記することに決めています。）

また、$$e^x$$のことを $$\exp{x}$$ のように書くことも多いです。

これらの表記を理解すれば $$(a^x)'=\ln a \cdot a^x$$ の意味も分かると思います。

ところで、 $$f'(x)=e^x$$  になるような都合の良い数は本当に存在するのでしょうか？$$e$$がどんな数なのか調べるために $$f(x)=a^x$$ の微分を定義通り計算してみることにします。  
$$(a^x)' = \lim_{h \to 0 } \frac{a^{x+h}-a^x}{h} = a^x \lim_{h \to 0} \frac{a^h-1}{h}$$  
ここで $$\frac{1}{t} = a^h-1$$ となるような $$t$$ を使うと、$$h= \log_a (1+\frac{1}{t})$$ となります。また $$\lim_{h \to 0}$$ は $$\lim_{t \to \infty}$$ に置き換えられます。よって、  
$$(a^x)' =~ a^x \lim_{h \to 0} \frac{a^h-1}{h} \\
= a^x \lim_{t \to \infty} \frac{1}{t \log_a (1+\frac{1}{t})} \\
= a^x \lim_{t \to \infty} \frac{1}{\log_a (1+\frac{1}{t})^t} \\
= a^x \frac{1}{\log_a \lim_{t \to \infty} (1+\frac{1}{t})^t} $$  
が成り立ちます。よって $$(a^x)'=a^x$$ となるためには$$a =  \lim_{t \to \infty} (1+\frac{1}{t})^t$$ であればよいことが分かります。この $$\lim_{t \to \infty} (1+\frac{1}{t})^t$$ が$$e$$の定義となります。

（参考: ネイピア数 e をいかにして自然に導入するか [http://tsujimotter-sub.hatenablog.com/entry/2015/08/10/015436）](http://tsujimotter-sub.hatenablog.com/entry/2015/08/10/015436）)

#### 対数関数の微分

$$(\log_a x)' = \frac{1}{x} \log_a{e}$$  
とくに  
$$(\ln x)' = \frac{1}{x}$$  
となります。

定義に従って計算すると  
$$(\log_a x)' = \lim_{h \to 0} \frac{\log_a(x+h)-\log_a x}{h} \\
= \lim_{h \to 0} \frac{1}{x} \log_a(1+\frac{h}{x})^{\frac{h}{x}} \\
= \frac{1}{x}\log_a e $$  
となるので成立します。

### 0.2.3 微分と極値

関数 $$f(x)$$ で、 $$x$$ を少し動かしたときに周囲のどの値よりも大きいか小さいとき、  
その値を極値といいます。周りより大きいときを極大値・小さいときを極小値といいます。極値では微分係数が0になるという性質があります。

---ここに具体例を書く---

### 0.2.4 偏微分

複数の変数を入力とする関数を多変数関数と呼びます。多変数関数についてある一つの変数に注目して微分したものを偏微分と呼び、$$\frac{\partial f}{\partial x}$$ のように書きます。

例:  
$$f(x, y) = x^2+xy+y^3$$ を$$x$$について偏微分すると、  
$$\frac{\partial f}{\partial x} = 2x + y$$  
となります。このとき$$y$$は定数のように扱うのがポイントです。$$y$$についての偏微分は  
$$\frac{\partial f}{\partial y} = x + 3y^2$$  
です。

