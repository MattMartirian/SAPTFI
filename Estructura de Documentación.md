# 📦 Estructura de Proyecto — Enterprise Architect

> [!NOTE]
> Este proyecto funciona como un **repositorio centralizado** de modelos UML, diagramas y elementos reutilizables.
> No representa el documento final entregable.

> [!IMPORTANT]
> Toda la documentación textual extensa (visión, alcance, introducción, historial, etc.) debe realizarse **externamente** en Word/Google Docs.

### Función principal

| Objetivo | Descripción |
|---|---|
| 🗂️ Organizar | Estructurar el sistema en paquetes coherentes |
| ♻️ Reutilizar | Elementos UML referenciados, sin duplicados |
| 🔗 Trazabilidad | Vincular requerimientos, CU, clases y pruebas |
| 📤 Exportar | Generar diagramas exportables desde EA |
| ✅ Fuente única | Servir como fuente única de verdad del modelo |

---

## Sistema XYZ — Estructura de paquetes

```
📦 Sistema XYZ
├── 00.Shared               ← Fuente de verdad central
├── 01.Requerimientos       ← Especificaciones formales
├── 02.Casos de Uso         ← Vistas funcionales
├── 03.Arquitectura         ← Estructura técnica
├── 04.Base de Datos        ← Modelo persistente
├── 05.UI                   ← Interfaz y navegación
└── 06.Testing              ← Validación y trazabilidad
```

---

## 00. Shared

> Contiene **todos los elementos reutilizables** del sistema. Los elementos aquí definidos deben reutilizarse en todos los diagramas mediante referencias, evitando crear duplicados.

```
00.Shared
├── Actores
├── Entidades
├── Servicios
├── Interfaces
├── DTOs
├── Enumeraciones
└── Objetos Comunes
```

### 00.Shared / Actores

Contiene los actores globales del sistema.

| Actor | Reutilizado en |
|---|---|
| Administrador | Casos de uso · Actividad · Negocio |
| Cliente | Casos de uso · Actividad · Negocio |
| Empleado | Casos de uso · Actividad · Negocio |
| Supervisor | Casos de uso · Actividad · Negocio |

### 00.Shared / Entidades

Contiene las entidades principales del dominio. Representan la estructura lógica del sistema.

| Entidad | Reutilizada en |
|---|---|
| Usuario | Clases · Secuencia · ER · Componentes |
| Cliente | Clases · Secuencia · ER · Componentes |
| Empresa | Clases · Secuencia · ER · Componentes |
| Pedido | Clases · Secuencia · ER · Componentes |
| Factura | Clases · Secuencia · ER · Componentes |

### 00.Shared / Servicios

Contiene servicios o lógica de aplicación reutilizable. Representan operaciones o lógica de negocio.

| Servicio | Reutilizado en |
|---|---|
| `AuthService` | Secuencia · Componentes · Clases |
| `ClienteService` | Secuencia · Componentes · Clases |
| `FacturaService` | Secuencia · Componentes · Clases |

### 00.Shared / Interfaces

Contiene contratos o interfaces reutilizables. Se utilizan para modelar desacoplamiento y arquitectura.

- `IRepository`
- `IAuthProvider`
- `ILogger`

### 00.Shared / DTOs

Contiene objetos de transferencia de datos. Se utilizan para representar intercambio de información entre capas.

- `ClienteDTO`
- `LoginRequestDTO`

### 00.Shared / Enumeraciones

Contiene enumeraciones globales del sistema.

- `EstadoPedido`
- `RolUsuario`
- `TipoDocumento`

### 00.Shared / Objetos Comunes

Contiene elementos reutilizables auxiliares.

- `ResponseModel`
- `AuditData`
- `BaseEntity`

---

## 01. Requerimientos

> **Ref:** §10.4.2 Especificaciones de requerimientos

Contiene los requerimientos formales del sistema. Deben vincularse con casos de uso, clases y testing para mantener trazabilidad.

```
01.Requerimientos
├── Funcionales
├── No Funcionales
└── Reglas de Negocio
```

### 01 / Funcionales

| ID | Nombre |
|---|---|
| `RF001` | Iniciar sesión |
| `RF002` | Registrar cliente |

### 01 / No Funcionales

| ID | Nombre |
|---|---|
| `RNF001` | Seguridad |
| `RNF002` | Rendimiento |

### 01 / Reglas de Negocio

| ID | Regla |
|---|---|
| `RN001` | Un cliente solo puede tener una cuenta activa |
| `RN002` | El email debe ser único |

---

## 02. Casos de Uso

> **Ref:** §10.5.2 Índice · §10.5.3 Casos de uso · §10.5.4 Diagramas de secuencia

Contiene las vistas funcionales específicas del sistema. Cada caso de uso posee sus propios diagramas y documentación asociada.

> [!CAUTION]
> Este paquete **NO debe contener clases reales nuevas**. Las clases utilizadas deben reutilizarse desde `00.Shared`.

