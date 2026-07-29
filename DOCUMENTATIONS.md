# Documentación de Funcionalidades del Proyecto CatalogoParametrosUcoLab

## Descripción General

El proyecto **CatalogoParametrosUcoLab** es una aplicación Spring Boot (WebFlux) que expone una API REST para la gestión de un catálogo de parámetros organizados en entidades jerárquicas: Organizaciones → Aplicaciones → Módulos → Funcionalidades → Parámetros.

La arquitectura sigue el patrón **Hexagonal (Ports & Adapters)** con separación en:
- **Primary Ports (Puertos Primarios):** Interactores y DTOs de entrada
- **Secondary Ports (Puertos Secundarios):** Repositorios, eventos y publishers
- **Use Cases:** Lógica de negocio y validación de reglas
- **Infrastructure:** Controladores REST y adaptadores de infraestructura

---

## 1. Funcionalidad: Crear Organización

### Atributos del DTO (`CrearOrganizacionDto`)

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `nombre` | `String` | Nombre de la organización |

### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `POST` | `/catalogo-parametros/api/v1/organizaciones` | Crea una nueva organización |
| `GET` | `/catalogo-parametros/api/v1/organizaciones/events` | Stream de eventos SSE (Server-Sent Events) |

### JSON de Request (POST)

```json
{
  "nombre": "Mi Organización"
}
```

### JSON de Response (Exitoso - 201 CREATED)

```json
"Organizacion creada exitosamente."
```

### JSON de Error Response (400 BAD REQUEST)

```json
"Error de validación: ..."
```

### Interactor

- **Interface:** [`CrearOrganizacionInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/organizacion/crearorganizacion/primaryports/interactor/CrearOrganizacionInteractor.java)
- **Implementación:** [`CrearOrganizacionInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/organizacion/crearorganizacion/primaryports/interactor/impl/CrearOrganizacionInteractorImpl.java)
- **Tipo:** `InteractorWithOutReturn<CrearOrganizacionDto>` — ejecuta sin retorno

### Use Case

- **Interface:** [`CrearOrganizacion`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/organizacion/crearorganizacion/usecase/CrearOrganizacion.java)
- **Implementación:** [`CrearOrganizacionImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/organizacion/crearorganizacion/usecase/crearorganizacionimpl/CrearOrganizacionImpl.java)
- **Validador:** [`CrearOrganizacionRuleValidatorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/organizacion/crearorganizacion/usecase/crearorganizacionimpl/CrearOrganizacionRuleValidatorImpl.java)

### Reglas de Negocio (Domain Rules)

| Regla | Descripción |
|-------|-------------|
| `OrganizacionNombreIsNotNullRule` | Valida que el nombre no sea nulo |
| `OrganizacionNombreIsNotEmptyRule` | Valida que el nombre no esté vacío |
| `OrganizacionNombreDoesNotExistRule` | Valida que el nombre no esté ya registrado |

### Evento

- **Clase:** [`CrearOrganizacionEvent`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/organizacion/crearorganizacion/secondaryports/event/CrearOrganizacionEvent.java)
- **Tipo de evento:** `EventType.CREATED`
- **Publisher:** [`CrearOrganizacionPublisher`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/organizacion/crearorganizacion/secondaryports/publisher/CrearOrganizacionPublisher.java)

### Entity

[`OrganizacionEntity`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/OrganizacionEntity.java)

| Atributo | Tipo |
|----------|------|
| `id` | `UUID` |
| `nombre` | `String` |

---

## 2. Funcionalidad: Crear Aplicación

### Atributos del DTO (`CrearAplicacionDto`)

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `nombre` | `String` | Nombre de la aplicación |
| `idOrganizacion` | `UUID` | Identificador de la organización a la que pertenece |
| `activa` | `boolean` | Indica si la aplicación está activa |
| `fechaInicio` | `LocalDateTime` | Fecha de inicio de la aplicación |
| `fechaFinal` | `LocalDateTime` | Fecha de finalización de la aplicación |

### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `POST` | `/catalogo-parametros/api/v1/aplicaciones` | Crea una nueva aplicación |
| `GET` | `/catalogo-parametros/api/v1/aplicaciones/events` | Stream de eventos SSE |

### JSON de Request (POST)

```json
{
  "nombre": "Mi Aplicación",
  "idOrganizacion": "550e8400-e29b-41d4-a716-446655440000",
  "activa": true,
  "fechaInicio": "2024-01-01T00:00:00",
  "fechaFinal": "2024-12-31T23:59:59"
}
```

### JSON de Response (Exitoso - 201 CREATED)

```json
"Aplicacion creada exitosamente."
```

### Interactor

- **Interface:** [`CrearAplicacionInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/aplicacion/crearaplicacion/primaryports/interactor/CrearAplicacionInteractor.java)
- **Implementación:** [`CrearAplicacionInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/aplicacion/crearaplicacion/primaryports/interactor/impl/CrearAplicacionInteractorImpl.java)
- **Tipo:** `InteractorWithOutReturn<CrearAplicacionDto>`

### Use Case

- **Interface:** [`CrearAplicacion`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/aplicacion/crearaplicacion/usecase/CrearAplicacion.java)
- **Implementación:** [`CrearAplicacionImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/aplicacion/crearaplicacion/usecase/crearaplicacionimpl/CrearAplicacionImpl.java)
- **Validador:** [`CrearAplicacionRuleValidatorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/aplicacion/crearaplicacion/usecase/crearaplicacionimpl/CrearAplicacionRuleValidatorImpl.java)

### Reglas de Negocio (Domain Rules)

| Regla | Descripción |
|-------|-------------|
| `AplicacionNombreIsNotNullRule` | Valida que el nombre no sea nulo |
| `AplicacionNombreIsNotEmptyRule` | Valida que el nombre no esté vacío |
| `AplicacionNombreDoesNotExistRule` | Valida que el nombre no esté ya registrado |
| `AplicacionOrganizacionExistsRule` | Valida que la organización referenciada exista |

### Evento

- **Clase:** [`CrearAplicacionEvent`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/aplicacion/crearaplicacion/secondaryports/event/CrearAplicacionEvent.java)
- **Tipo de evento:** `EventType.CREATED`
- **Publisher:** [`CrearAplicacionPublisher`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/aplicacion/crearaplicacion/secondaryports/publisher/CrearAplicacionPublisher.java)

### Entity

[`AplicacionEntity`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/AplicacionEntity.java)

| Atributo | Tipo |
|----------|------|
| `id` | `UUID` |
| `nombre` | `String` |
| `idOrganizacion` | `UUID` |
| `activa` | `boolean` |
| `fechaInicio` | `LocalDateTime` |
| `fechaFinal` | `LocalDateTime` |

---

## 3. Funcionalidad: Crear Módulo

### Atributos del DTO (`CrearModuloDto`)

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `nombre` | `String` | Nombre del módulo |
| `idAplicacion` | `UUID` | Identificador de la aplicación a la que pertenece |
| `activo` | `boolean` | Indica si el módulo está activo |
| `fechaInicio` | `String` | Fecha de inicio del módulo |
| `fechaFinal` | `String` | Fecha de finalización del módulo |

### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `POST` | `/catalogo-parametros/api/v1/modulos` | Crea un nuevo módulo |
| `GET` | `/catalogo-parametros/api/v1/modulos/events` | Stream de eventos SSE |

### JSON de Request (POST)

```json
{
  "nombre": "Mi Módulo",
  "idAplicacion": "550e8400-e29b-41d4-a716-446655440000",
  "activo": true,
  "fechaInicio": "2024-01-01",
  "fechaFinal": "2024-12-31"
}
```

### JSON de Response (Exitoso - 201 CREATED)

```json
{
  "mensajes": ["Modulo creado exitosamente."]
}
```

### Interactor

- **Interface:** [`CrearModuloInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/modulo/crearmodulo/primaryports/interactor/CrearModuloInteractor.java)
- **Implementación:** [`CrearModuloInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/modulo/crearmodulo/primaryports/interactor/impl/CrearModuloInteractorImpl.java)
- **Tipo:** `InteractorWithOutReturn<CrearModuloDto>`

