# Historia de Usuario: Consultar Parámetro

## ID
HU-PAR-003

## Título
Consultar Parámetro

## Descripción
Como usuario del sistema, quiero poder consultar los parámetros registrados en el catálogo, para que pueda buscar y revisar la información de los parámetros disponibles.

## Criterios de Aceptación

### Criterio 1: Consultar todos los parámetros
- **Dado** que existen parámetros registrados en el sistema
- **Cuando** el usuario solicita consultar todos los parámetros
- **Entonces** el sistema retorna la lista completa de parámetros disponibles

### Criterio 2: Consultar parámetro por identificador
- **Dado** que el usuario proporciona el identificador de un parámetro existente
- **Cuando** el usuario solicita consultar el parámetro por su identificador
- **Entonces** el sistema retorna la información del parámetro solicitado

### Criterio 3: Consultar parámetro inexistente
- **Dado** que el usuario proporciona un identificador de parámetro que no existe
- **Cuando** el usuario solicita consultar el parámetro por su identificador
- **Entonces** el sistema retorna un mensaje indicando que no se encontró el parámetro

### Criterio 4: Consultar parámetros con filtro por nombre
- **Dado** que el usuario proporciona un criterio de búsqueda por nombre
- **Cuando** el usuario solicita consultar parámetros
- **Entonces** el sistema retorna solo los parámetros que coinciden con el criterio de búsqueda

## Reglas de Negocio
1. La consulta de parámetros debe retornar solo parámetros activos por defecto.
2. La consulta por identificador debe retornar exactamente un resultado o ninguno.
3. La consulta con filtro debe ser case-insensitive.
4. Los resultados deben incluir la información básica del parámetro: identificador, nombre, funcionalidad asociada, tipo de parámetro y estado.

## Actor Principal
Usuario del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.

## Postcondiciones
- Se retorna la lista de parámetros que cumplen con los criterios de búsqueda.
- No se modifican datos en el sistema.