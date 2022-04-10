Postman HW_1

## MagicSearch: проверяем статус коды
Открываем документацию по Users `https://testbase.atlassian.net/wiki/spaces/USERS/pages/592511089/SOAP+REST)`, находим метод MagicSearch `(https://testbase.atlassian.net/wiki/spaces/USERS/pages/1249378773/MagicSearch)`.
<hr>

## Ваша задача — написать автотесты на блок «Статусы ответов».

<hr>

1. Регистрируем нового пользователя.

* `http://users.bugred.ru/tasks/rest/doregister` метод: `POST`.
* Входные параметры: email, name, password.
* Повторить тест с другими данными в фамилии и отчестве.
* Тест на статус код 200
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

2. Статус код 231 — найден 1 юзер.

* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query - имя созданного пользователя
* Тест на статус код 231
```js
pm.test("Status code is 231", function () {
    pm.response.to.have.status(231);
});
```

3. Статус код 232 — найдено больше 1 юзера (но без компаний)
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query - имя созданного пользователя
* Тест на статус код 232
```js
pm.test("Status code is 232", function () {
    pm.response.to.have.status(232);
});
```

4. Статус код 230 — никого не нашли по запросу, пустой ответ
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query - рандомный набор символов.
* Тест на статус код 230
```js
pm.test("Status code is 230", function () {
    pm.response.to.have.status(230);
});
```

5. Регистрируем новую компанию.
* `http://users.bugred.ru/tasks/rest/createcompany` метод: `POST`.
* Входные параметры: company_name, company_type, company_users, email_owner.
* После создания меняем параметры - company_users, email_owner и запускаем еще раз.

6. Статус код 233 — найдена 1 компания.
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query
```js
pm.test("Status code is 233", function () {
    pm.response.to.have.status(233);
});
```

7. Cтатус код 234 — найдено больше 1 компании (но без юзеров)
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query
```js
pm.test("Status code is 234", function () {
    pm.response.to.have.status(234);
});
```

8. Cтатус код 235 — найдены как юзеры, так и компании
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query
```js
pm.test("Status code is 235", function () {
    pm.response.to.have.status(235);
});
```

9. Cтатус код 455 — не указан параметр query в запросе. Body сообщения — “Не найден обязательный параметр query”
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: нет
```js
pm.test("Status code is 455", function () {
    pm.response.to.have.status(455);
});
```

10. Cтатус код 456 — длина запроса выше 1000 символов. Текст ошибки — “Длина запроса не должна превышать 1000 символов”
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: текст длинной 1000+ символов
```js
pm.test("Status code is 456", function () {
    pm.response.to.have.status(456);
});
```

11. Cтатус код 457 — неправильно задан partyType (значение не из доступного списка выбора). Текст ошибки — “Параметр partyType может принимать только значения: ALL, USER, COMPANY”
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query, partyType. 
```js
pm.test("Status code is 457", function () {
    pm.response.to.have.status(457);
});
```

12. 458 — неправильно задан параметр taskStatus (не из списка выбора значение). Текст ошибки — “Параметр taskStatus может принимать только значения: ALL, ACTUAL, COMPLETE, FAIL”
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query, taskStatus. 
```js
pm.test("Status code is 458", function () {
    pm.response.to.have.status(458);
});
```

13. Cтатус код 459 — неправильно задан параметр include (не из списка выбора значение). Текст ошибки — “Параметр include может принимать только значения: ALL, USER, COMPANY, TASK, WHY”
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* Входные параметры: query, include. 
```js
pm.test("Status code is 459", function () {
    pm.response.to.have.status(459);
});
```
