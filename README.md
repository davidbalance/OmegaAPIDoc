# Introducción

La aplicación de Omega expone ciertos endpoints para que sistemas externos puedan obtener y compartir información de forma segura. El presente documento tiene la finalidad de proveer información necesaria para la conexión con aplicaciones externas.

# Autenticación

Para el consumo o petición a cualquiera de los endpoints expuestos, se requiere de un **api-key**. Esta llave deberá ser colocada en la cabecera de la petición con el nombre `x-omega-key`.

# WebApi

Los presentes endpoints, exponen una sección de la aplicación, donde la aplicación que se conecte deberá pasar el id, con el que ustedes identifican o reconocen a sus datos de forma interna, hay excepciones como pacientes, cuyo DNI es usado para hacer la búsqueda correspondiente.

Cabe destacar que los parámetros del URL serán colocados como `:parámetro`. Donde parámetro es cualquier nombre asignado a dicho parámetro.

## Laboratorio

Estos endpoints permiten la administración de los exámenes disponibles en el laboratorio en base a la estructura:

- Tipo de examen.
- Subtipo de examen.
- Examen medico.

#### `GET` /external/exam-type/_:key_

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  typeId: string;
  typeName: string;
  hasSubtypes: boolean;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/exam-type/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/exam-type

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  typeKey: string;
  typeName: string;
}
```

**Responses** -> _application/json_

```typescript
{
  typeId: string;
  typeExternalKey: string;
  typeExternalKey: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/exam-type", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    typeKey: "",
    typeName: "",
  }),
});
```

#### `GET` /external/exam-subtype/_:key_

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  subtypeId: string;
  subtypeName: string;
  hasExams: boolean;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/exam-subtype/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/exam-subtype

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  typeKey: string;
  typeName: string;
  subtypeKey: string;
  subtypeName: string;
}
```

**Responses** -> _application/json_

```typescript
{
  subtypeId: string;
  subtypeExternalKey: string;
  subtypeExternalOwner: string;
  typeId: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/exam-subtype", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    typeKey: "",
    typeName: "",
    subtypeKey: "",
    subtypeName: "",
  }),
});
```

#### `GET` /external/exam/_:key_

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  examId: string;
  examName: string;
  subtypeId: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/exam/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/exam

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  typeKey: string;
  typeName: string;
  subtypeKey: string;
  subtypeName: string;
  examKey: string;
  examName: string;
}
```

**Responses** -> _application/json_

```typescript
{
  examId: string;
  examExternalKey: string;
  examExternalOwner: string;
  subtypeId: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/exam", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    typeKey: "",
    typeName: "",
    subtypeKey: "",
    subtypeName: "",
    examKey: "",
    examName: "",
  }),
});
```

## Localidades

Estos endpoints permiten la administración de ubicaciones empresariales como lo son:

- Grupos corporativos.
- Empresas.
- Sucursales.

#### `GET` /external/corporative

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  corporativeId: string;
  corporativeName: string;
  hasCompanies: boolean;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/corporative/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/corporative/_:key_

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  corporativeKey: string;
  corporativeName: string;
}
```

**Responses** -> _application/json_

```typescript
{
  corporativeId: string;
  corporativeExternalKey: string;
  corporativeExternalOwner: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/corporative", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    corporativeKey: "",
    corporativeName: "",
  }),
});
```

#### `GET` /external/company/_:key_

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  corporativeId: string;
  companyId: string;
  companyRuc: string;
  companyName: string;
  companyAddress: string;
  hasBranches: boolean;
  companyPhone: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/company/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/company

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  corporativeKey: string;
  corporativeName: string;
  companyKey: string;
  companyName: string;
  companyRuc: string; // String length of 13
  companyAddress: string;
  companyPhone: string;
}
```

**Responses** -> _application/json_

```typescript
{
  companyId: string;
  companyExternalKey: string;
  companyExternalOwner: string;
  corporativeId: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/company", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    corporativeKey: "",
    corporativeName: "",
    companyKey: "",
    companyName: "",
    companyRuc: "",
    companyAddress: "",
    companyPhone: "",
  }),
});
```

#### `GET` /external/branch/_:key_

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  branchId: string;
  branchName: string;
  companyId: string;
  cityName: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/branch/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/branch

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  companyPhone: string;
  corporativeKey: string;
  corporativeName: string;
  companyKey: string;
  companyName: string;
  companyRuc: string; // String length of 13
  companyAddress: string;
  cityId: number;
  branchKey: string;
  branchName: string;
}
```

**Responses** -> _application/json_

```typescript
{
  branchId: string;
  branchExternalKey: string;
  branchExternalOwner: string;
  companyId: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/branch", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    companyPhone: "",
    corporativeKey: "",
    corporativeName: "",
    companyKey: "",
    companyName: "",
    companyRuc: "",
    companyAddress: "",
    cityId: 1,
    branchKey: "",
    branchName: "",
  }),
});
```

## Area Medica

Estos endpoints permiten la administración de pacientes, pedidos, y examenes medicos.

