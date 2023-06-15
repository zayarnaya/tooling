Лекция 3: Тулинг
=============
Задание 2
--------

*NB: ширина экрана 1286px*

Вкладка Network
----

**Профиль загрузки ресурсов в HAR** лежит [тут](https://github.com/zayarnaya/tooling/blob/main/filesFast/www.gd.ru2.har "Профиль загрузки .har")

**Неоптимальные места:**

- **лишний размер**: картинки больше, чем место под них, но незначительно. Примеры:

  *ширина 395 нужно/460 грузится*

  `<img loading="lazy" src="/images/branding/10/imageTop_1628667062.7856.jpg" data-url="/images/branding/10/imageTop_1628667062.7856.jpg" alt="-">`

  `<img loading="lazy" src="/images/branding/10/imageRight_1628667062.7146.jpg" data-url="/images/branding/10/imageRight_1628667062.7146.jpg" alt="-">`

  *ширина 1100 нужно /1280 грузится*

  `<img loading="lazy" src="/images/branding/10/imageTop_1628667062.7856.jpg" data-url="/images/branding/10/imageTop_1628667062.7856.jpg" alt="-">`

  *ширина 90 нужно /140 грузится* – пустая картинка, в загрузке весит 500 kb, вероятно, ее можно было бы заменить на div  с фиксированной шириной и высотой

  `<img loading="lazy" class="moreInteresting__image" src="/assets/f8e4500d/assets/frontend/images/empty140x95.gif" alt="Генеральный Директор" data-url="https://www.gd.ru/images/covers/06-23_gd.png" title="Генеральный Директор">`

- **дубли**

  ![дубли](https://github.com/zayarnaya/tooling/blob/main/filesFast/moreDoubles.png "это дубли у нас простые")

- некоторые картинки выдают **редирект 302** temporarily moved. Во-первых, это вынуждает сайт делать два запроса вместо одного, во-вторых, код 302 удерживает поисковые роботы от обновления ссылок (что плохо для SEO)

  ![302](https://github.com/zayarnaya/tooling/blob/main/filesFast/problems_302.png "302")

- **несжатые файлы** со своего сервера

  ![unzipped](https://github.com/zayarnaya/tooling/blob/main/filesFast/noZipping.png "несжатые файлы")
  
- в части запросов используется **протокол https/1.1**, в котором меньше потоков, чем в 2 или 3

  ![http/1.1](https://github.com/zayarnaya/tooling/blob/main/filesFast/http1-1.png "протокол https/1.1")
  
- где-то зарыт **второй счетчик Яндекс.Метрики** (где именно - не нашла), соответственно запросы ходят в двойном объеме

  ![metrics](https://github.com/zayarnaya/tooling/blob/main/filesFast/twoTags.png "Два счетчика, шеф!")

- файлы bootstrap, во-первых, **загружаются из cdn** (возможно, имеет смысл держать их на собственном сервере), во-вторых, загружается и бандл, и отдельный js, что излишне
  
  ![bootstrap](https://github.com/zayarnaya/tooling/blob/main/filesFast/bootstrap.png "bootstrap")

- **медленно загружающиеся ресурсы**

  ![sloooooow](https://github.com/zayarnaya/tooling/blob/main/filesFast/Network%20long%20requests.png "меееедленные запросы")

Ресурсов, блокирующих загрузку, не нашла, однако медленные ресурсы со скрина выше откладывают событие полной загрузки страницы, возможно, имеет смысл их грузить через async/defer

Вкладка Perfomance
----

**Профиль загрузки страницы** лежит [тут](https://github.com/zayarnaya/tooling/blob/main/filesFast/Trace-20230613T224355.json.zip "Профиль загрузки страницы Perfomance") (.zip)

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

![WebVitals](https://github.com/zayarnaya/tooling/blob/main/filesFast/Vitals.png "Vitals")

Вкладка Coverage
----
**Профиль загрузки страницы** лежит [тут](https://github.com/zayarnaya/tooling/blob/main/filesFast/Coverage-20230613T224618.json "Профиль загрузуи страницы - Coverage")

**Скриншот** лежит [здесь](https://github.com/zayarnaya/tooling/blob/main/filesFast/CoverageByUsage.png "Скриншот Coverage") (длинннннный, как орбит полярная ночь), [тут только css](https://github.com/zayarnaya/tooling/blob/main/filesFast/CoverageByType_CSS.png "Coverage для CSS"), [тут только для js](https://github.com/zayarnaya/tooling/blob/main/filesFast/CoverageByType_JS.png "Coverage для js")

Объем неиспользованного **CSS**: ~ 444 884 bytes / 434.46kb

Объем неиспользованного **CSS + JS**: 109 157 bytes / 106.6kb

Объем неиспользованного **JS**: ~ 2 200 477 bytes / 2 148.9kb

(считалось из джейсона, поэтому не очень уверена, что правильно)

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

Все, что относится к **вкладкам Network и Coverage** более быстрой загрузки, применимо и для медленной, что, возможно, говорит о том, что страница не оптимизирована под плохой канал. Грузится чудовищно долго.

**Профиль загрузки страницы в HAR** лежит [здесь](https://github.com/zayarnaya/tooling/blob/main/filesSlow/www.gd.ru.har.zip "Профиль медленной загрузки страницы .har") (.zip)

**Профиль Coverage** лежит [тут](https://github.com/zayarnaya/tooling/blob/main/filesSlow/Coverage-20230614T211432.json "Профиль Coverage медленной загрузки")

**Скриншот вкладки Network**

![Network](https://github.com/zayarnaya/tooling/blob/main/filesSlow/network.png "Network slow")

**Скриншот вкладки Coverage**

![Coverage](https://github.com/zayarnaya/tooling/blob/main/filesSlow/coverage.png "Coverage slow")

Вкладка Perfomance
--
**Профиль загрузки страницы** лежит [тут](https://github.com/zayarnaya/tooling/blob/main/filesSlow/Trace-20230615T124208.json.zip "Профиль Perfomance медленной загрузки") (.zip)

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

![WebVitals](https://github.com/zayarnaya/tooling/blob/main/filesSlow/vitals.png "WebVitals slow")





