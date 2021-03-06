# Стекинг - отец вычислительной фотографии

В повседневной съемке смартфоны давно вытеснили громоздкие системные камеры. Заведомо проигрывая в оптических возможностях, карманные аппараты успешно конкурируют с ними, а где-то и значительно обходят.

## Как менялся рынок

Довольно наглядно ситуацию показывает график продаж смартфонов и фотоаппаратов соответственно.

<div align="center">
<img width=800 src=img/sales-graph.jpg/></div>

С ростом качества мобильных камер, они стали отбирать рынок.

## Все дело в свете

Разница в размере матриц не позволяет смартфонам захватывать столько же света, сколько могут позволить профессиональные камеры.
Однако, с ростом скорости обработки и передачи информации, появились попытки исправить это алгоритмическим путем.

Изначально недостаток света можно попытаться скомпенсировать двумя путями: увеличением выдержки (времени записи света матрицей) или повышением параметра светочувствительности (ISO). Первый вариант не подходит для смартфона, так как обычно съемка происходит с рук и присутствует естественное дрожание. Это ведет к смазыванию. 

<div align="center">
<img width=600 src=img/blurry-night.jpg/></div>

Остается второй и единственный вариант - повышение ISO. Таким образом мы устанавливаем уровень "доверия" сенсора ко входящей информации. Даже ослабленный электрический импульс (от слабого потока света) теперь может попасть в итоговое изображение. Но есть нюанс - такую возможность получают и шумы, постоянно присутствующие в пространстве, но обычно не проходящие "фейсконтроль" при считывании.

<div align="center">
<img width=600 src=img/noisy-coffee.jpg/></div>

Полученное изображение шумит, это заметно невооруженным взглядом.
Конечно, мы можем применить один из простейших вариантов шумоподавления. Адаптивная фильтрация или линейной усреднение пикселей по соседним дает весьма неплохие результаты, хоть и слегка мылит изображение

<div align="center">
<img width=600 src=img/denoised-coffee.jpg/></div>

Но что делать, если шума слишком много? Если руки оператора дрожат ну очень сильно, а на улице ночь? Именно тут открывается глава вычислительной фотографии

## Вычислительная фотография

Стоит напомнить, что современные смартфоны начинают съемку сразу после открытия приложения камеры. Все эти кадры записываются в буфер. 
В случае съемки (фото или видео) - буфер это область высокоскоростной памяти. Для моделей попроще это обычно оперативная память, в то время как флагманские решения оснащаются сверхскоростной "кэш-памятью" прилегающей к фотосенсору.

Процесс склеивания большого числа снимков называется стекингом. Без этой технологии мы бы не слышали почти ничего о великом "машинном обучении", "искусственном интеллекте" и "нейросетях" в камерах.

### Если кто-то или что-то движется слишком быстро

Перед вами происходит невероятной действо, которое точно нельзя не снять. И вот он - кадр мечты: идеальные пропорции, игриво лезущий в объектив лучик солнца и пролетающая на заднем плане чайка. 

Сначала ваш мозг всё это осознает, восхищается и наконец понимает, как кадр сильно нужен. Начинает движение палец над кнопкой затвора, касается экрана. Сенсорный слой экрана улавливает касание. 

<div align="center">
<img width=600 src=img/touch.webp/></div>

Оно обрабатывается процессором и запускается процесс записи кадра.

Только к этому моменту объекты съемки уже переместились, дрожание рук увело луч солнца, а чайка как раз вылетает за рамки кадра.

Чтобы подобное происходило реже, был разработан протокол Zero Shutter Lag - ZSL. Так и получается, что к моменту нажатия затвора - изображение, о котором вы думали, уже существует, осталось лишь снять дополнительные кадры для его улучшения (например - расширения динамического диапазона). 

<div align="center">
<img width=600 src=img/motion.gif/></div>

### Если перед объективом тьма

Тут пока не существует однозначного решения. В противовес ZSL корпорация Google представила PSL или Positive Shutter Lag для съемки в ночных условиях. 
Дело в том, что отснятые до нажатия кнопки кадры скорее вносят беспорядок в ночную съемку. PSL начинает съемку специально с запозданием, чтобы минимизировать даже микроскопическую тряску от касания экрана. Конечно, требуется держать телефон максимально ровно для получения оптимального результата. Полученные кадры объединяются для минимизации шумов и создания краевого контраста.

Обратите внимание на четкость дерева.

<div align="center">
<img width=900 src=img/psl.jpg/></div>

Стоит отметить, что в темноте цвета пространства никуда не пропадают. При наличии достаточного количества света, изображение легко перепутать с дневным. Структура человеческого глаза не позволяет нам использовать колбочки (цветовое зрение) при недостаточном освещении. В этом случае используются палочки (оттенки серого), которые отличаются большей светочувствительностью.