### Use Case

- **Interface:** [`CrearModulo`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/modulo/crearmodulo/CrearModulo.java)
- **Implementación:** [`CrearModuloImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/modulo/crearmodulo/usecase/crearmoduloimpl/CrearModuloImpl.java)
- **Validador:** [`CrearModuloRuleValidatorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/modulo/crearmodulo/usecase/crearmoduloimpl/CrearModuloRuleValidatorImpl.java)

### Reglas de Negocio (Domain Rules)

| Regla | Descripción |
|-------|-------------|
| `ModuloNombreIsNotNullRule` | Valida que el nombre no sea nulo |
| `ModuloNombreIsNotEmptyRule` | Valida que el nombre no esté vacío |
| `ModuloNombreDoesNotExistRule` | Valida que el nombre no esté ya registrado |
| `ModuloAplicacionExistsRule` | Valida que la aplicación referenciada exista |

### Evento

- **Clase:** [`CrearModuloEvent`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/modulo/crearmodulo/secondaryports/event/CrearModuloEvent.java)
- **Tipo de evento:** `EventType.CREATED`
- **Publisher:** [`CrearModuloPublisher`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/modulo/crearmodulo/secondaryports/publisher/CrearModuloPublisher.java)

### Entity

[`ModuloEntity`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/ModuloEntity.java)

| Atributo | Tipo |
|----------|------|
| `id` | `UUID` |
| `nombre` | `String` |
| `idAplicacion` | `UUID` |
| `activo` | `boolean` |
| `fechaInicio` | `LocalDateTime` |
| `fechaFinal` | `LocalDateTime` |

---

## 4. Funcionalidad: Crear Funcionalidad

### Atributos del DTO (`CrearFuncionalidadDto`)

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `nombre` | `String` | Nombre de la funcionalidad |
| `idModulo` | `UUID` | Identificador del módulo al que pertenece |
| `activo` | `boolean` | Indica si la funcionalidad está activa |
| `fechaInicio` | `LocalDateTime` | Fecha de inicio de la funcionalidad |
| `fechaFinal` | `LocalDateTime` | Fecha de finalización de la funcionalidad |

### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `POST` | `/catalogo-parametros/api/v1/funcionalidades` | Crea una nueva funcionalidad |
| `GET` | `/catalogo-parametros/api/v1/funcionalidades` | Consulta todas las funcionalidades |
| `GET` | `/catalogo-parametros/api/v1/funcionalidades/{id}` | Consulta funcionalidades por ID |
| `GET` | `/catalogo-parametros/api/v1/funcionalidades/events` | Stream de eventos SSE |

### JSON de Request (POST)

```json
{
  "nombre": "Mi Funcionalidad",
  "idModulo": "550e8400-e29b-41d4-a716-446655440000",
  "activo": true,
  "fechaInicio": "2024-01-01T00:00:00",
  "fechaFinal": "2024-12-31T23:59:59"
}
```

### JSON de Response (Exitoso - 201 CREATED)

```json
{
  "mensajes": ["Funcionalidad creada exitosamente."]
}
```

### JSON de Response para Consulta (GET /{id})

```json
{
  "funcionalidades": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "nombre": "Mi Funcionalidad",
      "idModulo": "550e8400-e29b-41d4-a716-446655440000",
      "activo": true,
      "fechaInicio": "2024-01-01T00:00:00",
      "fechaFinal": "2024-12-31T23:59:59"
    }
  ],
  "mensajes": []
}
```

### Interactor

