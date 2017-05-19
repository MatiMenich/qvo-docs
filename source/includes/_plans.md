# Planes

Un plan de suscripción, contiene la información de cobro para diferentes productos o niveles de características de tu sitio. Por ejemplo, puedes tener una plan de CLP$20.000/mes por caracterísitcas básicas y un plan distinto de CLP$40.000 por características "premium".


## El objeto plan

> Ejemplo de respuesta

```json
{
  "id": "oro",
  "name": "Plan oro",
  "price": "3000.0",
  "currency": "CLP",
  "trial_period_days": 0,
  "status": "active",
  "subscriptions": [
    {
      "id": "sub_HnKU4UmU5GtymRulcVOEow",
      "status": "active",
      "current_period_start": "2017-05-17T19:12:57.185Z",
      "current_period_end": "2017-06-17T19:12:57.185Z",
      "created_at": "2017-05-17T19:12:57.189Z",
      "updated_at": "2017-05-17T19:12:57.189Z",
      "customer": {
        "id": "cus_qos_6r3-4I4zIiou2BVMHg",
        "name": "Jon Snow",
        "email": "dabastard@thewatch.org"
      }
    }
  ],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```

### Atributos
|||
|--------- | -----------|
| id<p class="attr-desc">string</p> | Identificador único del objeto |
| name<p class="attr-desc">string</p> | El nombre de despliegue del plan. |
| price<p class="attr-desc">number</p> | El precio del plan. |
| currency<p class="attr-desc">string</p> | Código de <a href="https://www.iso.org/iso-4217-currency-codes.html">3 dígitos ISO de moneda</a> del plan. Puede ser: `CLP` o `USD` |
| trial_period_days<p class="attr-desc">integer</p> | Número de días de prueba otorgados cuando se suscribe un cliente al plan. Es `0` si no tiene un periodo definido. |
| status<p class="attr-desc">string</p> | Estado del plan. Puede ser: `active` o `inactive`. |
| subscriptions<p class="attr-desc">Array<<a href="#el-objeto-suscripci-n">Subscription</a>></p> | Suscripciones activas relacionadas al plan. |
| created_at<p class="attr-desc">datetime</p> | Fecha de creación del objeto |
| updated_at<p class="attr-desc">datetime</p> | Fecha de la última actualización del objeto |


## Crear plan

> Ejemplo de llamada

````shell
curl --request POST "https://api.qvo.cl/plans" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA" \
  -d id="oro" \
  -d name="Plan oro"
  -d price=15000,
  -d currency="CLP",
  -d trial_period_days=10
````


````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/plans', { method: 'POST'}, {
  id: "oro",
  name: "Plan Oro",
  price: 15000,
  currency: "CLP",
  trial_period_days: 10
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.post 'http://api.qvo.cl/plans', params:
  {
    id: "oro",
    name: "Plan Oro",
    price: 15000,
    currency: "CLP",
    trial_period_days: 10
  }

p JSON.parse(result)
````

````python
import requests

r = requests.post('http://api.qvo.cl/plans', params={
  id: "oro",
  name: "Plan Oro",
  price: 15000,
  currency: "CLP",
  trial_period_days: 10
})

print r.json()
````

> Ejemplo de respuesta

```json
{
  "id": "oro",
  "name": "Plan oro",
  "price": "15000.0",
  "currency": "CLP",
  "trial_period_days": 10,
  "status": "active",
  "subscriptions": [],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```

`POST /plans`

Crea un nuevo objeto plan.

### Parámetros
|||
|--------- | -----------|
| id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. **Único**. |
| name<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Nombre de despliegue del plan. |
| price<p class="attr-desc warning">Requerido</p><p class="attr-desc">number</p> | Precio del plan. |
| currency<p class="attr-desc warning">Requerido</p><p class="attr-desc">number</p> | Código de <a href="https://www.iso.org/iso-4217-currency-codes.html">3 dígitos ISO de moneda</a> del plan. Puede ser: `CLP` o `USD`. |
| trial_period_days<p class="attr-desc">integer</p> | Especifica el número de días de prueba del plan. Si incluyes un periodo de prueba, al cliente no se le cobrará hasta que termine este periodo. |


### Respuesta

Retorna un objeto de plan si la llamada es exitosa. Si existe otro plan con el mismo `id`, retornará <a href="#errores">un error</a>.



## Obtener plan

> Ejemplo de llamada

````shell
curl --request GET "https://api.qvo.cl/plans" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````

````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/plans/oro', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get 'http://api.qvo.cl/plans/oro'
p JSON.parse(result)
````

````python
import requests

r = requests.get('http://api.qvo.cl/plans/oro')

print r.json()
````

> Ejemplo de respuesta

```json
{
  "id": "oro",
  "name": "Plan oro",
  "price": "15000.0",
  "currency": "CLP",
  "trial_period_days": 10,
  "status": "active",
  "subscriptions": [],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```

