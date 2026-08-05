# Historia de Usuario: Consultar Organización

## ID
HU-ORG-003

## Título
Consultar Organización

## Descripción
Como usuario del sistema, quiero poder consultar las organizaciones registradas en el catálogo de parámetros, para que pueda buscar y revisar la información de las organizaciones disponibles.

## Criterios de Aceptación

### Criterio 1: Consultar todas las organizaciones
- **Dado** que existen organizaciones registradas en el sistema
- **Cuando** el usuario solicita consultar todas las organizaciones
- **Entonces** el sistema retorna la lista completa de organizaciones disponibles

### Criterio 2: Consultar organización por identificador
- **Dado** que el usuario proporciona el identificador de una organización existente
- **Cuando** el usuario solicita consultar la organización por su identificador
- **Entonces** el sistema retorna la información de la organización solicitada

### Criterio 3: Consultar organización inexistente
- **Dado** que el usuario proporciona un identificador de organización que no existe
- **Cuando** el usuario solicita consultar la organización por su identificador
- **Entonces** el sistema retorna un mensaje indicando que no se encontró la organización

### Criterio 4: Consultar organizaciones con filtro por nombre
- **Dado** que el usuario proporciona un criterio de búsqueda por nombre
- **Cuando** el usuario solicita consultar organizaciones
- **Entonces** el sistema retorna solo las organizaciones que coinciden con el criterio de búsqueda

## Reglas de Negocio
1. La consulta de organizaciones debe retornar solo organizaciones activas por defecto.
2. La consulta por identificador debe retornar exactamente un resultado o ninguno.
3. La consulta con filtro debe ser case-insensitive.
4. Los resultados deben incluir la información básica de la organización: identificador, nombre y estado.

## Actor Principal
Usuario del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.

## Postcondiciones
- Se retorna la lista de organizaciones que cumplen con los criterios de búsqueda.
- No se modifican datos en el sistema.