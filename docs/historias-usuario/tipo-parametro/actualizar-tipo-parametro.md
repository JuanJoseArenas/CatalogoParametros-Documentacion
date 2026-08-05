# Historia de Usuario: Actualizar Tipo de Parámetro

## ID
HU-TPAR-002

## Título
Actualizar Tipo de Parámetro

## Descripción
Como administrador del sistema, quiero poder actualizar los datos de un tipo de parámetro existente, para que los usuarios puedan mantener la información de los tipos de parámetros vigente y correcta.

## Criterios de Aceptación

### Criterio 1: Actualización exitosa
- **Dado** que el usuario ha proporcionado el identificador de un tipo de parámetro existente y los datos actualizados válidos
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el tipo de parámetro es actualizado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Tipo de parámetro debe existir
- **Dado** que el usuario proporciona un identificador de tipo de parámetro que no existe
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el tipo de parámetro no existe

### Criterio 3: Nombre de tipo de parámetro obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para el tipo de parámetro
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 4: Nombre de tipo de parámetro no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 5: Nombre de tipo de parámetro ya existe (para otro tipo)
- **Dado** que ya existe otro tipo de parámetro con el mismo nombre
- **Cuando** el usuario intenta actualizar un tipo de parámetro con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

## Reglas de Negocio
1. El nombre del tipo de parámetro no puede estar vacío.
2. El nombre del tipo de parámetro no puede ser nulo.
3. El nombre del tipo de parámetro debe ser único dentro del sistema.
4. Solo se pueden actualizar tipos de parámetro que existan previamente.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- El tipo de parámetro a actualizar debe existir previamente.

## Postcondiciones
- El tipo de parámetro queda actualizado en el sistema con los nuevos datos.
- Se genera un evento de actualización de tipo de parámetro.