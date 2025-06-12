# 🎢 Parque Nicole - Diseño de Base de Datos NoSQL (MongoDB)

### Nombres de los Integrantes:
Juan David Bermeo Castro
Daniel Arauz


## 📂 Colección: `zonas`

### Atributos Propuestos:
- `_id: ObjectId`
- `nombre: String`
- `descripcion: String`

### Relaciones:
- No se incrustan atracciones, se mantiene la referencia desde `atracciones`.

### Justificación:
Se evita incrustar porque las atracciones pueden cambiar frecuentemente y deben poder consultarse individualmente.

---

## 📂 Colección: `visitantes`

### Atributos Propuestos:
- `_id: ObjectId`
- `nombre: String`
- `apellido: String`
- `fecha_nacimiento: Date`
- `email: String`
- `historial_visitas: [Date]`

### Relaciones:
- Visitante → Ticket: **Uno a Muchos**

### Estrategia:
Los tickets referencian al visitante mediante su `_id`.

### Justificación:
Los tickets pueden ser grandes y frecuentes, y es mejor almacenarlos como documentos independientes para facilitar el control de fechas y tipos.

---

## 📂 Colección: `tickets`

### Atributos Propuestos:
- `_id: ObjectId`
- `tipo: String`
- `precio: Number`
- `fecha_compra: Date`
- `fecha_validez: Date`
- `visitante_id: ObjectId`

### Justificación:
Referencia simple al visitante, útil para filtrar por tickets o analizar comportamiento del cliente.

---

## 📂 Colección: `empleados`

### Atributos Propuestos:
- `_id: ObjectId`
- `nombre: String`
- `apellido: String`
- `cargo: String`
- `horario_trabajo: String`
- `atracciones_asignadas: [ObjectId]`

### Relaciones:
- Empleado → Atracción: **Muchos a Muchos**  
  (Un empleado puede manejar varias atracciones y viceversa en diferentes turnos)

### Estrategia:
Referencia.

### Justificación:
Flexibilidad para asignar y reestructurar asignaciones fácilmente.

---

## 📂 Colección: `eventos`

### Atributos Propuestos:
- `_id: ObjectId`
- `nombre: String`
- `descripcion: String`
- `horario: Date`
- `ubicacion_tipo: String` (`zona` o `atraccion`)
- `ubicacion_id: ObjectId`
- `empleados_responsables: [ObjectId]`

### Justificación:
Uso de referencia para ubicar fácilmente la zona o atracción asociada, y los empleados responsables.  
Permite mantener independencia de cambios en los datos.

---

## 📂 Colección: `mantenimientos`

### Atributos Propuestos:
- `_id: ObjectId`
- `fecha: Date`
- `descripcion: String`
- `costo: Number`
- `atraccion_id: ObjectId`
- `empleados: [ObjectId]`

### Justificación:
Se referencia tanto a atracciones como empleados responsables para mantener trazabilidad histórica.

---

## ✅ Conclusiones y Desafíos

El diseño de esta base de datos NoSQL para el **Parque Nicole** busca maximizar el rendimiento y la flexibilidad mediante el uso estratégico de **incrustación (embedding)** y **referencias (referencing)**.  
Se optó principalmente por **referencing** para relaciones entre entidades que cambian con frecuencia o que requieren independencia para su consulta.

Las decisiones se basaron en patrones comunes de modelado en MongoDB y las necesidades operativas de un parque de diversiones.

### Desafíos encontrados:

- Decidir cuándo incrustar y cuándo referenciar (especialmente con listas como atracciones por zona o empleados por evento).
- Asegurar que las relaciones muchos-a-muchos se mantuvieran eficientes en consultas futuras.

---

## 📁 Archivos

Todos los documentos `.json` de inserción están disponibles en el archivo incluido en este repositorio.


![Diagrama](./Diagrama.png)

