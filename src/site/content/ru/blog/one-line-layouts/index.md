---
title: Десять современных макетов одной строкой CSS
subhead: В этом посте освещаются несколько эффективных строк CSS, которые выполняют массу работы и помогают создавать надежные современные макеты.
authors:
  - una
description: В этом посте освещаются несколько эффективных строк CSS, которые выполняют массу работы и помогают создавать надежные современные макеты.
date: 2020-07-07
hero: image/admin/B07IzuMeRRGRLH9UQkwd.png
alt: Макет Святого Грааля.
tags:
  - blog
  - css
  - layout
  - mobile
---

{% YouTube 'qm0IfG1GyZU' %}

Современные CSS-макеты позволяют разработчикам писать поистине содержательные и надежные правила стилей всего несколькими нажатиями клавиш. В приведенном выше докладе и этой дополнительной публикации рассмотрены 10 эффективных строк CSS, которые выполняют массу работы.

{% Glitch { id: '1linelayouts', path: 'README.md', height: 480 } %}

Чтобы повторить действия этих демонстраций или самостоятельно попробовать нечто похожее, обратите внимание на блок Glitch выше или посетите [1linelayouts.glitch.me](https://1linelayouts.glitch.me).

## 01. Супер-центрирование: `place-items: center`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/01-place-items-center.mp4">
  </source></video></figure>

В первом «однострочном» макете разберемся с самой страшной тайной CSS — центрированием. Знайте: с использованием [`place-items: center`](https://developer.mozilla.org/docs/Web/CSS/place-items) все гораздо проще, чем вы думаете.

Сначала укажите `grid` в качестве значения `display`, а затем напишите `place-items: center` в том же элементе. `place-items` — это сокращение для одновременной установки `align-items` и `justify-items`. Если ему присвоить значение `center`, и для `align-items`, и для `justify-items` будет применен `center`.

```css/2
.parent {
  display: grid;
  place-items: center;
}
```

Это позволяет идеально центрировать контент внутри родительского элемента независимо от внутреннего размера.

## 02. Разрезанный блин: `flex: <grow> <shrink> <baseWidth>`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/02-deconstructed-pancake-1.mp4">
  </source></video></figure>

Дальше у нас разрезанный блин! Это распространенный макет, например, для маркетинговых сайтов, в котором может быть строка из 3 элементов, обычно с изображением, заголовком и каким-либо текстом, описывающим некоторые особенности продукта. Нам нужно, чтобы на мобильных устройствах эти элементы укладывались в пачку и расширялись по мере увеличения размера экрана.

Если задействовать Flexbox для этого эффекта, вам не потребуются медиа-запросы для позиционирования этих элементов при изменении размера экрана.

Сокращение [`flex`](https://developer.mozilla.org/docs/Web/CSS/flex) означает: `flex: <flex-grow> <flex-shrink> <flex-basis>`.

Поэтому если вы хотите, чтобы блоки занимали пространство размером `<flex-basis>`, уменьшались при меньших размерах, но не *растягивались*, заполняя дополнительное пространство, напишите: `flex: 0 1 <flex-basis>`. В этом случае ваш `<flex-basis>` равен `150px`, поэтому код выглядит так:

```css/5
.parent {
  display: flex;
}

.child {
  flex: 0 1 150px;
}
```

Если же вы *хотите*, чтобы блоки растягивались и заполняли пространство так же, как при переносе на следующую строку, установите для `<flex-grow>` значение `1`, чтобы это выглядело так:

```css/5
.parent {
  display: flex;
}

.child {
  flex: 1 1 150px;
}
```

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/02-deconstructed-pancake-2.mp4">
  </source></video></figure>

Теперь, когда вы увеличиваете или уменьшаете размер экрана, эти гибкие элементы как сжимаются, так и увеличиваются.

## 03. Слово боковой панели: `grid-template-columns: minmax(<min>, <max>) …)`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/03-sidebar-says.mp4">
  </source></video></figure>

В этой демонстрации используется функция [minmax](https://developer.mozilla.org/docs/Web/CSS/minmax) для макетов с сеткой. Здесь мы устанавливаем минимальный размер боковой панели `150px`, а на больших экранах позволяем ей растягиваться до `25%`. Боковая панель всегда будет занимать `25%` горизонтального пространства своего родителя, пока эти `25%` не станут меньше `150px`.

Добавьте это в качестве значения grid-template-columns: `minmax(150px, 25%) 1fr`. Элемент в первом столбце (боковой панели в данном случае) получает `minmax` из `150px` и `25%`, а второй элемент (здесь это раздел `main`) занимает остальную часть пространства в виде единого `1fr`.

```css/2
.parent {
  display: grid;
  grid-template-columns: minmax(150px, 25%) 1fr;
}
```

## 04. Стопка блинов: `grid-template-rows: auto 1fr auto`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/04-pancake-stack.mp4">
  </source></video></figure>

В отличие от разрезанного блина, в этом примере дочерние элементы не переносятся при изменении размера экрана. Этот макет, обычно называемый [липким нижним колонтитулом](https://developer.mozilla.org/docs/Web/CSS/Layout_cookbook/Sticky_footers), часто используется как для веб-сайтов, так и для приложений, в мобильных приложениях (нижний колонтитул обычно является панелью инструментов) и веб-сайтах (одностраничные приложения часто используют этот глобальный макет).

Добавление к компоненту `display: grid` даст вам сетку с одним столбцом, однако высота основной области будет равна высоте содержимого с нижним колонтитулом под ней.

Чтобы колонтитул прилипал к низу, добавьте:

```css/2
.parent {
  display: grid;
  grid-template-rows: auto 1fr auto;
}
```

Это заставляет содержимое верхнего и нижнего колонтитула автоматически принимать размер дочерних элементов и применяет оставшееся пространство (`1fr`) к основной области, в то время как строка масштабом `auto` будет принимать размер минимального содержимого своих дочерних элементов, так что когда контент будет увеличиваться, для корректировки вместе с ним будет увеличиваться и сама строка.

## 05. Классический макет Святого Грааля: `grid-template: auto 1fr auto / auto 1fr auto`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/05-holy-grail.mp4">
  </source></video></figure>

В классическом макете святого Грааля есть верхний колонтитул, нижний колонтитул, левая боковая панель, правая боковая панель и основной контент. Он похож на предыдущий макет, но теперь в нем есть боковые панели!

Чтобы описать всю эту сетку с помощью одной строки кода, используйте свойство `grid-template`. Оно позволяет одновременно задавать и строки, и столбцы.

Пара свойств-значений выглядит так: `grid-template: auto 1fr auto / auto 1fr auto`. Косая черта между первым и вторым списками, разделенными пробелами, — это разрыв между строками и столбцами.

```css/2
.parent {
  display: grid;
  grid-template: auto 1fr auto / auto 1fr auto;
}
```

Как и в последнем примере, где у верхнего и нижнего колонтитулов был контент с автоматическим размером, здесь левая и правая боковые панели автоматически масштабируются в зависимости от внутреннего размера своих дочерних элементов. Однако на этот раз это горизонтальный размер (ширина), а не вертикальный (высота).

## 06. 12-интервальная сетка: `grid-template-columns: repeat(12, 1fr)`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/06-12-span-1.mp4">
  </source></video></figure>

Далее по списку у нас еще один классический пример: сетка из 12 интервалов. Вы можете быстро описывать сетки в CSS с помощью функции `repeat()`. Использование `repeat(12, 1fr);` для столбцов шаблона сетки дает вам 12 столбцов по `1fr`.

```css/2,6
.parent {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
}

.child-span-12 {
  grid-column: 1 / 13;
}
```

Теперь у вас есть сетка из 12 столбцов, и мы можем разместить в ней наши дочерние элементы. Один из способов это сделать — разместить их с помощью линий сетки. Например, `grid-column: 1 / 13` займет все пространство от первой линии до последней (13-й) и растянется на 12 столбцов. `grid-column: 1 / 5;` охватит первые четыре.

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/06-12-span-2.mp4">
  </source></video></figure>

Другой способ это описать — использовать ключевое слово `span`. С помощью `span` вы устанавливаете начальную линию, а затем — число столбцов, которое нужно захватить от этой начальной точки. В этом случае `grid-column: 1 / span 12` будет эквивалентно `grid-column: 1 / 13`, а `grid-column: 2 / span 6` будет эквивалентно `grid-column: 2 / 8` .

```css/1
.child-span-12 {
  grid-column: 1 / span 12;
}
```

## 07. RAM (Repeat, Auto, MinMax): `grid-template-columns(auto-fit, minmax(<base>, 1fr))`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/07-ram-1.mp4">
  </source></video></figure>

В седьмом примере мы объединим некоторые концепции, о которых вы уже узнали, чтобы создать адаптивный макет с гибкими автоматически позиционируемыми дочерними элементами. Будет круто. Ключевые термины, которые следует запомнить, — это `repeat`, `auto-(fit|fill)` и `minmax()'` — вы их помните по аббревиатуре «RAM».

Все вместе это выглядит так:

```css/2
.parent {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
}
```

Вы снова используете repeat, но на этот раз с применением `auto-fit` вместо явного числового значения. Это позволяет автоматически позиционировать дочерние элементы. Потомки также имеют базовое минимальное значение `150px` с максимальным значением `1fr`, то есть на небольших экранах они будут занимать полную ширину `1fr`, и по мере достижения `150px` в ширину они начнут выстраиваться на одной и той же линии.

При `auto-fit` блоки будут растягиваться, если их горизонтальный размер превышает 150 пикселей, чтобы заполнить все оставшееся пространство. Однако, если изменить его на `auto-fill`, они не будут растягиваться при превышении своего базового размера в функции minmax:

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/07-ram-2.mp4">
  </source></video></figure>

```css/2
.parent {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
}
```

## 08. Линейка: `justify-content: space-between`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/08-lineup.mp4">
  </source></video></figure>

Основной момент, который нужно продемонстрировать в следующем макете, — это `justify-content: space-between`, который помещает первый и последний дочерние элементы по краям ограничивающего их блока, а оставшееся пространство равномерно распределяется между элементами. В примере карточки помещаются в режим отображения Flexbox с направлением, заданным по столбцу с использованием `flex-direction: column`.

Это помещает заголовок, описание и блок изображения в вертикальный столбец внутри родительской карточки. Затем применение `justify-content: space-between` привязывает первый (заголовок) и последний (блок изображения) элементы к краям флексбокса, а описательный текст между ними размещается с равным интервалом для каждой крайней точки.

```css/3
.parent {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
```

## 09. Захватываем мой стиль: `clamp(<min>, <actual>, <max>)`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/09-clamping.mp4">
  </source></video></figure>

Здесь мы познакомимся с некоторыми методами с [поддержкой в меньшем количестве браузеров](https://caniuse.com/#feat=css-math-functions), при этом используем впечатляющие возможности для реализации макетов и адаптивного дизайна пользовательского интерфейса. В этой демонстрации вы устанавливаете ширину с помощью clamp следующим образом: `width: clamp(<min>, <actual>, <max>)`.

Это устанавливает абсолютный минимальный и максимальный размер, а также фактический размер. Со значениями это выглядит так:

```css/1
.parent {
  width: clamp(23ch, 60%, 46ch);
}
```

Минимальный размер здесь составляет `23ch` или 23 символа, а максимальный — `46ch`, 46 символов. [Единицы ширины символа](https://meyerweb.com/eric/thoughts/2018/06/28/what-is-the-css-ch-unit/) основаны на размере шрифта элемента (в частности, на ширине знака `0`). «Фактический» размер составляет 50%, что составляет 50% ширины родительского элемента.

Здесь функция `clamp()` позволяет этому элементу сохранять ширину 50% *до тех пор, пока* 50% не станет больше, чем `46ch` (в более широких областях просмотра), или меньше, чем `23ch` (в меньших областях просмотра). Видно, что по мере того, как я растягиваю и сжимаю родительский элемент, ширина карточки увеличивается до максимальной точки и уменьшается до минимума. Затем она остается в центре родительского элемента, поскольку мы применили дополнительные свойства для ее центрирования. Это обеспечивает более разборчивые макеты, поскольку текст не будет слишком широким (более `46ch`) или слишком сжатым и узким (менее `23ch`).

Также это прекрасный способ реализовать адаптивную типографику. Например, вы можете написать: `font-size: clamp(1.5rem, 20vw, 3rem)`. В этом случае размер шрифта заголовка всегда будет оставаться в пределах от `1.5rem` до `3rem`, но будет увеличиваться и уменьшаться в зависимости от фактического значения `20vw`, чтобы соответствовать ширине области просмотра.

Это замечательный метод для обеспечения удобочитаемости с минимальным и максимальным значением размера, но помните, что он поддерживается не во всех современных браузерах, поэтому убедитесь, что у вас есть запасные варианты, и проведите тестирование.

## 10. Сохраняем масштаб: `aspect-ratio: <width> / <height>`

<figure class="w-figure">
  <video controls autoplay loop muted playsinline class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/one-line-layouts/10-aspectratio.mp4">
  </source></video></figure>

И, наконец, последний инструмент компоновки — наиболее экспериментальный. Недавно он был представлен в Chrome Canary версии Chromium 84, плюс Firefox прилагает активные усилия для его реализации, но в настоящее время его нет ни в одной стабильной версии браузера.

И все же я хочу упомянуть о нем, потому что эта проблема встречается очень часто. Речь идет всего лишь о поддержании соотношения сторон изображения.

Благодаря `aspect-ratio`, когда я изменяю размер карточки, зеленый визуальный блок поддерживает соотношение сторон 16 x 9. Мы соблюдаем соотношение сторон с помощью `aspect-ratio: 16 / 9`.

```css/1
.video {
  aspect-ratio: 16 / 9;
}
```

Чтобы сохранить соотношение сторон 16 x 9, не используя это свойство, вам нужно будет использовать [прием с `padding-top`](https://css-tricks.com/aspect-ratio-boxes/) и задать padding равным `56.25%`, чтобы установить отношение высоты к ширине. Скоро для этого у нас появится свойство, чтобы не приходилось использовать трюки и вычислять проценты. Вы можете сделать квадрат с соотношением `1 / 1` отношение, прямоугольник `2 / 1` и вообще что угодно для масштабирования изображения с заданным соотношением размеров.

```css/1
.square {
  aspect-ratio: 1 / 1;
}
```

Хотя эта функция все еще находится на стадии разработки, о ней стоит знать, поскольку она решает массу трудностей при разработке, с которыми я и сама сталкивалась не раз, особенно когда речь идет о видео и блоках iframe.

## Заключение

Благодарим вас за то, что вы прошлись с нами по 10 эффективным строкам CSS. Чтобы узнать больше, посмотрите [полное видео](https://youtu.be/qm0IfG1GyZU) и попробуйте поработать с [демонстрациями](https://1linelayouts.glitch.me).