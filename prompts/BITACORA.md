# Bitacora de prompts

Laboratorio 06: Fundamentos de Ingenieria de Prompts.

Herramienta de IA usada: Gemini

## Ejercicio 2: Tokens y ventana de contexto

### Registro de Tokens

| Texto | Caracteres | Tokens |
|---|---|---|
| Los estudiantes programan en Java. | 35 | 7 |
| The students program in Java. | 30 | 6 |
| desafortunadamente | 18 | 6 |

### 6. Explicación de la ventana de contexto

- **Dentro del mismo chat (Paso 4):** La IA respondió correctamente que la aplicación se llama TiendaTec y usa Java Swing porque la información formaba parte del historial guardado en su ventana de contexto activa.
- **En un chat nuevo (Paso 5):** La IA no pudo responder o indicó no tener esa información, ya que un chat nuevo inicia con la ventana de contexto completamente limpia y sin acceso a mensajes de otras sesiones.

## Ejercicio 3: Temperatura
### Registro de Resultados del Simulador

| Temperatura | % de BiblioTec | Nombres en los 5 intentos |
|---|---|---|
| 0 | 100.0% | BiblioTec, BiblioTec, BiblioTec, BiblioTec, BiblioTec |
| 0.5 | 62.2% | BiblioTec, LibroYa, BiblioTec, PrestaLibro, BiblioTec |
| 1 | 42.2% | BiblioTec, PrestaLibro, LibroYa, LectoGo, BiblioTec |
| 1.8 | 32.6% | LibroYa, LectoGo, NubeDeTinta, BiblioTec, PaginaLibre |

### Análisis del comportamiento
- Al aumentar la temperatura, la probabilidad asignada a la opción principal disminuye y los porcentajes se distribuyen entre las demás alternativas, generando respuestas más variadas y menos predecibles en cada intento.
- El simulador nunca inventa un nombre nuevo porque el modelo solo selecciona elementos existentes dentro de su vocabulario u opciones predefinidas; la temperatura únicamente cambia la probabilidad de elección entre lo que ya conoce, sin añadir conocimiento externo.

## Ejercicio 4: Prompt vago vs estructurado

### Comparación de resultados

| Criterio | Prompt vago | Prompt estructurado |
|---|---|---|
| Menciona el objetivo del sistema | No | Sí |
| Menciona a los usuarios principales | No | Sí |
| Tiene exactamente 3 funcionalidades | No | Sí |
| Esta en 3 párrafos | No | Sí |
| Lo usaría en un informe real | No | Sí |

### Análisis de la diferencia
- **Prompt vago:** Genera una respuesta genérica, desorganizada e imprecisa en su formato porque no se especificaron límites ni requerimientos claros.
- **Prompt estructurado:** Al definir un rol ("analista de sistemas"), contexto, formato (3 párrafos) y límites explícitos (3 funcionalidades), el modelo entrega una respuesta directa, organizada y lista para ser utilizada profesionalmente.
 
## Ejercicio 5: Anatomia de un prompt

### Identificación de componentes

| Componente | Texto de mi prompt |
|---|---|
| Rol | Actua como desarrollador Java. |
| Instruccion | Crea un programa en Java usando una clase Producto con los atributos codigo, nombre, precio y stock. |
| Contexto | para gestionar los productos de una tienda. |
| Ejemplo | Usa este estilo para los metodos: getPrecio(), setPrecio(double precio). |
| Formato | Explica primero la estructura de la clase y luego presenta el codigo Java. |

### Evolución por niveles

- **Nivel 1 (Básico):** Genera un programa genérico e impredecible (como un "Hola Mundo" o una calculadora simple).
- **Nivel 2 (+ Rol):** Adopta un tono más técnico y profesional orientado a buenas prácticas en Java.
- **Nivel 3 (+ Contexto):** Enfoca la solución específicamente en la temática solicitada (gestión de tienda).
- **Nivel 4 (+ Instrucción):** Incluye la estructura exacta requerida (clase Producto con código, nombre, precio y stock).
- **Nivel 5 (+ Formato y Ejemplo):** Presenta la explicación previa al código e implementa los nombres de métodos con la sintaxis solicitada.
 
## Ejercicio 6: Del prompt basico al profesional

### Lista de evaluación del prompt profesional

| Qué revisar | Cumple (Sí / No) |
|---|---|
| ¿Está escrito en Java y usa Swing? | Sí |
| ¿Pide correo y contraseña? | Sí |
| ¿Explica el funcionamiento antes o después del código? | Sí |
| ¿El código está organizado en clases? | Sí |
| ¿Valida los datos que ingresa el usuario? | Sí |

### Prompts utilizados en el ciclo de iteración

```text
PROMPT PROFESIONAL INICIAL:
Actua como desarrollador Java. Crea un ejemplo de login para una aplicacion de escritorio utilizando Swing. El usuario debe ingresar correo y contrasena. Explica brevemente el funcionamiento y presenta el codigo organizado por clases.

PROMPT DE MEJORA (ITERACIÓN):
Mejora el codigo anterior con estas restricciones: no uses librerias externas, valida que el correo contenga @ y que la contrasena tenga al menos 8 caracteres, y muestra los mensajes con JOptionPane.