- **Interface de creación:** [`CrearFuncionalidadInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/primaryports/interactor/CrearFuncionalidadInteractor.java)
- **Interface de consulta:** [`ConsultarFuncionalidadInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/primaryports/interactor/ConsultarFuncionalidadInteractor.java)
- **Implementación de creación:** [`CrearFuncionalidadInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/primaryports/interactor/impl/CrearFuncionalidadInteractorImpl.java)
- **Implementación de consulta:** [`ConsultarFuncionalidadInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/primaryports/interactor/impl/ConsultarFuncionalidadInteractorImpl.java)
- **Tipo de creación:** `InteractorWithOutReturn<CrearFuncionalidadDto>`
- **Tipo de consulta:** `InteractorWithReturn<UUID, List<FuncionalidadEntity>>`

### Use Case

- **Interface:** [`CrearFuncionalidad`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/usecase/CrearFuncionalidad.java)
- **Implementación:** [`CrearFuncionalidadImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/usecase/crearfuncionalidadimpl/CrearFuncionalidadImpl.java)
- **Validador:** [`CrearFuncionalidadRuleValidatorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/usecase/crearfuncionalidadimpl/CrearFuncionalidadRuleValidatorImpl.java)

### Reglas de Negocio (Domain Rules)

| Regla | Descripción |
|-------|-------------|
| `FuncionalidadNombreIsNotNullRule` | Valida que el nombre no sea nulo |
| `FuncionalidadNombreIsNotEmptyRule` | Valida que el nombre no esté vacío |
| `FuncionalidadNombreDoesNotExistRule` | Valida que el nombre no esté ya registrado |
| `FuncionalidadModuloExistsRule` | Valida que el módulo referenciado exista |

### Evento

- **Clase:** [`CrearFuncionalidadEvent`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/secondaryports/event/CrearFuncionalidadEvent.java)
- **Tipo de evento:** `EventType.CREATED`
- **Publisher:** [`CrearFuncionalidadPublisher`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/funcionalidad/crearfuncionalidad/secondaryports/publisher/CrearFuncionalidadPublisher.java)

### Entity

[`FuncionalidadEntity`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/FuncionalidadEntity.java)

| Atributo | Tipo |
|----------|------|
| `id` | `UUID` |
| `nombre` | `String` |
| `idModulo` | `UUID` |
| `activo` | `boolean` |
| `fechaInicio` | `LocalDateTime` |
| `fechaFinal` | `LocalDateTime` |

---

## 5. Funcionalidad: Gestión de Parámetros (CRUD Completo)

### 5.1 Crear Parámetro

#### Atributos del DTO (`CrearParametroDto`)

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `nombre` | `String` | Nombre del parámetro |
| `idFuncionalidad` | `UUID` | Identificador de la funcionalidad a la que pertenece |
| `idTipoParametro` | `UUID` | Identificador del tipo de parámetro |
| `activo` | `boolean` | Indica si el parámetro está activo |

#### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `POST` | `/catalogo-parametros/api/v1/parametros` | Crea un nuevo parámetro |

#### JSON de Request (POST)

```json
{
  "nombre": "Mi Parámetro",
  "idFuncionalidad": "550e8400-e29b-41d4-a716-446655440000",
  "idTipoParametro": "550e8400-e29b-41d4-a716-446655440001",
  "activo": true
}
```

#### JSON de Response (Exitoso - 201 CREATED)

```json
{
  "mensajes": ["Parametro creado exitosamente."]
}
```

#### Interactor

- **Interface:** [`CrearParametroInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/primaryports/interactor/CrearParametroInteractor.java)
- **Implementación:** [`CrearParametroInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/primaryports/interactor/impl/CrearParametroInteractorImpl.java)
- **Tipo:** `InteractorWithOutReturn<CrearParametroDto>`

#### Use Case

- **Interface:** [`CrearParametro`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/CrearParametro.java)
- **Implementación:** [`CrearParametroImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/usecase/crearparametroimpl/CrearParametroImpl.java)
- **Validador:** [`CrearParametroRuleValidatorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/usecase/crearparametroimpl/CrearParametroRuleValidatorImpl.java)

#### Reglas de Negocio (Domain Rules)

