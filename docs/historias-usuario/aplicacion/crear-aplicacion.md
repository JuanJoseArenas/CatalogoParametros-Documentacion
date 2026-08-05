# Historia de Usuario: Crear Aplicación

## ID
HU-APL-001

## Título
Crear Aplicación

## Descripción
Como administrador del sistema, quiero poder crear una nueva aplicación en el catálogo de parámetros, para que los usuarios puedan organizar y gestionar sus funcionalidades dentro de una aplicación específica.

## Criterios de Aceptación

### Criterio 1: Creación exitosa
- **Dado** que el usuario ha proporcionado los datos válidos de una nueva aplicación (nombre, organización)
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** la aplicación es creada exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Nombre de aplicación obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para la aplicación
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 3: Nombre de aplicación no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 4: Nombre de aplicación ya existe
- **Dado** que ya existe una aplicación con el mismo nombre
- **Cuando** el usuario intenta crear una nueva aplicación con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

### Criterio 5: Organización debe existir
- **Dado** que el usuario proporciona un identificador de organización que no existe
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la organización no existe

## Reglas de Negocio
1. El nombre de la aplicación no puede estar vacío.
2. El nombre de la aplicación no puede ser nulo.
3. El nombre de la aplicación debe ser único dentro del sistema.
4. La organización asociada a la aplicación debe existir previamente en el sistema.
5. La aplicación se crea en estado activo por defecto.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- La organización referenciada debe existir previamente.

## Postcondiciones
- La aplicación queda registrada en el sistema con un identificador único.
- Se genera un evento de creación de aplicación.