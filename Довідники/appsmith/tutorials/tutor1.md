# Інформаційна панель модератора

https://docs.appsmith.com/learning-and-resources/tutorials/review-moderator-dashboard

У цьому посібнику ви навчитеся створювати повнофункціональний внутрішній інструмент на основі реального бізнес-набору даних за допомогою Appsmith. Програма являє собою багатосторінкову інформаційну панель, яка дозволяє переглядати всю бізнес-інформацію та модерувати окремі відгуки, надані користувачами.

Який зовнішній вигляд матиме застосунок можна глянути [тут](https://youtu.be/QHOpLoSH7ws)

⭐ **Рівень**: Початківець\ ⏱️ **Час**: ~40 хвилин

🙌 **Що ви дізнаєтеся в цьому посібнику:**

- Підключення до джерел даних на Appsmith (запити API/БД)
- Прив'язка даних до різних віджетів інтерфейсу користувача.
- Написання JS на Appsmith для складних представлень.
- Розгортайте та керуйте своїми програмами.
- Використовуйте різні віджети, такі як діаграми, списки, карти, таблиці тощо.

Посібник складається з чотирьох частин, і ми рекомендуємо вам дотримуватися їх по порядку. Перш ніж почати, давайте налаштуємо Appsmith. Ви можете скористатися самостійною версією за допомогою хмари Docker або Appsmith і слідувати. Щоб налаштувати Appsmith локально за допомогою Docker, дотримуйтеся вказівок [тут](https://docs.appsmith.com/getting-started/setup/installation-guides/docker).Розпочнемо з посібника, тож спочатку **налаштуємо додаток.**

## Налаштування програми

Якщо ви вперше використовуєте Appsmith, вам потрібно буде ознайомитися з деякими початковими налаштуваннями. Коли ви ввійдете, ви будете перенаправлені на [панель Appsmith Dashboard](https://app.appsmith.com/applications). Ви побачите автоматично створений робочий простір під назвою apps (ваш робочий простір). Однак ви можете створити кілька робочих областей і впорядкувати програми відповідно до своїх уподобань.

У цьому підручнику ви створите програму Review Moderator у тому самому робочому просторі. Для цього виконайте наведені нижче дії.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/rDq4203aRQw?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/rDq4203aRQw?autoplay=1><img src=https://img.youtube.com/vi/rDq4203aRQw/maxresdefault.jpg alt='Creating and Renaming Appsmith Application'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Creating and Renaming Appsmith Application" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Створення та перейменування програми Appsmith*

1. Натисніть **Create New** під робочою областю.
2. Буде скеровано на сторінку конфігурації новоствореної програми.
3. Ви побачите два варіанти: **Build with drag & drop** або **Generate from the data table**.
4. Для цього підручника ми виберемо **build with drag & drop**.
5. Зверніть увагу, що програма матиме назву за замовчуванням **Untitled Application 1**
6. Перейменуйте його на **Review Moderator**, двічі клацнувши на існуючому.

Нова програма постачається з автоматично створеними каталогами, які створюють програму Appsmith. Нижче наведено знімок екрана провідника об’єктів.

![Application&#39;s dashboard](https://docs.appsmith.com/assets/images/screenshot_2022-05-04_at_7.19.09_pm-7bddd586118c8d17ce7dd4239d98bcca.png)

Entity Explorer – це місце, де ви можете створювати та впорядковувати віджети інтерфейсу користувача, запити/об’єкти JS і джерела даних. Ви також можете знайти різні бібліотеки в залежностях, які можна використовувати в цих розділах.

Тепер давайте перейменуємо сторінку з **Page1** на **Business Details**; ви можете зробити це, двічі клацнувши на існуючому імені.

Тепер ви налаштували програму. Далі переходимо до наступного розділу. Тут ви **підключитесь до джерела даних і напишете свій перший запит до БД на Appsmith!**

## Підключення до джерела даних

### **Підключення до Postgres Mock DB**

Appsmith підтримує різні джерела даних і дозволяє писати запити до них для виконання різних дій із програми. У цьому посібнику ви підключитесь до джерела даних Postgres, яке містить такі таблиці:

1. **Business Table**: містить детальну інформацію про кілька компаній, відфільтровану з Yelp Data.
2. **Review Table**: у цій таблиці є відгуки, пов’язані з компаніями, переліченими в бізнес-таблиці.

Appsmith підтримує різні бази даних, наприклад:

- [Amazon S3 (also Upcloud, Digital Ocean Spaces, Wasabi, DreamObjects)](https://docs.appsmith.com/reference/datasources/querying-amazon-s3)
- [ArangoDB](https://docs.appsmith.com/reference/datasources/querying-arango-db)
- [DynamoDB](https://docs.appsmith.com/reference/datasources/querying-dynamodb)
- [ElasticSearch](https://docs.appsmith.com/reference/datasources/querying-elasticsearch)
- [Firestore](https://docs.appsmith.com/reference/datasources/querying-firestore)
- [MongoDB](https://docs.appsmith.com/reference/datasources/querying-mongodb)
- [MySQL](https://docs.appsmith.com/reference/datasources/querying-mysql), and a [lot more](https://docs.appsmith.com/reference/datasources).

Давайте скористаємося цим фіктивним джерелом даних, щоб отримати всі бізнес-елементи для програми Review Moderator, виконавши наведені нижче дії.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/ZOSYloiB8ZY?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/ZOSYloiB8ZY?autoplay=1><img src=https://img.youtube.com/vi/ZOSYloiB8ZY/maxresdefault.jpg alt='Connecting to a Datasource on Appsmith'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Connecting to a Datasource on Appsmith" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Підключення до джерела даних на Appsmith*

1. Спочатку клацніть значок `+` поруч із `Datasources`.
2. Далі ви побачите список параметрів джерела даних, до яких можна підключитися.
3. Виберіть **Postgres** і перейменуйте джерело даних на `Postgres Mock DB`.
4. Далі скористайтеся наведеними нижче деталями, щоб підключитися до джерела даних.

```text
Connection Mode: Read / Write
Host Address: mockdb.internal.appsmith.com
Port: 5432
Database Name: yelp
User: yelp
Password: that-annoying-yelper
```

Щоб перевірити, чи це джерело даних дійсне чи ні, ви можете натиснути кнопку  `Test`  в правому середині. Ви повинні побачити спливаюче вікно зі статусом підключення. Тепер збережіть джерело даних, натиснувши кнопку **Save**. Ви побачите спливаюче вікно успіху у верхньому правому куті після успішного додавання вашої БД.

### **Написання вашого першого запиту**

Джерело даних успішно підключено; Тепер давайте напишемо простий запит до БД, щоб отримати всі бізнес-дані з бізнес-таблиці. Для цього виконайте наведені нижче дії.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/QoyzrOEG5to?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/QoyzrOEG5to?autoplay=1><img src=https://img.youtube.com/vi/QoyzrOEG5to/maxresdefault.jpg alt='Running Queries on Appsmith'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Running Queries on Appsmith" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Виконання запитів на Appsmith*

1. Спочатку клацніть значок `+` поруч із `Datasources`.
2. Знайдіть створене джерело даних `Postgres Mock DB` на вкладці Active  та натисніть `NEW QUERY`.
3. Буде створено новий запит до БД, який ви зможете використовувати на всій сторінці.
4. Назвіть цей запит як `getBusinessData` і натисніть кнопку select.
5. Використовуйте наступний запит на панелі запитів, щоб отримати всі бізнес-дані:

```sql
select * from yelp_business;
```

Щоб виконати цей запит, натисніть кнопку **RUN** у верхньому правому куті **DB query**. Тепер ви повинні побачити відповідь із запиту до БД на вкладці Response Pane нижче.

Далі прив’яжемо ці дані до потужного [table widget](https://docs.appsmith.com/reference/widgets/table)  Appsmith! 

### Прив'язка запитів до віджетів

У попередньому розділі ви створили запит до БД під назвою **`getBusinessData`**; давайте прив’яжемо запит до віджета таблиці. Ви можете досягти цього двома способами:

Перший і простий спосіб — відкрити вікно запиту та вибрати опцію таблиці на правій панелі властивостей. Він автоматично додасть віджет таблиці на ваше полотно. У відео нижче показано додавання віджета таблиці з вікна запиту.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/XgQ9AsRdLek?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/XgQ9AsRdLek?autoplay=1><img src=https://img.youtube.com/vi/XgQ9AsRdLek/maxresdefault.jpg alt='Adding a table widget from the query window'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Adding a table widget from the query window" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Додавання віджета таблиці з вікна запиту*

Зауважте, що наведений вище метод також автоматично зв’яже дані із запиту для вас.

Давайте розглянемо інший спосіб додавання віджета таблиці на полотно.

1. Натисніть опцію **`Widgets`** у **entity explorer.**
2. Тут ви знайдете чудовий набір віджетів інтерфейсу користувача, які можна використовувати для створення програми.
3. Перетягніть **`Table widget`** на полотно.

Appsmith надає різні віджети, наприклад  [tables](https://docs.appsmith.com/reference/widgets/table), [lists](https://docs.appsmith.com/reference/widgets/list), [buttons](https://docs.appsmith.com/reference/widgets/button), [maps](https://docs.appsmith.com/reference/widgets/maps), [audio](https://docs.appsmith.com/reference/widgets/audio), [charts](https://docs.appsmith.com/reference/widgets/chart), [forms](https://docs.appsmith.com/reference/widgets/form), та інше.

Ви помітите вікно властивостей у правій частині програми, щойно перетягнете віджет на полотно; ви можете назвати це **Widget Property Pane**. Усі конфігурації таблиці та властивості налаштування можна знайти тут. Ось знімок екрана віджета таблиці та його панелі властивостей:

![Appsmith Table Widget and Property Pane](https://docs.appsmith.com/assets/images/issue_12550_img3-5125f8c0a75ba818fa31b0be239b8112.png)

Ви можете отримати доступ до закріпленої панелі властивостей будь-якого віджета, просто клацнувши віджет на полотні. Давайте подивимося на панель властивостей таблиці:

**Table Data**: щоб додати дані до таблиці, ми можемо оновити властивість `Table Data` панелі властивостей. За замовчуванням він має деяку початкову конфігурацію; ви можете оновити його на основі ваших уподобань. Але також переконайтеся, що він прийматиме лише типи даних масиву. Перегляньте детальну документацію [тут](https://docs.appsmith.com/reference/widgets/table), щоб дізнатися більше про віджет таблиці.

**Table Columns**: під властивістю Table Data можна налаштувати всі дані стовпців. Ви можете натиснути піктограму шестерінки та встановити тип даних стовпця окремо.

Віджет таблиці відображає дані в рядках і стовпцях. Ви можете відображати дані з API у таблиці, запускати дію, коли користувач вибирає рядок, і навіть працювати зі значними наборами даних, розбитих на сторінки.

Це дві основні властивості, необхідні для віджета таблиці. Однак багато інших властивостей дозволяють додавати різні дії та налаштовувати інтерфейс користувача. Якщо ви хочете навчитися відображати дані та розбивати сторінки всередині таблиці,[ прочитайте цей посібник.](https://docs.appsmith.com/reference/widgets/table#transforming-table-data)

Тепер у властивості **`Table Data`** давайте зв’яжемо відповідь із запиту до БД. Для цього вам доведеться використовувати оператор Moustache.

В Appsmith оператор moustache **`{{ /\* This is JavaScript \*/ }}`** можна використовувати будь-де для написання JavaScript. Наприклад, під час прив’язки даних до віджетів, надсилання параметрів до API, обміну даними між сторінками тощо.

Тепер скопіюйте наступне у властивість `Table Data`:

```javascript
{{ getBusinessData.data  }}
```

Коли ви скопіюєте це в дані таблиці, ви побачите дані, чарівним чином заповнені таблицею. Потім, виходячи з ваших уподобань, ви можете налаштувати назви стовпців і стилізувати віджет таблиці з іншими властивостями. У відео нижче показано, як додати віджет таблиці та отримати дані.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/Ys1zN2GjNGA?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/Ys1zN2GjNGA?autoplay=1><img src=https://img.youtube.com/vi/Ys1zN2GjNGA/maxresdefault.jpg alt='Adding a table widget to the canvas'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Adding a table widget to the canvas" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Adding a table widget to the canvas*

*Додавання віджета таблиці на полотно*

Але що тут сталося? Тут ми отримуємо доступ до всього об’єкта запиту за допомогою назви запиту **`getBusinessData`**, а властивість **`.data`** дозволяє нам додавати дані.  Налаштування параметра Table Data на **`{{ getBusinessData.data }}`** також гарантує, що під час кожного завантаження бізнес-сторінки getBusinessData запускатиметься автоматично. Однак ви можете змінити цю поведінку за замовчуванням, перемикаючи поле «Run query on page load» на вкладці «Setting » getBusinessData.

У наступному розділі ви побачите, що зворотне цьому також можливе, і запит також може отримати доступ, наприклад, до стану віджета. Крім того, усі будівельні блоки сторінки Appsmith – віджети, запити до БД та API можуть отримувати доступ до даних один одного та/або станів, використовуючи свої імена.

## Створення інтерфейсу користувача та доступ до властивостей віджетів

### Налаштування віджета Table

Як бачите, віджет таблиці містить багато даних із запиту, але скажімо, ви можете показати лише кілька стовпців і приховати решту для кращої ясності.

Ви можете відкрити панель властивостей, знайти стовпці та перемкнути значок ока. Він приховує стовпці від таблиці. Тепер відкрийте панель властивостей і відобразіть лише такі стовпці:

- Name
- Address
- City

Нижче наведено відео про створення інтерфейсу користувача та редагування властивостей таблиці:

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/4ET9wtFFIF0?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/4ET9wtFFIF0?autoplay=1><img src=https://img.youtube.com/vi/4ET9wtFFIF0/maxresdefault.jpg alt='Building the UI and Editing Table Properties'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Building the UI and Editing Table Properties" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Створення інтерфейсу користувача та редагування властивостей таблиці*

Крім того, зробіть інтерфейс користувача кращим за допомогою віджета Container. Використовуючи це, ви можете групувати кілька віджетів на фоні з мінімальним пробілом. Для цього виконайте наведені нижче дії.

1. Перетягніть віджет **Container** на полотно.
2. Перемістіть віджет Table у віджет Container .
3. Крім того, додайте **Text widget** над віджетом Таблиця, щоб додати заголовок. Ви можете назвати цей текст «Інформаційна панель модератора перегляду».

Давайте додамо кілька додаткових компонентів, які відображатимуть інформацію щоразу, коли в рядку таблиці вибрано певний бізнес. Давайте спочатку перейменуємо віджет Table з **Table1** на **businessTable**. Ви можете змінити назву віджета на панелі властивостей.

### Додавання віджета карти

Щоб зробити інтерфейс більш інтуїтивно зрозумілим, додайте місцезнаходження компанії. Для цього додайте [Map Widget](https://docs.appsmith.com/reference/widgets/maps) і відобразіть розташування компанії, виконавши наведені нижче дії.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/J_xVn-TKPXY?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/J_xVn-TKPXY?autoplay=1><img src=https://img.youtube.com/vi/J_xVn-TKPXY/maxresdefault.jpg alt='Adding Map Widget'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Adding Map Widget" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Додавання віджета карти*

1. Перетягніть **Map widget** на полотно
2. Відкрийте панель властивостей віджета «Map ».
3. Ви помітите дві стандартні конфігурації: **Initial Location and Default markers.**
4. Початкове розташування – це положення маркера, яке приймає один об’єкт JSON із координатами широти та довжини.
5. Стандартні маркери встановлюють усі стандартні ринки на карті, і це звичайний масив об’єктів карти.
6. Потім оновіть властивості Початкове розташування (перемикання JS) і Маркери за замовчуванням до наступного:

**`Initial location:`**

```javascript
{
    "lat": {{businessTable.selectedRow.latitude}},
    "long": {{businessTable.selectedRow.longitude}}
}
```

**`Default markers:`**

```javascript
[
  {
    "lat": {{businessTable.selectedRow.latitude}},
    "long": {{businessTable.selectedRow.longitude}},
    "title": {{businessTable.selectedRow.name}}
  }
]
```

Тут ви використовуєте синтаксис moustache, прив’язуючи значення таблиці та налаштовуючи віджет карти.

Ви можете використовувати властивість **`selectedRow`** для віджета Таблиця, щоб отримати доступ до даних певного рядка, коли його вибрано.

Тепер виберіть будь-який рядок у таблиці, і карта автоматично оновиться зі згаданим місцезнаходженням підприємства.

Рівень масштабування можна використовувати для визначення точного розташування.

### Додавання текстових віджетів і зв'язування даних

Далі додайте кілька текстових віджетів і зв’яжіть всю інформацію про компанію під картою. Ви можете перекинути текстові віджети на полотно та додати пов’язані з ними імена та значення, наприклад:

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/jEhbeoc4sTE?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/jEhbeoc4sTE?autoplay=1><img src=https://img.youtube.com/vi/jEhbeoc4sTE/maxresdefault.jpg alt='Adding Text Widgets</i></figcaption>'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Adding Text Widgets</i></figcaption>" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Додавання текстових віджетів*

Перетягніть текстовий віджет на полотно та вставте наведений нижче запит у текстове поле.

```text
Name: {{businessTable.selectedRow.name}}
Address: {{businessTable.selectedRow.address}}
City: {{businessTable.selectedRow.city}}
Business ID: {{businessTable.selectedRow.business_id}}
Business Rating: {{businessTable.selectedRow.stars}}
Categories Rating: {{businessTable.selectedRow.categories}}
```

У наступному розділі ви дізнаєтесь, як писати функції JS у віджеті для створення інтерактивних переглядів. Ви також будете використовувати віджети списку та діаграми, щоб аналізувати відгуки з таблиці відгуків на основі вибраного бізнесу.

## Створення інтерактивних переглядів

### Зберігання даних в об’єкті контексту Appsmith

Тепер ви майже готові зі своєю надзвичайно крутою інформаційною панеллю. Щоб зробити вашу програму більш інтерактивною, додайте ще одну сторінку, яка показуватиме відгуки про цю конкретну компанію.

Почніть із додавання кнопки, яка переспрямовуватиме на нову сторінку. Крім того, на новій сторінці вам знадобиться **`business_id`**, щоб фільтрувати відгуки з таблиці оглядів. Отже, тепер збережіть значення в [Appsmith Context Object ](https://docs.appsmith.com/reference/appsmith-framework/context-object) і використовуйте його як посилання. Дотримуйтеся наведених нижче інструкцій.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/7xQid95aHuM?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/7xQid95aHuM?autoplay=1><img src=https://img.youtube.com/vi/7xQid95aHuM/maxresdefault.jpg alt='Storing Value and Redirecting to a Page'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Storing Value and Redirecting to a Page" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Зберігання значення та переспрямування на сторінку*

1. Перетягніть **button widget** під відомостями про компанію.
2. Відкрийте панель властивостей кнопок і змініть мітку на **View Reviews**.
3. У розділі Actions перейдіть до події onClick і **перемкніть кнопку JS і вставте наступний код:** 

```js
{ {
(function () {storeValue("business_id", businessTable.selectedRow.business_id); navigateTo("Business Reviews")})()
} }
```

Чудово, ви успішно написали свою першу функцію JS на Appsmith. Як ви можете помітити, це первинні викликані функції, що означає, що вони запускаються, як тільки визначено. Усередині функції використовуйте метод **`storeValue`**, щоб зберегти бізнес-ключ із `businessTable` у змінній **`business_id`**. Далі ви використали метод **`navigateTo`**, щоб мати можливість переспрямовувати на нову сторінку.

Тепер створіть нову сторінку та назвіть її «Business Reviews». Отже, коли ви натискаєте цю кнопку, ви переходите на сторінку під назвою **"Business Reviews".**

Як ви можете бачити тут, щойно глядач натискає кнопку, він переходить на нову сторінку. Крім того, у вибраному рядку збережено **`business_id`**.

### Використання Store Value в запитах до БД

Тепер, щоб отримати дані відгуків, напишіть запит для **Business Reviews Page**, який фільтрує відгуки з таблиці відгуків на основі вибраного business_id, виконавши наведені нижче дії:

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/7hQqJ2Cfj5o?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/7hQqJ2Cfj5o?autoplay=1><img src=https://img.youtube.com/vi/7hQqJ2Cfj5o/maxresdefault.jpg alt='Writing a query for Business Reviews Page'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Writing a query for Business Reviews Page" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Написання запиту для сторінки бізнес-оглядів*

1. Знайдіть і виберіть джерело даних **Postgres Mock DB** на вкладці Explorer.
2. Натисніть **`NEW QUERY`** у верхньому правому куті.
3. Перейменуйте запит на **`filterBusinessReviews`**.
4. Тепер вставте наступний запит на панель запитів:

```text
select * from yelp_reviews where business_id = {{appsmith.store.business_id}}
```

Переконайтеся, що ви виконуєте цей запит для сторінки «Business Reviews».

Ви вибираєте всі рядки з таблиці **`yelp_review`** і фільтруєте їх за змінною **`business_id`**, яку ви зберегли в appsmith store під час переходу на нову сторінку. Отже, ви використали його для пропозиції WHERE за допомогою синтаксису moustache. **Тепер натисніть RUN.**

Запустивши запит, ви можете переглянути всі відгуки на основі вибраного **`business_id`**. На вкладці налаштувань запиту переконайтеся, що ви вимкнули параметр **Run query on the page load option**

Крім того, вам потрібно буде **знову отримати відомості про компанію на цій сторінці**, щоб на інформаційних панелях було легше відображати повну інформацію із запиту до БД. Виконайте наведені нижче дії.

1. Знайдіть створене джерело даних **Postgres Mock DB** на вкладці Explorer і натисніть **NEW QUER**Y.
2. Перейменуйте запит на **`getBusinessDetails`**.
3. Тепер вставте наступний запит на панель запитів:

```text
select * from yelp_business where business_id={{appsmith.store.business_id}}
```

Якщо ви запустите це, ви побачите лише один рядок, який отримує всі відомості про бізнес із бізнес-таблиці на основі **`business_id`**, що зберігається в об’єкті контексту appsmith.

Тепер створіть інформаційну панель, яка показуватиме всі відгуки, отримані з таблиці відгуків.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/dFcX2fs38ak?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/dFcX2fs38ak?autoplay=1><img src=https://img.youtube.com/vi/dFcX2fs38ak/maxresdefault.jpg alt='Creating a UI for the Business Reviews Page'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Creating a UI for the Business Reviews Page" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Створення інтерфейсу користувача для сторінки оглядів бізнесу*

1. Спочатку перетягніть віджет-контейнер і переставте його на всю сторінку.
2. Далі додайте текстовий віджет і вставте наступне на панель властивостей значення:

```text
Found {{filterBusinessReviews.data.length}} Reviews for {{getBusinessDetails.data[0].name}}
```

3. Додайте кілька текстових віджетів для відображення назви та ідентифікатора підприємства. Наведений нижче запит можна використовувати для додавання імені. Ви можете використовувати ідентифікатор компанії або будь-яке інше значення замість імені.

```text
To get name - {{getBusinessDetails.data[0].name}}

To get business_id-{{getBusinessDetails.data[0].business_id}}
```

Порада. Ви також можете запускати запити чи API за допомогою комбінацій клавіш `CMD + return` або `CTRL + enter` на Appsmith!

### **Використання віджета списку для відображення відгуків**

Тепер відобразіть усі відгуки в [list view](https://docs.appsmith.com/reference/widgets/list). Віджет «List » надає готову можливість переглядати колекцію структурованих даних. Набори даних можуть бути статичними або згенерованими відповіддю API/запитів.

Тепер скористайтеся віджетом List , щоб відобразити всі відгуки із запиту filterBusinessReviews. Виконайте наведені нижче дії.

1. Перетягніть **list widget** на полотно.
2. Прив’яжіть дані з **`filterBusinessReviews`** до віджета списку.
3. Відкрийте панель властивостей віджета списку та вставте наступне в **Items**.

```text
{{filterBusinessReviews.data}}
```

Тепер налаштуйте перегляд списку відповідно до ваших потреб і видаліть елементи, які вам не потрібні.

1. Видаліть уже заповнені дані у віджеті списку та додайте кілька текстових віджетів у подання списку.
2. Зверніть увагу, що віджети автоматично додаються до інших елементів списку віджетів.
3. Ви можете прив’язати елементи до цих віджетів за допомогою властивості **`currentItem`**.
4. У тексті віджети використовують синтаксис moustache і зв’язують дані як `{{currentItem.text}}`.
5. Тепер у налаштуваннях переповнення змініть його на «scroll contents». Отже, це робить текстове подання прокручуваним.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/e4f1QMq2zoA?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/e4f1QMq2zoA?autoplay=1><img src=https://img.youtube.com/vi/e4f1QMq2zoA/maxresdefault.jpg alt='Using the List Widget'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Using the List Widget" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Використання віджета списку*

Тепер ви можете спробувати відобразити решту даних у віджеті списку за допомогою властивості `currentItem`.

### **Відображення дати**

Тепер зробіть перегляд списку ще більш інтуїтивно зрозумілим. Перетягніть текстовий віджет у таблицю та додайте наступний фрагмент коду у властивість Text з його панелі властивостей:

```text
{{currentItem.date}}
```

Тут, якщо ви помітили, дата не читається. Ви можете використовувати ``moment.js``, щоб перетворити це, яке вже налаштовано в середовищі Appsmith. Тепер оновіть значення до такого:

```text
{{moment(currentItem.date).format("LL")}}
```

Дата автоматично форматується на основі типу, заданого в методі `.format()`.

### **Відображення оцінок**

Відображайте відгуки в кольоровій формі. Додайте кілька текстових віджетів у список.

Далі додайте відгуки із запиту за такими параметрами в текстові віджети:

```text
Stars Ratings: { { `Stars: ${currentItem.stars}` } }

Funny Ratings: { { `Funny: ${currentItem.funny}` } }

Useful Ratings: { { `Useful: ${currentItem.useful}` } }

Cool Ratings: { { `Cool: ${currentItem.cool}` } }
```

Після цього ви можете налаштувати текстовий віджет, знайти властивість background-color на панелі властивостей текстового віджета та додати будь-які фонові кольори. Тепер, нарешті, ось як виглядає програма:

![Customizing the List Widget](https://docs.appsmith.com/assets/images/issue_12550_img4-1f876fcfa31ea35d41850975b715ee94.png)

### Додавання віджета діаграми

Віджет діаграми chart на Appsmith використовується для перегляду графічного представлення ваших даних. Він доступний у кількох конфігураціях; однак, якщо ви хочете зробити розширену візуалізацію, ви можете вибрати спеціальну конфігурацію та використати `Custom Fusion Chart Configuration`.

Існує майже 100+ варіантів конфігурації Fusion Chart; дізнайтеся більше з офіційних документів [тут](https://www.fusioncharts.com/dev/chart-guide/list-of-charts/).

Appsmith використовує заголовок властивості Chart Series для надання даних і деталей, пов’язаних з ідентифікацією точок даних.

- `Series Title` - назва серії.
- `Series Data` - зберігає точки даних для загальної кількості помилок.
- `Мітка осі Х` - для визначення заголовка для осі Х.
- `Y-axis Label` - щоб визначити заголовок для осі Y

Тепер виконайте наведені нижче дії, щоб створити діаграму для візуалізації рейтингів компанії на основі відгуків.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/ujmjVmkSO9c?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/ujmjVmkSO9c?autoplay=1><img src=https://img.youtube.com/vi/ujmjVmkSO9c/maxresdefault.jpg alt='Adding Chart Widget'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Adding Chart Widget" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Додавання віджета діаграми*

1. Перетягніть **chart widget** на полотно.
2. Відкрийте панель властивостей віджета діаграми та встановіть тип діаграми на **Line chart**.
3. Далі встановіть заголовок як **Star Ratings of Business** та скористайтеся наведеним нижче фрагментом коду для передачі узгоджених даних діаграми.

```text
{{filterBusinessReviews.data.map((item, index)=>{return {x:moment(item.date).format("L"), y:item.stars}})}}
```

Чудово! Ви повинні побачити всі дані, нанесені на віджет діаграми. Так само ви можете побудувати інші рейтинги, натиснувши опцію **`ADD SERIES`**. У наведеному нижче відео показано, як додати ряд до діаграми.

<iframe style="width: 100%; height: auto; aspect-ratio: 16 / 9; border-radius: 0.5rem; overflow: hidden;" src="https://youtube.com/embed/fIBjUCBL6wA?autoplay=1" srcdoc="<style>*{padding:0;margin:0;overflow:hidden}html,body{height:100%}img,span{position:absolute;width:100%;top:0;bottom:0;margin:auto}span{height:100px;text-align:center;font:48px/1.5 sans-serif;color:white;text-shadow:0 0 0.25em gray}</style><a href=https://youtube.com/embed/fIBjUCBL6wA?autoplay=1><img src=https://img.youtube.com/vi/fIBjUCBL6wA/maxresdefault.jpg alt='Customizing Chart Widget'><span><svg width=&quot;100px&quot; height=&quot;100px&quot; viewBox=&quot;0 0 463 462&quot; fill=&quot;none&quot; xmlns=&quot;http://www.w3.org/2000/svg&quot;><circle opacity=&quot;0.5&quot; cx=&quot;231.742&quot; cy=&quot;230.999&quot; r=&quot;231&quot; fill=&quot;#FE5011&quot;></circle><path d=&quot;M181.703 165.53C181.703 156.392 191.812 150.873 199.499 155.814L301.34 221.283C308.412 225.83 308.412 236.168 301.34 240.715L199.499 306.184C191.812 311.125 181.703 305.606 181.703 296.468V165.53Z&quot; fill=&quot;#FFFFFF&quot;></path></svg></span></a>" allowfullscreen="" title="Customizing Chart Widget" loading="lazy" allow="autoplay; picture-in-picture" frameborder="0"></iframe>

*Налаштування віджета діаграми*

Таким чином, ви створили інтерактивну та красиву інформаційну панель на Appsmith.

Нижче наведено живе посилання на повністю налаштовану програму.

https://app.appsmith.com/applications/60caeaa2d79dbb613bcb7761/pages/60caeaa2d79dbb613bcb7763

### Поділіться своєю програмою

Розгорніть свою програму в останній раз. Після розгортання ви можете поділитися своїм розгорнутим додатком із внутрішніми та зовнішніми користувачами:

1. Натисніть кнопку **"Share"** у верхньому правому куті
2. Запросіть користувача, використовуючи його ідентифікатор електронної пошти
3. Виберіть відповідну роль для користувача
4. Поділіться URL-адресою програми з користувачем

Ви також можете зробити заявку публічною. У такому випадку будь-хто, хто має URL-адресу програми, зможе переглядати програму, не входячи в систему. Ви можете прочитати більше про [контроль доступу тут](https://docs.appsmith.com/advanced-concepts/access-control).