# Historia de Usuario: Eliminar Metadato

## ID
HU-MET-002

## Título
Eliminar Metadato

## Descripción
Como administrador del sistema, quiero poder eliminar un metadato existente, para que los usuarios puedan remover metadatos que ya no son necesarios o están obsoletos.

## Criterios de Aceptación

### Criterio 1: Eliminación exitosa
- **Dado** que el usuario proporciona el identificador de un metadato existente
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el metadato es eliminado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Metadato debe existir
- **Dado** que el usuario proporciona un identificador de metadato que no existe
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el metadato no existe

## Reglas de Negocio
1. Solo se pueden eliminar metadatos que existan previamente en el sistema.
2. La eliminación de un metadato es una operación irreversible.
3. Al eliminar un metadato, se genera un evento de eliminación.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- El metadato a eliminar debe existir previamente.

## Postcondiciones
- El metadato queda eliminado del sistema.
- Se genera un evento de eliminación de metadato.