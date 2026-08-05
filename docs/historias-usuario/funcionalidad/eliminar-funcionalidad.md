# Historia de Usuario: Eliminar Funcionalidad

## ID
HU-FUN-004

## Título
Eliminar Funcionalidad

## Descripción
Como administrador del sistema, quiero poder eliminar una funcionalidad existente del catálogo, para que los usuarios puedan remover funcionalidades que ya no son necesarias o están obsoletas.

## Criterios de Aceptación

### Criterio 1: Eliminación exitosa
- **Dado** que el usuario proporciona el identificador de una funcionalidad existente que no está siendo utilizada por ningún parámetro
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** la funcionalidad es eliminada exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Funcionalidad debe existir
- **Dado** que el usuario proporciona un identificador de funcionalidad que no existe
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la funcionalidad no existe

### Criterio 3: Funcionalidad en uso no puede eliminarse
- **Dado** que la funcionalidad a eliminar está siendo utilizada por uno o más parámetros
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la funcionalidad está en uso y no puede ser eliminada

## Reglas de Negocio
1. Solo se pueden eliminar funcionalidades que existan previamente en el sistema.
2. Una funcionalidad que esté siendo utilizada por algún parámetro no puede ser eliminada.
3. La eliminación de una funcionalidad es una operación irreversible.
4. Al eliminar una funcionalidad, se genera un evento de eliminación.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- La funcionalidad a eliminar debe existir previamente.
- La funcionalidad no debe estar siendo utilizada por ningún parámetro.

## Postcondiciones
- La funcionalidad queda eliminada del sistema.
- Se genera un evento de eliminación de funcionalidad.