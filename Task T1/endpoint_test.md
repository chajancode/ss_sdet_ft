# План тестирования.

### 1. Объект тестирования:

- Эндпоинт: GET /products/

### 2. Методы тестирования:
- Позитивные сценарии
- Негативные сценарии
- Граничные значения параметров
- Попарное тестирование параметров

##  Test-case #1. Тестирование токена авторизации.
### Предусловия:
1. Используется productID со значением: 1325
2. Для позитивного сценария используется валидный токен: "aB3kL9mN2pQ7rT4w"
### Шаги:
- ### Выполнить запросы из таблицы:
<table border="1">
  <thead>
    <tr>
      <th>№</th>
      <th>Запрос</th>
      <th>Описание токена</th>
      <th>Ожидаемый результат</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td><code>/products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>Валидный токен. 16 символов, содержит цифры и латиницу</td>
      <td>Ответ в формате json с http‑кодом 200 <code>{"productStatus": 1}</code> или <code>{"productStatus": 0}</code></td>
    </tr>
    <tr>
      <td>2</td>
      <td><code>/products/1325/status?authToken=aB3kL9mN2pQ7rT4&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>15 символов, содержит цифры и латиницу</td>
      <td rowspan="6">Ответ в формате json с http‑кодом 500 <code>{"errorMessage": }</code></td>
    </tr>
    <tr>
      <td>3</td>
      <td><code>/products/1325/status?authToken=aB3kL9mN2pQ7rT4wq&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>17 символов, содержит цифры и латиницу</td>
    </tr>
    <tr>
      <td>4</td>
      <td><code>/products/1325/status?authToken=aBBkLqmNvpQyrTew&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>16 символов, содержит только латиницу</td>
    </tr>
    <tr>
      <td>5</td>
      <td><code>/products/1325/status?authToken=1513105883615340&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>16 символов, содержит только цифры</td>
    </tr>
    <tr>
      <td>6</td>
      <td><code>/products/1325/status?authToken=!@$akNmOPt#b4nII&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>16 символов, содержит цифры, латиницу и спецсимволы</td>
    </tr>
    <tr>
      <td>7</td>
      <td><code>/products/1325/status?authToken=aB3kL9mNйЪ7rэT4w&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>16 символов, содержит цифры, латиницу и кириллицу</td>
    </tr>
    <tr>
      <td>8</td>
      <td><code>/products/1325/status?authToken=alrkL9mN2pQ7rT41&amp;recalculate=&amp;owner=&amp;region=</code></td>
      <td>Невалидный токен. 16 символов, содержит цифры и латиницу</td>
      <td>Ответ с http‑кодом 401 </td>
    </tr>
  </tbody>
</table>

##  Test-case #2. Тестирование productId.
### Предусловия:
1. Используется валидный токен: "aB3kL9mN2pQ7rT4w"
2. Для проверки позитивного сценария используется валидный productId: 1325
3. Для проверки негативного сценария используется невалидный productId: 0
### Шаги:
- ### Выполнить запросы из таблицы:
<table border="1"><thead>
  <tr>
    <th>№</th>
    <th>Запрос<br></th>
    <th>Значение productId<br></th>
    <th>Ожидаемый результат</th>
  </tr></thead>
<tbody>
  <tr>
    <td>1<br></td>
    <td>/products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=&amp;region=</td>
    <td>Валидный productId: 1325</td>
    <td>Ответ в формате json с http‑кодом 200 {"productStatus": 1} или {"productStatus": 0}</td>
  </tr>
  <tr>
    <td>2<br></td>
    <td>/products/0/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=&amp;region=</td>
    <td>0</td>
    <td>Ответ с http-кодом 404</td>
  </tr>
  <tr>
    <td></td>
    <td>/products/-1/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=&amp;region=</td>
    <td>-1</td>
    <td>Ответ с http-кодом 404</td>
  </tr>
</tbody>
</table>

##  Test-case #3. Тестирование параметров recalculate, owner, region.
### Предусловия:
1. Используется валидный токен: "aB3kL9mN2pQ7rT4w"
2. Используется валидный productId: 1325
### Шаги:
- ### Выполнить запросы из таблицы:

