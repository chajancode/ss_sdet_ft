# План тестирования
## 1. Объект тестирования:

REST API GET /products/{productId}/cost?authToken=&count=&start= 
Возвращает стоимость продукта по его productID.
В качестве  входных данных принимает следующие параметры:
- productId - идентификатор продукта
- authToken - токен авторизации
- count - количество экземпляров продукта, за которое нужно получить стоимость
- start - индекс, с которого необходимо вычислять стоимость (количество уже приобретенных продуктов)
## 2. Области тестирования:
Функциональные области, подлежащие тестированию:
	- Авторизация запроса посредством передачи параметра authToken
	- Получение стоимости продукта по productId
	- Проверка передачи параметров count, start
	- Проверка корректности вычислений
	- Проверка ответов от сервера
## 3. Методы тестирования:
- Позитивные сценарии
- Негативные сценарии
- Граничные значения параметров
## Тест-кейс #1.  Тестирование параметров запроса count, start
### Предусловия:
1.  Используется валидный токен: "aB3kL9mN2pQ7rT4w"
2.  Для позитивного сценария используется валидный productId: 1325
### Шаги:
### - Выполнить запросы из таблицы:
<table border="1"><thead>
  <tr>
    <th>№</th>
    <th>count</th>
    <th>start</th>
    <th>Запрос</th>
    <th>Ожидаемый результат</th>
  </tr></thead>
<tbody>
  <tr>
    <td>1<br></td>
    <td>5</td>
    <td>0</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=5&amp;start=0<br><br></td>
    <td>- код ответа: 200<br>- тело ответа:<br>&nbsp;&nbsp;&nbsp;{"cost": 100}</td>
  </tr>
  <tr>
    <td>2</td>
    <td>2</td>
    <td>2</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=2&amp;start=2</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 35}</td>
  </tr>
  <tr>
    <td>3</td>
    <td>1</td>
    <td>0</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=1&amp;start=0</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 30}</td>
  </tr>
  <tr>
    <td>4</td>
    <td>6</td>
    <td>0</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=6&amp;start=0</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 130}</td>
  </tr>
  <tr>
    <td>5</td>
    <td>1</td>
    <td>4</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=1&amp;start=4</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 10}</td>
  </tr>
  <tr>
    <td>6</td>
    <td>1<br></td>
    <td>5</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=5&amp;start=1</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 30}</td>
  </tr>
  <tr>
    <td>7</td>
    <td>1<br></td>
    <td>6</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=1&amp;start=6</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 25}</td>
  </tr>
  <tr>
    <td>8</td>
    <td>4</td>
    <td>0<br></td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=4&amp;start=0</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 90}</td>
  </tr>
  <tr>
    <td>9</td>
    <td>5</td>
    <td>6<br></td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=5&amp;start=6</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 100}</td>
  </tr>
  <tr>
    <td>10</td>
    <td>6</td>
    <td>5</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=6&amp;start=5</td>
    <td>- код: 200<br>- тело ответа:<br>   {"cost": 130}</td>
  </tr>
  <tr>
    <td>11</td>
    <td>1</td>
    <td>-1</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=1&amp;start=-1</td>
    <td>- код: 400<br>- сообщение о некорректных параметрах</td>
  </tr>
  <tr>
    <td>12</td>
    <td>0</td>
    <td>0</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=0&amp;start=0</td>
    <td>- код: 400<br>- сообщение о некорректных параметрах</td>
  </tr>
  <tr>
    <td>13</td>
    <td>-1</td>
    <td>0</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=-1&amp;start=0</td>
    <td>- код: 400<br>- сообщение о некорректных параметрах</td>
  </tr>
</tbody></table>

##  Test-case #2. Тестирование токена авторизации.
### Предусловия:
1. Используется productID со значением: 1325
2. Для позитивного сценария используется валидный токен: "aB3kL9mN2pQ7rT4w"
3. Параметр count используется со значением: 5
4. Параметр start используется со значением: 0
### Шаги:
- ### Выполнить запросы из таблицы:
<table border="1"><thead>
  <tr>
    <th>№</th>
    <th>Запрос</th>
    <th>Описание токена</th>
    <th>Ожидаемый результат</th>
  </tr></thead>