```
02.Casos de Uso
├── Generales                      ← Índice y overview funcional
└── CU001_Login
    ├── Descomposición Funcional   §10.5.3.x.1
    ├── Caso de Uso                §10.5.3.x.2
    ├── Especificación             §10.5.3.x.3
    ├── Secuencia                  §10.5.3.x.4
    ├── Actividad                  §10.5.3.x.5
    ├── Vista de Clases            §10.5.3.x.6
    ├── Vista ER                   §10.5.3.x.7
    └── GUI                        §10.5.3.x.8
```

### 02 / Generales

Contiene el índice general de casos de uso, diagramas generales de interacción y overview funcional.

### 02 / CU001\_Login — Estructura uniforme

Cada caso de uso debe seguir esta estructura:

| Sección | Ref. | Contenido |
|---|---|---|
| Descomposición Funcional | §10.5.3.x.1 | Desglose funcional del CU |
| Caso de Uso | §10.5.3.x.2 | Diagrama UML del caso de uso |
| Especificación | §10.5.3.x.3 | ID · Nombre · Estado · Actores · Precondiciones · Escenario principal · Flujos alternativos · Postcondiciones |
| Secuencia | §10.5.3.x.4 | Interacción temporal entre objetos (elementos desde `00.Shared`) |
| Actividad | §10.5.3.x.5 | Flujo operativo interno |
| Vista de Clases | §10.5.3.x.6 | Vista parcial de clases reutilizadas desde `00.Shared` — sin clases nuevas |
| Vista ER | §10.5.3.x.7 | Entidades relevantes al caso de uso |
| GUI | §10.5.3.x.8 | Referencias a Figma · exportaciones · wireframes · mockups |

---

## 03. Arquitectura

> **Ref:** §10.5.5 Paquetes · §10.5.6 Componentes · §10.5.9 Despliegue

Contiene la arquitectura técnica del sistema.

```
03.Arquitectura
├── Paquetes     ← Organización lógica, capas, módulos, dependencias
├── Componentes  ← Servicios, APIs, frontend, backend, integraciones
└── Despliegue   ← Servidores, clientes, bases de datos, infraestructura
```

| Subpaquete | Representa |
|---|---|
| **Paquetes** | Organización lógica · capas · módulos · dependencias |
| **Componentes** | Servicios · APIs · frontend · backend · integraciones |
| **Despliegue** | Servidores · clientes · bases de datos · infraestructura |

---

## 04. Base de Datos

> **Ref:** §10.5.8 Diagrama Entidad Relación

Contiene el modelo persistente del sistema.

```
04.Base de Datos
├── Modelo ER General   ← DER completo del sistema
├── Tablas              ← Entidades/tablas individuales
└── Relaciones          ← PK/FK · cardinalidades · dependencias
```

---

## 05. UI

Contiene todos los elementos relacionados con interfaz y navegación visual.

```
05.UI
├── Navegación   ← Mapa de navegación y flujo entre pantallas
├── Wireframes   ← Estructuras visuales básicas (sin diseño final)
└── Mockups      ← Mockups finales · exportaciones de Figma
```

| Subpaquete | Descripción |
|---|---|
| **Navegación** | Mapa de navegación · flujo entre pantallas · estructura visual de interacción |
| **Wireframes** | Estructuras visuales básicas. No incluyen diseño final |
| **Mockups** | Mockups finales · exportaciones de Figma · referencias visuales |

---

## 06. Testing

> **Ref:** §10.5.10 Especificación de Casos de Prueba

Contiene validaciones y trazabilidad.

```
06.Testing
├── Casos de Prueba   ← CP001, CP002, ...
├── Escenarios        ← Login válido · Login inválido · Error de permisos
└── Trazabilidad      ← Requerimientos ↔ CU ↔ Clases ↔ Pruebas
```

### 06 / Trazabilidad

Relaciona requerimientos, casos de uso, clases y pruebas. Permite identificar:

- Cobertura
- Impacto
- Elementos faltantes
- Validaciones pendientes

---

## ⚠️ Reglas importantes del proyecto

### Regla 1 — Nunca duplicar elementos

> Las clases, actores y servicios deben existir **una sola vez** dentro de `00.Shared`. Todos los diagramas deben reutilizar referencias.

### Regla 2 — Los diagramas son vistas

> Los diagramas **no son la fuente de verdad**. La fuente de verdad son los elementos UML reutilizables.

### Regla 3 — Mantener diagramas pequeños

> Enterprise Architect 12 funciona mejor con diagramas simples y reducidos. Se recomienda entre **5 y 15 elementos** por diagrama.

### Regla 4 — Separar modelo y presentación

| Paquete | Rol |
|---|---|
| `00.Shared` | Elementos reales |
| `02.Casos de Uso` | Vistas funcionales |
| `03.Arquitectura` | Estructura técnica |
| `05.UI` | Navegación visual |
| `06.Testing` | Validación |

### Regla 5 — Utilizar nombres consistentes

| Tipo | Ejemplo |
|---|---|
| Caso de uso | `CU001_Login` |
| Requerimiento funcional | `RF001_Login` |
| Caso de prueba | `CP001_LoginValido` |

> Evitar nombres ambiguos o inconsistentes.
