## Интерфейс для CRM-системы на языке Javascript

****

#### Web-интерфейс для CRM системы со следующим функционалом:

+ Просмотр списка клиентов в виде таблицы
+ Добавление нового клиента
+ Изменение информации о существующем клиенте (ФИО и контактная информация)

### Для запуска:
- перейдите в терминале в папку **`crm-backend`**    

- напишите команду **`node index`** для включения сервера

Сервер CRM запущен. Вы можете использовать его по адресу http://localhost:3000

- после этого откройте папку проекта **`src`**
  
- затем откройте файл **`index.html`**, нажав правой кнопкой мыши на пункт **`"Open with live server"`**

- Нажмите **`CTRL+C`**, чтобы остановить сервер

### Доступные методы:
+ `GET /api/clients` - получить список клиентов, в query параметр search можно передать поисковый запрос
+ `POST /api/clients` - создать клиента, в теле запроса нужно передать объект `{ name: string, surname: string, lastName?: string, contacts?: object[] }`
  + contacts - массив объектов контактов вида { type: string, value: string }
+ `GET /api/clients/{id}` - получить клиента по его ID
+ `PATCH /api/clients/{id}` - изменить клиента с ID, в теле запроса нужно передать объект { name?: string, surname?: string, lastName?: string, contacts?: object[] }
  + contacts - массив объектов контактов вида { type: string, value: string }
+ `DELETE /api/clients/{id}` - удалить клиента по ID

****
### Техническое задание
<details><summary>Разработать web-интерфейс для CRM системы, в которой должны быть следующие возможности:</summary>   

1. Просмотр списка людей в виде таблицы
2. Добавление нового клиента
3. Изменение информации о существующем клиенте

</details>

<details><summary>Каждый контакт представляет из себя следующий набор данных:</summary>

- Имя
- Фамилия
- Отчество
- Массив объектов с контактными данными, где каждый объект содержит:
- Тип контакта (телефон, email, VK и т.п.)
- Значение контакта (номер телефона, адрес email, ссылка на страницу в VK и т.п.)

-  Интерфейс представляет из себя единственную страницу, на которой располагается таблица клиентов, кнопка для добавления нового клиента, а также шапка с логотипом компании и строкой поиска клиентов.
</details>

### Описание экранов приложения

<details><summary><i>Таблица со списком людей имеет следующие колонки:</i></summary>
  
- ID
- ФИО (Фамилия Имя Отчество через пробел)
- Дата и время создания
- Дата и время последнего изменения
- Контакты
- Действия (кнопки)
    - изменить клиента
    - удалить клиента
 
  Таблица должна строиться на основе данных из АРІ. При первичной загрузке нужно отображать индикатор загрузки, пока таблица с данными не будет построена.
</details>


<details><summary><i>Сортировка</i></summary>
Все заголовки колонок, кроме контактов и действий, можно нажать, чтобы установить сортировку по соответствующему полю. Первое нажатие устанавливает сортировку по возрастанию, повторное - по убыванию.    
Сортировка должна происходить из JavaScript, то есть АРІ передаёт данные в неотсортированном виде.     
По умолчанию должна быть установлена сортировка по возрастанию по ID.     
Состояние сортировки должно корректно отображаться в виде соответствующих иконок около заголовков.
</details>

<details><summary><i>Поиск</i></summary>
При вводе текста в поле для поиска данные для таблицы должны быть перезапрошены из АРІ с введённым поисковым запросом.    
При этом запрос должен отправляться только по прошествии 300мс с момента последнего ввода символа в поле (то есть нужно ожидать, пока пользователь не завершит ввод поискового запроса).
</details>

<details><summary><i>Отображение контактов клиента</i></summary>
В колонке с контактами для контактов VK, Facebook, телефона и email должны отображаться соответствующие иконки.    
Все остальные виды контактов отображаются с одинаковыми иконками с человечком.   

При наведении указателя на контакт должна показываться всплывающая подсказка с типом и значением этого контакта в формате "**Тип**: значение" (Например: "**Emai|**: abc@abc.ru"
"**Телефон**: +71234567890", "**Twitter**: @nnn").
 </details>

<details><summary><i>Действия над клиентами</i></summary>
При нажатии на кнопку "Изменить" должно появиться модальное окно с формой изменения клиента. При нажатии на кнопку "Удалить" должно появиться модальное окно с подтверждением действия. Если пользователь подтверждает удаление, то человек должен быть удалён из списка. Также на сервер с АРІ должен посылаться запрос на удаление.
 </details>
 
### Формы создания или редактирования данных о клиентах

<details><summary><i>Автозаполнить форму</i></summary>

  - Форма создания клиента должна открываться в виде модального окна по нажатию на кнопку "Добавить клиента", находящуюся под таблицей.
  - Форма редактирования клиента должна открываться по нажатию на кнопку "Изменить" в таблице клиентов.
  - Форма создания клиента открывается сразу с незаполненными полями.
  - При изменении клиента перед открытием формы из АРІ должны быть запрошены свежие данные клиента, только после получения этих данных должна открыться форма.
    При этом форма должна быть заполнена соответствующими данными клиента.
 </details>

<details><summary><i>Контакты клиента</i></summary>
В блоке контактов нужно предусмотреть возможность добавления до 10 контактов включительно. Для этого под добавленными контактами должна быть кнопка "Добавить контакт".    
  Если у клиента уже добавлено 10 контактов, кнопка не должна отображаться.    
  Тип контакта выбирается из выпадающего списка с выбором одного из значений:
  
  - Телефон
  - Email
  - Facebook
  - VK
  - Другое

Каждый контакт можно удалить из списка по нажатию на крестик справа от него.
</details>

<details><summary><i>Кнопки</i></summary>
  
- Под формой должна располагаться кнопка "Сохранить".
- Кнопка "Удалить клиента" добавляется, если это форма редактирования существующего в базе данных человека.
- По нажатию на кнопку удаления клиент должен быть удалён из таблицы, а на сервер API должен быть отправлен запрос на удаление клиента.
- Модальное окно с формой должно закрыться. По нажатию на кнопку сохранения изменения должны быть отправлены на сервер с использованием метода создания или изменения существующего клиента.
- Далее в зависимости от ответа сервера:
    + `Если сохранение прошло успешно (статус ответа 200 или 201), модальное окно с формой закрывается. При этом таблица должна быть отрисована заново с новым запросом на список людей.`
    + `Если при сохранении произошла ошибка (статус ответа 422, 404 или 5хх), то нужно отобразить сообщения об ошибках, полученные в ответе сервера, над блоком с кнопками. При этом если ответ сервера не удалось разобрать или в нём нет сообщений об ошибке, нужно отобразить сообщение по умолчанию "Что-то пошло не так...".`