| Regla | Descripción |
|-------|-------------|
| `ParametroNameIsNotNullRule` | Valida que el nombre no sea nulo |
| `ParametroNameIsNotEmptyRule` | Valida que el nombre no esté vacío |
| `ParametroNameLengthIsValidRule` | Valida que la longitud del nombre sea válida |
| `ParametroNameFormatIsValidRule` | Valida que el formato del nombre sea válido |
| `ParametroFuncionalidadExistsRule` | Valida que la funcionalidad referenciada exista |
| `ParametroFuncionalidadIsValidRule` | Valida que la funcionalidad sea válida |
| `ParametroTipoParametroIsValidRule` | Valida que el tipo de parámetro sea válido |
| `ParametroNameDoesNotExistRule` | Valida que el nombre no esté ya registrado |

#### Evento

- **Clase:** [`CrearParametroEvent`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/secondaryports/event/CrearParametroEvent.java)
- **Tipo de evento:** `EventType.CREATED`
- **Publisher:** [`CrearParametroPublisher`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/secondaryports/publisher/CrearParametroPublisher.java)

---

### 5.2 Actualizar Parámetro

#### Atributos del DTO (`ActualizarParametroDto`)

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `nombre` | `String` | Nombre del parámetro |
| `idFuncionalidad` | `UUID` | Identificador de la funcionalidad |
| `idTipoParametro` | `UUID` | Identificador del tipo de parámetro |
| `activo` | `boolean` | Indica si el parámetro está activo |

#### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `PUT` | `/catalogo-parametros/api/v1/parametros/{id}` | Actualiza un parámetro existente |

#### JSON de Request (PUT)

```json
{
  "nombre": "Mi Parámetro Actualizado",
  "idFuncionalidad": "550e8400-e29b-41d4-a716-446655440000",
  "idTipoParametro": "550e8400-e29b-41d4-a716-446655440001",
  "activo": false
}
```

#### JSON de Response (Exitoso - 200 OK)

```json
{
  "mensajes": ["Parametro actualizado exitosamente."]
}
```

#### Interactor

- **Interface:** [`ActualizarParametroInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/actualizarparametro/primaryports/interactor/ActualizarParametroInteractor.java)
- **Implementación:** [`ActualizarParametroInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/actualizarparametro/primaryports/interactor/impl/ActualizarParametroInteractorImpl.java)
- **Firma:** `void execute(UUID id, ActualizarParametroDto data)`

#### Use Case

- **Interface:** [`ActualizarParametro`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/actualizarparametro/ActualizarParametro.java)
- **Implementación:** [`ActualizarParametroImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/actualizarparametro/usecase/actualizarparametroimpl/ActualizarParametroImpl.java)
- **Validador:** [`ActualizarParametroRuleValidatorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/actualizarparametro/usecase/actualizarparametroimpl/ActualizarParametroRuleValidatorImpl.java)

#### Reglas de Negocio (Domain Rules)

| Regla | Descripción |
|-------|-------------|
| `ActualizarParametroNombreIsNotNullRule` | Valida que el nombre no sea nulo |
| `ActualizarParametroNombreIsNotEmptyRule` | Valida que el nombre no esté vacío |
| `ActualizarParametroFuncionalidadExistsRule` | Valida que la funcionalidad referenciada exista |
| `ActualizarParametroFuncionalidadIsValidRule` | Valida que la funcionalidad sea válida |
| `ActualizarParametroTipoParametroIsValidRule` | Valida que el tipo de parámetro sea válido |

#### Evento

- **Clase:** [`ActualizarParametroEvent`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/actualizarparametro/secondaryports/event/ActualizarParametroEvent.java)
- **Tipo de evento:** `EventType.UPDATED`
- **Publisher:** [`ActualizarParametroPublisher`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/actualizarparametro/secondaryports/publisher/ActualizarParametroPublisher.java)

---

### 5.3 Eliminar Parámetro

#### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `DELETE` | `/catalogo-parametros/api/v1/parametros/{id}` | Elimina un parámetro por su ID |

#### JSON de Response (Exitoso - 200 OK)

```json
{
  "mensajes": ["Parametro eliminado exitosamente."]
}
```

#### Interactor

