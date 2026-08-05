# Historia de Usuario: Crear Metadato

## ID
HU-MET-001

## Título
Crear Metadato

## Descripción
Como administrador del sistema, quiero poder crear un nuevo metadato en el catálogo de parámetros, para que los usuarios puedan registrar información adicional y descriptiva asociada a los parámetros.

## Criterios de Aceptación

### Criterio 1: Creación exitosa
- **Dado** que el usuario ha proporcionado los datos válidos de un nuevo metadato (clave, valor)
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el metadato es creado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Clave de metadato obligatoria
- **Dado** que el usuario no ha proporcionado una clave para el metadato
- **Cuando** el usuario envía la solicitud de creación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la clave es obligatoria

### Criterio 3: Clave de metadato no puede ser nula
- **Dado** que el usuario envía una solicitud con clave nula
- **Cuando** el sistema procesa la solicitud
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error

### Criterio 4: Clave de metadato ya existe
- **Dado** que ya existe un metadato con la misma clave
- **Cuando** el usuario intenta crear un nuevo metadato con esa clave
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la clave ya está en uso

## Reglas de Negocio
1. La clave del metadato no puede estar vacía.
2. La clave del metadato no puede ser nula.
3. La clave del metadato debe ser única dentro del sistema.
4. El metadato se crea en estado activo por defecto.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.

## Postcondiciones
- El metadato queda registrado en el sistema con un identificador único.
- Se genera un evento de creación de metadato.