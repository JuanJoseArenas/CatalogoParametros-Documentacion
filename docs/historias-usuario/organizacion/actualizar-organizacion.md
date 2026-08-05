# Historia de Usuario: Actualizar Organización

## ID
HU-ORG-002

## Título
Actualizar Organización

## Descripción
Como administrador del sistema, quiero poder actualizar los datos de una organización existente, para que los usuarios puedan mantener la información de la organización vigente y correcta.

## Criterios de Aceptación

### Criterio 1: Actualización exitosa
- **Dado** que el usuario ha proporcionado el identificador de una organización existente y los datos actualizados válidos
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** la organización es actualizada exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Organización debe existir
- **Dado** que el usuario proporciona un identificador de organización que no existe
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la organización no existe

### Criterio 3: Nombre de organización obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para la organización
- **Cuando** el usuario envía la solicitud de actualización
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 4: Nombre de organización no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 5: Nombre de organización ya existe (para otra organización)
- **Dado** que ya existe otra organización con el mismo nombre
- **Cuando** el usuario intenta actualizar una organización con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

## Reglas de Negocio
1. El nombre de la organización no puede estar vacío.
2. El nombre de la organización no puede ser nulo.
3. El nombre de la organización debe ser único dentro del sistema.
4. Solo se pueden actualizar organizaciones que existan previamente.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- La organización a actualizar debe existir previamente.

## Postcondiciones
- La organización queda actualizada en el sistema con los nuevos datos.
- Se genera un evento de actualización de organización.