- **Interface:** [`EliminarParametroInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/eliminarparametro/primaryports/interactor/EliminarParametroInteractor.java)
- **Implementación:** [`EliminarParametroInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/eliminarparametro/primaryports/interactor/impl/EliminarParametroInteractorImpl.java)
- **Tipo:** `InteractorWithOutReturn<UUID>`

#### Use Case

- **Interface:** [`EliminarParametro`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/eliminarparametro/EliminarParametro.java)
- **Implementación:** [`EliminarParametroImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/eliminarparametro/usecase/eliminarparametroimpl/EliminarParametroImpl.java)

#### Evento

- **Clase:** [`EliminarParametroEvent`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/eliminarparametro/secondaryports/event/EliminarParametroEvent.java)
- **Tipo de evento:** `EventType.DELETED`
- **Publisher:** [`EliminarParametroPublisher`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/eliminarparametro/secondaryports/publisher/EliminarParametroPublisher.java)

---

### 5.4 Consultar Todos los Parámetros

#### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `GET` | `/catalogo-parametros/api/v1/parametros` | Consulta todos los parámetros |

#### JSON de Response (200 OK)

```json
{
  "parametros": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "nombre": "Mi Parámetro",
      "idFuncionalidad": "550e8400-e29b-41d4-a716-446655440001",
      "idTipoParametro": "550e8400-e29b-41d4-a716-446655440002",
      "activo": true
    }
  ],
  "mensajes": []
}
```

#### Interactor

- **Interface:** [`ConsultarParametroInteractor`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/primaryports/interactor/ConsultarParametroInteractor.java)
- **Implementación:** [`ConsultarParametroInteractorImpl`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/features/parametro/crearparametro/primaryports/interactor/impl/ConsultarParametroInteractorImpl.java)
- **Tipo:** `InteractorWithReturn<UUID, List<ParametroEntity>>`

---

### 5.5 Consultar Parámetro por ID

#### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `GET` | `/catalogo-parametros/api/v1/parametros/{id}` | Consulta un parámetro por su ID |

#### JSON de Response (200 OK)

```json
{
  "parametros": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "nombre": "Mi Parámetro",
      "idFuncionalidad": "550e8400-e29b-41d4-a716-446655440001",
      "idTipoParametro": "550e8400-e29b-41d4-a716-446655440002",
      "activo": true
    }
  ],
  "mensajes": []
}
```

#### JSON de Response (404 NOT FOUND)

```json
{
  "parametros": [],
  "mensajes": ["No se encontro el parametro con el id especificado."]
}
```

---

### 5.6 Stream de Eventos de Parámetros (SSE)

#### URL y Método HTTP

| Método | URL | Descripción |
|--------|-----|-------------|
| `GET` | `/catalogo-parametros/api/v1/parametros/events` | Stream de eventos SSE para crear, actualizar y eliminar parámetros |

El stream fusiona los eventos de los tres publishers: `CrearParametroPublisher`, `ActualizarParametroPublisher` y `EliminarParametroPublisher`.

---

## 6. Entidades del Dominio

### Resumen de Entities

| Entity | Archivo | Atributos |
|--------|---------|-----------|
| `OrganizacionEntity` | [`OrganizacionEntity.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/OrganizacionEntity.java) | `id` (UUID), `nombre` (String) |
| `AplicacionEntity` | [`AplicacionEntity.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/AplicacionEntity.java) | `id` (UUID), `nombre` (String), `idOrganizacion` (UUID), `activa` (boolean), `fechaInicio` (LocalDateTime), `fechaFinal` (LocalDateTime) |
| `ModuloEntity` | [`ModuloEntity.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/ModuloEntity.java) | `id` (UUID), `nombre` (String), `idAplicacion` (UUID), `activo` (boolean), `fechaInicio` (LocalDateTime), `fechaFinal` (LocalDateTime) |
| `FuncionalidadEntity` | [`FuncionalidadEntity.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/FuncionalidadEntity.java) | `id` (UUID), `nombre` (String), `idModulo` (UUID), `activo` (boolean), `fechaInicio` (LocalDateTime), `fechaFinal` (LocalDateTime) |
| `ParametroEntity` | [`ParametroEntity.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/entity/ParametroEntity.java) | `id` (UUID), `nombre` (String), `idFuncionalidad` (UUID), `idTipoParametro` (UUID), `activo` (boolean) |

