# Дзен
## Содержание

* ### [Тема и целевая аудитория](#1)
* ### [Расчет нагрузки](#2)

## 1. Тема и целевая аудитория <a name="1"></a>
**Дзен** — блог-платформа, позволяющая просматривать и создавать свои статьи.

### MVP
- Регистрация
- Лента статей
- Создание статей 
- Комментирование статей
- Лайки

### Целевая аудитория 
[Статистика](https://ru.m.wikipedia.org/wiki/%D0%94%D0%B7%D0%B5%D0%BD_(%D0%BA%D0%BE%D0%BD%D1%82%D0%B5%D0%BD%D1%82%D0%BD%D0%B0%D1%8F_%D0%BF%D0%BB%D0%B0%D1%82%D1%84%D0%BE%D1%80%D0%BC%D0%B0)) показывает, что в среднем каждый день сервисом пользуются 20 млн. человек.

## 2. Расчет нагрузки <a name="2"></a>

* аудитория - 547 * 1млн + 937 * 0.5млн + 5000 * 0.1млн = 1.516 млрд([источник](https://vc.ru/media/186520-45-tysyach-blogerov-i-20-mln-polzovateley-v-den-yandeks-dzen-podvel-itogi-goda-i-rasskazal-ob-obnovleniyah-platformy))
* около 20 млн. пользователей ежедневно ([источник](https://vc.ru/media/186520-45-tysyach-blogerov-i-20-mln-polzovateley-v-den-yandeks-dzen-podvel-itogi-goda-i-rasskazal-ob-obnovleniyah-platformy))
* среднее время, проведенное в Дзен - 45 мин./день ([источник](https://vc.ru/media/186520-45-tysyach-blogerov-i-20-mln-polzovateley-v-den-yandeks-dzen-podvel-itogi-goda-i-rasskazal-ob-obnovleniyah-platformy))

Обычно, пользователь заходит на сайт по несколько раз в день.
Зная, что среднее время, проведенное в Instagram - 45 мин./день, предположим,
что пользователь заходит 5 раз в день, проводя на сайте по 9 минуты.

Теперь оценим трафик среднестатистического пользователя за одну сессию.

За 9 минуты пользования сайтом(просмотр ленты), я прочитал 2 статьи и 32 поста 
* на формирование ленты - 415 запросов и 15 мб
Их них:
* на комментарии - 32 запросов и 216 кб
* на картинки - 311 запросов и 10.5 мб
* на остальную статику - 72 запросов и 4.3 мб

Тогда за сутки среднестатистический пользователь:
* для динамики <br/>
  * для формирования ленты:
    * загрузит ```5 * 15 мб = 75 мб``` данных <br/>
    * сделает ```5 * 415 = 2075``` запросов
  * для просмотра комментариев: 
    * загрузит ```5 * 216 = 1080 кб``` данных <br/>
    * сделает ```5 * 32 = 160``` запроса

* для картинок <br/>
  * загрузит ```5 * 10.5 = 55.5 мб``` данных <br/>
  * сделает ```5 * 311 = 1555``` запросов

* для остальной статики <br/>
  * загрузит ```5 * 4.3 = 21.5 мб``` данных <br/>
  * сделает ```5 * 72 = 360``` запроса

Примем, что в день публикуется каждым активным блогером 1 пост - всего 45000([источник](https://vc.ru/media/186520-45-tysyach-blogerov-i-20-mln-polzovateley-v-den-yandeks-dzen-podvel-itogi-goda-i-rasskazal-ob-obnovleniyah-platformy)),
т.е. ~62 постов в секунду.
Согласно источнику([источник](https://vc.ru/media/186520-45-tysyach-blogerov-i-20-mln-polzovateley-v-den-yandeks-dzen-podvel-itogi-goda-i-rasskazal-ob-obnovleniyah-platformy)) при аудитории в 20 млн. пользователей, ежесекундно публиковалось 625 комментариев. 
Примем, что в каждом посте публикуется по 1 фото, тогда объем переданных данных равен ~130 кб(учитывая средний размер
фото в 125 кб и размер записи в таблице постов в 332 байт).
При лайке поста передается 75 байт, а при публикации комментария ~ 500 байт. Получается:
* на публикацию постов ```(130 кб * 1158) * (8/1024/1024) = 61 Мбит/с```
* на публикацию комментариев ```(500 байт * 625) * (8/1024/1024) = 2.4 Мбит/с```

Примем, что единовременная нагрузка на сервис равняется 80% ежедневной аудитории. Тогда, можем рассчитать среднюю 
нагрузку с учетом всех видов активностей пользователя:

Расcчитаем средний трафик:
* динамика:
  * формирование ленты и просмотр постов:```(75 мб * 16 000 000) * (8/1024/1024) = 9.376 Гбит/с```
  * публикация комментариев: ```(1080 кб * 16 000 000) * (8/1024/1024) = 131.8 Мбит/с```
* картинки: ```(55.5 мб * 16 000 000) * (8/1024/1024) = 6.9 Гбит/c```
* остальная статика:```(21.5 мб * 16 000 000) * (8/1024/1024) = 2.68 Гбит/c```

Расcчитаем средний RPS:
* формирование ленты и просмотр постов:```(2075 * 16 000 000) / (24 * 60 * 60) = 384 300 RPS```
* просмотр комментариев: ```(160 * 16 000 000) / (24 * 60 * 60) = 29 630 RPS```
* картинки: ```(1555 * 16 000 000) / (24 * 60 * 60) = 288 000 RPS```
* остальная статика: ```(360 * 16 000 000) / (24 * 60 * 60) = 66 670 RPS```
