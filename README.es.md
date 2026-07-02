# Barbershop Manager

🌐 Idioma: [English](./README.md) | **Español**

[![Demo online](https://img.shields.io/badge/Demo_online-Vercel-black?style=for-the-badge&logo=vercel)](https://barbershop-project-frontend.vercel.app)
[![Backend](https://img.shields.io/badge/API-Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)](https://barbershop-project-backend.onrender.com)
[![Frontend](https://img.shields.io/badge/Frontend-Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)](https://github.com/GabiAntico/barbershop-project-frontend)
[![Backend repo](https://img.shields.io/badge/Backend-Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)](https://github.com/GabiAntico/barbershop-project-backend)
[![Database](https://img.shields.io/badge/Database-PostgreSQL%20%2F%20Neon-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](#tecnologías)
[![Responsive](https://img.shields.io/badge/UI-Responsive-7C3AED?style=for-the-badge)](#capturas)

Sistema full stack para la gestión operativa de barberías: agenda de turnos, clientes, responsables, empleados, sucursales, disponibilidad horaria, visitas, pagos y estadísticas comerciales.

La aplicación está pensada para un escenario real de trabajo: que una barbería pueda organizar su día desde el celular o la computadora, evitar dobles reservas, registrar quién atendió cada turno, controlar pagos y tomar mejores decisiones con datos simples.

## Demo online

[Ver demo online](https://barbershop-project-frontend.vercel.app)

> Nota: el backend está desplegado en Render con sleeping, por lo que la primera request puede tardar un poco mientras el servicio despierta.

Usuario demo: `admin@barbershop.com`  
Contraseña demo: `admin123`

## Repositorios

- Frontend: [barbershop-project-frontend](https://github.com/GabiAntico/barbershop-project-frontend)
- Backend: [barbershop-project-backend](https://github.com/GabiAntico/barbershop-project-backend)

## Descripción del problema

Muchas barberías gestionan turnos con mensajes, agendas manuales o planillas. Ese flujo alcanza al principio, pero se vuelve frágil cuando aparecen cancelaciones, clientes recurrentes, más de un barbero, sucursales, pagos pendientes y la necesidad de medir ingresos.

Barbershop Manager centraliza ese flujo:

- Evita superposiciones de turnos según sucursal, disponibilidad y barberos trabajando.
- Permite registrar clientes aunque el contacto real sea un responsable, como madres, padres o tutores.
- Mantiene clientes compartidos dentro de la barbería, pero turnos y visitas separados por sucursal.
- Permite atender turnos, registrar movimientos de pago y editar visitas después.
- Ofrece estadísticas generales y por cliente para entender presentismo, recaudación y frecuencia.
- Está diseñada para usarse en escritorio y en celular, con tablas en desktop y cards en mobile.

## Funcionalidades principales

- Registro de barbería con usuario administrador y sucursal inicial.
- Login con JWT firmado.
- Creación de empleados con contraseña temporal y cambio obligatorio en el primer ingreso.
- Gestión de sucursales y selector de sucursal activa.
- Gestión de clientes con teléfono obligatorio, email opcional, notas internas y contacto responsable.
- Vista detallada de cliente con acceso a notas y estadísticas.
- Agenda diaria responsive con navegación por fecha.
- Creación y edición de turnos mediante bloques horarios.
- Capacidad por horario según cantidad de barberos disponibles.
- Asignación automática o manual del barbero que atenderá el turno.
- Horarios laborales personalizables por empleado y sucursal.
- Configuración de monto estimado, moneda por defecto y disponibilidad de turnos.
- Configuración de disponibilidad por fecha única, rango de fechas o todos los días.
- Atender turnos y generar visitas.
- Edición de visitas para completar o corregir pagos.
- Movimientos financieros por visita: pagos, reembolsos y bonificaciones.
- Estados de pago derivados del balance de movimientos.
- Registro del empleado que atendió cada visita.
- Dashboard general de presentismo y recaudación.
- Estadísticas por cliente con presentismo, recaudación mensual, histórico y frecuencia promedio.
- Exportación de turnos a PDF como respaldo.
- Recordatorio manual por WhatsApp desde la agenda.
- UI responsive con cards en pantallas móviles.

## Tecnologías

Backend:

- Java 17
- Spring Boot 4
- Spring Security
- JWT firmado
- Spring Data JPA
- Hibernate
- Bean Validation
- Flyway
- H2 para desarrollo
- PostgreSQL para demo/deploy
- Maven
- Docker

Frontend:

- Angular 19
- TypeScript
- RxJS
- Angular Router
- Guards e interceptores HTTP
- PrimeNG
- Tailwind CSS
- Vercel

Infraestructura demo:

- Neon PostgreSQL
- Render
- Vercel

## Arquitectura general

El sistema está separado en dos aplicaciones independientes. Este repositorio central, `barbershop-project`, funciona como hub documental para presentar la demo, la arquitectura y las capturas del producto.

```text
barbershop-project/
|-- docs/
|   `-- screenshots/     Capturas del producto
|-- README.md            Presentación general en inglés
|-- README.es.md         Presentación general en español
`-- .gitignore
```

Flujo principal:

```text
Angular App
   |
   | Authorization: Bearer <JWT>
   | X-Branch-Id: <sucursal activa>
   v
Spring Boot API
   |
   | JPA / Hibernate + Flyway
   v
PostgreSQL / H2
```

Modelo de negocio resumido:

```text
Barbería
|-- Sucursales
|-- Empleados
|   `-- Horarios laborales por sucursal
|-- Clientes compartidos
|   `-- Contacto responsable opcional
`-- Configuración general

Sucursal
|-- Turnos
|   `-- Barbero asignado
|-- Visitas
|   `-- Movimientos de pago
`-- Disponibilidad horaria
```

La app trabaja por contexto: el usuario inicia sesión, elige una sucursal activa y las operaciones de turnos, visitas, disponibilidad, empleados y configuración se filtran por esa sucursal cuando corresponde.

## Capturas

### Login

![Login](docs/screenshots/login.png)

### Agenda

![Agenda diaria](docs/screenshots/agenda.png)

### Crear turno

![Crear turno](docs/screenshots/create-shift.png)

### Clientes

![Vista de clientes](docs/screenshots/clients-view.png)

### Detalle de cliente

![Detalle de cliente](docs/screenshots/client-detail.png)

### Visitas y pagos

![Visitas y pagos](docs/screenshots/visit.png)

### Estadísticas generales

![Estadísticas generales](docs/screenshots/general-stats.png)

### Estadísticas por cliente

![Estadísticas por cliente](docs/screenshots/client-stats.png)

### Configuración de empleados

![Configuración de empleados](docs/screenshots/employee-configuration.png)

## Decisiones técnicas

- Separación frontend/backend para permitir despliegues independientes.
- Autenticación stateless con JWT firmado.
- Interceptor Angular para adjuntar token y sucursal activa.
- Clientes compartidos a nivel barbería para no duplicar información entre sucursales.
- Turnos y visitas asociados a sucursal para mantener operación y métricas separadas.
- Capacidad de turnos calculada en backend según empleados asignados, horarios laborales y reservas existentes.
- Validaciones de disponibilidad también en backend para proteger la integridad aunque falle el frontend.
- Contactos responsables para representar casos reales como padres que gestionan turnos de sus hijos.
- Pagos modelados como movimientos para soportar parciales, reembolsos y bonificaciones sin perder historial.
- Flyway para versionar cambios de base de datos.
- Perfiles separados: `dev` para desarrollo local y `demo` para despliegue demostrable.
- `data.sql` idempotente para levantar una demo con datos precargados.
- Diseño responsive: tablas en escritorio y cards en celular.
- PDF de respaldo para turnos, pensado como contingencia operativa.

## Próximas mejoras

- Recordatorios automáticos por WhatsApp Business API.
- Roles y permisos más granulares.
- Eliminación lógica y auditoría para clientes, turnos y visitas.
- Clientes en riesgo según ausencias o tiempo desde la última visita.
- Reportes por empleado, sucursal y período.
- Historial de cambios de turnos.
- Tests automatizados de disponibilidad, pagos y multi-sucursal.
- Perfil `prod` con configuración productiva completa.
- Backups automatizados y monitoreo de errores.

## Documentación

Este repositorio funciona como documentación central del proyecto: resume el problema, la solución, las principales decisiones técnicas, la arquitectura general, la demo publicada y capturas del producto.
