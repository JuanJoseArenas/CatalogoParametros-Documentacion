# Historia de Usuario: Consultar Tipo de Parámetro

## ID
HU-TPAR-003

## Título
Consultar Tipo de Parámetro

## Descripción
Como usuario del sistema, quiero poder consultar los tipos de parámetros registrados en el catálogo, para que pueda buscar y revisar la información de los tipos de parámetros disponibles.

## Criterios de Aceptación

### Criterio 1: Consultar todos los tipos de parámetro
- **Dado** que existen tipos de parámetro registrados en el sistema
- **Cuando** el usuario solicita consultar todos los tipos de parámetro
- **Entonces** el sistema retorna la lista completa de tipos de parámetro disponibles

### Criterio 2: Consultar tipo de parámetro por identificador
- **Dado** que el usuario proporciona el identificador de un tipo de parámetro existente
- **Cuando** el usuario solicita consultar el tipo de parámetro por su identificador
- **Entonces** el sistema retorna la información del tipo de parámetro solicitado

### Criterio 3: Consultar tipo de parámetro inexistente
- **Dado** que el usuario proporciona un identificador de tipo de parámetro que no existe
- **Cuando** el usuario solicita consultar el tipo de parámetro por su identificador
- **Entonces** el sistema retorna un mensaje indicando que no se encontró el tipo de parámetro

### Criterio 4: Consultar tipos de parámetro con filtro por nombre
- **Dado** que el usuario proporciona un criterio de búsqueda por nombre
- **Cuando** el usuario solicita consultar tipos de parámetro
- **Entonces** el sistema retorna solo los tipos de parámetro que coinciden con el criterio de búsqueda

## Reglas de Negocio
1. La consulta de tipos de parámetro debe retornar solo tipos de parámetro activos por defecto.
2. La consulta por identificador debe retornar exactamente un resultado o ninguno.
3. La consulta con filtro debe ser case-insensitive.
4. Los resultados deben incluir la información básica del tipo de parámetro: identificador, nombre y descripción.

## Actor Principal
Usuario del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.

## Postcondiciones
- Se retorna la lista de tipos de parámetro que cumplen con los criterios de búsqueda.
- No se modifican datos en el sistema.