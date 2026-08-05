# Historia de Usuario: Crear Organización

## ID
HU-ORG-001

## Título
Crear Organización

## Descripción
Como administrador del sistema, quiero poder crear una nueva organización en el catálogo de parámetros, para que los usuarios puedan gestionar sus aplicaciones y parámetros dentro de una organización específica.

## Criterios de Aceptación

### Criterio 1: Creación exitosa
- **Dado** que el usuario ha proporcionado los datos válidos de una nueva organización (nombre)
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** la organización es creada exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Nombre de organización obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para la organización
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 3: Nombre de organización no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 4: Nombre de organización ya existe
- **Dado** que ya existe una organización con el mismo nombre
- **Cuando** el usuario intenta crear una nueva organización con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

## Reglas de Negocio
1. El nombre de la organización no puede estar vacío.
2. El nombre de la organización no puede ser nulo.
3. El nombre de la organización debe ser único dentro del sistema.
4. La organización se crea en estado activo por defecto.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.

## Postcondiciones
- La organización queda registrada en el sistema con un identificador único.
- Se genera un evento de creación de organización.