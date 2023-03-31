# SQL, XSS, Code и другие инъекции
#### Ссылка на задание/требования: https://github.com/netology-code/ibqa-homeworks/blob/main/3.%20SQL_XSS_Code/homework_lecture3.md

#### Сайт, где демонстрируется работа с dvwa: https://russianblogs.com/article/2929518970/

#### Инструкция по установке XAMPP + DVWA на MacOS: https://www.youtube.com/watch?v=RCYZ2j8iLi4

#### SQL - payloads: https://github.com/payloadbox/sql-injection-payload-list

#### XSS - payloads: https://github.com/payloadbox/xss-payload-list


## Задание 1 - План тестирования карточки товара для выявления XSS- и SQL-инъекций
## Выявление XSS-инъекций
## DOM XSS - ИНЪЕКЦИИ

#### 1. Скрипт с алертом с текстом
```
STR:
    1. Перейти в карточку товара
    2. В строку URL дополнительно к URL дописать: <script>alert("XSS");</script>
    3. Обновить страницу
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 2. Скрипт с алертом файла куков
```
 STR:
    1. Перейти в карточку товара
    2. В строку URL дополнительно к URL дописать: <script>alert(document.cookie);</script>
    3. Обновить страницу
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 3. Селект с алертом
```
STR:
    1. Перейти в карточку товара
    2. В строку URL дополнительно к URL дописать: <select><body onload=alert("XSS")>
    3. Обновить страницу
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 4. Амперсанд + скрипт с алертом с текстом
```
STR:
    1. Перейти в карточку товара
    2. В строку URL дополнительно к URL дописать: &<script>alert("XSS");</script>
    3. Обновить страницу
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
## ОТРАЖЕННЫЕ XSS -ИНЪЕКЦИИ

#### 1. XSS - инъекция в поле "Цена"

#### 1.1 Скрипт с алертом с текстом в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: <sript>alert("XSS");</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 1.2 Скрипт с измененным регистром букв с текстом в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: "<Script>alert("XSS");</sCript>"
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 1.3 Img в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: <img src=x onerror=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 1.4 Скрипт с алертом файла куков в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: <script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 1.5 "Кавычки-больше" перед скриптом в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: “><script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 1.6 Svg/onload c алертом в поле "Цена"
```
 STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: <svg/onload=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 2. XSS - инъекция в поле "Остаток товара на складе"

#### 2.1 Скрипт с алертом с текстом в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: <script>alert("XSS");</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 2.2 Скрипт с измененным регистром букв с текстом в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: "<Script>alert("XSS");</sCript>"
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 2.3 Img в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: <img src=x onerror=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 2.4 Скрипт с алертом файла куков в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: <script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 2.5 "Кавычки-больше" перед скриптом в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: “><script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 2.6 Svg/onload c алертом в поле "Описание товара"
```
 STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: <svg/onload=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 3. XSS - инъекция в поле "Название товара"

#### 3.1 Скрипт с алертом с текстом в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: <script>alert("XSS");</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 3.2 Скрипт с измененным регистром букв с текстом в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: "<Script>alert("XSS");</sCript>"
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 3.3 Img в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: <img src=x onerror=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 3.4 Скрипт с алертом файла куков в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: <script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 3.5 "Кавычки-больше" перед скриптом в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: “><script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 3.6 Svg/onload c алертом в поле "Название товара"
```
 STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: <svg/onload=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 4. XSS - инъекция в поле "Описание товара"

#### 4.1 Скрипт с алертом с текстом в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: <script>alert("XSS");</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 4.2 Скрипт с измененным регистром букв с текстом в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: "<Script>alert("XSS");</sCript>"
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 4.3 Img в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: <img src=x onerror=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
#### 4.4 Скрипт с алертом файла куков в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: <script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 4.5 "Кавычки-больше" перед скриптом в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: “><script>alert(document.cookie)</script>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с куками (в т.ч id сессии) не появляется.
```
#### 4.6 Svg/onload c алертом в поле "Описание товара"
```
 STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: <svg/onload=alert("XSS")>
    3. Остальные поля заполнить валидными значениями
ОР: Изменений нет. Всплывающее сообщение с текстом "XSS" не появляется.
```
## Выявления SQL-инъекций
#### 1. SQL -инъекция в поле "Цена"

