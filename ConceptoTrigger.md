

![logo cafam](/Imagen1.png)

# Reportes

---

## Presentación

**Nombre del estudiante:** Gabriela Bautista Soriano  
**Asignatura:** DA  
**Nombre del docente:** Víctor Recio  
**Tema:** Reportes  
**Fecha:** 30/5/2025  

---

#
#
#
#
#

# Documentación sobre Triggers en Bases de Datos


## 1. ¿Qué es un Trigger?
Un **Trigger** (o disparador) es un objeto de base de datos que se asocia a una tabla o vista y se ejecuta automáticamente cuando ocurre un evento específico. Es una forma de automatizar tareas, asegurando que ciertas acciones se realicen en respuesta a modificaciones en los datos.

---

## 2. ¿Para qué sirve un Trigger?
Los Triggers sirven para:

- Mantener la integridad de los datos.
- Implementar reglas de negocio complejas.
- Automatizar tareas como auditorías, cálculos o sincronización entre tablas.
- Realizar validaciones o transformaciones de datos antes o después de una operación.

---

## 3. ¿Cuándo se puede usar un Trigger?
Los Triggers se pueden usar en situaciones como:

- Registrar un historial de cambios en una tabla (auditoría).
- Validar que los datos cumplen ciertas reglas antes de ser insertados.
- Actualizar automáticamente datos relacionados en otras tablas.
- Evitar operaciones no permitidas.

---

## 4. Estructura de un Trigger
Un Trigger sigue esta estructura general:

```sql
CREATE TRIGGER nombre_del_trigger
ON tabla_o_vista
AFTER | INSTEAD OF [INSERT, UPDATE, DELETE]
AS
BEGIN
END
```

### Elementos principales:
- `ON`: Define sobre qué tabla o vista actúa el Trigger.
- `AFTER` o `INSTEAD OF`: Determina cuándo se ejecuta el Trigger.
- `[INSERT, UPDATE, DELETE]`: Especifica los eventos que activan el Trigger.
- `AS` y `BEGIN-END`: Contienen el código del Trigger.

---

## 5. Tipos de Trigger

1. **AFTER Trigger**:
   - Se ejecuta después de que la operación (INSERT, UPDATE o DELETE) se complete exitosamente.

2. **INSTEAD OF Trigger**:
   - Se ejecuta en lugar de la operación que activó el evento.

---

## 6. ¿Cuándo ejecuta su acción un Trigger?
Un Trigger ejecuta su acción automáticamente cuando ocurre uno de los eventos definidos (INSERT, UPDATE o DELETE) en la tabla o vista asociada.

- **AFTER Trigger**: Después de que la operación haya tenido éxito.
- **INSTEAD OF Trigger**: En lugar de ejecutar la operación que lo activó.

---

## 7. Ejemplo de un Trigger

```sql
CREATE TRIGGER tr_auditoria_inserciones
ON Clientes
AFTER INSERT
AS
BEGIN
    INSERT INTO Auditoria (Evento, Fecha, Detalle)
    SELECT 'INSERT', GETDATE(), 'Cliente insertado con ID ' + CAST(Inserted.ID AS VARCHAR)
    FROM Inserted;
END;
```

Este Trigger registra automáticamente un evento en una tabla de auditoría cada vez que se inserta un nuevo cliente.

---

## 8. Trigger Marketing

En marketing digital, un Trigger se refiere a un evento o acción que activa una respuesta automatizada, como enviar un correo electrónico o notificación.

### Ejemplo:
- Cuando un cliente abandona un carrito de compras, se puede activar un Trigger que envíe un recordatorio por correo electrónico.

---

## 9. ¿Cómo hacer un Trigger?

### Pasos generales:
1. **Definir el objetivo**: ¿Qué deseas automatizar o controlar?
2. **Seleccionar la tabla**: ¿Dónde ocurrirá el evento?
3. **Determinar el evento**: ¿Es un INSERT, UPDATE o DELETE?
4. **Escribir el código SQL**: Implementar la lógica dentro del Trigger.
5. **Probar el Trigger**: Asegurarse de que cumple con los requisitos.

---

## 10. Características de un Trigger

- Son específicos de la tabla o vista.
- Se ejecutan automáticamente.
- Pueden ser complejos, incluyendo transacciones y manejo de errores.
- No se pueden llamar directamente.
- Pueden afectar el rendimiento si no se diseñan correctamente.

---

## 11. Desventajas de un Trigger

- **Rendimiento**: Pueden ralentizar las operaciones si contienen lógica compleja.
- **Depuración**: Son difíciles de depurar y rastrear.
- **Visibilidad**: Su ejecución es implícita, lo que dificulta el seguimiento.
- **Mantenimiento**: Los cambios en la lógica pueden requerir ajustes complejos.

---

## 12. Sustitutos de los Triggers en otras bases de datos

- **Procedimientos almacenados**: Ejecutados manualmente o mediante programación.
- **Funciones**: Utilizadas dentro de consultas o procedimientos.
- **Jobs**: Programas que realizan tareas automatizadas en un horario.

### Ejemplo:
En MongoDB, los Triggers pueden sustituirse por funciones de monitoreo (`change streams`).