<table border="1"><thead>
  <tr>
    <th> <br>№</th>
    <th> <br>recalculate </th>
    <th> <br>owner</th>
    <th> <br>region</th>
    <th> <br>Запрос</th>
    <th>Ожидаемый результат</th>
  </tr></thead>
<tbody>
  <tr>
    <td> <br>1</td>
    <td> <br>true</td>
    <td> <br>создатель</td>
    <td> <br>Северо-Запад</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=true&amp;owner=Создатель&amp;region=Северо-Запад</td>
    <td rowspan="16">Ответ в формате json с http‑кодом 200 <code>{"productStatus": 1}<code> или <code>{"productStatus": 0}<code></td>
  </tr>
  <tr>
    <td> <br>2</td>
    <td> <br>true</td>
    <td> <br>Пользователь</td>
    <td> <br>Сибирь</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=true&amp;owner=Пользователь&amp;region=Сибирь</td>
  </tr>
  <tr>
    <td> <br>3</td>
    <td> <br>true</td>
    <td> <br>null</td>
    <td> <br>Поволжье</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=true&amp;owner=null&amp;region=Поволжье </td>
  </tr>
  <tr>
    <td> <br>4</td>
    <td> <br>true</td>
    <td> <br>  </td>
    <td> <br>  </td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=true&amp;owner=&amp;region= </td>
  </tr>
  <tr>
    <td> <br>5</td>
    <td> <br>false</td>
    <td> <br>Пользователь</td>
    <td> <br>Поволжье</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=false&amp;owner=Пользователь&amp;region=Поволжье </td>
  </tr>
  <tr>
    <td> <br>6 </td>
    <td> <br>false</td>
    <td> <br>null</td>
    <td> <br>  </td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=false&amp;owner=null&amp;region= </td>
  </tr>
  <tr>
    <td> <br>7 </td>
    <td> <br>false</td>
    <td> <br>  </td>
    <td> <br>Северо-Запад</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=false&amp;owner=&amp;region=Северо-Запад </td>
  </tr>
  <tr>
    <td> <br>8</td>
    <td> <br>false</td>
    <td> <br>Создатель</td>
    <td> <br>Сибирь</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=false&amp;owner=Создатель&amp;region=Сибирь </td>
  </tr>
  <tr>
    <td> <br>9</td>
    <td> <br>null</td>
    <td> <br>null</td>
    <td> <br>Северо-Запад</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=null&amp;owner=null&amp;region=Северо-Запад</td>
  </tr>
  <tr>
    <td> <br>10</td>
    <td> <br>null</td>
    <td> <br>  </td>
    <td> <br>Сибирь</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=null&amp;owner=&amp;region=Сибирь </td>
  </tr>
  <tr>
    <td> <br>11</td>
    <td> <br>null</td>
    <td> <br>Создатель</td>
    <td> <br>Поволжье</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=null&amp;owner=Создатель&amp;region=Поволжье </td>
  </tr>
  <tr>
    <td> <br>12</td>
    <td> <br>null</td>
    <td> <br>Пользователь</td>
    <td> <br>  </td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=null&amp;owner=Пользователь&amp;region= </td>
  </tr>
  <tr>
    <td> <br>13</td>
    <td> <br>  </td>
    <td> <br>  </td>
    <td> <br>Поволжье</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=&amp;region=Поволжье </td>
  </tr>
  <tr>
    <td> <br>14</td>
    <td> <br>  </td>
    <td> <br>Создатель</td>
    <td> <br>  </td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=Создатель&amp;region= </td>
  </tr>
  <tr>
    <td> <br>15</td>
    <td> <br>  </td>
    <td> <br>Пользователь</td>
    <td> <br>Северо-Запад</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=Пользователь&amp;region=Северо-Запад </td>
  </tr>
  <tr>
    <td> <br>16</td>
    <td> <br>  </td>
    <td> <br>null</td>
    <td> <br>Сибирь</td>
    <td> <br> /products/1325/status?authToken=aB3kL9mN2pQ7rT4w&amp;recalculate=&amp;owner=null&amp;region=Сибирь </td>
  </tr>
</tbody></table>