#### 1.1 "Or 1=1" в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: ' or '1'='1
    3. Остальные поля заполнить валидными значениями
ОР: Записи из таблицы не получены.
```
#### 1.2 Одиночная кавычка в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: '
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 1.3 Номер несуществующей колонки в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести:
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 1.4 Union и sleep в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: UNION ALL SELECT 1
    3. Остальные поля заполнить валидными значениями
```
#### 1.5 Sleep в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: 1' UNION SELECT sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должен быть отправлен запрос через 5 сек
```
#### 1.6 Sleep в поле "Цена"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Цена" ввести: 1 or sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должн быть отправлен запрос через 5 сек
```
#### 2. SQL - инъекция в поле "Остаток товара на складе"

#### 2.1 "Or 1=1" в поле "Остаток товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: ' or '1'='1
    3. Остальные поля заполнить валидными значениями
ОР: Записи из таблицы не получены.
```
#### 2.2 Одиночная кавычка в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: '
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 2.3 Номер несуществующей колонки в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: 1' ORDER BY 1--+
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 2.4 Union в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести:UNION ALL SELECT 1
    3. Остальные поля заполнить валидными значениями
```
#### 2.5 Union и Sleep в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: 1' UNION SELECT sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должн быть отправлен запрос через 5 сек
```
#### 2.6 Sleep в поле "Остаток товара на складе"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Остаток товара на складе" ввести: 1 or sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должен быть отправлен запрос через 5 сек
```
#### 3. SQL -инъекция в поле "Название товара"

#### 3.1 "Or 1=1" в поле "Названиие товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: ' or '1'='1
    3. Остальные поля заполнить валидными значениями
ОР: Записи из таблицы не получены.
```
#### 3.2 Одиночная кавычка в поле "Названиие товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: '
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 3.3 Номер несуществующей колонки в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: 1' ORDER BY 1--+
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 3.4 Union в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести:UNION ALL SELECT 1
    3. Остальные поля заполнить валидными значениями
```
#### 3.5 Union и Sleep в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: 1' UNION SELECT sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должн быть отправлен запрос через 5 сек
```
#### 3.6 Sleep в поле "Название товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Название товара" ввести: 1 or sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должен быть отправлен запрос через 5 сек
```
#### 4. SQL -инъекция в поле "Описание товара"

#### 4.1 "Or 1=1" в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: ' or '1'='1
    3. Остальные поля заполнить валидными значениями
ОР: Записи из таблицы не получены.
```
#### 4.2 Одиночная кавычка в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: '
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 4.3 Номер несуществующей колонки в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: 1' ORDER BY 1--+
    3. Остальные поля заполнить валидными значениями
ОР: Не появляется сообщение об ошибке со следующим текстом "Uncaught mysqli_sql_exception: You have an error in your SQL syntax;"
```
#### 4.4 Union в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести:  UNION ALL SELECT 1
    3. Остальные поля заполнить валидными значениями
```
#### 4.5 Union и Sleep в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: 1' UNION SELECT sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должен быть отправлен запрос через 5 сек
```
#### 4.6 Sleep в поле "Описание товара"
```
STR:
    1. Перейти в карточку товара
    2. В поле "Описание товара" ввести: 1 or sleep(5)#
    3. Остальные поля заполнить валидными значениями
ОР: Не должн быть отправлен запрос через 5 сек
```
## Дополнительные проверки на инъекцию команд

#### Команды:

mail.ru;ls - содержимое (папки)

mail.ru;cat /etc/passwd - список пользователей

mail.ru | cat /etc/passwd - список пользователей

mail.ru|cat /etc/passwd - список пользователей