#### `GET` /external/patient/:patientDni

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  patientGender: string;
  patientDni: string;
  patientName: string;
  patientLastname: string;
  patientBirthday: Date;
  patientRole: string | null | undefined;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/patient/{patientDni}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/patient

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  patientGender: "male" | "female";
  patientDni: string; // Length of 10
  patientName: string;
  patientLastname: string;
  patientEmail: string;
  patientBirthday: Date;
}
```

**Responses** -> _application/json_

```typescript
{
  patientGender: string;
  patientDni: string;
  patientName: string;
  patientLastname: string;
  patientBirthday: Date;
  patientRole: string | undefined | null;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/patient", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    patientGender: "male",
    patientDni: "",
    patientName: "",
    patientLastname: "",
    patientEmail: "",
    patientBirthday: "",
  }),
});
```

#### `GET` /external/medical-order/_:key_

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
  orderStatus: string;
  orderId: string;
  orderMail: boolean;
  orderProcess: string;
  orderEmissionDate: Date;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/medical-order/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/medical-order

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  patientGender: "male" | "female";
  patientDni: string; // Length of 10
  patientName: string;
  patientLastname: string;
  patientEmail: string;
  patientBirthday: Date;
  corporativeName: string;
  companyRuc: string;
  companyName: string;
  branchName: string;
  doctorDni: string | undefined | null; // Optional
  doctorFullname: string | undefined | null; // Optional
  orderKey: string;
  orderProcess: string;
  orderYear: number; // Min value: 1900
  branchKey: string | undefined | null; // Optional
  companyKey: string | undefined | null; // Optional
  corporativeKey: string | undefined | null; // Optional
}
```

**Responses** -> _application/json_

```typescript
{
  orderId: string;
  orderExternalKey: string;
  orderExternalOwner: string;
  patientDni: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/medical-order", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    patientGender: "male",
    patientDni: "",
    patientName: "",
    patientLastname: "",
    patientEmail: "",
    patientBirthday: "",
    corporativeName: "",
    companyRuc: "",
    companyName: "",
    branchName: "",
    doctorDni: "0000000000",
    doctorFullname: "NO ESPECIFICO",
    orderKey: "",
    orderProcess: "",
    orderYear: 1,
    branchKey: "",
    companyKey: "",
    corporativeKey: "",
  }),
});
```

#### `GET` /external/medical-test/_:key_

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
{
    testId: string;
    testCheck: boolean;
    resultHasFile: boolean;
    reportHasContent: boolean;
    orderId: string;
    examName: string;
    examSubtype: string;
    examType: string;
    diseases: string[];
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/medical-test/{key}", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `GET` /external/medical-test/_:key_/result

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/pdf_

```
stringFormat:binary
binary data, used to describe files
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/medical-test/{key}/result", {
  headers: {
    "x-omega-key": "<your-key>",
  },
});
```

#### `POST` /external/medical-test

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  patientGender: "male" | "female";
  patientDni: string; // Length of 10
  patientName: string;
  patientLastname: string;
  patientEmail: string;
  patientBirthday: Date;
  corporativeName: string;
  companyRuc: string;
  companyName: string;
  branchName: string;
  doctorDni: string | undefined | null; // Optional - Default: '0000000000'
  doctorFullname: string | undefined | null; // Optional - Default: 'NO ESPECIFICO'
  orderKey: string;
  orderProcess: string;
  orderYear: number; // Min value: 1900
  branchKey: string | undefined | null; // Optional
  companyKey: string | undefined | null; // Optional
  corporativeKey: string | undefined | null; // Optional
  testKey: string;
  examName: string;
  examSubtype: string | undefined | null; // Optional - Default: Default
  examType: string | undefined | null; // Optional - Default: Default
  examTypeKey: string | undefined | null; // Optional
  examSubtypeKey: string | undefined | null; // Optional
  examKey: string | undefined | null; // Optional
}
```

**Responses** -> _application/json_

```typescript
{
  testId: string;
  testExternalKey: string;
  testExternalOwner: string;
}
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/medical-test", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    patientGender: "male",
    patientDni: "",
    patientName: "",
    patientLastname: "",
    patientEmail: "",
    patientBirthday: "",
    corporativeName: "",
    companyRuc: "",
    companyName: "",
    branchName: "",
    doctorDni: "0000000000",
    doctorFullname: "NO ESPECIFICO",
    orderKey: "",
    orderProcess: "",
    orderYear: 1,
    branchKey: "",
    companyKey: "",
    corporativeKey: "",
    testKey: "",
    examName: "",
    examSubtype: "Default",
    examType: "Default",
    examTypeKey: "",
    examSubtypeKey: "",
    examKey: "",
  }),
});
```

#### `POST` /external/medical-test/:key/result/base64

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> _application/json_

```typescript
{
  base64: string;
}
```

**Responses** -> _application/json_

```
Ok
```

**Uso**

```javascript
fetch("http://<ip>:<port>/external/medical-test/{key}/result/base64", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    base64: "",
  }),
});
```

#### `POST` /external/medical-test/:key/result/file

**Path Parameters**
key - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Body** -> multipart/form-data\_

| Property | Type   |
| -------- | ------ |
| file     | string |

**Responses** -> _application/json_

```
Ok
```

**Uso**

```javascript
const form = new FormData();
form.append("file", "<your-file>");
fetch("http://<ip>:<port>/external/medical-test/{key}/result/file", {
  method: "POST",
  headers: {
    "x-omega-key": "<your-key>",
    "Content-Type": "multipart/form-data",
  },
  body: form,
});
```