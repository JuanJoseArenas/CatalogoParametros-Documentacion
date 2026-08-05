# Historia de Usuario: Crear Parámetro

## ID
HU-PAR-001

## Título
Crear Parámetro

## Descripción
Como administrador del sistema, quiero poder crear un nuevo parámetro en el catálogo, para que los usuarios puedan registrar y gestionar valores configurables asociados a una funcionalidad y tipo de parámetro específico.

## Criterios de Aceptación

### Criterio 1: Creación exitosa
- **Dado** que el usuario ha proporcionado los datos válidos de un nuevo parámetro (nombre, funcionalidad, tipo de parámetro)
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el parámetro es creado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Nombre de parámetro obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para el parámetro
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 3: Nombre de parámetro no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 4: Nombre de parámetro ya existe
- **Dado** que ya existe un parámetro con el mismo nombre
- **Cuando** el usuario intenta crear un nuevo parámetro con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

### Criterio 5: Funcionalidad debe existir
- **Dado** que el usuario proporciona un identificador de funcionalidad que no existe
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la funcionalidad no existe

### Criterio 6: Tipo de parámetro debe ser válido
- **Dado** que el usuario proporciona un identificador de tipo de parámetro inválido
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el tipo de parámetro no es válido

### Criterio 7: Formato del nombre válido
- **Dado** que el usuario proporciona un nombre con formato inválido
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el formato del nombre no es válido

### Criterio 8: Longitud del nombre válida
- **Dado** que el usuario proporciona un nombre que excede la longitud permitida
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la longitud del nombre no es válida

## Reglas de Negocio
1. El nombre del parámetro no puede estar vacío.
2. El nombre del parámetro no puede ser nulo.
3. El nombre del parámetro debe ser único dentro del sistema.
4. El nombre del parámetro debe cumplir con el formato establecido.
5. La longitud del nombre del parámetro debe estar dentro del rango permitido.
6. La funcionalidad asociada al parámetro debe existir previamente en el sistema.
7. El tipo de parámetro asociado debe ser válido.
8. El parámetro se crea en estado activo por defecto.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- La funcionalidad referenciada debe existir previamente.
- El tipo de parámetro referenciado debe existir previamente.

## Postcondiciones
- El parámetro queda registrado en el sistema con un identificador único.
- Se genera un evento de creación de parámetro.