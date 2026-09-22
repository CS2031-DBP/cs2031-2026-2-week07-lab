# Week 07 Lab — Flight Booking API (Fly Away Travel)

Laboratorio del curso **CS2031** (UTEC) — Desarrollo Basado en Plataformas. Construirás, desde cero, el API REST de reservas de vuelos para la aerolínea ficticia **Fly Away Travel**.

Este repositorio **no incluye scaffolding ni código inicial**: es la guía de la misión. Tu equipo debe crear el proyecto Spring Boot desde cero (estructura de paquetes, entidades, DTOs, servicios, controllers, seguridad, etc.) siguiendo lo que se pide aquí y lo visto en las diapositivas de la semana.

---

## Historia

**Fly Away Travel** necesita héroes, ¡y ese eres tú y tu equipo! Tu quest: construir un API épico para reservar vuelos.

- **Objetivos:** completar las misiones principales (obligatorias para completar el nivel).
- **Recompensa total:** hasta **1 punto adicional** para tu PC1.
- Cada misión indica su recompensa individual — la suma de todas las misiones completadas da el puntaje total (máximo 1 punto).

¿Aceptas el desafío?

---

## Stack sugerido

| | |
|---|---|
| Java | 26 |
| Spring Boot | 4.x |
| Spring Security | 7.x (JWT) |
| Base de datos | PostgreSQL (Docker) |
| Build | Maven Wrapper |

No hay una estructura de paquetes obligatoria: organiza tu proyecto siguiendo las convenciones vistas en clase (por ejemplo, separación por dominio con `application/domain/infrastructure/dto`, como en los labs anteriores).

---

## Misiones

### 1. Crear Vuelo

**Endpoint:** `POST /flights/create` *(sin protección)*

**Constraints:**

- Todos los campos son requeridos.
- Número de vuelo: solo `A-Z` y `0-9`, máximo 6 caracteres (ej: `AA984`).
- Hora de salida debe ser anterior a la hora de llegada.
- Asientos disponibles debe ser mayor a 0.
- Los números de vuelo deben ser únicos.

**Recompensa:** `+0.1 puntos`

---

### 2. Registro de Usuarios

**Endpoint:** `POST /users/register` *(sin protección)*

**Constraints:**

- Email válido.
- Nombre y apellido: mínimo 1 letra mayúscula (`A-Z`).
- Contraseña: mínimo 8 caracteres, al menos 1 letra y 1 número.
- La respuesta solo debe incluir el `id` del usuario (usa DTOs — no expongas la entidad completa ni la contraseña).

**Recompensa:** `+0.1 puntos` (validaciones) + `+0.1 puntos` (uso correcto de DTOs)

---

### 3. Autenticación

**Endpoint:** `POST /auth/login` *(sin protección)*

**Constraints:**

- Email y contraseña obligatorios.
- Validar el caso de email desconocido.
- Validar el caso de contraseña incorrecta.
- Retorna un token JWT para las operaciones protegidas.
- El token debe devolverse con el siguiente formato:

```json
{ "token": "<jwt>" }
```

**Recompensa:** `+0.2 puntos`

---

### 4. Búsqueda de Vuelos

**Endpoint:** `GET /flights/search` *(protegido — requiere JWT)*

**Constraints:**

- Búsqueda por número de vuelo parcial.
- Búsqueda por nombre de aerolínea parcial.
- Búsqueda por rango de fechas de salida.

**Recompensa:** `+0.1 puntos` (filtros de búsqueda) + `+0.1 puntos` (protección del endpoint)

---

### 5. Reservar Vuelo

**Endpoint:** `POST /flights/book` *(protegido — requiere JWT)*

**Constraints:**

- Input: `flightId`.
- Auto-calcular a partir del usuario autenticado: `customerId`, nombres, fecha de reserva.
- No sobrevender vuelos (no exceder los asientos disponibles).
- No permitir reservar vuelos pasados o que ya estén en tránsito.
- Evitar reservas con conflicto de horario (mismo usuario, vuelos que se superponen en el tiempo).
- Endpoint adicional para ver una reserva: `GET /flight/book/{id}`.

**Recompensa:** `+0.1 puntos` (reglas de negocio de la reserva) + `+0.1 puntos` (endpoint de consulta)

---

### 6. Email de Confirmación

**Funcionalidad:** al confirmarse una reserva, generar un archivo de "email" con el siguiente nombre:

```
flight_booking_email_${booking_id}.txt
```

**Debe incluir:**

- Nombres del pasajero.
- Número de vuelo.
- Fechas en formato **ISO 8601**.

**Recompensa:** `+0.1 puntos`

---

## Cómo entregar

1. Trabaja en equipo sobre este repositorio (o un fork/repo del equipo, según indique tu profesor).
2. Implementa las misiones en el orden que prefieras — no son necesariamente secuenciales, pero autenticación (misión 3) es prerequisito para las misiones protegidas (4 y 5).
3. Verifica cada endpoint con Postman/curl antes de darlo por completado, revisando que cumple **todos** los constraints listados.
4. Asegúrate de que el proyecto levante con Docker Compose + Maven Wrapper, y documenta cualquier variable de entorno necesaria (`.env.example`).

---

## Recursos

- Diapositivas de la semana (revisa el campus virtual).
- Documentación oficial de [Spring Boot](https://docs.spring.io/spring-boot/index.html) y [Spring Security](https://docs.spring.io/spring-security/reference/index.html).
- Labs anteriores del curso (`cs2031-2026-2-week*`) como referencia de estructura y convenciones del proyecto.

---

© 2026 Departamento Ciencia de Computación - Universidad de Ingeniería y Tecnología
