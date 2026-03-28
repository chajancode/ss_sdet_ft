# План тестирования.

### 1. Объект тестирования:

- Эндпоинт: GET /products/{productId}/status

### 2. Методы тестирования:
- Позитивные сценарии
- Негативные сценарии
- Граничные значения параметров
- Попарное тестирование параметров

##  Test-case #1. Тестирование токена авторизации.
### Предусловия:
1. Использовать productID со значением: 1325
2. Для позитивного сценария использовать валидный токен: "aB3kL9mN2pQ7rT4w"
### Выполнить запросы из таблицы:
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
      <td>Ответ в формате json с http‑кодом 200 <code>{"productStatus": 1}</code> или <code>{"productStatus": 1}</code></td>
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
    </tr>
  </tbody>
</table>