<tbody>
  <tr>
    <td>1</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=5&amp;start=0</td>
    <td>Валидный токен. 16 символов, содержит цифры и латиницу</td>
    <td>- код ответа: 200<br>- тело ответа:<br>&nbsp;&nbsp;&nbsp;{"cost": 100}</td>
  </tr>
  <tr>
    <td>2</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4&amp;count=5&amp;start=0</td>
    <td>15 символов, содержит цифры и латиницу</td>
    <td rowspan="8">код ответа: 401</td>
  </tr>
  <tr>
    <td>3</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w5&amp;count=5&amp;start=0</td>
    <td>17 символов, содержит цифры и латиницу</td>
  </tr>
  <tr>
    <td>4</td>
    <td>/products/1325/cost?authToken=aBlkLPmNUpQjrTWw&amp;count=5&amp;start=0</td>
    <td>16 символов, содержит только латиницу</td>
  </tr>
  <tr>
    <td>5</td>
    <td>/products/1325/cost?authToken=4637497721779845&amp;count=5&amp;start=0</td>
    <td>16 символов, содержит только цифры</td>
  </tr>
  <tr>
    <td>6</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2*Q7&amp;T4w&amp;count=5&amp;start=0</td>
    <td>16 символов, содержит цифры, латиницу и спецсимволы</td>
  </tr>
  <tr>
    <td>7</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4й&amp;count=5&amp;start=0</td>
    <td>16 символов, содержит цифры, латиницу и кириллицу</td>
  </tr>
  <tr>
    <td>8</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4G&amp;count=5&amp;start=0</td>
    <td>Невалидный токен. 16 символов, содержит цифры и латиницу</td>
  </tr>
  <tr>
    <td>9</td>
    <td>/products/1325/cost?authToken=&amp;count=5&amp;start=0</td>
    <td>Токен отсутствует</td>
  </tr>
</tbody></table>

##  Test-case #. Тестирование параметра пути productId.
### Предусловия:
1. Для позитивного сценария используется валидный productId: 1325
2. Используется валидный токен: "aB3kL9mN2pQ7rT4w"
3. Параметр count используется со значением: 5
4. Параметр start используется со значением: 0
### Шаги:
- ### Выполнить запросы из таблицы:
<table border="1"><thead>
  <tr>
    <th>№</th>
    <th>Запрос</th>
    <th>Значение productId</th>
    <th>Ожидаемый результат</th>
  </tr></thead>
<tbody>
  <tr>
    <td>1</td>
    <td>/products/1325/cost?authToken=aB3kL9mN2pQ7rT4w&amp;count=5&amp;start=0</td>
    <td>Валидный productId: 1325</td>
    <td>- код ответа: 200 - тело ответа: {"cost": 100}</td>
  </tr>
  <tr>
    <td>2</td>
    <td>/products/0/cost?authToken=aB3kL9mN2pQ7rT4&amp;count=5&amp;start=0</td>
    <td>0</td>
    <td>- код ответа: 500<br>- тело ответа:<br>{"errorMessage":&nbsp;&nbsp;"productId не может быть нулевым"}<br></td>
  </tr>
  <tr>
    <td>3</td>
    <td>/products/-1/cost?authToken=aB3kL9mN2pQ7rT4w5&amp;count=5&amp;start=0</td>
    <td>-1</td>
    <td>- код ответа: 500<br>- тело ответа:<br>{"errorMessage":  "productId не может быть отрицательным"}</td>
  </tr>
  <tr>
    <td>4</td>
    <td>/products/376543890500/cost?authToken=aB3kL9mN2pQ7rT4w5&amp;count=5&amp;start=0</td>
    <td>Невалидный productId: 376543890500</td>
    <td>- код ответа: 404</td>
  </tr>
</tbody></table>