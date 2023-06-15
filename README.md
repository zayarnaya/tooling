Лекция 3: Тулинг
=============
Задание 2
--------

*NB: ширина экрана 1286px*

Вкладка Network
----

**Профиль загрузки ресурсов в HAR** лежит тут

**Скриншот** лежит здесь (длинннннный, как орбит полярная ночь)

**Неоптимальные места:**

- лишний размер: картинки больше, чем место под них, но незначительно. Примеры:

  **ширина 395 нужно/460 грузится**

  `<img loading="lazy" src="/images/branding/10/imageTop_1628667062.7856.jpg" data-url="/images/branding/10/imageTop_1628667062.7856.jpg" alt="-">`

  `<img loading="lazy" src="/images/branding/10/imageRight_1628667062.7146.jpg" data-url="/images/branding/10/imageRight_1628667062.7146.jpg" alt="-">`

  **ширина 1100 нужно /1280 грузится**

  `<img loading="lazy" src="/images/branding/10/imageTop_1628667062.7856.jpg" data-url="/images/branding/10/imageTop_1628667062.7856.jpg" alt="-">`

  **ширина 90 нужно /140 грузится** – пустая картинка, в загрузке весит 500 kb, вероятно, ее можно было бы заменить на div  с фиксированной шириной и высотой

  `<img loading="lazy" class="moreInteresting__image" src="/assets/f8e4500d/assets/frontend/images/empty140x95.gif" alt="Генеральный Директор" data-url="https://www.gd.ru/images/covers/06-23_gd.png" title="Генеральный Директор">`

- дубли

  <скрин>

- некоторые картинки выдают редирект 302 temporarily moved. Во-первых, это вынуждает сайт делать два запроса вместо одного, во-вторых, код 302 удерживает поисковые роботы от обновления ссылок (что плохо для SEO)

  <тут должен быть скрин>

- несжатые файлы со своего сервера

  <скрин>
- в части запросов используется протокол https/1.1, в котором меньше потоков, чем в 2 или 3

  <скрин>
- где-то зарыт второй счетчик Яндекс.Метрики (где именно - не нашла), соответственно запросы ходят в двойном объеме

  <скрин метрики>

- файлы bootstrap, во-первых, загружаются из cdn (возможно, имеет смысл держать их на собственном сервере), во-вторых, загружается и бандл, и отдельный js, что излишне
  
  <скрин >

- медленно загружающиеся ресурсы

  <скрин>

Ресурсов, блокирующих загрузку, не нашла, однако медленные ресурсы со скрина выше откладывают событие полной загрузки страницы, возможно, имеет смысл их грузить через async/defer

Вкладка Perfomance
----

**Профиль загрузки страницы** лежит тут (.zip)

**First Paint / FP**: 548.79ms

**First Contentful Paint / FCP**: 548.79ms

**Largest Contentful Paint / LCP**: 1481.8ms

**DOM Content Loaded / DCL**: 1232.9ms

**Load / L**: 31143.1ms

**Элемент, на котором происходит LCP**: `<img loading="lazy" src="/images/branding/10/imageTop_1628667062.7856.jpg" data-url="/images/branding/10/imageTop_1628667062.7856.jpg" alt="-">`

**Loading**: 43ms

**Scripting**: 2168ms

**Rendering**: 734ms

**Painting**: 221ms
<скрин>

Вкладка Coverage
----
**Профиль загрузки страницы** лежит тут

<скрин вкладки>

**Unused CSS**: ~ 444 884 bytes

**Unused CSS + JS**: 109157 bytes

**Unused JS**: ~ 2200477 bytes

Часть файлов и вовсе не используется:
`https://www.gd.ru/assets/f8e4500d/widgets/views/ContentRatingWidget/assets/css/rating.css?cache=5a6fa72bdfc8007242bf089feb2ff92203bc8762`

`https://www.gd.ru/assets/f8e4500d/modules/id2Auth/assets/css/social-buttons.css?cache=5a6fa72bdfc8007242bf089feb2ff92203bc8762`

В целом 
---
- Страница не оптимизирована под мою ширину экрана, часть контента “вылезает” за края экрана
- Очень много всплывающих окон
- Очень много файлов .css, .js, которые тормозят загрузку
- В консоль выводится некоторая отладочная информация – это на проде!


Задание 2*
---

Все, что относится к **вкладкам Network и Coverage** более быстрой загрузки, применимо и для медленной, что, возможно, говорит о том, что страница не оптимизирована под плохой канал.

**Профиль загрузки страницы в HAR** лежит здесь

**Профиль Coverage** лежит тут

<скрин нетворк>

<скрин покрытие>

Вкладка Perfomance
--
**Профиль загрузки страницы** лежит тут (.zip)

**First Paint / FP**: 9231ms

**First Contentful Paint / FCP**: 9231ms

**Largest Contentful Paint / LCP**: 44112.9ms

**DOM Content Loaded / DCL**: 36121.3ms

**Load / L**: 60142.3ms

**Элемент, на котором происходит LCP**: `<img loading="lazy" src="/images/branding/10/imageTop_1628667062.7856.jpg" data-url="/images/branding/10/imageTop_1628667062.7856.jpg" alt="-">`

**Loading**: 183ms

**Scripting**: 7492ms

**Rendering**: 13538ms

**Painting**: 4867ms

<скрин>