---

## 7. Arquitectura de Eventos (SSE)

### Flujo de Eventos

El sistema utiliza **Server-Sent Events (SSE)** para notificar en tiempo real las operaciones de creación sobre las entidades principales. Cada recurso expone un endpoint `/events` que devuelve un stream de eventos.

### Flujo General de Publicación de Eventos

```
Controller (POST) → Interactor → UseCase → Domain → Repository → Publisher.sendEvent() → SSE Stream
```

### Eventos por Recurso

| Recurso | Evento | Tipo | Publisher |
|---------|--------|------|-----------|
| Organización | `CrearOrganizacionEvent` | `CREATED` | `CrearOrganizacionPublisher` |
| Aplicación | `CrearAplicacionEvent` | `CREATED` | `CrearAplicacionPublisher` |
| Módulo | `CrearModuloEvent` | `CREATED` | `CrearModuloPublisher` |
| Funcionalidad | `CrearFuncionalidadEvent` | `CREATED` | `CrearFuncionalidadPublisher` |
| Parámetro | `CrearParametroEvent` | `CREATED` | `CrearParametroPublisher` |
| Parámetro | `ActualizarParametroEvent` | `UPDATED` | `ActualizarParametroPublisher` |
| Parámetro | `EliminarParametroEvent` | `DELETED` | `EliminarParametroPublisher` |

### Interfaz Publisher

[`Publisher<T>`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/publisher/Publisher.java)

```java
public interface Publisher<T> {
    void sendEvent(T event);
    Flux<T> getStream();
}
```

---

## 8. Resumen de URLs del API

### Organizaciones

| Método | URL | Acción |
|--------|-----|--------|
| `POST` | `/catalogo-parametros/api/v1/organizaciones` | Crear organización |
| `GET` | `/catalogo-parametros/api/v1/organizaciones/events` | Stream de eventos SSE |

### Aplicaciones

| Método | URL | Acción |
|--------|-----|--------|
| `POST` | `/catalogo-parametros/api/v1/aplicaciones` | Crear aplicación |
| `GET` | `/catalogo-parametros/api/v1/aplicaciones/events` | Stream de eventos SSE |

### Módulos

| Método | URL | Acción |
|--------|-----|--------|
| `POST` | `/catalogo-parametros/api/v1/modulos` | Crear módulo |
| `GET` | `/catalogo-parametros/api/v1/modulos/events` | Stream de eventos SSE |

### Funcionalidades

| Método | URL | Acción |
|--------|-----|--------|
| `POST` | `/catalogo-parametros/api/v1/funcionalidades` | Crear funcionalidad |
| `GET` | `/catalogo-parametros/api/v1/funcionalidades` | Consultar todas las funcionalidades |
| `GET` | `/catalogo-parametros/api/v1/funcionalidades/{id}` | Consultar funcionalidad por ID |
| `GET` | `/catalogo-parametros/api/v1/funcionalidades/events` | Stream de eventos SSE |

### Parámetros

| Método | URL | Acción |
|--------|-----|--------|
| `POST` | `/catalogo-parametros/api/v1/parametros` | Crear parámetro |
| `PUT` | `/catalogo-parametros/api/v1/parametros/{id}` | Actualizar parámetro |
| `DELETE` | `/catalogo-parametros/api/v1/parametros/{id}` | Eliminar parámetro |
| `GET` | `/catalogo-parametros/api/v1/parametros` | Consultar todos los parámetros |
| `GET` | `/catalogo-parametros/api/v1/parametros/{id}` | Consultar parámetro por ID |
| `GET` | `/catalogo-parametros/api/v1/parametros/events` | Stream de eventos SSE (crear, actualizar, eliminar) |

---

## 9. Estructura de Response General

### Response Base

