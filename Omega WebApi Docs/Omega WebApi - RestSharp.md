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

```csharp
var client = new RestClient("http://<ip>:<port>/external/exam-type/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/exam-type");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"typeKey\": \"\",\n  \"typeName\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/exam-subtype/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/exam-subtype");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"typeKey\": \"\",\n  \"typeName\": \"\",\n  \"subtypeKey\": \"\",\n  \"subtypeName\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/exam/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/exam");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"typeKey\": \"\",\n  \"typeName\": \"\",\n  \"subtypeKey\": \"\",\n  \"subtypeName\": \"\",\n  \"examKey\": \"\",\n  \"examName\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/corporative/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/corporative");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"corporativeKey\": \"\",\n  \"corporativeName\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/company/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/company");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"corporativeKey\": \"\",\n  \"corporativeName\": \"\",\n  \"companyKey\": \"\",\n  \"companyName\": \"\",\n  \"companyRuc\": \"\",\n  \"companyAddress\": \"\",\n  \"companyPhone\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/branch/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/branch");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"companyPhone\": \"\",\n  \"corporativeKey\": \"\",\n  \"corporativeName\": \"\",\n  \"companyKey\": \"\",\n  \"companyName\": \"\",\n  \"companyRuc\": \"\",\n  \"companyAddress\": \"\",\n  \"cityId\": 1,\n  \"branchKey\": \"\",\n  \"branchName\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/patient/%7BpatientDni%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/patient");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"patientGender\": \"male\",\n  \"patientDni\": \"\",\n  \"patientName\": \"\",\n  \"patientLastname\": \"\",\n  \"patientEmail\": \"\",\n  \"patientBirthday\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-order/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-order");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"patientGender\": \"male\",\n  \"patientDni\": \"\",\n  \"patientName\": \"\",\n  \"patientLastname\": \"\",\n  \"patientEmail\": \"\",\n  \"patientBirthday\": \"\",\n  \"corporativeName\": \"\",\n  \"companyRuc\": \"\",\n  \"companyName\": \"\",\n  \"branchName\": \"\",\n  \"doctorDni\": \"0000000000\",\n  \"doctorFullname\": \"NO ESPECIFICO\",\n  \"orderKey\": \"\",\n  \"orderProcess\": \"\",\n  \"orderYear\": 1,\n  \"branchKey\": \"\",\n  \"companyKey\": \"\",\n  \"corporativeKey\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-test/%7Bkey%7D");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
```

#### `GET` /external/medical-test/_:orderKey_/many

**Path Parameters**
orderKey - _string_ - <span style="color: red;">required</span>

**Headers**
x-omega-key - _string_ - <span style="color: red;">required</span>

**Responses** -> _application/json_

```typescript
[
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
]
```

**Uso**

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-test/%7BorderKey%7D/many");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-test/%7Bkey%7D/result");
var request = new RestRequest(Method.GET);
request.AddHeader("x-omega-key", "");
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-test");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"patientGender\": \"male\",\n  \"patientDni\": \"\",\n  \"patientName\": \"\",\n  \"patientLastname\": \"\",\n  \"patientEmail\": \"\",\n  \"patientBirthday\": \"\",\n  \"corporativeName\": \"\",\n  \"companyRuc\": \"\",\n  \"companyName\": \"\",\n  \"branchName\": \"\",\n  \"doctorDni\": \"0000000000\",\n  \"doctorFullname\": \"NO ESPECIFICO\",\n  \"orderKey\": \"\",\n  \"orderProcess\": \"\",\n  \"orderYear\": 1,\n  \"branchKey\": \"\",\n  \"companyKey\": \"\",\n  \"corporativeKey\": \"\",\n  \"testKey\": \"\",\n  \"examName\": \"\",\n  \"examSubtype\": \"Default\",\n  \"examType\": \"Default\",\n  \"examTypeKey\": \"\",\n  \"examSubtypeKey\": \"\",\n  \"examKey\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

#### `POST` /external/medical-test/many

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
  tests: Array<{
    testKey: string;
    examName: string;
    examSubtype: string | undefined | null; // Optional - Default: Default
    examType: string | undefined | null; // Optional - Default: Default
    examTypeKey: string | undefined | null; // Optional
    examSubtypeKey: string | undefined | null; // Optional
    examKey: string | undefined | null; // Optional
  }>;
}
```

**Responses** -> _application/json_

```typescript
{
  patientDni: string;
  orderId: string;
  orderExternalKey: string;
  orderExternalOwner: string;
  tests: Array<{
    testId: string;
    testExternalKey: string;
    testExternalOwner: string;
  }>;
}
```

**Uso**

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-test/many");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"patientGender\": \"male\",\n  \"patientDni\": \"\",\n  \"patientName\": \"\",\n  \"patientLastname\": \"\",\n  \"patientEmail\": \"\",\n  \"patientBirthday\": \"\",\n  \"corporativeName\": \"\",\n  \"companyRuc\": \"\",\n  \"companyName\": \"\",\n  \"branchName\": \"\",\n  \"doctorDni\": \"0000000000\",\n  \"doctorFullname\": \"NO ESPECIFICO\",\n  \"orderKey\": \"\",\n  \"orderProcess\": \"\",\n  \"orderYear\": 1,\n  \"branchKey\": \"\",\n  \"companyKey\": \"\",\n  \"corporativeKey\": \"\",\n  \"tests\": [\n    {\n      \"testKey\": \"\",\n      \"examName\": \"\",\n      \"examSubtype\": \"Default\",\n      \"examType\": \"Default\",\n      \"examTypeKey\": \"\",\n      \"examSubtypeKey\": \"\",\n      \"examKey\": \"\"\n    }\n  ]\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-test/%7Bkey%7D/result/base64");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"base64\": \"\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
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

```csharp
var client = new RestClient("http://<ip>:<port>/external/medical-test/%7Bkey%7D/result/file");
var request = new RestRequest(Method.POST);
request.AddHeader("x-omega-key", "");
request.AddHeader("Content-Type", "multipart/form-data");
request.AddParameter("multipart/form-data", "{\"file\":\"\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```