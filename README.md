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
   8. [Ordenes médicas](#endpoint-medical-order)
   9. [Resultados médicos](#endpoint-medical-result)
   10. [Archivos](#endpoint-medical-files)
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

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre del grupo corporativo. Este es único.

```typescript
{
  name: string;
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/corporative/groups/${source}/${key}`, {
  method: "POST",
  body: {
    name: "LA FAVORITA",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

```typescript
{
  id: number,
  name: string
}
```

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre del grupo corporativo. Este es único.

```typescript
{
  name: string;
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/corporative/groups/${source}/${key}`, {
  method: "PATCH",
  body: {
    name: "LA FAVORITA",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

<div id='endpoint-companies'/>

### Empresas

---

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

<details>
  <summary><b>Request</b></summary></br>

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

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/company/${source}/${key}`, {
  method: "POST",
  body: {
    corporativeGroup: {
      key: "0000001",
      name: "LA FAVORITA",
    },
    ruc: "1234567890001",
    name: "SUPERMAXI",
    address: "Av.Amazonas" // Direccion de la matriz
    phone: "0999999999",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

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

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/company/${source}/${key}`, {
  method: "PATCH",
  body: {
    name: "SUPERMAXI",
    address: "Av.Inca y los alamos",
    phone: "0999999999",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

<div id='endpoint-branch'/>

### Sucursal

---

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

<details>
  <summary><b>Request</b></summary></br>

- **company**:
  - **key**: Identificador único. Este dato es opcional
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
    key: string | undefined,
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

  <details>
    <summary><b>Ejemplo: <i>Todos los datos</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/branch/${source}/${key}`, {
  method: "POST",
  body: {
  company: {
    key: 'comany-000001',
    corporativeGroup: {
      key: 'group-000001',
      name: 'LA FAVORITA'
    },
    ruc: '1234567890001',
    name: 'SUPERMAXI',
    address: 'Av.Amazonas',
    phone: '0999999999'
  },
  name: 'Sucursal de la Amazonas',
  city: 'Quito'
}
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    "accept": "application/json",
  },
});
```

  </details>

  <details>
    <summary><b>Ejemplo: <i>Empresa sin key</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/branch/${source}/${key}`, {
  method: "POST",
  body: {
  company: {
    corporativeGroup: {
      key: 'group-000001',
      name: 'LA FAVORITA'
    },
    ruc: '1234567890001',
    name: 'SUPERMAXI',
    address: 'Av.Amazonas',
    phone: '0999999999'
  },
  name: 'Sucursal de la Amazonas',
  city: 'Quito'
}
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    "accept": "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre de la sucursal. Este es único.

```typescript
{
  name: string;
}
```

  <details>
    <summary><b>Ejemplos</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/branch/${source}/${key}`, {
  method: "PATCH",
  body: {
  name: 'Sucursal del Inca',
}
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    "accept": "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

<div id='endpoint-job-position'/>

### Puestos de trabajo

---

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

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre del puesto de trabajo. Este es único.

```typescript
{
  name: string;
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/job/position/${source}/${key}`, {
  method: "POST",
  body: {
    name: 'Abogado',
  }
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    "accept": "application/json",
  },
});

```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

```typescript
{
  id: number,
  name: string
}
```

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre de la posicion de trabajo. Este es único.

```typescript
{
  name: string;
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/job/position/${source}/${key}`, {
  method: "PATCH",
  body: {
    name: 'Administrador',
  }
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    "accept": "application/json",
  },
});

```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

```typescript
{
  id: number,
  name: string
}
```

</details>

<div id='endpoint-patient'/>

### Pacientes

---

#### `POST` /external/connection/patients/_{source}_

Crea un paciente.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

<details>
  <summary><b>Request</b></summary></br>

- **email**: Correo electronico del paciente.
- **jobPosition**: Dato opcional.
  - **key**: Llave con la que identificara la posicion del trabajo en su aplicacion.
  - **name**: Nombre de la posicion de trabajo.
- **gender**: Género del paciente. Debe colocarse `male` o `female`.
- **birthday**: Fecha de cumpleaños del paciente. Formato: `YYYY-MM-DD`.
- **name**: Nombre del paciente.
- **lastname**: Apellido del paciente.
- **dni**: DNI del paciente. Debe tener una longitud de 10 caracteres y ser único.
- **role**: Role del paciente (Solo aplica para eeq).

```typescript
{
  email: string,
  jobPosition: {
    key: string,
    name: string
  } | undefined,
  gender: male | female,
  birthday: Date,
  name: string,
  lastname: string,
  dni: string,
  role: string | undefined
}
```

  <details>
    <summary><b>Ejemplo: <i>Todos los datos</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/patients/${source}`, {
  method: "POST",
  body: {
    email: "test@email.com",
    jobPosition: {
      key: "00001",
      name: "Abogado",
    },
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "Juan Pablo",
    lastname: "Astudillo Barba",
    dni: "1234567890",
    role: "my-sample-roles",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

  <details>
    <summary><b>Ejemplo: <i>Sin rol</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/patients/${source}`, {
  method: "POST",
  body: {
    email: "test@email.com",
    jobPosition: {
      key: "00001",
      name: "Abogado",
    },
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "Juan Pablo",
    lastname: "Astudillo Barba",
    dni: "1234567890",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

  <details>
    <summary><b>Ejemplo: <i>Sin posicion de trabajo</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/patients/${source}`, {
  method: "POST",
  body: {
    email: "test@email.com",
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "Juan Pablo",
    lastname: "Astudillo Barba",
    dni: "1234567890",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

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

  <details>
    <summary><b>Ejemplos</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const dni = "1234567890";

fetch(`${baseUrl}/external/connection/patients/${source}/${dni}`, {
  method: "PATCH",
  body: {
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "Juan Pablo",
    lastname: "Astudillo Barba",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

<div id='endpoint-doctor'/>

### Medicos

---

#### `POST` /external/connection/doctor

Crea un doctor.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

<details>
  <summary><b>Request</b></summary></br>

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

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";

fetch(`${baseUrl}/external/connection/doctor`, {
  method: "POST",
  body: {
    name: "JUAN PEREZ",
    lastname: "ASTUDILLO BARBA",
    email: "test@email.com",
    dni: "1234567890",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

#### `PATCH` /external/connection/doctor/_{dni}_

Actualiza un medico.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `dni`: El DNI del médico.
  - **Type**: _String_

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre del médico.
- **lastname**: Apellido del médico.

```typescript
{
  name: string,
  lastname: string,
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const dni = "1234567890";

fetch(`${baseUrl}/external/connection/doctor/${dni}`, {
  method: "PATCH",
  body: {
    name: "JUAN PEREZ",
    lastname: "ASTUDILLO BARBA",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

<div id='endpoint-exams'/>

### Examenes

---

#### `POST` /external/connection/exams/_{source}_/_{key}_

Crea un examen de laboratorio. Este podrá ser utilizado para la creación y gestión de pacientes y órdenes médicas.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre del examen médico. Este es único.
- **type**: Datos Opcionales
  - **key**: Identificador único del tipo de examen.
  - **name**: Nombre de un tipo de examen. Este es único.
- **subtype**: Datos Opcionales
  - **key**: Identificador único del subtipo de examen.
  - **name**: Nombre de un subtipo de examen médico. Este es único.

```typescript
{
  name: string,
  type: {
    key: string,
    name: string
  } | undefined,
  subtype: {
    key: string,
    name: string,
  } | undefined
}
```

  <details>
    <summary><b>Ejemplo: <i>Peticion Base</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/exams/${source}/${key}`, {
  method: "POST",
  body: {
    name: "COLESTEROL",
    type: {
      key: "TYPE-0001",
      name: "LABORATORIO CLINICO",
    },
    subtype: {
      key: "SUBTYPE-0001",
      name: "LABORATORIO CLINICO",
    },
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

  <details>
    <summary><b>Ejemplo: <i>Sin tipo de examen</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/exams/${source}/${key}`, {
  method: "POST",
  body: {
    name: "COLESTEROL",
    subtype: {
      key: "SUBTYPE-0001",
      name: "LABORATORIO CLINICO",
    },
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

  <details>
    <summary><b>Ejemplo: <i>Sin subtipo de examen</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/exams/${source}/${key}`, {
  method: "POST",
  body: {
    name: "COLESTEROL",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

```typescript
{
  id: number,
  name: string
}
```

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

- **name**: Nombre actualizado del examen médico. Debe ser único.

```typescript
{
  name: string;
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/exams/${source}/${key}`, {
  method: "PATCH",
  body: {
    name: 'COLESTEROL';
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

```typescript
{
  id: number,
  name: string
}
```

</details>

<div id='endpoint-medical-order'/>

### Ordenes médicas

---

#### `GET` /external/connection/medical/orders/dni/_{dni}_

Obtiene un arreglo de órdenes médicas pertenecientes a un paciente, utilizando su DNI.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `dni`: El DNI del paciente.
  - **Type**: _String_

<details>
  <summary><b>Request</b></summary></br>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const dni = "1234567890";

fetch(`${baseUrl}/external/connection/medical/orders/${dni}`, {
  method: "GET",
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/orders/${source}/${key}`, {
  method: "GET",
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

#### `GET` /external/connection/medical/orders/_{id}_

Obtiene una orden médica utilizando su identificador único.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `id`: Identificador unico de la orden medica.
  - **Type**: _Number_

<details>
  <summary><b>Request</b></summary></br>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const id = "01"; // IDENTIFICADOR QUE LA APLICACION ENTREGA CUANDO CREA UNA ORDEN MEDICA

fetch(`${baseUrl}/external/connection/medical/orders/${id}`, {
  method: "GET",
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

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

  <details>
    <summary><b>Ejemplo: <i>Peticion Base</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/orders/${source}/${key}`, {
  method: "POST",
  body: {
    branch: {
      company: {
        key: "COMPANY-0001",
        corporativeGroup: {
          key: "CORPORATIVE-0001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Sucursal de la Amazonas",
      city: "Quito",
      key: "BRANCH-0001",
    },
    jobPosition: {
      key: "JOBPOSITION-0001",
      name: "Abogado",
    },
    patient: {
      gender: "male",
      birthday: new Date("2000-01-01"),
      name: "JUAN GABRIEL",
      lastname: "ASTUDILLO BARBA",
      dni: "1234567890",
      email: "test@email.com",
      role: "my-sample-role",
    },
    process: "Post Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Sin posicion de trabajo</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/orders/${source}/${key}`, {
  method: "POST",
  body: {
    branch: {
      company: {
        key: "COMPANY-0001",
        corporativeGroup: {
          key: "CORPORATIVE-0001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Sucursal de la Amazonas",
      city: "Quito",
      key: "BRANCH-0001",
    },
    patient: {
      gender: "male",
      birthday: new Date("2000-01-01"),
      name: "JUAN GABRIEL",
      lastname: "ASTUDILLO BARBA",
      dni: "1234567890",
      email: "test@email.com",
      role: "my-sample-role",
    },
    process: "Post Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Empresa sin key</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/orders/${source}/${key}`, {
  method: "POST",
  body: {
    branch: {
      company: {
        corporativeGroup: {
          key: "CORPORATIVE-0001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Sucursal de la Amazonas",
      city: "Quito",
      key: "BRANCH-0001",
    },
    patient: {
      gender: "male",
      birthday: new Date("2000-01-01"),
      name: "JUAN GABRIEL",
      lastname: "ASTUDILLO BARBA",
      dni: "1234567890",
      email: "test@email.com",
      role: "my-sample-role",
    },
    process: "Post Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

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
            key: string | undefined,
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
    jobPosition: {
        key: string,
        name: string
    } | undefined,
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

  <details>
    <summary><b>Ejemplo: <i>Peticion Base</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/order/${source}/${key}`, {
  method: "POST",
  body: {
    results: [
      {
        key: "prueba-000001",
        exam: {
          type: {
            name: "LABORATORIO CLINICO",
            key: "exam-type-00001",
          },
          subtype: {
            name: "ELECTROCARDIOGRAMA",
            key: "exam-subtype-00001",
          },
          key: "exam-000001",
          name: "COLESTEROL",
        },
        doctor: {
          name: "LUIS JAVIER",
          lastname: "PEREZ ASTUDILLO",
          email: "test@email.com",
          dni: "1234567890",
        },
      },
    ],
    branch: {
      key: "branch-00001",
      company: {
        key: "company-00001",
        corporativeGroup: {
          key: "corporative-00001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Av.Amazonas",
      city: "Quito",
    },
    jobPosition: {
      key: "jobposition-0001",
      name: "ABOGADO",
    },
    patient: {
      name: "XIMENA ALEJANDRA",
      lastname: "GARCIA FEIJOO",
      dni: "1234567890",
      gender: "female",
      birthday: new Date("2000-01-01"),
      email: "test@email.com",
    },
    process: "Post. Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Pruebas/Resultados sin key</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/order/${source}/${key}`, {
  method: "POST",
  body: {
    results: [
      {
        exam: {
          type: {
            name: "LABORATORIO CLINICO",
            key: "exam-type-00001",
          },
          subtype: {
            name: "ELECTROCARDIOGRAMA",
            key: "exam-subtype-00001",
          },
          key: "exam-000001",
          name: "COLESTEROL",
        },
        doctor: {
          name: "LUIS JAVIER",
          lastname: "PEREZ ASTUDILLO",
          email: "test@email.com",
          dni: "1234567890",
        },
      },
    ],
    branch: {
      key: "branch-00001",
      company: {
        key: "company-00001",
        corporativeGroup: {
          key: "corporative-00001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Av.Amazonas",
      city: "Quito",
    },
    jobPosition: {
      key: "jobposition-0001",
      name: "ABOGADO",
    },
    patient: {
      name: "XIMENA ALEJANDRA",
      lastname: "GARCIA FEIJOO",
      dni: "1234567890",
      gender: "female",
      birthday: new Date("2000-01-01"),
      email: "test@email.com",
    },
    process: "Post. Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Sin tipo de examen</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/order/${source}/${key}`, {
  method: "POST",
  body: {
    results: [
      {
        exam: {
          subtype: {
            name: "ELECTROCARDIOGRAMA",
            key: "exam-subtype-00001",
          },
          key: "exam-000001",
          name: "COLESTEROL",
        },
        doctor: {
          name: "LUIS JAVIER",
          lastname: "PEREZ ASTUDILLO",
          email: "test@email.com",
          dni: "1234567890",
        },
      },
    ],
    branch: {
      key: "branch-00001",
      company: {
        key: "company-00001",
        corporativeGroup: {
          key: "corporative-00001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Av.Amazonas",
      city: "Quito",
    },
    jobPosition: {
      key: "jobposition-0001",
      name: "ABOGADO",
    },
    patient: {
      name: "XIMENA ALEJANDRA",
      lastname: "GARCIA FEIJOO",
      dni: "1234567890",
      gender: "female",
      birthday: new Date("2000-01-01"),
      email: "test@email.com",
    },
    process: "Post. Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Sin subtipo de examen</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/order/${source}/${key}`, {
  method: "POST",
  body: {
    results: [
      {
        exam: {
          key: "exam-000001",
          name: "COLESTEROL",
        },
        doctor: {
          name: "LUIS JAVIER",
          lastname: "PEREZ ASTUDILLO",
          email: "test@email.com",
          dni: "1234567890",
        },
      },
    ],
    branch: {
      key: "branch-00001",
      company: {
        key: "company-00001",
        corporativeGroup: {
          key: "corporative-00001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Av.Amazonas",
      city: "Quito",
    },
    jobPosition: {
      key: "jobposition-0001",
      name: "ABOGADO",
    },
    patient: {
      name: "XIMENA ALEJANDRA",
      lastname: "GARCIA FEIJOO",
      dni: "1234567890",
      gender: "female",
      birthday: new Date("2000-01-01"),
      email: "test@email.com",
    },
    process: "Post. Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Sin posicion de trabajo</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/order/${source}/${key}`, {
  method: "POST",
  body: {
    results: [
      {
        exam: {
          key: "exam-000001",
          name: "COLESTEROL",
        },
        doctor: {
          name: "LUIS JAVIER",
          lastname: "PEREZ ASTUDILLO",
          email: "test@email.com",
          dni: "1234567890",
        },
      },
    ],
    branch: {
      key: "branch-00001",
      company: {
        key: "company-00001",
        corporativeGroup: {
          key: "corporative-00001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Av.Amazonas",
      city: "Quito",
    },
    patient: {
      name: "XIMENA ALEJANDRA",
      lastname: "GARCIA FEIJOO",
      dni: "1234567890",
      gender: "female",
      birthday: new Date("2000-01-01"),
      email: "test@email.com",
    },
    process: "Post. Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Empresa sin key</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/order/${source}/${key}`, {
  method: "POST",
  body: {
    results: [
      {
        exam: {
          key: "exam-000001",
          name: "COLESTEROL",
        },
        doctor: {
          name: "LUIS JAVIER",
          lastname: "PEREZ ASTUDILLO",
          email: "test@email.com",
          dni: "1234567890",
        },
      },
    ],
    branch: {
      key: "branch-00001",
      company: {
        corporativeGroup: {
          key: "corporative-00001",
          name: "LA FAVORITA",
        },
        ruc: "1234567890001",
        name: "SUPERMAXI",
        address: "Av.Amazonas",
        phone: "0999999999",
      },
      name: "Av.Amazonas",
      city: "Quito",
    },
    patient: {
      name: "XIMENA ALEJANDRA",
      lastname: "GARCIA FEIJOO",
      dni: "1234567890",
      gender: "female",
      birthday: new Date("2000-01-01"),
      email: "test@email.com",
    },
    process: "Post. Ocupacional",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

#### `POST` /external/connection/medical/order/_{source}_/_{key}_/results/laboratorio/clinico/base64

Permite enviar un archivo en base64 junto con su mimetype.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único de la orden médica.
  - **Type**: _String_

<details>
  <summary><b>Request</b></summary></br>

- **doctor**: Medico que creo la orden medica
  - **name**: Nombre del medico
  - **lastname**: Apellido del medico
  - **email**: Correo electronico del medico
  - **dni**: DNI del medico
- **mimetype**: Tipo de dato del archivo a enviar
- **base64**: Archivo en base64

```typescript
{
  doctor: {
    name: string,
    lastname: string,
    email: string,
    dni: string
  },
  mimetype: string,
  base64: string
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE DE LA ORDEN MEDICA CON LA QUE IDENTIFICAN SUS DATOS EN LA APLICACION

fetch(
  `${baseUrl}/external/connection/medical/order/${source}/${key}/laboratorio/clinico/base64`,
  {
    method: "POST",
    body: {
      doctor: {
        name: "JUAN LEONARDO",
        lastname: "PEREZ ALBUJA",
        email: "test@email.com",
        dni: "1234567890",
      },
      mimetype: "application/pdf",
      base64: "my-base64-file",
    },
    headers: {
      "x-api-key": "my-sample-api-key",
      "content-type": "application/json",
      accept: "application/json",
    },
  }
);
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

```typescript
{
  id: number,
  results: [
    {
      id: number,
      examType: string,
      examSubtype:  string,
      examName: string,
      hasFile: boolean
    }
  ],
  process: string,
  createAt: Date,
  orderStatus: "created" | "validated"
}
```

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

- **process**: Nombre actualizado del proceso médico.

```typescript
{
  process: string;
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/order/${source}/${key}`, {
  method: "PATCH",
  body: {
    process: "Post Ocupacional";
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

<div id='endpoint-medical-result'/>

### Resultados médicos

---

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

<details>
  <summary><b>Request</b></summary></br>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}`, {
  method: "GET",
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
    accept: "application/json",
  },
});
```

</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

#### `POST` /external/connection/medical/result/_{source}_/_{key}_

Crea un resultado médico utilizando la aplicación de origen especificada.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_

<details>
  <summary><b>Request</b></summary></br>

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

  <details>
    <summary><b>Ejemplo: <i>Peticion Base</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const order = {
  key: "order-00001",
  branch: {
    company: {
      key: "COMPANY-0001",
      corporativeGroup: {
        key: "CORPORATIVE-0001",
        name: "LA FAVORITA",
      },
      ruc: "1234567890001",
      name: "SUPERMAXI",
      address: "Av.Amazonas",
      phone: "0999999999",
    },
    name: "Sucursal de la Amazonas",
    city: "Quito",
    key: "BRANCH-0001",
  },
  jobPosition: {
    key: "JOBPOSITION-0001",
    name: "Abogado",
  },
  patient: {
    email: "patient@email.com",
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "JUAN GABRIEL",
    lastname: "ASTUDILLO BARBA",
    dni: "1234567890",
    role: "my-sample-role",
  },
  process: "Post Ocupacional",
};

const doctor = {
  name: "EDUARDO XAVIER",
  lastname: "JIMENEZ EDMUNDO",
  email: "doctor@email.com",
  dni: "1234567891",
};

const exam = {
  type: {
    key: "EXAMTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  subtype: {
    key: "EXAMSUBTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  key: "EXAM-0001",
  name: "COLESTEROL",
};

const form = new FormData();
form.append("file", file);
form.append("order", order);
form.append("doctor", doctor);
form.append("exam", exam);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}`, {
  method: "POST",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Empresa sin key</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const order = {
  key: "order-00001",
  branch: {
    company: {
      corporativeGroup: {
        key: "CORPORATIVE-0001",
        name: "LA FAVORITA",
      },
      ruc: "1234567890001",
      name: "SUPERMAXI",
      address: "Av.Amazonas",
      phone: "0999999999",
    },
    name: "Sucursal de la Amazonas",
    city: "Quito",
    key: "BRANCH-0001",
  },
  jobPosition: {
    key: "JOBPOSITION-0001",
    name: "Abogado",
  },
  patient: {
    email: "patient@email.com",
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "JUAN GABRIEL",
    lastname: "ASTUDILLO BARBA",
    dni: "1234567890",
    role: "my-sample-role",
  },
  process: "Post Ocupacional",
};

const doctor = {
  name: "EDUARDO XAVIER",
  lastname: "JIMENEZ EDMUNDO",
  email: "doctor@email.com",
  dni: "1234567891",
};

const exam = {
  type: {
    key: "EXAMTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  subtype: {
    key: "EXAMSUBTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  key: "EXAM-0001",
  name: "COLESTEROL",
};

const form = new FormData();
form.append("file", file);
form.append("order", order);
form.append("doctor", doctor);
form.append("exam", exam);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}`, {
  method: "POST",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Sin posicion de trabajo</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const order = {
  key: "order-00001",
  branch: {
    company: {
      corporativeGroup: {
        key: "CORPORATIVE-0001",
        name: "LA FAVORITA",
      },
      ruc: "1234567890001",
      name: "SUPERMAXI",
      address: "Av.Amazonas",
      phone: "0999999999",
    },
    name: "Sucursal de la Amazonas",
    city: "Quito",
    key: "BRANCH-0001",
  },
  patient: {
    email: "patient@email.com",
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "JUAN GABRIEL",
    lastname: "ASTUDILLO BARBA",
    dni: "1234567890",
    role: "my-sample-role",
  },
  process: "Post Ocupacional",
};

const doctor = {
  name: "EDUARDO XAVIER",
  lastname: "JIMENEZ EDMUNDO",
  email: "doctor@email.com",
  dni: "1234567891",
};

const exam = {
  type: {
    key: "EXAMTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  subtype: {
    key: "EXAMSUBTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  key: "EXAM-0001",
  name: "COLESTEROL",
};

const form = new FormData();
form.append("file", file);
form.append("order", order);
form.append("doctor", doctor);
form.append("exam", exam);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}`, {
  method: "POST",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Paciente sin rol</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const order = {
  key: "order-00001",
  branch: {
    company: {
      corporativeGroup: {
        key: "CORPORATIVE-0001",
        name: "LA FAVORITA",
      },
      ruc: "1234567890001",
      name: "SUPERMAXI",
      address: "Av.Amazonas",
      phone: "0999999999",
    },
    name: "Sucursal de la Amazonas",
    city: "Quito",
    key: "BRANCH-0001",
  },
  patient: {
    email: "patient@email.com",
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "JUAN GABRIEL",
    lastname: "ASTUDILLO BARBA",
    dni: "1234567890",
  },
  process: "Post Ocupacional",
};

const doctor = {
  name: "EDUARDO XAVIER",
  lastname: "JIMENEZ EDMUNDO",
  email: "doctor@email.com",
  dni: "1234567891",
};

const exam = {
  type: {
    key: "EXAMTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  subtype: {
    key: "EXAMSUBTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  key: "EXAM-0001",
  name: "COLESTEROL",
};

const form = new FormData();
form.append("file", file);
form.append("order", order);
form.append("doctor", doctor);
form.append("exam", exam);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}`, {
  method: "POST",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Examen sin tipo de examen</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const order = {
  key: "order-00001",
  branch: {
    company: {
      corporativeGroup: {
        key: "CORPORATIVE-0001",
        name: "LA FAVORITA",
      },
      ruc: "1234567890001",
      name: "SUPERMAXI",
      address: "Av.Amazonas",
      phone: "0999999999",
    },
    name: "Sucursal de la Amazonas",
    city: "Quito",
    key: "BRANCH-0001",
  },
  patient: {
    email: "patient@email.com",
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "JUAN GABRIEL",
    lastname: "ASTUDILLO BARBA",
    dni: "1234567890",
  },
  process: "Post Ocupacional",
};

const doctor = {
  name: "EDUARDO XAVIER",
  lastname: "JIMENEZ EDMUNDO",
  email: "doctor@email.com",
  dni: "1234567891",
};

const exam = {
  subtype: {
    key: "EXAMSUBTYPE-0001",
    name: "LABORATORIO CLINICO",
  },
  key: "EXAM-0001",
  name: "COLESTEROL",
};

const form = new FormData();
form.append("file", file);
form.append("order", order);
form.append("doctor", doctor);
form.append("exam", exam);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}`, {
  method: "POST",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
  <details>
    <summary><b>Ejemplo: <i>Examen sin subtipo</i></b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const order = {
  key: "order-00001",
  branch: {
    company: {
      corporativeGroup: {
        key: "CORPORATIVE-0001",
        name: "LA FAVORITA",
      },
      ruc: "1234567890001",
      name: "SUPERMAXI",
      address: "Av.Amazonas",
      phone: "0999999999",
    },
    name: "Sucursal de la Amazonas",
    city: "Quito",
    key: "BRANCH-0001",
  },
  patient: {
    email: "patient@email.com",
    gender: "male",
    birthday: new Date("2000-01-01"),
    name: "JUAN GABRIEL",
    lastname: "ASTUDILLO BARBA",
    dni: "1234567890",
  },
  process: "Post Ocupacional",
};

const doctor = {
  name: "EDUARDO XAVIER",
  lastname: "JIMENEZ EDMUNDO",
  email: "doctor@email.com",
  dni: "1234567891",
};

const exam = {
  key: "EXAM-0001",
  name: "COLESTEROL",
};

const form = new FormData();
form.append("file", file);
form.append("order", order);
form.append("doctor", doctor);
form.append("exam", exam);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}`, {
  method: "POST",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>

</details>

<details>
  <summary><b>Response</b></summary></br>

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

  </details>
</details>

---

#### `POST` /external/connection/medical/result/_{source}_/_{key}_/base64/file

Permite enviar un archivo en base64 junto con su mimetype.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `application/json`
- `Accept`: `application/json`

##### URL Parameters

- `source`: El nombre de la aplicación de origen. Debe estar en minúsculas y los espacios deben ser reemplazados por guión medio.
  - **Type**: _String_
- `key`: Identificador único del resultado médico.
  - **Type**: _String_

<details>
  <summary><b>Request</b></summary></br>

- **mimetype**: Tipo de dato del archivo a enviar
- **base64**: Archivo en base64

```typescript
{
  mimetype: string,
  base64: string
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

fetch(
  `${baseUrl}/external/connection/medical/result/${source}/${key}/base64/file`,
  {
    method: "POST",
    body: {
      mimetype: "application/pdf",
      base64: "my-base64-file",
    },
    headers: {
      "x-api-key": "my-sample-api-key",
      "content-type": "application/json",
      accept: "application/json",
    },
  }
);
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

- **file**: Archivo PDF que se desea subir para adjuntarlo al resultado médico.

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | true      |

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const form = new FormData();
form.append("file", file);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}/file`, {
  method: "POST",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

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

<details>
  <summary><b>Request</b></summary></br>

- **file**: Archivo PDF que se desea subir para adjuntarlo al resultado médico.

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | true      |

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const key = "01"; // REEMPLAZAR POR LA LLAVE CON LA QUE IDENTIFICARAN SUS DATOS EN LA APLICACION

const form = new FormData();
form.append("file", file);

fetch(`${baseUrl}/external/connection/medical/result/${source}/${key}/file`, {
  method: "PATCH",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

---

#### `PATCH` /external/connection/medical/result/_{id}_/file

Permite subir un archivo PDF y asociarlo a un resultado médico.

##### Request Headers

- `x-api-key`: Requiere un API key. Este será un string.
- `Content-Type`: `multipart/form-data`
- `Accept`: `application/json`

##### URL Parameters

- `id`: Identificador unico proporcionado por el sistema
  - **Type**: _Number_

<details>
  <summary><b>Request</b></summary></br>

- **file**: Archivo PDF que se desea subir para adjuntarlo al resultado médico.

| Subject | Type            | Mandatory |
| ------- | --------------- | --------- |
| file    | string($binary) | true      |

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION
const id = "01"; // IDENTIFICADOR QUE LA APLICACION ENTREGA CUANDO CREA UN RESULTADO/PRUEBA MEDICA

const form = new FormData();
form.append("file", file);

fetch(`${baseUrl}/external/connection/medical/result/${source}/file`, {
  method: "PATCH",
  body: form,
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "multipart/form-data",
    accept: "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

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

</details>

<div id='endpoint-medical-files'/>

### Archivos

---

#### `POST` /medical/file

Obtiene un archivo médico específico basado en el identificador único proporcionado por Omega Sistema de Reporteria Medica.

##### Request Headers

- `Content-Type`: `application/json`

<details>
  <summary><b>Request</b></summary></br>

- **id**: Identificador único de Omega Sistema de Reporteria Medica para el resultado o reporte.
- **type**: Tipo del archivo requerido. Debe ser `result` o `report`.

```typescript
{
  id: number,
  type: "report" | "result"
}
```

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION

fetch(`${baseUrl}/medical/file`, {
  method: "POST",
  body: {
    id: 1 // IDENTIFICADOR QUE LA APLICACION ENTREGA CUANDO CREA UNA ORDEN MEDICA
    type: "result",
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

Retorna un archivo en formato PDF

</details>

---

#### `POST` /medical/file/multiple

Obtiene varios archivos médicos específicos basados en los identificadores únicos proporcionados por Omega Sistema de Reporteria Medica.

##### Request Headers

- `Content-Type`: `application/json`

<details>
  <summary><b>Request</b></summary></br>

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

  <details>
    <summary><b>Ejemplo</b></summary>

```typescript
const baseUrl = "REEMPLAZAR POR EL DOMINIO O IP PROPORCIONADO";
const source = "omega-app"; // REEMPLAZAR POR EL NOMBRE DE SU APLICACION

fetch(`${baseUrl}/medical/file`, {
  method: "POST",
  body: {
    files: [
      {
        id: 1 // IDENTIFICADOR QUE LA APLICACION ENTREGA CUANDO CREA UNA ORDEN MEDICA
        type: "result",
      },
    ],
  },
  headers: {
    "x-api-key": "my-sample-api-key",
    "content-type": "application/json",
  },
});
```

  </details>
</details>

<details>
  <summary><b>Response</b></summary></br>

Retorna un archivo en formato PDF

</details>

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
