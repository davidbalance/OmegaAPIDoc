# Omega Sistema de Reporteria Medica

## Table of contents

1. [Introducción](#introduction)
   1. [Autenticación](#authentication)
2. [Endpoints](#endpoints)
   1. [Grupos Corporativos](#enpoint-corporative-groups)
   2. [Empresas](#endpoint-companies)
   3. [Sucursales](#endpoint-branch)
   4. [Puestos de trabajo](#endpoint-job-position)
   5. [Pacientes](#endpoint-patient)
   6. [Medicos](#endpoint-doctor)
   7. [Examenes](#endpoint-exams)
   8. [Tipo de examen](#endpoint-exam-types)
   9. [Ordenes médicas](#endpoint-medical-order)
   10. [Resultados médicos](#endpoint-medical-result)
   11. [Archivos](#endpoint-medical-files)
3. [Ciudades](#cities)

<div id='introduction'/>

## Introducción

La aplicación de Omega Sistema de Reportería Médica expone varios endpoints que pueden ser usados por sistemas externos. El presente documento tiene la finalidad de proveer información necesaria para la conexión de aplicaciones externas.

Los endpoints expuestos permiten el acceso, creación y modificación de información mediante los parámetros `source` y `key`, los cuales representan a la aplicación de origen desde donde se busca consumir el endpoint y un identificador único que la aplicación de origen provee para identificar sus datos.

<div id='authentication'/>

### Autenticación

Para el consumo del API se requiere una API-KEY. Esta llave será proporcionada por `Omega Sistema de Reportería Médica` y deberá ser usada antes de realizar cualquier petición a los endpoints. La llave deberá ser colocada en la cabecera de la petición con el nombre de `x-api-key`.

<div id='endpoints'/>

## Endpoints

Los endpoints presentes identifican un URL PARAM nombrado como `source`. Este representa a la aplicación de origen y deberá ser colocada en minúsculas y, si posee espacios, reemplazarlos usando guiones medios (-).

- Aplicación Ejemplo: _`<api>/aplicacion-ejemplo`_
- Aplicación: _`<api>/aplicacion`_

<div id='enpoint-corporative-groups'/>

### Grupos Corporativos

#### `POST` /external/connection/corporative/groups/_{source}_/_{key}_

Crea un grupo corporativo. Este grupo podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **name**: Nombre del grupo corporativo. Este es único.

```typescript
{
  name: string;
}
```

##### Response

```typescript
{
  id: number,
  name: string,
  companies: [
    {
      id: number,
      ruc: string,
      name: string,
      address: string,
      phone: string,
      branches: [
        {
          id: number,
          name: string,
          city: {
            id: number,
            name: string
          }
        }
      ]
    }
  ]
}
```

#### `PATCH` /external/connection/corporative/groups/_{source}_/_{key}_

Actualiza un grupo corporativo. Este grupo podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **name**: Nombre del grupo corporativo. Este es único.

```typescript
{
  name: string;
}
```

##### Response

```typescript
{
  id: number,
  name: string,
  companies: [
    {
      id: number,
      ruc: string,
      name: string,
      address: string,
      phone: string,
      branches: [
        {
          id: number,
          name: string,
          city: {
            id: number,
            name: string
          }
        }
      ]
    }
  ]
}
```

<div id='endpoint-companies'/>

### Empresas

#### `POST` /external/connection/company/_{source}_/_{key}_

Crea una empresa. Esta podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **corporativeGroup**:
  - **key**: Identificador único del grupo corporativo.
  - **name**: Nombre del grupo corporativo. Este es único.
- **ruc**: RUC de la empresa. Este debe ser único.
- **name**: Nombre de la empresa. Este es único.
- **address**: Dirección de la empresa.
- **phone**: Teléfono de la empresa.

```typescript
{
  corporativeGroup: {
    key: string,
    name: string
  },
  ruc: string,
  name: string,
  address: string,
  phone: string
}
```

##### Response

```typescript
{
  id: number,
  ruc: string,
  name: string,
  address: string,
  phone: string,
  branches: [
    {
      id: number,
      name: string,
      city: {
        id: number,
        name: string
      }
    }
  ]
}
```

#### `PATCH` /external/connection/company/_{source}_/_{key}_

Actualiza una empresa. Esta empresa podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **name**: Nombre de la empresa. Este es único.
- **address**: Dirección de la empresa.
- **phone**: Teléfono de la empresa.

```typescript
{
  name: string,
  address: string,
  phone: string
}
```

##### Response

```typescript
{
  id: number,
  ruc: string,
  name: string,
  address: string,
  phone: string,
  branches: [
    {
      id: number,
      name: string,
      city: {
        id: number,
        name: string
      }
    }
  ]
}
```

<div id='endpoint-branch'/>

### Sucursal

#### `POST` /external/connection/branch/_{source}_/_{key}_

Crea una sucursal. Esta podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **company**:
  - **key**: Identificador único.
  - **corporativeGroup**:
    - **key**: Identificador único.
    - **name**: Nombre del grupo corporativo. Este es único.
  - **ruc**: RUC de la empresa. Este debe ser único.
  - **name**: Nombre de la empresa. Este es único.
  - **address**: Dirección de la empresa.
  - **phone**: Teléfono de la empresa.
- **name**: Nombre de la sucursal.
- **city**: Ciudad. Esta puede ser una de las indicadas al final del documento.

```typescript
{
  company: {
    key: string,
    corporativeGroup: {
      key: string,
      name: string
    },
    ruc: string,
    name: string,
    address: string,
    phone: string
  },
  name: string,
  city: string
}
```

##### Response

```typescript
{
  id: number,
  name: string,
  city: {
    id: number,
    name: string
  }
}
```

#### `PATCH` /external/connection/branch/_{source}_/_{key}_

Actualiza una sucursal. Esta sucursal podrá ser utilizada para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **name**: Nombre de la sucursal. Este es único.

```typescript
{
  name: string;
}
```

##### Response

```typescript
{
  id: number,
  name: string,
  city: {
    id: number,
    name: string
  }
}
```

<div id='endpoint-job-position'/>

### Puestos de trabajo

#### `POST` /external/connection/job/position/_{source}_/_{key}_

Crea un puesto de trabajo. Esta podrá ser utilizada para la creación y gestión de puestos de trabajo.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **name**: Nombre del puesto de trabajo. Este es único.

```typescript
{
  name: string;
}
```

##### Response

```typescript
{
  id: number,
  name: string
}
```

#### `PATCH` /external/connection/job/position/_{source}_/_{key}_

Actualiza una posicion de trabajo.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **name**: Nombre de la posicion de trabajo. Este es único.

```typescript
{
  name: string;
}
```

##### Response

```typescript
{
  id: number,
  name: string
}
```

<div id='endpoint-patient'/>

### Pacientes

#### `POST` /external/connection/patients/_{source}_

Crea un paciente.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

##### Request Body

- **gender**: Género del paciente. Debe colocarse `male` o `female`.
- **birthday**: Fecha de cumpleaños del paciente. Formato: `YYYY-MM-DD`.
- **name**: Nombre del paciente.
- **lastname**: Apellido del paciente.
- **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
- **lastname**: Apellido del paciente.
- **role**: Role del paciente (Solo aplica para eeq).

```typescript
{
  email: string,
  jobPosition: {
    key: string,
    name: string
  },
  gender: male | female,
  birthday: Date,
  name: string,
  lastname: string,
  dni: string,
  role: string | undefined
}
```

##### Response

```typescript
{
  id: number,
  gender: "male" | "female",
  birthday: Date,
  user: number,
  dni: string,
  name: string,
  lastname: string
}
```

#### `PATCH` /external/connection/patients/_{source}_/_{dni}_

Actualiza un paciente.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `dni`: El DNI del paciente.
  - **Type**: _String_

##### Request Body

- **gender**: Género del paciente. Debe colocarse `male` o `female`.
- **birthday**: Fecha de cumpleaños del paciente. Formato: `YYYY-MM-DD`.
- **name**: Nombre del paciente.
- **lastname**: Apellido del paciente.

```typescript
{
  gender: "male" | "female",
  birthday: Date,
  name: string,
  lastname: string
}
```

##### Response

```typescript
{
  id: number,
  gender: "male" | "female",
  birthday: Date,
  user: number,
  dni: string,
  name: string,
  lastname: string
}
```

<div id='endpoint-doctor'/>

### Medicos

#### `POST` /external/connection/doctor

Crea un doctor.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### Request Body

- **name**: Nombre del médico.
- **lastname**: Apellido del médico.
- **email**: Correo electrónico del médico.
- **dni**: DNI del médico. Debe tener una longitud de 10 caracteres y ser único.

```typescript
{
  name: string,
  lastname: string,
  email: string,
  dni: string,
}
```

##### Response

```typescript
{
  id: number,
  dni: string,
  email: string,
  name: string,
  lastname: string,
  hasCredential: boolean,
  user: number,
  hasFile: boolean
}
```

#### `PATCH` /external/connection/doctor/_{dni}_

Actualiza un medico.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `dni`: El DNI del médico.
  - **Type**: _String_

##### Request Body

- **name**: Nombre del médico.
- **lastname**: Apellido del médico.

```typescript
{
  name: string,
  lastname: string,
}
```

##### Response

```typescript
{
  id: number,
  dni: string,
  email: string,
  name: string,
  lastname: string,
  hasCredential: boolean,
  user: number,
  hasFile: boolean
}
```

<div id='endpoint-exams'/>

### Examenes

#### `POST` /external/connection/exams/_{source}_/_{key}_

Crea un examen de laboratorio. Este podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

##### Request Body

- **name**: Nombre del examen médico. Este es único.
- **type**:
  - **key**: Identificador único del tipo de examen.
  - **name**: Nombre de un tipo de examen. Este es único.
- **subtype**:
  - **key**: Identificador único del subtipo de examen.
  - **name**: Nombre de un subtipo de examen médico. Este es único.

```typescript
{
  name: string,
  type: {
    key: string,
    name: string
  },
  subtype: {
    key: string,
    name: string,
  }
}
```

##### Response

```typescript
{
  id: number,
  name: string
}
```

#### `PATCH` /external/connection/exams/_{source}_/_{key}_

Actualiza un examen de laboratorio. Este podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único.
  - **Type**: _String_

##### Request Body

- **name**: Nombre actualizado del examen médico. Debe ser único.

```typescript
{
  name: string;
}
```

##### Response

```typescript
{
  id: number,
  name: string
}
```

<div id='endpoint-exam-types'/>

### Tipos de examenes

<div id='endpoint-medical-order'/>

### Ordenes médicas

#### `GET` /external/connection/medical/orders/dni/_{dni}_

Obtiene un arreglo de órdenes médicas pertenecientes a un paciente, utilizando su DNI.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `dni`: El DNI del paciente.
  - **Type**: _String_

##### Response

```typescript
{
  data: [
    {
      id: number,
      process: string,
      createAt: Date,
      mailStatus: boolean,
      orderStatus: string,
      client: {
        dni: string,
        name: string,
        lastname: string,
        managementId: number,
        areaId: number,
        email: [
          {
            id: number,
            email: string,
            default: boolean,
          },
        ],
      },
      results: [
        {
          id: number,
          examType: string,
          examSubtype: string,
          examName: string,
          hasFile: boolean,
          diseases: [
            {
              id: number,
              diseaseId: string,
              diseaseName: string,
              diseaseGroupId: string,
              diseaseGroupName: string,
              diseaseCommentary: string,
            },
          ],
          report: {
            id: number,
            content: string,
            hasFile: boolean,
          },
        },
      ],
    },
  ];
}
```

#### `GET` /external/connection/medical/orders/_{source}_/_{key}_

Obtiene una orden médica utilizando su identificador único y su pertenencia a la aplicación original.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único de la orden médica.
  - **Type**: _String_

##### Response

```typescript
{
  id: number,
  process: string,
  createAt: Date,
  mailStatus: boolean,
  orderStatus: string,
  client: {
    dni: string,
    name: string,
    lastname: string,
    managementId: number,
    areaId: number,
    email: [
      {
        id: number,
        email: string,
        default: boolean
      }
    ]
  },
  results: [
    {
      id: number,
      examType: string,
      examSubtype: string,
      examName: string,
      hasFile: boolean,
      diseases: [
        {
          id: number,
          diseaseId: string,
          diseaseName: string,
          diseaseGroupId: string,
          diseaseGroupName: string,
          diseaseCommentary: string
        }
      ],
      report: {
        id: number,
        content: string,
        hasFile: boolean
      }
    }
  ]
}
```

#### `GET` /external/connection/medical/orders/_{id}_

Obtiene una orden médica utilizando su identificador único.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `id`: Identificador unico de la orden medica.
  - **Type**: _Number_

##### Response

```typescript
{
  id: number,
  process: string,
  createAt: Date,
  mailStatus: boolean,
  orderStatus: string,
  client: {
    dni: string,
    name: string,
    lastname: string,
    managementId: number,
    areaId: number,
    email: [
      {
        id: number,
        email: string,
        default: boolean
      }
    ]
  },
  results: [
    {
      id: number,
      examType: string,
      examSubtype: string,
      examName: string,
      hasFile: boolean,
      diseases: [
        {
          id: number,
          diseaseId: string,
          diseaseName: string,
          diseaseGroupId: string,
          diseaseGroupName: string,
          diseaseCommentary: string
        }
      ],
      report: {
        id: number,
        content: string,
        hasFile: boolean
      }
    }
  ]
}
```

#### `POST` /external/connection/medical/orders/_{source}_/_{key}_

Crea una orden médica.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único de la orden médica.
  - **Type**: _String_

##### Request Body

- **branch**:
  - **company**:
    - **key**: Identificador único de la empresa.
    - **corporativeGroup**:
      - **key**: Identificador único del grupo corporativo.
      - **name**: Nombre del grupo corporativo. Debe ser único.
    - **ruc**: RUC de la empresa. Debe ser único.
    - **name**: Nombre de la empresa. Debe ser único.
    - **address**: Dirección de la empresa.
    - **phone**: Teléfono de la empresa.
  - **name**: Nombre de la sucursal.
  - **city**: Ciudad de la sucursal. Debe ser una de las ciudades especificadas al final del documento.
  - **key**: Identificador único de la sucursal.
- **jobPosition**:
  - **key**: Identificador único del puesto de trabajo.
  - **name**: Nombre del puesto de trabajo.
- **patient**:
  - **gender**: Género del paciente. Debe ser `male` o `female`.
  - **birthday**: Fecha de cumpleaños del paciente.
  - **name**: Nombre del paciente.
  - **lastname**: Apellido del paciente.
  - **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
  - **email**: Correo del paciente
  - **role**: Role del paciente (Solo aplica para eeq).
- **process**: Nombre del proceso médico.

```typescript
{
  branch: {
    company: {
      key: string,
      corporativeGroup: {
        key: string,
        name: string
      },
      ruc: string,
      name: string,
      address: string,
      phone: string
    },
    name: string,
    city: string,
    key: string
  },
  jobPosition: {
    key: string,
    name: string
  },
  patient: {
    gender: "male" | "female",
    birthday: Date,
    name: string,
    lastname: string,
    dni: string,
    email: string,
    role: string | undefined
  },
  process: string
}
```

#### `POST` /external/connection/medical/order/_{source}_/_{key}_/results

Crea una orden médica.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único de la orden médica.
  - **Type**: _String_

##### Request Body

- **results**: Arreglo de pruebas/examenes
  - **key**: Identificador unico para cada resultado
  - **exam**:
    - **key**: Identificador unico para cada examen
    - **name**: Nombre del examen
    - **type**: Dato opcional
      - **name**: Nombre del tipo de examen
      - **key**: Identificador unico del tipo de examen
  - **subtype**: Dato optional
    - **name**: Nombre del subtipo de examne
    - **key**: Identificador unico del subtipo de examen
  - **doctor**:
  - **name**: Nombre del medico acargo de la prueba
  - **lastname**: Apellido del medico acargo de la prueba
  - **email**: Correo electronico del medico
  - **dni**: DNI del medico acargo de la prueba
- **branch**:
  - **company**:
    - **key**: Identificador único de la empresa.
    - **corporativeGroup**:
      - **key**: Identificador único del grupo corporativo.
      - **name**: Nombre del grupo corporativo. Debe ser único.
    - **ruc**: RUC de la empresa. Debe ser único.
    - **name**: Nombre de la empresa. Debe ser único.
    - **address**: Dirección de la empresa.
    - **phone**: Teléfono de la empresa.
  - **name**: Nombre de la sucursal.
  - **city**: Ciudad de la sucursal. Debe ser una de las ciudades especificadas al final del documento.
  - **key**: Identificador único de la sucursal.
- **jobPosition**:
  - **key**: Identificador único del puesto de trabajo.
  - **name**: Nombre del puesto de trabajo.
- **patient**:
  - **gender**: Género del paciente. Debe ser `male` o `female`.
  - **birthday**: Fecha de cumpleaños del paciente.
  - **name**: Nombre del paciente.
  - **lastname**: Apellido del paciente.
  - **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
  - **email**: Correo del paciente
  - **role**: Role del paciente (Solo aplica para eeq).
- **process**: Nombre del proceso médico.

```typescript
{
  results: [
        {
            key: string | undefined,
            exam: {
                type: {
                    name: string,
                    key: string
                } | undefined,
                subtype: {
                    name: string,
                    key: string
                } | undefined,
                key: string,
                name: string
            },
            doctor: {
                name: string,
                lastname: string,
                email: string,
                dni: string
            }
        }
    ],
    branch: {
        key: string,
        company: {
            key: string,
            corporativeGroup: {
                key: string,
                name: string
            },
            ruc: string,
            name: string,
            address: string,
            phone: string
        },
        name: string,
        city: string
    },
    jobPosition?: {
        key: string,
        name: string
    }: undefined,
    patient: {
        name: string,
        dni: string,
        lastname: string,
        gender: 'male' | 'female',
        birthday: Date,
        email: string
    },
    process: string
}
```

##### Response

```typescript
{
  results: [
    {
      id: number,
      examType: string,
      examSubtype: string,
      examName: string,
      hasFile: boolean
    },
  ],
  id: number,
  process: string,
  createAt: Date,
  mailStatus: boolean,
  orderStatus: 'created' | 'validated'
}
```

#### `PATCH` /external/connection/medical/orders/_{source}_/_{key}_

Actualiza una orden médica.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del registro de la orden médica.
  - **Type**: _String_

##### Request Body

- **process**: Nombre actualizado del proceso médico.

```typescript
{
  process: string;
}
```

##### Response

```typescript
{
  id: number,
  process: string,
  createAt: Date,
  mailStatus: boolean,
  orderStatus: string,
  client: {
    dni: string,
    name: string,
    lastname: string,
    managementId: number,
    areaId: number,
    email: [
      {
        id: number,
        email: string,
        default: boolean
      }
    ]
  },
  results: [
    {
      id: number,
      examType: string,
      examSubtype: string,
      examName: string,
      hasFile: boolean,
      diseases: [
        {
          id: number,
          diseaseId: string,
          diseaseName: string,
          diseaseGroupId: string,
          diseaseGroupName: string,
          diseaseCommentary: string
        }
      ],
      report: {
        id: number,
        content: string,
        hasFile: boolean
      }
    }
  ]
}
```

<div id='endpoint-medical-result'/>

### Resultados médicos

#### `GET` /external/connection/medical/result/_{source}_/_{key}_

Obtiene un resultado médico utilizando su identificador único y su pertenencia a la aplicación original.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del resultado médico.
  - **Type**: _String_

##### Response

```typescript
{
  id: number,
  examType: string,
  examSubtype: string,
  examName: string,
  hasFile: boolean,
  diseases: [
    {
      id: number,
      diseaseId: string,
      diseaseName: string,
      diseaseGroupId: string,
      diseaseGroupName: string,
      diseaseCommentary: string
    }
  ],
  report: {
    id: number,
    content: string,
    hasFile: boolean
  }
}
```

#### `POST` /external/connection/medical/result/_{source}_/_{key}_

Crea un resultado médico utilizando la aplicación de origen especificada.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

##### Request Body

El cuerpo de la peticion es un formulario con los siguientes campos:

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | false     |
| exam    | object          | true      |
| doctor  | object          | true      |
| order   | object          | true      |

Acontinuacion se describe cada campo:

- **file**: Archivo en formato PDF (Opcional).
- **exam**:
  - **type**:
    - **key**: Identificador único del tipo de examen.
    - **name**: Nombre de un tipo de examen. Este es único.
  - **subtype**: (Opcional)
    - **key**: Identificador único del subtipo de examen.
    - **name**: Nombre de un subtipo de examen médico. Este es único.
  - **key**: Identificador único del examen.
  - **name**: Nombre del examen médico. Este es único.
- **doctor**:
  - **name**: Nombre del médico.
  - **lastname**: Apellido del médico.
  - **email**: Correo electrónico del médico.
  - **dni**: DNI del médico. Debe tener una longitud de 10 caracteres y ser único.
  - **role**: Role del médico (Solo aplica para eeq).
- **order**:
  - **key**: Identificador único de la orden medica.
  - **branch**:
    - **company**:
      - **key**: Identificador único de la empresa.
      - **corporativeGroup**:
        - **key**: Identificador único del grupo corporativo.
        - **name**: Nombre del grupo corporativo.
      - **ruc**: RUC de la empresa. Debe ser único.
      - **name**: Nombre de la empresa.
      - **address**: Dirección de la empresa.
      - **phone**: Teléfono de la empresa.
    - **name**: Nombre de la sucursal.
    - **city**: Ciudad donde se encuentra la sucursal.
    - **key**: Identificador único de la sucursal.
  - **jobPosition**:
    - **key**: Identificador único del puesto de trabajo.
    - **name**: Nombre del puesto de trabajo. Este es único.
  - **patient**:
    - **gender**: Género del paciente. Debe ser `male` o `female`.
    - **birthday**: Fecha de cumpleaños del paciente.
    - **name**: Nombre del paciente.
    - **lastname**: Apellido del paciente.
    - **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
    - **email**: Correo del paciente.
    - **role**: Role del paciente (Solo aplica para eeq).
  - **process**: Nombre del proceso médico.

**Exam (object)**

```typescript
{
  type: {
    key: string,
    name: string
  },
  subtype: {
    key: string,
    name: string
  } | undefined,
  key: string,
  name: string
}
```

**Doctor (object)**

```typescript
{
  name: string,
  lastname: string,
  email: string,
  dni: string,
  role: string | undefined
}
```

**Order (object)**

```typescript
{
  key: string,
  branch: {
    company: {
      key: string,
      corporativeGroup: {
        key: string,
        name: string
      },
      ruc: string,
      name: string,
      address: string,
      phone: string
    },
    name: string,
    city: string,
    key: string
  },
  jobPosition: {
    key: string,
    name: string
  },
  patient: {
    gender: "male" | "female",
    birthday: Date,
    name: string,
    lastname: string,
    dni: string,
    role: string | undefined
  },
  process: string
}
```

##### Response

```typescript
{
  id: number,
  examType: string,
  examSubtype: string,
  examName: string,
  hasFile: boolean,
  diseases: [
    {
      id: number,
      diseaseId: string,
      diseaseName: string,
      diseaseGroupId: string,
      diseaseGroupName: string,
      diseaseCommentary: string
    }
  ],
  report: {
    id: number,
    content: string,
    hasFile: boolean
  } | undefined
}
```

#### `POST` /external/connection/medical/result/_{source}_/_{key}_/base64/file

Permite enviar un archivo en base64 junto con su mimetype.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del resultado médico.
  - **Type**: _String_

##### Request Body

- **mimetype**: Tipo de dato archivo que va a ser compartido.
- **base64**: Archivo en base64.

```typescript
{
  mimetype: string;
  base64: string;
}
```

##### Response

```typescript
{
  id: number,
  examType: string,
  examSubtype: string,
  examName: string,
  hasFile: boolean,
  diseases: [
    {
      id: number,
      diseaseId: string,
      diseaseName: string,
      diseaseGroupId: string,
      diseaseGroupName: string,
      diseaseCommentary: string
    }
  ],
  report: {
    id: number,
    content: string,
    hasFile: boolean
  }
}
```

#### `POST` /external/connection/medical/result/_{source}_/_{key}_/file

Permite subir un archivo PDF y asociarlo a un resultado médico.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del resultado médico.
  - **Type**: _String_

##### Request Body

- **file**: Archivo PDF que se desea subir para adjuntarlo al resultado médico.

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | true      |

##### Response

```typescript
{
  id: number,
  examType: string,
  examSubtype: string,
  examName: string,
  hasFile: boolean,
  diseases: [
    {
      id: number,
      diseaseId: string,
      diseaseName: string,
      diseaseGroupId: string,
      diseaseGroupName: string,
      diseaseCommentary: string
    }
  ],
  report: {
    id: number,
    content: string,
    hasFile: boolean
  }
}
```

#### `PATCH` /external/connection/medical/result/_{source}_/_{key}_/file

Permite subir un archivo PDF y asociarlo a un resultado médico.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del resultado médico.
  - **Type**: _String_

##### Request Body

- **file**: Archivo PDF que se desea subir para adjuntarlo al resultado médico.

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | true      |

##### Response

```typescript
{
  id: number,
  examType: string,
  examSubtype: string,
  examName: string,
  hasFile: boolean,
  diseases: [
    {
      id: number,
      diseaseId: string,
      diseaseName: string,
      diseaseGroupId: string,
      diseaseGroupName: string,
      diseaseCommentary: string
    }
  ],
  report: {
    id: number,
    content: string,
    hasFile: boolean
  }
}
```

#### `PATCH` /external/connection/medical/result/_{id}_/file

Permite subir un archivo PDF y asociarlo a un resultado médico.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

##### URL Parameters

- `id`: Identificador unico proporcionado por el sistema
  - **Type**: _Number_

##### Request Body

- **file**: Archivo PDF que se desea subir para adjuntarlo al resultado médico.

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | true      |

##### Response

```typescript
{
  id: number,
  examType: string,
  examSubtype: string,
  examName: string,
  hasFile: boolean,
  diseases: [
    {
      id: number,
      diseaseId: string,
      diseaseName: string,
      diseaseGroupId: string,
      diseaseGroupName: string,
      diseaseCommentary: string
    }
  ],
  report: {
    id: number,
    content: string,
    hasFile: boolean
  }
}
```

<div id='endpoint-medical-files'/>

### Archivos

#### `POST` /medical/file

Obtiene un archivo médico específico basado en el identificador único proporcionado por Omega Sistema de Reporteria Medica.

##### Request Headers

- `Content-Type`: `application/json`

##### Request Body

- **id**: Identificador único de Omega Sistema de Reporteria Medica para el resultado o reporte.
- **type**: Tipo del archivo requerido. Debe ser `result` o `report`.

```typescript
{
  id: number,
  type: "report" | "result"
}
```

##### Response

Retorna un archivo en formato PDF

#### `POST` /medical/file/multiple

Obtiene varios archivos médicos específicos basados en los identificadores únicos proporcionados por Omega Sistema de Reporteria Medica.

##### Request Headers

- `Content-Type`: `application/json`

##### Request Body

- **files**: Lista de objetos que especifican los archivos médicos requeridos.
  - **id**: Identificador único de Omega Sistema de Reporteria Medica para el resultado o reporte.
  - **type**: Tipo del archivo requerido. Debe ser `result` o `report`.

```typescript
{
  files: [
    {
      id: number,
      type: "report" | "result",
    },
  ];
}
```

##### Response

Retorna un archivo en formato ZIP

<div id='cities' />

## Ciudades

|                             |                              |                     |                 |               |                             |             |             |                   |              |
| --------------------------- | ---------------------------- | ------------------- | --------------- | ------------- | --------------------------- | ----------- | ----------- | ----------------- | ------------ |
| Ambato                      | Arajuno                      | Archidona           | Atacames        | Atuntaqui     | Azogues                     | Babahoyo    | Baeza       | Bahía de Caráquez | Balao        |
| Balsas                      | Balzar                       | Baños de Agua Santa | Bucay           | Calceta       | Carlos Julio Arosemena Tola | Catarama    | Chone       | Coca              | Colimes      |
| Coronel Marcelino Maridueña | Cotacachi                    | Cuenca              | Daule           | Durán         | El Chaco                    | El Empalme  | El Guabo    | El Triunfo        | Esmeraldas   |
| Gualaquiza                  | Guaranda                     | Guayaquil           | Huaquillas      | Ibarra        | Isidro Ayora                | Jama        | Jujan       | La Concordia      | La Libertad  |
| Lago Agrio                  | Latacunga                    | Limones             | Logroño         | Loja          | Lomas de Sargentillo        | Macas       | Machala     | Manta             | Mera         |
| Milagro                     | Montecristi                  | Muisne              | Naranjal        | Nobol         | Nuevo Rocafuerte            | Otavalo     | Paján       | Palestina         | Palora       |
| Pasaje                      | Pedernales                   | Pedro Carbo         | Pichincha       | Pimampiro     | Piñas                       | Playas      | Portovelo   | Portoviejo        | Puerto Ayora |
| Puerto Baquerizo Moreno     | Puerto El Carmen de Putumayo | Puerto López        | Puerto Villamil | Puyo          | Quevedo                     | Quinindé    | Quito       | Riobamba          | Rioverde     |
| Rocafuerte                  | San Lorenzo                  | San Vicente         | Santa Rosa      | Santo Domingo | Salinas                     | Samborondón | Santa Elena | Simón Bolívar     | Sucre        |
| Sucúa                       | Tarapoa                      | Tena                | Tosagua         | Tulcán        | Urcuquí                     | Valencia    | Ventanas    | Vinces            | Yaguachi     |
| Yantzaza                    | Zamora                       | Zaruma              |
