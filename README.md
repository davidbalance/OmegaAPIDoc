# Omega Sistema de Reporteria Medica

## Table of contents

1. [Introducción](#introduction)
2. [Autenticación](#authentication)
3. [Endpoints](#endpoints)
   1. [`POST` /external/connection/corporative/groups/_{source}_](#endpoint-1)
   2. [`PATCH` /external/connection/corporative/groups/_{source}_/_{key}_](#endpoint-2)
   3. [`POST` /external/connection/company/_{source}_](#endpoint-3)
   4. [`PATCH` /external/connection/corporative/groups/_{source}_/_{key}_](#endpoint-4)
   5. [`POST` /external/connection/branch/_{source}_](#endpoint-5)
   6. [`PATCH` /external/connection/branch/_{source}_/_{key}_](#endpoint-6)
   7. [`POST` /external/connection/patients](#endpoint-7)
   8. [`PATCH` /external/connection/patients/_{dni}_](#endpoint-8)
   9. [`POST` /external/connection/doctor](#endpoint-9)
   10. [`PATCH` /external/connection/doctor/_{dni}_](#endpoint-10)
   11. [`POST` /external/connection/exams/_{source}_](#endpoint-11)
   12. [`PATCH` /external/connection/exams/_{source}_/_{key}_](#endpoint-12)
   13. [`GET` /external/connection/medical/order/dni/_{dni}_](#endpoint-13)
   14. [`GET` /external/connection/medical/order/dni/_{source}_/order/_{key}_](#endpoint-14)
   15. [`POST` /external/connection/medical/order/_{source}_](#endpoint-15)
   16. [`PATCH` /external/connection/medical/order/_{source}_/_{key}_](#endpoint-16)
   17. [`GET` /external/connection/medical/result/_{source}_/key/_{key}_](#endpoint-17)
   18. [`POST` /external/connection/medical/result/_{source}_](#endpoint-18)
   19. [`PATCH` /external/connection/medical/result/_{source}_/file/_{key}_](#endpoint-19)
   20. [`POST` /medical/file](#endpoint-20)
   21. [`POST` /medical/file/multiple](#endpoint-21)

<div id='introduction'/>

## Introducción

La aplicación de Omega Sistema de Reportería Médica expone varios endpoints que pueden ser usados por sistemas externos. El presente documento tiene la finalidad de proveer información necesaria para la conexión de aplicaciones externas.

Los endpoints expuestos permiten el acceso, creación y modificación de información mediante los parámetros `source` y `key`, los cuales representan a la aplicación de origen desde donde se busca consumir el endpoint y un identificador único que la aplicación de origen provee para identificar sus datos.

<div id='authentication'/>

## Autenticación

Para el consumo del API se requiere una API-KEY. Esta llave será proporcionada por `Omega Sistema de Reportería Médica` y deberá ser usada antes de realizar cualquier petición a los endpoints. La llave deberá ser colocada en la cabecera de la petición con el nombre de `x-api-key`.

<div id='endpoints'/>

## Endpoints

Los endpoints presentes identifican un URL PARAM nombrado como `source`. Este representa a la aplicación de origen y deberá ser colocada en minúsculas y, si posee espacios, reemplazarlos usando guiones medios (-).

- Aplicación Ejemplo: _`<api>/aplicacion-ejemplo`_
- Aplicación: _`<api>/aplicacion`_

<div id='endpoint-1'/>

### `POST` /external/connection/corporative/groups/_{source}_

Crea un grupo corporativo. Este grupo podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

#### Request Body

- **name**: Nombre del grupo corporativo. Este es único.
- **key**: Identificador único.

```json
{
  "name": "string",
  "key": "string"
}
```

#### Response

##### Response Status Code

- 201 Created
- 409 Conflict

##### Response Body

```json
{
  "id": "number",
  "name": "string"
}
```

<div id='endpoint-2'/>

### `PATCH` /external/connection/corporative/groups/_{source}_/_{key}_

Actualiza un grupo corporativo. Este grupo podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

#### Request Body

- **name**: Nombre del grupo corporativo. Este es único.

```json
{
  "name": "string"
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "name": "string"
}
```

<div id='endpoint-3'/>

### `POST` /external/connection/company/_{source}_

Crea una empresa. Esta podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

#### Request Body

- **key**: Identificador único.
- **ruc**: RUC de la empresa. Este debe ser único.
- **name**: Nombre de la empresa. Este es único.
- **address**: Dirección de la empresa.
- **phone**: Teléfono de la empresa.
- **corporativeGroup**:
  - **name**: Nombre del grupo corporativo. Este es único.
  - **key**: Identificador único.

```json
{
  "key": "string",
  "ruc": "string",
  "name": "string",
  "address": "string",
  "phone": "string",
  "corporativeGroup": {
    "name": "string",
    "key": "string"
  }
}
```

#### Response

##### Response Status Code

- 201 Created
- 409 Conflict

##### Response Body

```json
{
  "id": "number",
  "ruc": "string",
  "name": "string",
  "address": "string",
  "phone": "string"
}
```

<div id='endpoint-4'/>

### `PATCH` /external/connection/corporative/groups/_{source}_/_{key}_

Actualiza una empresa. Esta empresa podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

#### Request Body

- **name**: Nombre de la empresa. Este es único.
- **address**: Dirección de la empresa.
- **phone**: Teléfono de la empresa.

```json
{
  "name": "string",
  "address": "string",
  "phone": "string"
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "ruc": "string",
  "name": "string",
  "address": "string",
  "phone": "string"
}
```

<div id='endpoint-5'/>

### `POST` /external/connection/branch/_{source}_

Crea una sucursal. Esta podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

#### Request Body

- **key**: Identificador único.
- **name**: Nombre de la sucursal.
- **city**: Ciudad. Esta puede ser una de las indicadas al final del documento.
- **company**:
  - **key**: Identificador único.
  - **ruc**: RUC de la empresa. Este debe ser único.
  - **name**: Nombre de la empresa. Este es único.
  - **address**: Dirección de la empresa.
  - **phone**: Teléfono de la empresa.
  - **corporativeGroup**:
    - **name**: Nombre del grupo corporativo. Este es único.
    - **key**: Identificador único.

```json
{
  "key": "string",
  "name": "string",
  "city": "string",
  "company": {
    "key": "string",
    "ruc": "string",
    "name": "string",
    "address": "string",
    "phone": "string",
    "corporativeGroup": {
      "name": "string",
      "key": "string"
    }
  }
}
```

#### Response

##### Response Status Code

- 201 Created

##### Response Body

```json
{
  "id": "number",
  "name": "string",
  "city": {
    "name": "string"
  }
}
```

<div id='endpoint-6'/>

### `PATCH` /external/connection/branch/_{source}_/_{key}_

Actualiza una sucursal. Esta sucursal podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

#### Request Body

- **name**: Nombre de la sucursal. Este es único.

```json
{
  "name": "string"
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "name": "string",
  "city": {
    "name": "string"
  }
}
```

<div id='endpoint-7'/>

### `POST` /external/connection/patients

Crea un paciente.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### Request Body

- **gender**: Género del paciente. Debe colocarse `male` o `female`.
- **birthday**: Fecha de cumpleaños del paciente. Formato: `YYYY-MM-DD`.
- **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
- **name**: Nombre del paciente.
- **lastname**: Apellido del paciente.

```json
{
  "gender": "male" | "female",
  "birthday": "date",
  "dni": "string",
  "name": "string",
  "lastname": "string",
}
```

#### Response

##### Response Status Code

- 201 Created

##### Response Body

```json
{
  "id": "number",
  "gender": "male" | "female",
  "birthday": "date",
  "user": {
    "id": "number",
    "dni": "string",
    "name": "string",
    "lastname": "string"
  }
}
```

<div id='endpoint-8'/>

### `PATCH` /external/connection/patients/_{dni}_

Actualiza un paciente.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `dni`: El DNI del paciente.
  - **Type**: _String_

#### Request Body

- **gender**: Género del paciente. Debe colocarse `male` o `female`.
- **birthday**: Fecha de cumpleaños del paciente. Formato: `YYYY-MM-DD`.
- **name**: Nombre del paciente.
- **lastname**: Apellido del paciente.

```json
{
  "gender": "male" | "female",
  "birthday": "date",
  "name": "string",
  "lastname": "string",
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "gender": "male" | "female",
  "birthday": "date",
  "user": {
    "id": "number",
    "dni": "string",
    "name": "string",
    "lastname": "string"
  }
}
```

<div id='endpoint-9'/>

### `POST` /external/connection/doctor

Crea un doctor.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### Request Body

- **dni**: DNI del médico. Debe tener una longitud de 10 caracteres y ser único.
- **name**: Nombre del médico.
- **lastname**: Apellido del médico.
- **email**: Correo electrónico del médico.

```json
{
  "dni": "string",
  "name": "string",
  "lastname": "string",
  "email": "string"
}
```

#### Response

##### Response Status Code

- 201 Created

##### Response Body

```json
{
  "id": "number",
  "user": {
    "id": "number",
    "dni": "string",
    "name": "string",
    "lastname": "string",
    "email": "string"
  }
}
```

<div id='endpoint-10'/>

### `PATCH` /external/connection/doctor/_{dni}_

Actualiza un medico.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `dni`: El DNI del médico.
  - **Type**: _String_

#### Request Body

- **name**: Nombre del médico.
- **lastname**: Apellido del médico.
- **email**: Correo electrónico del médico.

```json
{
  "gender": "male" | "female",
  "birthday": "date",
  "dni": "string",
  "name": "string",
  "lastname": "string",
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "gender": "male" | "female",
  "birthday": "date",
  "user": {
    "id": "number",
    "dni": "string",
    "name": "string",
    "lastname": "string"
  }
}
```

<div id='endpoint-11'/>

### `POST` /external/connection/exams/_{source}_

Crea un examen de laboratorio. Este podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

#### Request Body

- **key**: Identificador único.
- **name**: Nombre del examen médico. Este es único.

```json
{
  "key": "string",
  "name": "string"
}
```

#### Response

##### Response Status Code

- 201 Created

##### Response Body

```json
{
  "id": "number",
  "name": "string"
}
```

<div id='endpoint-12'/>

### `PATCH` /external/connection/exams/_{source}_/_{key}_

Actualiza un examen de laboratorio. Este podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

#### Request Body

- **name**: Nombre actualizado del examen médico. Debe ser único.

```json
{
  "name": "string"
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "name": "string"
}
```

<div id='endpoint-13'/>

### `GET` /external/connection/medical/order/dni/_{dni}_

Obtiene un arreglo de órdenes médicas pertenecientes a un paciente, utilizando su DNI.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `dni`: El DNI del paciente.
  - **Type**: _String_

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "orders": [
    {
      "id": "number",
      "process": "string",
      "createAt": "date",
      "client": {
        "dni": "string",
        "fullname": "string"
      },
      "results": [
        {
          "id": "number",
          "examName": "string",
          "hasFile": "boolean",
          "report": { "id": "number" } | null
        }
      ]
    }
  ]
}
```

<div id='endpoint-14'/>

### `GET` /external/connection/medical/order/dni/_{source}_/order/_{key}_

Obtiene una orden médica utilizando su identificador único y su pertenencia a la aplicación original.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único de la orden médica.
  - **Type**: _String_

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "process": "string",
  "createAt": "date",
  "client": {
    "dni": "string",
    "fullname": "string"
  },
  "results": [
    {
      "id": "number",
      "examName": "string",
      "hasFile": "boolean",
      "report": { "id": "number" } | null
    }
  ]
}
```

<div id='endpoint-15'/>

### `POST` /external/connection/medical/order/_{source}_

Crea una orden médica.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

#### Request Body

- **key**: Identificador único de la orden médica.
- **process**: Nombre del proceso médico.
- **branch**:
  - **key**: Identificador único de la sucursal.
  - **name**: Nombre de la sucursal.
  - **city**: Ciudad de la sucursal.
  - **company**:
    - **key**: Identificador único de la empresa.
    - **ruc**: RUC de la empresa. Debe ser único.
    - **name**: Nombre de la empresa. Debe ser único.
    - **address**: Dirección de la empresa.
    - **phone**: Teléfono de la empresa.
    - **corporativeGroup**:
      - **name**: Nombre del grupo corporativo. Debe ser único.
      - **key**: Identificador único del grupo corporativo.
- **patient**:
  - **key**: Identificador único del paciente.
  - **gender**: Género del paciente. Debe ser `male` o `female`.
  - **birthday**: Fecha de cumpleaños del paciente.
  - **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
  - **name**: Nombre del paciente.
  - **lastname**: Apellido del paciente.
  - **email**: Correo del paciente

```json
{
  "key": "string",
  "process": "string",
  "branch": {
    "key": "string",
    "name": "string",
    "city": "string",
    "company": {
      "key": "string",
      "ruc": "string",
      "name": "string",
      "address": "string",
      "phone": "string",
      "corporativeGroup": {
        "name": "string",
        "key": "string"
      }
    }
  },
  "patient": {
    "gender": "male" | "female",
    "birthday": "date",
    "dni": "string",
    "name": "string",
    "lastname": "string",
    "email": "string"
  }
}
```

#### Response

##### Response Status Code

- 201 Created

##### Response Body

```json
{
  "id": "number",
  "process": "string",
  "createAt": "date",
  "client": {
    "dni": "string",
    "fullname": "string"
  },
  "results": [
    {
      "id": "number",
      "examName": "string",
      "hasFile": true,
      "report": { "id": 0 } | null
    }
  ]
}
```

<div id='endpoint-16'/>

### `PATCH` /external/connection/medical/order/_{source}_/_{key}_

Actualiza una orden médica.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del registro de la orden médica.
  - **Type**: _String_

#### Request Body

- **process**: Nombre actualizado del proceso médico.

```json
{
  "process": "string"
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "process": "string",
  "createAt": "date",
  "client": {
    "dni": "string",
    "fullname": "string"
  },
  "results": [
    {
      "id": "number",
      "examName": "string",
      "hasFile": true,
      "report": { "id": 0 } | null
    }
  ]
}
```

<div id='endpoint-17'/>

### `GET` /external/connection/medical/result/_{source}_/key/_{key}_

Obtiene un resultado médico utilizando su identificador único y su pertenencia a la aplicación original.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del resultado médico.
  - **Type**: _String_

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "examName": "string",
  "hasFile": true,
  "report": { "id": 0 } | null
}
```

<div id='endpoint-18'/>

### `POST` /external/connection/medical/result/_{source}_

Crea un resultado médico utilizando la aplicación de origen especificada.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

#### Request Body

- **key**: Identificador único del resultado médico.
- **file**: Archivo en formato PDF.
- **exam**:
  - **key**: Identificador único del examen médico.
  - **name**: Nombre del examen médico.
- **doctor**:
  - **dni**: DNI del médico. Debe tener una longitud de 10 caracteres y ser único.
  - **name**: Nombre del médico.
  - **lastname**: Apellido del médico.
  - **email**: Correo electrónico del médico.
- **order**:
  - **process**: Nombre del proceso médico.
  - **branch**:
    - **key**: Identificador único de la sucursal.
    - **name**: Nombre de la sucursal.
    - **city**: Ciudad donde se encuentra la sucursal.
    - **company**:
      - **key**: Identificador único de la empresa.
      - **ruc**: RUC de la empresa. Debe ser único.
      - **name**: Nombre de la empresa.
      - **address**: Dirección de la empresa.
      - **phone**: Teléfono de la empresa.
      - **corporativeGroup**:
        - **name**: Nombre del grupo corporativo.
        - **key**: Identificador único del grupo corporativo.
  - **patient**:
    - **key**: Identificador único del paciente.
    - **gender**: Género del paciente. Debe ser `male` o `female`.
    - **birthday**: Fecha de cumpleaños del paciente.
    - **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
    - **name**: Nombre del paciente.
    - **lastname**: Apellido del paciente.
    - **email**: Correo del paciente

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | false     |
| key     | string          | true      |
| exam    | object          | true      |
| doctor  | object          | true      |
| order   | object          | true      |

Los objetos que se requieren son los siguientes:

**Exam (object)**

```json
{
  "key": "string",
  "name": "string"
}
```

**Doctor (object)**

```json
{
  "dni": "string",
  "name": "string",
  "lastname": "string",
  "email": "string"
}
```

**Order (object)**

```json
{
  "key": "string",
  "process": "string",
  "branch": {
    "key": "string",
    "name": "string",
    "city": "string",
    "company": {
      "key": "string",
      "ruc": "string",
      "name": "string",
      "address": "string",
      "phone": "string",
      "corporativeGroup": {
        "name": "string",
        "key": "string"
      }
    }
  },
  "patient": {
    "gender": "male" | "female",
    "birthday": "date",
    "dni": "string",
    "name": "string",
    "lastname": "string",
    "email": "string"
  }
}
```

#### Response

##### Response Status Code

- 201 Created

##### Response Body

```json
{
  "id": "number",
  "examName": "string",
  "hasFile": "boolean",
  "report": { "id": 0 } | null
}
```

<div id='endpoint-19'/>

### `PATCH` /external/connection/medical/result/_{source}_/file/_{key}_

Permite subir un archivo PDF si no fue proporcionado al momento de crear el resultado médico.

#### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

#### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del resultado médico.
  - **Type**: _String_

#### Request Body

- **file**: Archivo PDF que se desea subir para adjuntarlo al resultado médico.

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | true      |

#### Response

##### Response Status Code

- 200 OK

##### Response Body

```json
{
  "id": "number",
  "examName": "string",
  "hasFile": true,
  "report": { "id": 0 } | null
}
```

<div id='endpoint-20'/>

### `POST` /medical/file

Obtiene un archivo médico específico basado en el identificador único proporcionado por Omega Sistema de Reporteria Medica.

#### Request Headers

- `Content-Type`: `application/json`

#### Request Body

- **id**: Identificador único de Omega Sistema de Reporteria Medica para el resultado o reporte.
- **type**: Tipo del archivo requerido. Debe ser `result` o `report`.

```json
{
  "id": "number",
  "type": "report" | "result"
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

Retorna un archivo en formato PDF

<div id='endpoint-21'/>

### `POST` /medical/file/multiple

Obtiene varios archivos médicos específicos basados en los identificadores únicos proporcionados por Omega Sistema de Reporteria Medica.

#### Request Headers

- `Content-Type`: `application/json`

#### Request Body

- **files**: Lista de objetos que especifican los archivos médicos requeridos.
  - **id**: Identificador único de Omega Sistema de Reporteria Medica para el resultado o reporte.
  - **type**: Tipo del archivo requerido. Debe ser `result` o `report`.

```json
{
  "files": [
    {
      "id": "number",
      "type": "report" | "result"
    }
  ]
}
```

#### Response

##### Response Status Code

- 200 OK

##### Response Body

Retorna un archivo en formato ZIP
