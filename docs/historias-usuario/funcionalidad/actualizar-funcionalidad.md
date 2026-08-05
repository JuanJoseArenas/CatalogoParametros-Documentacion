# Historia de Usuario: Actualizar Funcionalidad

## ID
HU-FUN-002

## Título
Actualizar Funcionalidad

## Descripción
Como administrador del sistema, quiero poder actualizar los datos de una funcionalidad existente en el catálogo, para que los usuarios puedan mantener la información de la funcionalidad vigente y correcta.

## Criterios de Aceptación

### Criterio 1: Actualización exitosa
- **Dado** que el usuario ha proporcionado el identificador de una funcionalidad existente y los datos actualizados válidos
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** la funcionalidad es actualizada exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Funcionalidad debe existir
- **Dado** que el usuario proporciona un identificador de funcionalidad que no existe
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la funcionalidad no existe

### Criterio 3: Nombre de funcionalidad obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para la funcionalidad
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 4: Nombre de funcionalidad no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 5: Nombre de funcionalidad ya existe (para otra funcionalidad)
- **Dado** que ya existe otra funcionalidad con el mismo nombre
- **Cuando** el usuario intenta actualizar una funcionalidad con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

### Criterio 6: Módulo debe existir
- **Dado** que el usuario proporciona un identificador de módulo que no existe
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el módulo no existe

## Reglas de Negocio
1. El nombre de la funcionalidad no puede estar vacío.
2. El nombre de la funcionalidad no puede ser nulo.
3. El nombre de la funcionalidad debe ser único dentro del sistema.
4. El módulo asociado a la funcionalidad debe existir previamente en el sistema.
5. Solo se pueden actualizar funcionalidades que existan previamente.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- La funcionalidad a actualizar debe existir previamente.
- El módulo referenciado debe existir previamente.

## Postcondiciones
- La funcionalidad queda actualizada en el sistema con los nuevos datos.
- Se genera un evento de actualización de funcionalidad.