[`Response.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/primaryadapters/response/Response.java)

```java
public class Response {
    private List<String> mensajes = new ArrayList<>();
    // getMensajes()
}
```

### ParametroResponse

[`ParametroResponse.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/primaryadapters/response/parametro/ParametroResponse.java)

```java
public final class ParametroResponse extends Response {
    private List<ParametroEntity> parametros = new ArrayList<>();
    // getParametros()
}
```

### FuncionalidadResponse

[`FuncionalidadResponse.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/primaryadapters/response/funcionalidad/FuncionalidadResponse.java)

```java
public final class FuncionalidadResponse extends Response {
    private List<FuncionalidadEntity> funcionalidades = new ArrayList<>();
    // getFuncionalidades()
}
```

---

## 10. Repositorios (Secondary Adapters)

Todos los repositorios extienden la interfaz `ReactiveCrudRepository` de Spring Data y están implementados para **SurrealDB** como base de datos.

| Repositorio | Interface | Implementación |
|-------------|-----------|----------------|
| `AplicacionRepository` | [`AplicacionRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/repository/AplicacionRepository.java) | [`SurrealDbAplicacionRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/secondaryadapters/repository/aplicacion/SurrealDbAplicacionRepository.java) |
| `FuncionalidadRepository` | [`FuncionalidadRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/repository/FuncionalidadRepository.java) | [`SurrealDbFuncionalidadRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/secondaryadapters/repository/funcionalidad/SurrealDbFuncionalidadRepository.java) |
| `ModuloRepository` | [`ModuloRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/repository/ModuloRepository.java) | [`SurrealDbModuloRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/secondaryadapters/repository/modulo/SurrealDbModuloRepository.java) |
| `OrganizacionRepository` | [`OrganizacionRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/repository/OrganizacionRepository.java) | [`SurrealDbOrganizacionRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/secondaryadapters/repository/organizacion/SurrealDbOrganizacionRepository.java) |
| `ParametroRepository` | [`ParametroRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/application/secondaryports/repository/ParametroRepository.java) | [`SurrealDbParametroRepository.java`](src/main/java/co/edu/uco/CatalogoParametrosUcoLab/infraestructure/secondaryadapters/repository/parametro/SurrealDbParametroRepository.java) |

---

## 11. Flujo de Ejecución por Funcionalidad

### Flujo de Creación (ej. Crear Organización)

```
1. Cliente envia POST /catalogo-parametros/api/v1/organizaciones con JSON body
2. AplicacionController.crear() recibe el request
3. CrearOrganizacionInteractor.execute(dto) es invocado
4. CrearOrganizacionInteractorImpl ejecuta el use case
5. CrearOrganizacionImpl ejecuta la lógica de negocio:
   a. CrearOrganizacionRuleValidatorImpl valida las reglas de dominio
   b. Si todas las reglas pasan, se crea la OrganizacionEntity
   c. Se persiste via OrganizacionRepository.save()
   d. Se publica un CrearOrganizacionEvent via CrearOrganizacionPublisher.sendEvent()
6. ResponseEntity con "Organizacion creada exitosamente." y status 201 CREATED es retornado
```

### Flujo de Consulta (ej. Consultar Funcionalidades por ID)

```
1. Cliente envia GET /catalogo-parametros/api/v1/funcionalidades/{id}
2. FuncionalidadController.consultarFuncionalidadesPorId(id) recibe el request
3. ConsultarFuncionalidadInteractor.execute(id) es invocado
4. ConsultarFuncionalidadInteractorImpl ejecuta el use case
5. Consulta la FuncionalidadRepository por id
6. Retorna FuncionalidadResponse con la lista de funcionalidades encontradas
```

### Flujo de Eventos SSE

```
1. Cliente abre conexión GET /catalogo-parametros/api/v1/{recurso}/events
2. El Controller retorna Flux<ServerSentEvent<T>>
3. Cada vez que un Publisher.sendEvent() es llamado, el evento es emitido al stream
4. El cliente recibe el evento en tiempo real via SSE
```

---

*Documentación generada para el proyecto CatalogoParametrosUcoLab.*