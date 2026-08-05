# Historia de Usuario: Eliminar Tipo de Parámetro

## ID
HU-TPAR-004

## Título
Eliminar Tipo de Parámetro

## Descripción
Como administrador del sistema, quiero poder eliminar un tipo de parámetro existente, para que los usuarios puedan remover tipos de parámetros que ya no son necesarios o están obsoletos.

## Criterios de Aceptación

### Criterio 1: Eliminación exitosa
- **Dado** que el usuario proporciona el identificador de un tipo de parámetro existente que no está siendo utilizado por ningún parámetro
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el tipo de parámetro es eliminado exitosamente y se retorna un mensaje de confirmación

### Criterio 2: Tipo de parámetro debe existir
- **Dado** que el usuario proporciona un identificador de tipo de parámetro que no existe
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el tipo de parámetro no existe

### Criterio 3: Tipo de parámetro en uso no puede eliminarse
- **Dado** que el tipo de parámetro a eliminar está siendo utilizado por uno o más parámetros
- **Cuando** el usuario envía la solicitud de eliminación
- **Entonces** el sistema rechaza la solicitud y muestra un mensaje de error indicando que el tipo de parámetro está en uso y no puede ser eliminado

## Reglas de Negocio
1. Solo se pueden eliminar tipos de parámetro que existan previamente en el sistema.
2. Un tipo de parámetro que esté siendo utilizado por algún parámetro no puede ser eliminado.
3. La eliminación de un tipo de parámetro es una operación irreversible.
4. Al eliminar un tipo de parámetro, se genera un evento de eliminación.

## Actor Principal
Administrador del sistema

## Precondiciones
- El usuario debe estar autenticado en el sistema.
- El tipo de parámetro a eliminar debe existir previamente.
- El tipo de parámetro no debe estar siendo utilizado por ningún parámetro.

## Postcondiciones
- El tipo de parámetro queda eliminado del sistema.
- Se genera un evento de eliminación de tipo de parámetro.