---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе 3"
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

Построить упрощенную модель боевых действий с помощью Python.

# Задание

**Вариант 49**
Между страной $Х$ и страной $У$ идет война. Численности состава войск исчисляются от начала войны 
и являются временными функциями $x(t)$ и $y(t)$. В начальный момент времени страна $Х$ имеет армию 
численностью 36 800 человек, а в распоряжении страны $У$ армия численностью в 41 700 человек. Для 
упрощения модели считаем, что коэффициенты $a, b, c, h$ постоянны. Также считаем $P(t)$ и $Q(t)$
непрерывными функциями.

Постройте графики изменения численности войск армии $Х$ и армии $У$ для следующих случаев:

1. Модель боевых действий между регулярными войсками
$$\frac{\partial x}{\partial t} = -0,35x(t)-0,776y(t)+\sin (5,5t)+1$$
$$\frac{\partial y}{\partial t} = -0,519x(t)-0,573y(t)+\cos (2,5t)+1$$

2. Модель ведение боевых действий с участием регулярных войск и партизанских отрядов
$$\frac{\partial x}{\partial t} = -0,342x(t)-0,615y(t)+|\sin (2t)|$$
$$\frac{\partial y}{\partial t} = -0,443x(t)y(t)-0,4y(t)+|\cos (13t)|$$

# Выполнение лабораторной работы

**Боевые действия между регулярными войсками**

Изучила начальные условия. Коэффициент смертности, не связанный с боевыми действиями, у первой
армии 0,35, а у второй -- 0,573. Коэффициент эффективности первой и второй армии 0,519 и 
0,776 соответственно.  Функция, описывающая подход подкрепление первой армии, $P(t) = \sin (5,5t)\ + 1$, 
подкрепление второй армии описывается функцией $Q(t) = \cos (2,5t)\ + 1$. $x_{0} = 36800$ -- численность
1-ой армии, $y_{0} = 41700$ -- численность 2-ой армии.

**Боевые действия с участием регулярных войск и партизанских отрядов**

Изучила начальные условия. Коэффициент смертности, не связанный с боевыми действиями, у первой
армии 0,342, а у второй -- 0,4. Коэффициент эффективности первой и второй армии 0,443 и 
0,615 соответственно.  Функция, описывающая подход подкрепление первой армии, $P(t) = |\sin (2t)|$, 
подкрепление второй армии описывается функцией $Q(t) = |\cos (13t)|$. $x_{0} = 36800$ -- численность
1-ой армии, $y_{0} = 41700$ -- численность 2-ой армии.

1. Оформила начальные условия в код на Python:

![Выполнение работы 01](image/1.png){ #fig:001 width=70% }

2. Добавила в программу условия, описывающие время:

![Выполнение работы 02](image/2.png){ #fig:002 width=70% }

3. Запрограммировала заданную систему дифференциальных уравнений, описывающих изменение численности
армий:

![Выполнение работы 03](image/3.png){ #fig:003 width=70% }

![Выполнение работы 04](image/4.png){ #fig:004 width=70% }

4. Создала вектор начальной численности армий:

![Выполнение работы 05](image/5.png){ #fig:005 width=70% }

5. Запрограммировала решение системы уравнений;
 Описала построение графика изменения численности армий:

![Выполнение работы 06](image/6.png){ #fig:006 width=70% }

![Выполнение работы 07](image/7.png){ #fig:007 width=70% }

# Выводы

Построила упрощенную модель боевых действий с помощью Python.

В боевых действиях между регулярными войсками победит армия Y, причем ей на это потребуется довольно 
много времени и как мы можем заметить, сражение происходило достаточно долго (видим по графику, 
что численность армии X будет на исходе практический в предельный момент времени).

В боевых действиях с участием регулярных войск и партизанских отрядов  победит армия Х, причем 
длстаточно быстро (видим по графику, что армия Y потеряла всех бойцов практически
сразу после начала войны).
