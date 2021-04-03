---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе 4"
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

Построить модель гармонических колебаний с помощью Python.

# Задание

**Вариант 49**
Постройте фазовый портрет гармонического осциллятора и решение уравнения гармонического осциллятора для следующих случаев:

1. Колебания гармонического осциллятора без затуханий и без действий внешней силы $\ddot {x} + 18x = 0$

2. Колебания гармонического осциллятора c затуханием и без действий внешней силы $\ddot {x} + 8 \dot {x} + 2x = 0$

3. Колебания гармонического осциллятора c затуханием и под действием внешней силы $\ddot {x} + 3 \dot {x} + 7x = 3 \sin (7t)$

На интервале $t \in [0; 73]$ (шаг 0,05) с начальными условиями $x_0 = 1,3, y_0 = -0,3$

# Выполнение лабораторной работы

1.Уравнение свободных колебаний гармонического осциллятора имеет следующий вид:
$$ \ddot {x} + 2 \gamma \dot {x} + \omega _0^2x = f(t) $$

Изучила начальные условия для колебания без затухания и без действий внешней силы. 
Перед нами уравнение консервативного осциллятора, энергия колебания которого сохраняется во времени. Т. е. потери в системе 
отсутствуют, значит, $\gamma = 0$. Собственная частота колебаний $\omega = 18$. $x_{0} = 1,3, y_{0} = -0,3$. Правая часть уравнения $f(t) = 0$.

Изучила начальные условия для колебания c затуханием и без действий внешней силы. 
Потери энергии в системе $\gamma = 8$. Собственная частота колебаний $\omega = 2$. $x_{0}$ и $y_{0}$ те же, что и выше. 
Правая часть уравнения такая же, как и выше.

Изучила начальные условия для колебания c затуханием и под действием внешней силы. 
Потери энергии в системе $\gamma = 3$. Собственная частота колебаний $\omega = 7$. $x_{0}$ и $y_{0}$ те же, что и выше.
Правая часть уравнения $f(t) = 3 \sin (7t)$.

2. Оформила начальные условия в код на Python;
Решение ищем на интервале $t \in [0; 37]$ (шаг 0,05), значит, $t_{0} = 0$ -- начальный момент времени, $t_{max} = 73$ -- предельный момент времени, 
$dt = 0,05$ -- шаг изменения времени.

![Выполнение работы 01](image/1.png){ #fig:001 width=70% }

![Выполнение работы 02](image/2.png){ #fig:002 width=70% }

3. Добавила в программу условия, описывающие время:

![Выполнение работы 03](image/3.png){ #fig:003 width=70% }

4. Представила заданное уравнение второго порядка в виде системы двух уравнений первого порядка и запрограммировала: 

![Выполнение работы 04](image/4.png){ #fig:004 width=70% }

5. Запрограммировала решение системы уравнений:

![Выполнение работы 05](image/5.png){ #fig:005 width=70% }

6. Описала построение фазового портрета:

![Выполнение работы 06](image/6.png){ #fig:006 width=70% }

![Выполнение работы 07](image/7.png){ #fig:007 width=70% }

![Выполнение работы 08](image/8.png){ #fig:008 width=70% }

# Выводы

Построила модель гармонических колебаний с помощью Python.

# Ответы на вопросы к лабораторной работе

1. $x = x_m cos (\omega t + \varphi _0)$. 

3.

$$\frac{\partial ^2 \alpha}{\partial t^2} + \frac{g}{L} sin{\alpha} = 0$$ 
 $\sin(\alpha ) ≈ \alpha$. 
$$\frac{\partial ^2 \alpha}{\partial t^2} + \frac{g}{L} \alpha = 0$$ или $$\frac{\partial ^2 \alpha}{\partial t^2} + \omega ^2 \alpha = 0$$

4. $$ \ddot {x} + \omega _0^2x = f(t) $$

$$ y = \dot{x} $$

  \begin{equation*} 
    \begin{cases}
      y = \dot{x}
      \\ 
      \dot{y} = - \omega _0^2x
    \end{cases}
  \end{equation*} 

