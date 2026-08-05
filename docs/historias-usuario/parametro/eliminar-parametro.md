# Historia de Usuario: Eliminar Parámetro

## ID
HU-PAR-004

## Título
Eliminar Parámetro

## Descripción
Como administrador del sistema, quiero poder eliminar un parámetro existente del catálogo, para que los usuarios puedan remover parámetros que ya no son necesarios o están obsoletos.

## Criterios de Aceptación

### Criterio 1: Eliminación exitosa
- **Dado** que el usuario proporciona el identificador de un parámetro existente que no está siendo utilizado por ninguna funcionalidad
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el parámetro es eliminado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Parámetro debe existir
- **Dado** que el usuario proporciona un identificador de parámetro que no existe
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el parámetro no existe

### Criterio 3: Parámetro en uso no puede eliminarse
- **Dado** que el parámetro a eliminar está siendo utilizado por una o más funcionalidades
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el parámetro está en uso y no puede ser eliminado

## Reglas de Negocio
1. Solo se pueden eliminar parámetros que existan previamente en el sistema.
2. Un parámetro que esté siendo utilizado por alguna funcionalidad no puede ser eliminado.
3. La eliminación de un parámetro es una operación irreversible.
4. Al eliminar un parámetro, se genera un evento de eliminación.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- El parámetro a eliminar debe existir previamente.
- El parámetro no debe estar siendo utilizado por ninguna funcionalidad.

## Postcondiciones
- El parámetro queda eliminado del sistema.
- Se genera un evento de eliminación de parámetro.