`GET /plans/{plan_id}`

Obtiene los detalles de un plan existente. Se necesita proporcionar sólo el identificador único del cliente el cual fue retornado al momento de su creación.

### Parámetros
|||
|--------- | -----------|
| plan_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. |


### Respuesta

Retorna un objeto de plan si se provee de un identificador válido.




## Actualizar plan

> Ejemplo de llamada

````shell
curl --request PUT "https://api.qvo.cl/plans/oro" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA" \
  -d name="Di Oro"
````


````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/plans/oro', { method: 'PUT'}, {
  name: "Di Oro"
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.put 'http://api.qvo.cl/plans/oro', params:
  {
    name: "Di Oro"
  }

p JSON.parse(result)
````

````python
import requests

r = requests.put('http://api.qvo.cl/plans/oro', params={
  name: "Di Oro"
})

print r.json()
````

> Ejemplo de respuesta

```json
{
  "id": "oro",
  "name": "Di Oro",
  "price": "15000.0",
  "currency": "CLP",
  "trial_period_days": 10,
  "status": "active",
  "subscriptions": [],
  "created_at": "2017-05-17T19:12:55.450Z",
  "updated_at": "2017-05-17T19:12:55.450Z"
}
```


`PUT /plans/{plan_id}`

Actualiza el plan especificado con los parametros provistos. Cualquier parámetro que no se provea quedará inalterado.


### Parámetros
|||
|--------- | -----------|
| plan_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. |
| name<p class="attr-desc">string</p> | Nombre de despliegue del plan. |


### Respuesta

Retorna el objeto de plan si la actualización es exitosa. Retorna <a href="#errores">un error</a> si algun parámetro de actualización es inválido.

## Eliminar plan

> Ejemplo de llamada

````shell
curl -x DELETE "https://api.qvo.cl/plans/oro" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````


````javascript
const request = require('node-fetch');
fetch('http://api.qvo.cl/plans/oro', { method: 'DELETE'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.delete 'http://api.qvo.cl/plans/oro'
p JSON.parse(result)
````

````python
import requests

r = requests.delete('http://api.qvo.cl/plans/oro')

print r.json()
````

`DELETE /plans/{plan_id}`

Elimina permanentemente un plan. Esta acción es irreversible. Si existieran suscripciones activas asociadas al plan, este no se podrá eliminar

### Parámetros
|||
|--------- | -----------|
| plan_id<p class="attr-desc warning">Requerido</p><p class="attr-desc">string</p> | Identificador único del plan. |



### Respuesta

Retorna una respuesta sin contenido si el plan fue eliminado con éxito. Si el identificador del cliente no es válido, retornará <a href="#errores">un error</a>.



## Obtener una lista de planes

> Ejemplo de llamada

````shell
curl --request GET "https://api.qvo.cl/plans" \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoiVGVzdCBjb21tZXJjZSIsImFwaV90b2tlbiI6dHJ1ZX0.AXt3ep_r23w9rSPTv-AnK42s2m-1O0okMYrYYDlRyXA"
````

````javascript
const request = require('node-fetch');
fetch('https://api.qvo.cl/plans', { method: 'GET'})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});
````

````ruby
require 'rest-client'
require 'json'

result = RestClient.get 'https://api.qvo.cl/plans', params:
  {
    # TODO
  }

p JSON.parse(result)
````

````python
import requests

r = requests.get('https://api.qvo.cl/plans', params={
  # TODO
})

print r.json()
````

> Ejemplo de respuesta

```json
[
  {
    "id": "oro",
    "name": "Plan Oro",
    "price": "15000.0",
    "currency": "CLP",
    "trial_period_days": 10,
    "status": "active",
    "subscriptions": [
      {
        "id": "sub_HnKU4UmU5GtymRulcVOEow",
        "status": "active",
        "current_period_start": "2017-05-17T19:12:57.185Z",
        "current_period_end": "2017-06-17T19:12:57.185Z",
        "created_at": "2017-05-17T19:12:57.189Z",
        "updated_at": "2017-05-17T19:12:57.189Z",
        "customer": {
          "id": "cus_qos_6r3-4I4zIiou2BVMHg",
          "name": "Jon Snow",
          "email": "dabastard@winterfell.com"
        }
      }
    ],
    "created_at": "2017-05-17T19:12:55.450Z",
    "updated_at": "2017-05-17T19:12:55.450Z"
  }
]
```

`GET /customers`

Retorna una lista de planes. Los planes se encuentran ordenados por defecto por la fecha de creación, donde los mas recientes aparecerán primero.

<aside class="notice">
Este endpoint puede ser utilizado con <a href="#paginaci-n-filtros-y-orden">paginación, filtros y orden</a>
</aside>

### Respuesta

Un arreglo donde cada entrada representa a un plan con su respectiva información.