<div align="center">
<img width=800 src=img/night.png/></div>

### Трудные световые условия

Было бы странно не упомянуть самую старшую и широко применимую технику с использованием стекинга - HDR. Расширение динамического диапазона позволяет получить сбалансированное по свету и тени изображение, раскрывая нюансы кадра. 

<div align="center">
<img width=900 src=img/hdr-plus.jpg/></div>

Тут в дело вступает вычислительный конвеер на примере технологии HDR+
Сюда же можно отнести наращивание четкости с помощью избыточной информации серии снимков.

<div align="center">
<img width=900 src=img/sharp.jpg/></div>

Пример использования вспышки, где съемка началась до подсветки.

<div align="center">
<img width=900 src=img/flash.jpg/></div>

### Склеивание в движении

Самым известным применением склеивания в движении являются панорамные снимки. Просто нажать кнопку и провести телефон в сторону.

<div align="center">
<img width=900 src=img/pano.jpg/></div>

Сейчас таким подходом пользуется, например, Super Res Zoom. Данные от смещения восстанавливают детали изображения.

<div align="center">
<img width=900 src=img/superes.jpg/></div>

Ну и конечно - имитация длинной выдержки для создания интересного эффекта

<div align="center">
<img width=900 src=img/long-expo.jpg/></div>

### Карты глубины

Все вышеописанные алгоритмы обработки упираются в небольшую, но очень важную деталь - камера не видит пространство в объеме, как это делает человек. 
Преодоление этого барьера позволило бы в значительной степени продвинуться в генеративных возможностях обработки. Понимая, как объекты расположены в пространстве, можно дорисовывать их, быстрее фокусироваться и наоборот - имитировать фокус. 

В 2011 году компания Lytro представила ни на что не похожую пленоптическую "камеру светового поля". Она записывала не готовое изображение, как это принято, а данные светового потока. Постобработка позволяла выбирать точку фокуса, глубину резкости и создавать искусственные искажения кадра вроде tilt-shift. Мы привыкли говорить о растровой фотографии, в то время как здесь был совершенно другой подход - векторный. Она не обладала высоким качеством и была скорее демонстрацией возможностей.

К сожалению, технология не получила массового распространения, найдя себя лишь в узких производственных сферах. 

<div align="center">
<img width=600 src=img/lytro.webp/></div>

Но идея получения пространственных данных не покидала инженеров, занимающихся вычислительной фотографией. Первые попытки были сделаны с добавлением дополнительных фото-датчиков

<div align="center">
<img width=900 src=img/cameras.webp/></div>

Это происходит подобно тому, как мозг человека осознает пространство и объем, получая стереоскопическое изображение с двух глаз.

Представьте, что вы никогда не двигались с места. Вы не можете представить объем объекта, не обойдя его со всех сторон, или представить масштабы помещения, не имея данных о своей ходьбе из прошлого. Так же и смартфон. 

Открывая камеру каждый раз в новом месте, мы не даем информации о размерах и глубине объектов вокруг. Для получения этих данных необходимо перемещаться с постоянно включенной записью. 

Частично эту проблему решают сенсоры расстояния вроде лидара (датчик, замеряющий глубину пространства) или его ~~удешевленныйт~~ упрощенный аналог - камера ToF (Time of Flight).

<div align="center">
<img width=600 src=img/tof.jpg/></div>

Однако, для более доступных смартфонов возможно лишь извлечение данных глубины из системы камер. В этом наибольшую эффективность показывают обученные модели нейронных сетей. Непрерывная съемка позволяет определять края движущихся объектов, оценивать перспективу и получать примерные данные глубины. Таким образом стекинг без специализированных датчиков решает проблему.

<div align="center">
<img width=900 src=img/depth.jpg/></div>

Полученные данные применяются для создания портретных снимков, дополненной реальности (AR) и прочей обработки финального изображения.

<div align="center">
<img width=600 src=img/portrait.jpg/></div>

Качественное отслеживание поверхностей средствами лишь фото-модулей.

<div align="center">
<img width=600 src=img/ar-bug.webp/></div>

<div align="center">
<img width=600 src=img/ar-dance.webp/></div>

Как видно - в обоих случаях отслеживанию пространства не мешают ни тряска, ни повороты камеры. Для смартфона при открытии камеры создается "микро-мир", ограниченный радиусом получаемых данных.

<div align="center">
<img width=900 src=img/world.jpg/></div>

## Заключение

Когда-нибудь камеры в носимых устройствах (может и не смартфонах) смогут сами понимать, какой объект перед ними находится, и дорисовывать сложные участки, основываясь на собственной памяти или открытых источниках данных. Уже сейчас, эти источники активно пополняются.

Что касается съемки с использованием стекинга - иногда лучше сделать много плохих снимков, чем попытаться сделать один хороший и случайно его испортить :)

