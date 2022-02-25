- Start Date: 2022-02-24
- Members: (fill me with the names of the RFC creators)
- RFC PR:

# Summary

Este RFC describe los datos, su esquema y tipo, que serán necesarios para panel de administración, el inicio de sesión y gestión de usuarios. 

# Basic example
<!--
If the proposal involves a new or changed API, include a basic code example.
Omit this section if it's not applicable.
-->
N/A

# Motivation

Why are we doing this? What use cases does it support? What is the expected
outcome?

Please focus on explaining the motivation so that if this RFC is not accepted,
the motivation could be used to develop alternative solutions. In other words,
enumerate the constraints you are trying to solve without coupling them too
closely to the solution you have in mind.

# Detailed design

## Perfiles de administradores

Solo tendrán la opción para crear nuevos admins y super admins y eso se hará por medio de invitaciones vía email (se pueden generar las invitaciones en la vista de admin management), la cual tendrá una opción (en forma de checkbox) para darle o no permisos de superadmin.

- **Admin** → Puede validar, editar, eliminar y banear usuarios y alojamientos
- **SuperAdmin** → Puede validar, editar, eliminar y banear usuarios y alojamientos. Además puede gestionar perfiles de admins y superadmins.
- La opción para agregar admin solo estará habilitada para los super admins. Consultar endpoint para verificar si la sesión pertenece a un admin o un super admin y así habilitar o desabilidad la opción.


### Formas de crear perfiles de admin/super admin

> Esta función solo está disponible para SUPERADMINS
> 
1. Enviado invitación vía email
2. Dándole permisos de admin o super admin a un usuario existente desde la tabla de users management (podría ser una opción nativa de la tabla o desde el modal para editar al usuaro

## Estructura perfil de usuarios (pendiente)

## Validación de usuarios

Se asignará un administrador por región geográfica que estará encargado de la validación de usuarios correspondientes a esa región. Aplicar sistema de notificación por correo.

Si el usuario no está validado, se mostrará un ícono de alerta en la vista de tabla al lado de su foto y en la organización se les da prioridad (llevar al top de la tabla)

## Manejo de usuarios

**Datos** → Usuario válido/Usuario por validar. Nombre. Foto (si la tiene, si no un icono). Fecha de registro y ultima modificación (en la tabla solo mostrar ultima modificación)

**Acciones** → Banear, modificar, eliminar, Validar (si aplica)

## Login de administradores

- Se debe tener una vista de inicio de sesión exclusiva para los dos tipos de admins → [bookingsystem.com/admin](http://bookingsystem.com/admin). Mi recomendación es que solo se pueda acceder por medio de la url para que los demás usuarios no tenga forma de verla.}
- Datos para inicio de sesión → Email, contraseña. **Nice to have** ✨ → 2fa aut

## Manejo de Admins y super admins

**Datos** → Tipo de perfil (admin/superadmin). Nombre. Foto (si la tiene, si no un icono). Fecha de registro y ultima modificación (en la tabla solo mostrar ultima modificación)

**Acciones** → Modificar, eliminar

**Nice to have** ✨ → Una vista de tabla aparte para gestionar las invitaciones pendientes de admins y super admins.

## Opciones de filtrado

Las vitas de tablas deben ser capaz de filtrarse ya sea por fecha de creación, ultima modificación, nombre de usuario o nombre de admin, si estamos en la tabla de admins filtrar también por tipo de perfil


___________________________________________
# Drawbacks

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people React
- integration of this feature with other existing and planned features
- cost of migrating existing React applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

# Alternatives

What other designs have been considered? What is the impact of not doing this?

# Adoption strategy

If we implement this proposal, how will existing C9 developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries?

# How we teach this

What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing C9 projects patterns?

Would the acceptance of this proposal mean the C9 documentation must be
re-organized or altered? Does it change how C9 is taught to new developers
at any level?

How should this feature be taught to existing C9 developers?

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?
