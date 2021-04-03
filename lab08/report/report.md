---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе 8"
subtitle: "дисциплина: Математическое моделирование"
author: "Бурба Анна Владимировна, НПИбд-02-18"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Построить модель конкуренции двух фирм с помощью Python.

# Задание

**Вариант 49**

**Случай 1.** Рассмотрим две фирмы, производящие взаимозаменяемые товары одинакового качества и находящиеся в одной рыночной нише. Считаем, что в рамках
нашей модели конкурентная борьба ведётся только рыночными методами. То есть, конкуренты могут влиять на противника путем изменения параметров своего
производства: себестоимость, время цикла, но не могут прямо вмешиваться в ситуацию на рынке («назначать» цену или влиять на потребителей каким-либо иным
способом). Будем считать, что постоянные издержки пренебрежимо малы, и в модели учитывать не будем. В этом случае динамика изменения объемов продаж фирмы 1 
и фирмы 2 описывается следующей системой уравнений:

$$ \begin{cases} \frac{\partial M_1}{\partial \theta} = M_1 - \frac{b}{c_1} M_1 M_2 - \frac{a_1}{c_1} M_1^2 \\ \frac{\partial M_2}{\partial \theta} = 
\frac{c_2}{c_1} M_2 -\frac{b}{c_1} M_1 M_2 - \frac{a_2}{c_1} M_2^2 \end{cases} $$

где

$$ a_1 = \frac{p_{cr}}{\tau_1^2 \tilde{p}_1^2 Nq}, a_2 = \frac{p_{cr}}{\tau_2^2 \tilde{p}_2^2 Nq}, b = \frac{p_{cr}}{\tau_1^2 \tilde{p}_1^2 
\tau_2^2 \tilde{p}_2^2 Nq}, c_1 = \frac{p_{cr} - \tilde{p}_1}{\tau_1^2 \tilde{p}_1^2}, c_2 = \frac{p_{cr} - \tilde{p}_2}{\tau_2^2 \tilde{p}_2^2} $$

Также введена нормировка $t = c_1 \theta$.

**Случай 2.** Рассмотрим модель, когда, помимо экономического фактора влияния (изменение себестоимости, производственного цикла, использование кредита и т.п.), 
используются еще и социально-психологические факторы -- формирование общественного предпочтения одного товара другому, не зависимо от их качества и цены. В 
этом случае взаимодействие двух фирм будет зависеть друг от друга, соответственно коэффициент перед $M_1 M_2$ будет отличаться. Пусть в рамках 
рассматриваемой модели динамика изменения объемов продаж фирмы 1 и фирмы 2 описывается следующей системой уравнений:

$$ \begin{cases} \frac{\partial M_1}{\partial \theta} = M_1 - (\frac{b}{c_1} + 0.00029) M_1 M_2 - \frac{a_1}{c_1} M_1^2 \\ \frac{\partial M_2}{\partial 
\theta} = \frac{c_2}{c_1} M_2 -\frac{b}{c_1} M_1 M_2 - \frac{a_2}{c_1} M_2^2 \end{cases} $$

Для обоих случаев рассмотрим задачу со следующими начальными условиями и параметрами:

$M_{1.0} = 5.4, M_{2.0} = 5.1, p_{cr} = 27, N = 30, q = 1, \tau_1 = 8, \tau_2 = 9, \tilde{p}_1 = 13, \tilde{p}_2 = 10.1$

