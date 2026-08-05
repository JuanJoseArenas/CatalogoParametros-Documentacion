# Historia de Usuario: Consultar Funcionalidad

## ID
HU-FUN-003

## Título
Consultar Funcionalidad

## Descripción
Como usuario del sistema, quiero poder consultar las funcionalidades registradas en el catálogo de parámetros, para que pueda buscar y revisar la información de las funcionalidades disponibles.

## Criterios de Aceptación

### Criterio 1: Consultar todas las funcionalidades
- **Dado** que existen funcionalidades registradas en el sistema
- **Cuando** el usuario solicita consultar todas las funcionalidades
- **Entonces** el sistema retorna la lista completa de funcionalidades disponibles

### Criterio 2: Consultar funcionalidad por identificador
- **Dado** que el usuario proporciona el identificador de una funcionalidad existente
- **Cuando** el usuario solicita consultar la funcionalidad por su identificador
- **Entonces** el sistema retorna la información de la funcionalidad solicitada

### Criterio 3: Consultar funcionalidad inexistente
- **Dado** que el usuario proporciona un identificador de funcionalidad que no existe
- **Cuando** el usuario solicita consultar la funcionalidad por su identificador
- **Entonces** el sistema retorna un mensaje indicando que no se encontró la funcionalidad

### Criterio 4: Consultar funcionalidades con filtro por nombre
- **Dado** que el usuario proporciona un criterio de búsqueda por nombre
- **Cuando** el usuario solicita consultar funcionalidades
- **Entonces** el sistema retorna solo las funcionalidades que coinciden con el criterio de búsqueda

## Reglas de Negocio
1. La consulta de funcionalidades debe retornar solo funcionalidades activas por defecto.
2. La consulta por identificador debe retornar exactamente un resultado o ninguno.
3. La consulta con filtro debe ser case-insensitive.
4. Los resultados deben incluir la información básica de la funcionalidad: identificador, nombre, módulo asociado y estado.

## Actor Principal
Usuario del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.

## Postcondiciones
- Se retorna la lista de funcionalidades que cumplen con los criterios de búsqueda.
- No se modifican datos en el sistema.