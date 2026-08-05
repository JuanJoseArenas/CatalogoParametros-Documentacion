# Historia de Usuario: Actualizar Parámetro

## ID
HU-PAR-002

## Título
Actualizar Parámetro

## Descripción
Como administrador del sistema, quiero poder actualizar los datos de un parámetro existente en el catálogo, para que los usuarios puedan mantener la información del parámetro vigente y correcta.

## Criterios de Aceptación

### Criterio 1: Actualización exitosa
- **Dado** que el usuario ha proporcionado el identificador de un parámetro existente y los datos actualizados válidos
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el parámetro es actualizado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Parámetro debe existir
- **Dado** que el usuario proporciona un identificador de parámetro que no existe
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el parámetro no existe

### Criterio 3: Nombre de parámetro obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para el parámetro
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 4: Nombre de parámetro no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 5: Nombre de parámetro ya existe (para otro parámetro)
- **Dado** que ya existe otro parámetro con el mismo nombre
- **Cuando** el usuario intenta actualizar un parámetro con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

### Criterio 6: Funcionalidad debe existir
- **Dado** que el usuario proporciona un identificador de funcionalidad que no existe
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la funcionalidad no existe

### Criterio 7: Tipo de parámetro debe ser válido
- **Dado** que el usuario proporciona un identificador de tipo de parámetro inválido
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el tipo de parámetro no es válido

### Criterio 8: Formato del nombre válido
- **Dado** que el usuario proporciona un nombre con formato inválido
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el formato del nombre no es válido

## Reglas de Negocio
1. El nombre del parámetro no puede estar vacío.
2. El nombre del parámetro no puede ser nulo.
3. El nombre del parámetro debe ser único dentro del sistema.
4. El nombre del parámetro debe cumplir con el formato establecido.
5. La funcionalidad asociada al parámetro debe existir previamente en el sistema.
6. El tipo de parámetro asociado debe ser válido.
7. Solo se pueden actualizar parámetros que existan previamente.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- El parámetro a actualizar debe existir previamente.
- La funcionalidad referenciada debe existir previamente.
- El tipo de parámetro referenciado debe existir previamente.

## Postcondiciones
- El parámetro queda actualizado en el sistema con los nuevos datos.
- Se genera un evento de actualización de parámetro.