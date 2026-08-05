# Historia de Usuario: Crear Tipo de Parámetro

## ID
HU-TPAR-001

## Título
Crear Tipo de Parámetro

## Descripción
Como administrador del sistema, quiero poder crear un nuevo tipo de parámetro, para que los usuarios puedan clasificar y categorizar los parámetros según su naturaleza o propósito.

## Criterios de Aceptación

### Criterio 1: Creación exitosa
- **Dado** que el usuario ha proporcionado los datos válidos de un nuevo tipo de parámetro (nombre, descripción)
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el tipo de parámetro es creado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Nombre de tipo de parámetro obligatorio
- **Dado** que el usuario no ha proporcionado un nombre para el tipo de parámetro
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre es obligatorio

### Criterio 3: Nombre de tipo de parámetro no puede ser nulo
- **Dado** que el usuario envía una solicitud con nombre nulo
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 4: Nombre de tipo de parámetro ya existe
- **Dado** que ya existe un tipo de parámetro con el mismo nombre
- **Cuando** el usuario intenta crear un nuevo tipo de parámetro con ese nombre
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el nombre ya está en uso

## Reglas de Negocio
1. El nombre del tipo de parámetro no puede estar vacío.
2. El nombre del tipo de parámetro no puede ser nulo.
3. El nombre del tipo de parámetro debe ser único dentro del sistema.
4. El tipo de parámetro se crea en estado activo por defecto.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.

## Postcondiciones
- El tipo de parámetro queda registrado en el sistema con un identificador único.
- Se genera un evento de creación de tipo de parámetro.