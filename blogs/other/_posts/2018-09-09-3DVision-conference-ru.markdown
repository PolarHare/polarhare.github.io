---
layout: ru/blogs/other/post
title:  "3D Vision 2018: заметки"
date:   2018-09-09 21:30:00 +0300
lang:   ru
id:     22_3d_vision
---

[Программа конференции.](http://3dv18.uniud.it/program.html#program)


*День первый:*
-------------

**[Plane-Based Optimization of Geometry and Texture for RGB-D Reconstruction of Indoor Scenes](https://www.utdallas.edu/~xguo/3DV2018.pdf)**
=============================================================================================================================================

``TODO``: почитать, кажется можно найти хорошие идеи для описания моделей зданий плоскостями (т.е. для векторизации зданий).

*День второй:*
-------------

**Robust Fitting of Subdivision Surfaces for Smooth Shape Analysis**
=======================================================================

``TODO``: почитать, кажется много хороших идей с хорошей математикой про децимацию модели.

**FEATS: Synthetic Feature Tracks for Structure from Motion Evaluation**
===========================================================================

Проблемы:

 - Нет выводов по тому какие перепады углов/масштаба и другие характеристики имеет смысл требовать от хорошего облета
 - Не планируется развитие до motion planner-а (автор сказал что он закончил свой PhD)

Плюсы:

 - Успех/неуспех предполагаемого пролета оценивается по ключевым точкам (поэтому быстрый прогноз)

**Semantic Classification of 3D Point Clouds with Multiscale Spherical Neighborhoods**
=========================================================================================

Проблемы:

 - Автор не увидел почти такой же статьи от [Pix4D](https://pdfs.semanticscholar.org/67bc/85ec9591d41c015f9570fe7121eac71c3d4b.pdf) (т.е. сравнения нет)
 - Причина выбора сфер вместо KNN - субъективная симпатия к математической красоте и четкой обусловленности, реальные же проблемы KNN упомянутые в статье Pix4D успешно решают используя пирамиду облаков точек с фиксированной детализацией
 - Не опробовал GBT (только random forest), по словам автора т.к. в статье от которой они отталкивались GBT идет наравне с random forest

Плюсы:

 - Хорошая работа по классификации, могут быть полезные фичи которых не было в Pix4D
 
*День третий:*
-------------

Keynote Session: **[Geometric deep learning](http://geometricdeeplearning.com/)**
=================================================================================

``TODO``: почитать, кажется хорошим и обоснованным подходом, с нормальной математикой и глубоким взглядом.

*День четвертый:*
-----------------

Tutorial: **[Learning-based depth estimation from stereo and monocular images: successes, limitations and future challenges](https://sites.google.com/view/3dv-2018-depth-from-image/home)**
============================================================================================================================================================================================

1. По картинке (чтобы увидеть что это небо/бестекстурный фон) и по карте глубины (чтобы увидеть что она неконсистентна, несмотря на консистентную текстуру) подавлять небо/фон. Данные будет несложно сделать насыщенными и не domain-biased навязав учитывание вариации цвета, а не самого цвета (случайно линейно преобразуя интенсивности и т.п.). И вероятно карта глубины не нужна, возможно достаточно и надежнее будет давать бинарную маску наличия пикселя в карте глубины (что он прошел left-right consistency check и т.п.).
2. SGM aggregation w.r.t. confidence for each direction.
3. Более широкое множество параметров P можно настраивать нейронкой по картинке. В нашем случае должно быть полезно и достаточно аккуратно выбрав датасет перебрать и фиксировать те P и коэффициент учета градиента, которые уже есть.
4. SGM aggregation: выбор победителя через random forest. (SGM-forest)
5. Можно confidence ведь рассчитать из того насколько согласованы между направлениями победители.
6. Забавный пейпер - [EdgeStereo](https://arxiv.org/pdf/1803.05196.pdf) - предсказывают одновременно карту диспаритета и карту границ.
7. [MVSNet](https://github.com/YoYo000/MVSNet) очень достойное место занимает в [Tanks and Temples](https://www.tanksandtemples.org/leaderboard/).
8. Любопытное направление: **Volume sweeping and learned photo-consistency**.
9. [Zoom and learn](https://arxiv.org/pdf/1803.06641.pdf) чтобы четче была глубина на границах untrained domain предсказывают по апкскейлу. Это кажется признаком того что они плохо понимают что происходит.