![Начальные условия](image/3.png){ #fig:001 width=70% }

**Замечание:** Значения $p_{cr}, \tilde{p}_{1,2}, N$ указаны в тысячах единиц, а значения $M_{1,2}$ указаны в млн единиц.

**Обозначения:**

$N$ -- число потребителей производимого продукта;

$\tau$ -- длительность производственного цикла;

$p$ -- рыночная цена товара;

$\tilde{p}$ -- себестоимость продукта, то есть переменные издержки на производство единицы продукции;

$q$ -- максимальная потребность одного человека в продукте в единицу времени;

$\theta = \frac{t}{c_1}$ -- безразмерное время.

1. Постройте графики изменения оборотных средств фирмы 1 и фирмы 2 без учета постоянных издержек и с веденной нормировкой для случая 1.

2. Постройте графики изменения оборотных средств фирмы 1 и фирмы 2 без учета постоянных издержек и с веденной нормировкой для случая 2.

3. Найдите стационарное состояние системы для первого случая.

# Теоретическое введение

Для построения модели конкуренции хотя бы двух фирм необходимо рассмотреть модель одной фирмы. Вначале рассмотрим модель фирмы, производящей продукт 
долговременного пользования, когда цена его определяется балансом спроса и предложения. Примем, что этот продукт занимает определенную нишу рынка и 
конкуренты в ней отсутствуют.

Обозначим:

$N$ -- число потребителей производимого продукта.

$S$ -- доходы потребителей данного продукта. Считаем, что доходы всех потребителей одинаковы. Это предположение справедливо, если речь идет об одной 
рыночной нише, т.е. производимый продукт ориентирован на определенный слой населения.

$M$ -- оборотные средства предприятия.

$\tau$ -- длительность производственного цикла.

$p$ -- рыночная цена товара.

$\tilde{p}$ -- себестоимость продукта, то есть переменные издержки на производство единицы продукции.

$\delta$ -- доля оборотных средств, идущая на покрытие переменных издержек.

$\kappa$ -- постоянные издержки, которые не зависят от количества выпускаемой продукции.

$Q(S/p)$ -- функция спроса, зависящая от отношения дохода S к цене p. Она равна количеству продукта, потребляемого одним потребителем в единицу времени.

Функцию спроса товаров долговременного использования часто представляют в простейшей форме:

$$ \tag{1} Q = q - k \frac{P}{S} = q(1 - \frac{p}{p_{cr}}), $$

где $q$ -- максимальная потребность одного человека в продукте в единицу времени. Эта функция падает с ростом цены и при $p = p_{cr}$ (критическая стоимость 
продукта)потребители отказываются от приобретения товара. Величина $p_{cr} = \frac{Sq}{k}$. Параметр $k$ -- мера эластичности функции спроса по цене. Таким 
образом, функция спроса в форме (1) является пороговой (то есть $Q(S/p) = 0$ при $p \geq p_{cr}$) и обладает свойствами насыщения.

Уравнения динамики оборотных средств можно записать в виде

$$ \tag{2} \frac{\partial M}{\partial t} = -\frac{M \delta}{\tau} + NQp - \kappa = -\frac{M \delta}{\tau} + NQ(1 - \frac{p}{p_{cr}})p - \kappa$$

Уравнение для рыночной цены p представим в виде

$$ \tag{3} \frac{\partial p}{\partial t} = \gamma (-\frac{M \delta}{\tau \tilde{p}} + NQ(1 - \frac{p}{p_{cr}}) $$

Первый член соответствует количеству поставляемого на рынок товара (то есть предложению), а второй член -- спросу.

Параметр $\gamma$ зависит от скорости оборота товаров на рынке. Как правило, время торгового оборота существенно меньше времени производственного цикла 
$\tau$. При заданном $M$ уравнение (3) описывает быстрое стремление цены к равновесному значению цены, которое устойчиво.

В этом случае уравнение (3) можно заменить алгебраическим соотношением

$$ \tag{4} -\frac{M \delta}{\tau \tilde{p}} + NQ(1 - \frac{p}{p_{cr}}) = 0 $$

Из (4) следует, что равновесное значение цены p равно

$$ \tag{5} p = p_{cr}(1 - \frac{M \delta}{\tau \tilde{p} Nq}) $$

Уравнение (2) с учетом (5) приобретает вид

$$ \tag{6} \frac{\partial M}{\partial t} = M \frac{\delta}{\tau}(\frac{p_{cr}}{\tilde{p}} - 1) - M^2 (\frac{\delta}{\tau \delta{p}})^2 \frac{p_{cr}}{Nq} 
- \kappa $$

Уравнение (6) имеет два стационарных решения, соответствующих условию $\frac{\partial M}{\partial t}$ = 0

$$ \tag{7} \tilde{M}_{1,2} = \frac{1}{2}a \pm \sqrt{\frac{a^2}{4} - b}$$

где

$$ \tag{8} a = Nq(1 - \frac{\tilde{p}}{p_{cr}}) \tilde{p} \frac{\tau}{\delta}, b = \kappa Nq \frac{(\tau \tilde{p})^2}{p_{cr} \delta^2} $$

Из (7) следует, что при больших постоянных издержках (в случае $a^2 < 4b$) стационарных состояний нет. Это означает, что в этих условиях фирма не может 
функционировать стабильно, то есть, терпит банкротство. Однако как правило, постоянные затраты малы по сравнению с переменными (то есть, $b \ll a^2$) и 
играют роль только в случае, когда оборотные средства малы. При $b \ll a$ стационарные значения M равны

$$ \tag{9} \tilde{M}_+ = Nq \frac{\tau}{\delta}(1 - \frac{\tilde{p}}{p_{cr}}) \tilde{p}, \tilde{M}_- = \kappa \tilde{p} \frac{\tau}{\delta(p_{cr} 
- \tilde{p})}$$

Первое состояние $\tilde{M}_+$ устойчиво и соответствует стабильному функционированию предприятия. Второе состояние $\tilde{M}_-$ неустойчиво, так что 
при $M < \tilde{M}_-$ оборотные средства падают ($\partial M / \partial t < 0$), то есть, фирма идет к банкротству. По смыслу $\tilde{M}_-$ соответствует 
начальному капиталу, необходимому для входа в рынок.

В обсуждаемой модели параметр $\delta$ всюду входит в сочетании с $\tau$. Это значит, что уменьшение доли оборотных средств, вкладываемых в производство, 
эквивалентно удлинению производственного цикла. Поэтому мы в дальнейшем положим: $\delta$ = 1, а параметр $\tau$ будем считать временем цикла с учётом 
сказанного.

Рассмотрим две фирмы, производящие взаимозаменяемые товары одинакового качества и находящиеся в одной рыночной нише. Последнее означает, что у потребителей 
в этой нише нет априорных предпочтений, и они приобретут тот или иной товар, не обращая внимания на знак фирмы.

В этом случае, на рынке устанавливается единая цена, которая определяется балансом суммарного предложения и спроса. Иными словами, в рамках нашей модели 
конкурентная борьба ведётся только рыночными методами. То есть, конкуренты могут влиять на противника путем изменения параметров своего производства: 
себестоимость, время цикла, но не могут прямо вмешиваться в ситуацию на рынке («назначать» цену или влиять на потребителей какимлибо иным способом).

Уравнения динамики оборотных средств запишем по аналогии с (2) в виде

$$ \tag{10} \begin{cases} \frac{\partial M_1}{\partial t} = - \frac{M_1}{\tau_1} + N_1q(1 - \frac{p}{p_{cr}})p - \kappa_1 \\ \frac{\partial M_2}{\partial t} 
= - \frac{M_2}{\tau_2} + N_2q(1 - \frac{p}{p_{cr}})p - \kappa_2 \end{cases} $$

где использованы те же обозначения, а индексы 1 и 2 относятся к первой и второй фирме соответственно. Величины $N_1$ и $N_2$ -- числа потребителей, 
приобревших товар первой и второй фирмы.

Учтем, что товарный баланс устанавливается быстро, то есть, произведенный каждой фирмой товар не накапливается, а реализуется по цене $p$. Тогда

$$ \tag{11} \begin{cases} \frac{M_1}{\tau_1 \tilde{p}_1} = - N_1q(1 - \frac{p}{p_{cr}}) \\ \frac{M_2}{\tau_2 \tilde{p}_2} = - N_2q(1 - \frac{p}{p_{cr}}) 
\end{cases} $$

где $\tilde{p}_1$ и $\tilde{p}_2$ -- себестоимости товаров в первой и второй фирме.

С учетом (10) представим (11) в виде

$$ \tag{12} \begin{cases} \frac{\partial M_1}{\partial t} = - \frac{M_1}{\tau_1}(1 - \frac{p}{\tilde{p}_1}) - \kappa_1 \\ \frac{\partial M_2}{\partial t} 
= - \frac{M_2}{\tau_2}(1 - \frac{p}{\tilde{p}_2}) - \kappa_2 \end{cases} $$

Уравнение для цены по аналогии с (3)

$$ \tag{13} \frac{\partial p}{\partial t} = - \gamma (\frac{M_1}{\tau_1 \tilde{p}_1} + \frac{M_2}{\tau_2 \tilde{p}_2} - Nq (1 - \frac{p}{p_{cr}}) $$

Считая, как и выше, что ценовое равновесие устанавливается быстро, получим:

$$ \tag{14} p = p_{cr} (1 - \frac{1}{Nq} (\frac{M_1}{\tau_1 \tilde{p}_1} + \frac{M_2}{\tau_2 \tilde{p}_2})) $$

Подставив (14) в (12) имеем:

$$ \tag{15} \begin{cases} \frac{\partial M_1}{\partial t} = c_1 M_1 - b M_1 M_2 - a_1 M_1^2 - \kappa_1 \\ \frac{\partial M_2}{\partial t} = c_2 M_2 
- b M_1 M_2 - a_2 M_2^2 - \kappa_2 \end{cases} $$

где

$$ \tag{16} a_1 = \frac{p_{cr}}{\tau_1^2 \tilde{p}_1^2 Nq}, a_2 = \frac{p_{cr}}{\tau_2^2 \tilde{p}_2^2 Nq}, b = \frac{p_{cr}}{\tau_1^2 \tilde{p}_1^2 
\tau_2^2 \tilde{p}_2^2 Nq}, c_1 = \frac{p_{cr} - \tilde{p}_1}{\tau_1^2 \tilde{p}_1^2}, c_2 = \frac{p_{cr} - \tilde{p}_2}{\tau_2^2 \tilde{p}_2^2} $$

Исследуем систему (15) в случае, когда постоянные издержки ($κ_1, κ_2$) пренебрежимо малы. И введем нормировку $t = c_1 \theta$. Получим следующую систему:

$$ \tag{17} \begin{cases} \frac{\partial M_1}{\partial \theta} = M_1 - \frac{b}{c_1} M_1 M_2 - \frac{a_1}{c_1} M_1^2 \\ \frac{\partial M_2}{\partial \theta} 
= \frac{c_2}{c_1} M_2 -\frac{b}{c_1} M_1 M_2 - \frac{a_2}{c_1} M_2^2 \end{cases} $$

# Выполнение лабораторной работы

1. Изучила начальные условия. Начальные значения объема оборотных средств первой и второй фирмы соответственно 5,4 и 5,1 млн единиц. Критическая стоимость 
продукта 27 тыс. единиц. 30 тыс. потребителей производимого продукта. Максимальная потребность одного человека в продукте в единицу времени равна 1. 
Длительность производственного цикла первой фирмы равна 8, а второй -- 9. Себестоимость продукта первой фирмы составляет 13, а второй -- 10,1.

2. Оформила начальные условия в код на Python:

![Выполнение работы 1](image/1.png){ #fig:002 width=70% }

![Выполнение работы 2](image/2.png){ #fig:003 width=70% }

3. Задала условия для времени: $t_{0} = 0$ -- начальный момент времени, $t_{max} = 50$ -- предельный момент времени, $dt = 0,01$ -- шаг изменения времени.

![Выполнение работы 3](image/4.png){ #fig:004 width=70% }

4. Запрограммировала вычисление коэффициентов $a_1, a_2, b, c_1, c_2$ для последующего использования в уравнениях: 

![Выполнение работы 4](image/5.png){ #fig:005 width=70% }

5. Запрограммировала функцию, описывающую систему уравнений для 1-ого и 2-ого случаев и запрограммировала решение всех систем уравнений: 

![Выполнение работы 5](image/6.png){ #fig:006 width=70% }

6. Для 1-ого случая нашла стационарное состояние системы.

Приравняла каждое уравнение системы к 0 и получила следующие корни:

$\begin{cases}
  \left[ 
    \begin{gathered} 
      M_{1.1} = 0, \\ 
      M_{1.2} = \frac{c_1 a_2 - b c_2}{a_1 a_2 - b^2} \\ 
    \end{gathered} 
  \right.
  \\
  \left[ 
    \begin{gathered} 
      M_{2.1} = 0, \\ 
      M_{2.2} = \frac{a_1 c_2 - b c_1}{a_1 a_2 - b^2} \\ 
    \end{gathered} 
  \right.
\end{cases}$

При этом стационарное состояние не может быть равно 0.

И получила следующее решение:

$$ \begin{cases} M_1 = \frac{c_1 a_2 - b c_2}{a_1 a_2 - b^2} \\ M_2 = \frac{a_1 c_2 - b c_1}{a_1 a_2 - b^2} \end{cases} $$

7. Запрограммировала подсчет стационарного состояния (на рисунке уже есть резульат):

![Выполнение работы 6](image/7.png){ #fig:007 width=70% }

8. Описала построение графиков и отметку стационарного состояния для 1-ого и 2-ого случаев:

![Выполнение работы 7](image/8.png){ #fig:008 width=70% }

![Выполнение работы 8](image/9.png){ #fig:009 width=70% }

# Выводы

Построила модель конкуренции двух фирм с помощью Python.

Нашла стационарное состояние системы для 1-ого случая.

В двух случаях вторая фирма  будет иметь по итогу больше оборотных средств, чем первая.