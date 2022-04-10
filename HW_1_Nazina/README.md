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

6. Статус код 233 — найдена 1 компания.
* `http://users.bugred.ru/tasks/rest/magicsearch` метод: `POST`.
* 
