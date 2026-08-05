# Historia de Usuario: Eliminar Organización

## ID
HU-ORG-004

## Título
Eliminar Organización

## Descripción
Como administrador del sistema, quiero poder eliminar una organización existente, para que los usuarios puedan remover organizaciones que ya no son necesarias o están obsoletas.

## Criterios de Aceptación

### Criterio 1: Eliminación exitosa
- **Dado** que el usuario proporciona el identificador de una organización existente que no está siendo utilizada por ninguna aplicación
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** la organización es eliminada exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Organización debe existir
- **Dado** que el usuario proporciona un identificador de organización que no existe
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la organización no existe

### Criterio 3: Organización en uso no puede eliminarse
- **Dado** que la organización a eliminar está siendo utilizada por una o más aplicaciones
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que la organización está en uso y no puede ser eliminada

## Reglas de Negocio
1. Solo se pueden eliminar organizaciones que existan previamente en el sistema.
2. Una organización que esté siendo utilizada por alguna aplicación no puede ser eliminada.
3. La eliminación de una organización es una operación irreversible.
4. Al eliminar una organización, se genera un evento de eliminación.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- La organización a eliminar debe existir previamente.
- La organización no debe estar siendo utilizada por ninguna aplicación.

## Postcondiciones
- La organización queda eliminada del sistema.
- Se genera un evento de eliminación de organización.