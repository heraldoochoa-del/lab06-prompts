# Tarea: Mi prompt profesional

## Funcionalidad elegida

Un **CRUD de productos** para el inventario de una tienda pequeña: crear, leer, actualizar y eliminar productos (nombre, precio, stock, categoría).

## Versión 1: prompt básico

```text
Hazme un CRUD de productos.
```

**Qué cambié:** nada todavía, es el punto de partida.
**Por qué:** quería ver qué asumía la IA sin ninguna guía.
**Qué mejoró en la respuesta:** nada — la respuesta fue genérica, eligió un lenguaje y una base de datos al azar, no explicó las validaciones ni el formato de salida, y mezcló backend y frontend sin que se lo pidiera.

## Versión 2

```text
Actúa como desarrollador backend. Necesito un CRUD de productos en Node.js
con Express y una base de datos SQLite. Cada producto tiene: id, nombre,
precio y stock. Incluye las rutas para crear, leer, actualizar y eliminar,
con validación básica de datos (precio y stock no pueden ser negativos).
```

**Qué cambié:** agregué el rol (desarrollador backend), el contexto técnico (Node.js, Express, SQLite), los campos exactos del producto y una restricción de validación.
**Por qué:** en la v1 la IA no tenía marco de referencia y decidía todo por su cuenta; necesitaba fijar el stack y los datos para que la solución fuera consistente.
**Qué mejoró en la respuesta:** el código ya usaba el stack correcto y las validaciones pedidas, pero seguía sin un formato de entrega claro (todo el código junto, sin separar archivos), no traía ejemplos de peticiones/respuestas, y no explicaba cómo manejar errores (por ejemplo, producto no encontrado).

## Versión 3: prompt final

```text
Rol: Actúa como desarrollador backend senior especializado en Node.js.

Instrucción: Crea un CRUD de productos con Express y SQLite. Cada producto
tiene: id (autoincremental), nombre (string), precio (float, mayor a 0) y
stock (entero, mayor o igual a 0). Implementa las 5 rutas REST (crear, leer
todos, leer uno, actualizar, eliminar) con manejo de errores (404 si el
producto no existe, 400 si los datos son inválidos).

Contexto: Es para el inventario de una tienda pequeña que recién está
digitalizando sus procesos, así que el código debe ser simple de mantener
por alguien con conocimientos básicos de Node.js.

Ejemplos:
- Petición: POST /productos { "nombre": "Mouse", "precio": 15.5, "stock": 20 }
  Respuesta: 201 { "id": 1, "nombre": "Mouse", "precio": 15.5, "stock": 20 }
- Petición: GET /productos/99 (no existe)
  Respuesta: 404 { "error": "Producto no encontrado" }

Formato: Entrega el código separado en dos archivos (db.js para la conexión
y routes.js para las rutas), cada uno dentro de su propio bloque de código,
con un breve comentario arriba de cada ruta explicando qué hace.

Restricción: No uses librerías externas de ORM (como Sequelize); trabaja
directamente con el driver de SQLite.
```

**Qué cambié:** organicé el prompt en los 5 componentes explícitos, agregué ejemplos concretos de petición/respuesta, definí el formato exacto de entrega y sumé una restricción técnica.
**Por qué:** sin ejemplos la IA interpretaba libremente los códigos de estado HTTP y sin formato entregaba un solo bloque de código desordenado; la restricción evita que use un ORM que complicaría el mantenimiento pedido en el contexto.
**Qué mejoró en la respuesta:** el resultado llegó ya separado en los dos archivos pedidos, con los códigos de estado exactos de los ejemplos, comentarios por ruta y sin ninguna dependencia externa de ORM.

## Componentes del prompt final

| Componente   | Contenido en el prompt final                                                                 |
|--------------|------------------------------------------------------------------------------------------------|
| Rol          | Desarrollador backend senior especializado en Node.js                                          |
| Instrucción  | Crear un CRUD de productos con Express y SQLite, con las 5 rutas REST y manejo de errores      |
| Contexto     | Inventario de una tienda pequeña, código simple de mantener                                    |
| Ejemplos     | Petición/respuesta de creación exitosa y de error 404                                          |
| Formato      | Dos archivos (db.js y routes.js), cada uno en su bloque de código, con comentarios por ruta     |

## Evaluación del resultado

| Criterio                                                        | Sí / No |
|-------------------------------------------------------------------|---------|
| ¿El código usa el stack solicitado (Node.js, Express, SQLite)?    | Sí      |
| ¿Respeta el formato de entrega pedido (dos archivos separados)?  | Sí      |
| ¿Maneja los errores según los ejemplos (404, 400)?                | Sí      |
| ¿Evita librerías de ORM como se restringió?                       | Sí      |

## Errores que evité

- **Ser demasiado general:** en la v1 el prompt no especificaba lenguaje, base de datos ni estructura de datos, lo que dejaba a la IA decidir todo por su cuenta. Lo evité en la v3 fijando el stack exacto (Node.js, Express, SQLite) y los campos del producto.
- **No indicar el formato:** en la v2 pedí el CRUD pero no dije cómo quería recibir el código, así que llegó todo mezclado en un solo bloque. En la v3 especifiqué exactamente en qué archivos y con qué comentarios debía entregarse.