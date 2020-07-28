---
title: CAS Miura

language_tabs:
  - java: Request Body
  - javascript: Success Response
  - csharp: Error Response

toc_footers:
  - <a href='http://kokonutstudio.com/'>CAS Miura</a>

search: true
---



# CAS Miura

Link al código fuente: [CAS Miura](https://github.com/KokonutStudioRepository/CAS_CMS_Backend).

## URL

Ambiente        | Value
----------------|----------------------------------------
Dev v2          | https://cas-api2.kokonutstudio.com
Dev v1          | https://cas-dev-api.kokonutstudio.com
QA              | https://cas-qa-api.kokonutstudio.com
Pruebas Cliente | NO DISPONIBLE AÚN
Producción      | NO DISPONIBLE AÚN


## Estatus de usuarios
Se muestra listado de los estatus disponibles para un usuario.

ID | Estatus
---|----------------------
1  | Activo
0  | Desactivado


## Tipo de usuarios
Se muestra listado de los tipos de usuarios.

id  | Rol
----|--------------------
 1  | Admin
 2  | Moderador
 3  | Primario Enterprise
 4  | Secundario Enterprise
 5  | Primario
 6  | Secundario
 7  | Individual


# Auth
## Inicio de sesión
> Inicio de sesión

```java
{
    "email": "example@testmail.com",
    "password": "123Qwe1"
}
```
```javascript
{
    "success": 1,
    "message": "Éxito",
    "data": {
        "token_type": "Bearer",
        "expires_in": 31622400,
        "access_token": "eyJ0eX...",
        "refresh_token": "def50200ecbfff..."
        "user_type": 1,
    }
}
```
```csharp
{
    "success": 0,
    "message": "El correo o contraseña son erroneos",
    "data": null
}
{
    "success": 0,
    "message": "Usuario no registrado",
    "data": null
}
{
    "success": 0,
    "message": "Te hace falta información para iniciar sesión",
    "data": null
}
```

Este endpoint inicia la sesión de un usuario y devuelve el Bearer token para futuras peticiones


HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|--------------------
POST          |Login          | {{url}}/api/login

### Header
No aplica.

### Body
Key                   | Descripción                 | Type   | Mandatory
----------------------|-----------------------------|--------|-------------
email                 | Correo del usuario          | String | Obligatorio
password              | Contraseña del usuario      | String | Obligatorio







## Cerrar sesión
>Cerrar sesión:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Sesión cerrada correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": null
}
```

Este endpoint cierra la sesión de un usuario

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|-----------
POST          | Logout        | {{url}}/api/oauth/logout

### Headers
Key           | Value
--------------|-----
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido





## Actualiza token de sesión
>Actualiza token sesión:

```java
{
    "refresh_token": "def50200c22a902ff0b5e3ea..."
}
```
```javascript
{
    "success": 1,
    "message": "Éxito",
    "data": {
        "token_type": "Bearer",
        "expires_in": 31536000,
        "access_token": "eyJ0eXAiOiJ...",
        "refresh_token": "def50200c...",
        "user_type": 1
    }
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": null
}
```

Este endpoint actualiza el token de sesión

HTTP Request  | Name Endpoint        |  Endpoint
--------------|----------------------|-----------
POST          | Refresh token        | {{url}}/api/token

### Headers
Key           | Value
--------------|--------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                 | Descripción            | Type   | Mandatory
--------------------|------------------------|--------|-------------
refresh_token       | Refresh token          | String | Obligatorio












## Recuperar contraseña
>Recuperar contraseña:

```java
{
    "email": "magdiel@kokonutstudio.com"
}
```
```javascript
{
    "success": 1,
    "message": "Se envió un correo de recuperación exitosamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint manda un correo al usuario que desea recuperar su contraseña

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|-----------
POST          | Logout        | {{url}}/api/restore_password

### Headers
No requerido

### Body
Key         | Descripción                 | Type   | Mandatory
------------|-----------------------------|--------|-------------
email       | Correo del usuario          | String | Obligatorio






## Resetear contraseña
>Resetear contraseña:

```java
{
    "password": "123Qwe1",
    "password_confirmation": "123Qwe1",
}
```
```javascript
{
    "success": 1,
    "message": "Se actualizó correctamente la contraseña",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint actualiza la nueva contraseña del usuario

HTTP Request  | Name Endpoint |  Endpoint
--------------|---------------|-----------
POST          | Reset pass    | {{url}}/api/reset_password

### Headers
No requerido

### Body
Key                     | Descripción                 | Type   | Mandatory
------------------------|-----------------------------|--------|-------------
password                | New Password                | String | Obligatorio
password_confirmation   | New Password confirmation   | String | Obligatorio






# User
## Registrar usuarios desde CMS
> Registro de usuarios

```java
{
	"user_id" : 2,
	"email_users" : [
      {"email": "magdiel.1@koko.studio"},
      {"email": "magdiel.2@koko.studio"},
      {"email": "magdiel.n@koko.studio"}
	],
	"create_group": true,
	"group_name": "Group Two"
}
```
```javascript
{
    "success": 1,
    "message": "Usuario creado con éxito",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
{
    "success": 0,
    "message": "Correo electronico ya registrado",
    "data": null
}
{
    "success": 0,
    "message": "Hacen falta datos para completar el registro",
    "data": null
}
```

Este endpoint manda una invitación a un usuario.
Si se utiliza desde el

HTTP Request  | Name Endpoint | Endpoint
--------------|---------------|-----------------------
POST          | Register      | {{url}}/api/oauth/users

### Headers
Key           | Value
--------------|-----
Authorization | Bearer eyJ0eXAiOiJKV1Q...
Content-Type  | application/json
Accept        | application/json

### Body
Key           | Descripción                                               | Type    | Mandatory
--------------|-----------------------------------------------------------|---------|-------------
user_id       | User id de la persona que manda invitación                | Int     | User ID de la persona que manda invitación. (Requerido si se consume desde CMS)
email_user    | Arreglo con los email para mandar invitación              | Array   | Obligatorio
creaet_group  | Indica si se va a crear un grupo o no                     | Boolean | Obligatorio
* group_name   | User id de la persona que manda invitación               | String  | Group name de la persona que manda invitación. (Requerido si es desde CMS)
* group_id     | User id de la persona que manda invitación               | Int     | User ID de la persona que manda invitación. (Requerido si es desde CMS)






## Mostrar perfil logueado
>Mostrar perfil logueado:

```java
// No aplica
```
```javascript
{
    "success": 1,
    "message": "Consulta de información exitosa",
    "data": {
        "id": 1,
        "name": "Interphy",
        "first_lastname": null,
        "second_lastname": null,
        "birthdate": null,
        "home_phone": null,
        "cell_phone": null,
        "email": "magdiel@interphysoft.com",
        "address": null,
        "status": 1,
        "created_at": null,
        "updated_at": "2020-02-25T17:28:08.000000Z",
        "login_status": null,
        "cat_type_user_id": 1
    }
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint muestra la información básica del usuario logueado

HTTP Request  | Name Endpoint          | Endpoint
--------------|------------------------|---------------------
GET           | Show personal profile  | {{url}}/api/oauth/users/me

### Headers
Key           | Value
--------------|-----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.





## Mostrar perfil
>Mostrar perfil:

```java
// No aplica
```
```javascript
{
    "success": 1,
    "message": "Consulta de información exitosa",
    "data": [
        {
          "id": 1,
          "name": "Interphy",
          "first_lastname": null,
          "second_lastname": null,
          "birthdate": null,
          "home_phone": null,
          "cell_phone": null,
          "email": "magdiel@interphysoft.com",
          "address": null,
          "status": null,
          "created_at": null,
          "updated_at": "2020-02-12 23:00:02",
          "deleted_at": null,
          "login_status": null,
          "cat_type_user_id": 1
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint muestra la información básica de un usuario respecto de su ID


HTTP Request  | Name Endpoint | Endpoint
--------------|---------------|---------------------
GET           | Show profile  | {{url}}/api/oauth/users/{user_id}

### Headers
Key           | Value
--------------|-----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.




## Listado usuarios primarios
>Listado usuarios primarios:

```java
// No aplica
```
```javascript
{
    "success": 0,
    "message": "Consulta de información correcta",
    "data": [
        {
            "primary_user": {
                "id": 1,
                "name": "Interphy",
                "first_lastname": null,
                "second_lastname": null,
                "birthdate": null,
                "home_phone": null,
                "cell_phone": null,
                "email": "magdiel@interphysoft.com",
                "address": null,
                "status": null,
                "created_at": null,
                "updated_at": "2020-02-12 23:00:02",
                "deleted_at": null,
                "login_status": null,
                "cat_type_user_id": 1,
                "uuid": "1ab09c0f-f911-4a05-ac35-c00284160447"
            },
            "location": {
                "id": 1,
                "fk_users_id": "2",
                "latitude": "19.388235",
                "longitude": "-99.163294",
                "address": "2ᵃ Cda. Concepción Beistegui 6, Narvarte Poniente, Benito Juárez, 03100 Ciudad de México, CDMX",
                "description": "Software Company",
                "created_at": null,
                "updated_at": null
            },
            "secondary_users": [
                {
                    "secondary_user": {
                        "id": 1,
                        "name": null,
                        "first_lastname": null,
                        "second_lastname": null,
                        "birthdate": null,
                        "home_phone": null,
                        "cell_phone": null,
                        "email": "magdiel@kokonutstudio.com",
                        "address": null,
                        "status": null,
                        "created_at": "2020-02-12 23:07:58",
                        "updated_at": "2020-02-13 19:58:52",
                        "deleted_at": null,
                        "login_status": null,
                        "cat_type_user_id": 2,
                        "uuid": "1ab09c0f-f911-4a05-ac35-c00284160447"
                    },
                    "location": {
                        "id": 2,
                        "fk_users_id": "3",
                        "latitude": "19.388235",
                        "longitude": "-99.163294",
                        "address": "2ᵃ Cda. Concepción Beistegui 6, Narvarte Poniente, Benito Juárez, 03100 Ciudad de México, CDMX",
                        "description": "Software Company",
                        "created_at": null,
                        "updated_at": null
                    }
                }
            ]
        },
        {
            "primary_user": {
                "id": 1,
                "name": null,
                "first_lastname": null,
                "second_lastname": null,
                "birthdate": null,
                "home_phone": null,
                "cell_phone": null,
                "email": "magdiel@interphy.com",
                "address": null,
                "status": null,
                "created_at": "2020-02-12 17:55:39",
                "updated_at": "2020-02-13 23:22:47",
                "deleted_at": null,
                "login_status": null,
                "cat_type_user_id": 1
            },
            "location": {
                "id": 3,
                "fk_users_id": "4",
                "latitude": "19.388235",
                "longitude": "-99.163294",
                "address": "2ᵃ Cda. Concepción Beistegui 6, Narvarte Poniente, Benito Juárez, 03100 Ciudad de México, CDMX",
                "description": "Software Company",
                "created_at": null,
                "updated_at": null
            },
            "secondary_users": []
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint lista los usarios primarios con sus respectivos usuarios secundarios


HTTP Request  | Name Endpoint | Endpoint
--------------|---------------|---------------------
GET           | List users    | {{url}}/api/oauth/users

### Headers
Key           | Value
--------------|-----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.






## Editar usuario
>Editar usuario:

```java
{
    "user_id": 1,
    "name": "Interphy",
    "first_lastname": "Lastname1",
    "second_lastname": "Lastname2",
    "birthdate": "1991-12-12 01:36:12",
    "home_phone": "5512341234",
    "cell_phone": "5512341234",
    "email": "magdiel@interphysoft.com",
    "address": "address",
    "device_id": "89ABCDEF-01234567-89ABCDEF",
    "firebase_token": "akdfbve82b4e...",
}
```
```javascript
{
    "success": 1,
    "message": "Información de usuario actualizada correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Error al obtener los contactos de emergencia",
    "data": null
}
{
    "success": 0,
    "message": "El ID de usuario es inválido",
    "data": null
}
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint actualizará la información de un usuario respecto de los parámetros del Body de la petición

HTTP Request  | Name Endpoint   |  Endpoint
--------------|-----------------|----------------------
POST          | Update profile  | {{url}}/api/oauth/users/{user_id}?_method=PUT

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
name                  | String | Opcional
first_lastname        | String | Opcional
second_lastname       | String | Opcional
birthdate             | String | Opcional
home_phone            | String | Opcional
cell_phone            | String | Opcional
email                 | String | Opcional
address               | String | Opcional
firebase_token        | String | Opcional







## Eliminar usuarios secundarios
>Eliminar usuarios secundarios:

```java
// No aplica
```
```javascript
{
    "success": 1,
    "message": "Se ha eliminado este usuario",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
{
    "success": 0,
    "message": "El usuario no existe",
    "data": null
}
{
    "success": 0,
    "message": "No tienes permisos para realizar esta acción",
    "data": null
}
{
    "success": 0,
    "message": "Hubo un error al eliminar al usuario",
    "data": null
}
```
Este endpoint elimina un usuario secundario utilizando su ID


HTTP Request  | Name Endpoint | Endpoint
--------------|---------------|---------------------
DELETE        | Delete user   | {{url}}/api/oauth/users/{user_id}

### Headers
Key           | Value
--------------|-----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido.











## Deshabilitar usuario
>Deshabilitar usuario:

```java
{
    "user_id": 1
}
```
```javascript
{
    "success": 1,
    "message": "Información de usuario actualizada correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "Hubo un error al actualizar la información de usuario",
    "data": null
}
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint habilitará/deshabilitará a un usuario

HTTP Request  | Name Endpoint   |  Endpoint
--------------|-----------------|----------------------
POST          | Disable profile | {{url}}/api/oauth/disable_user

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | Int    | Obligatorio






## Detalle de usuario
>Detalle usuario:

```java
{
    "user_id": 2
}
```
```javascript
{
    "success": 1,
    "message": "Detalle de información realizada con éxito",
    "data": {
        "principal": {
            "id": 2,
            "name": "DEVELOPER",
            "first_lastname": "Dev",
            "second_lastname": "Dev",
            "birthdate": null,
            "home_phone": null,
            "cell_phone": null,
            "email": "magdiel@kokonutstudio.com",
            "address": null,
            "status": 1,
            "created_at": null,
            "updated_at": "2020-07-22T17:30:14.000000Z",
            "login_status": 1,
            "cat_type_user_id": 3,
            "uuid": null
        },
        "emergency_contacts": {
            "id": 1,
            "name": "Emergency",
            "first_lastname": "Emergency",
            "second_lastname": "Emergency",
            "cell_phone": "5511112222",
            "job_phone": null,
            "relationship": null,
            "fk_users_id": 2,
            "created_at": "2020-07-16 18:04:06",
            "updated_at": "2020-07-16 18:04:06"
        },
        "history_locations": [],
        "membership": {
            "id": 1,
            "payday": "2020-07-16 17:56:13",
            "status": 1,
            "qtt_users": 0,
            "fk_cat_membership_id": 3,
            "fk_user_id": 2,
            "created_at": null,
            "updated_at": "2020-07-16 18:02:54",
            "details": {
                "id": 3,
                "name": "Familiar",
                "description": null,
                "price": null,
                "membership_type": null
            }
        },
        "groups": [
            {
                "id": 1,
                "name": "Group Four",
                "users": null
            },
            {
                "id": 2,
                "name": "Group Tree",
                "users": [
                    {
                        "id": 3,
                        "name": "Develop",
                        "first_lastname": "Mag",
                        "second_lastname": "Dev",
                        "birthdate": null,
                        "home_phone": null,
                        "cell_phone": null,
                        "email": "magdiel.3@koko.studio",
                        "address": null,
                        "status": 0,
                        "created_at": "2020-07-16T23:01:04.000000Z",
                        "updated_at": "2020-07-22T17:48:33.000000Z",
                        "login_status": null,
                        "cat_type_user_id": 6,
                        "uuid": null
                    }
                ]
            },
            {
                "id": 3,
                "name": "Group Two",
                "users": [
                    {
                        "id": 4,
                        "name": "Develop",
                        "first_lastname": "Mag",
                        "second_lastname": "Dev",
                        "birthdate": null,
                        "home_phone": null,
                        "cell_phone": null,
                        "email": "magdiel.2@koko.studio",
                        "address": null,
                        "status": 1,
                        "created_at": "2020-07-16T23:01:56.000000Z",
                        "updated_at": "2020-07-22T17:30:14.000000Z",
                        "login_status": null,
                        "cat_type_user_id": 6,
                        "uuid": null
                    }
                ]
            }
        ],
        "users": null
    }
}
```
```csharp
{
    "success": 0,
    "message": "Hubo un error al actualizar la información de usuario",
    "data": null
}
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint mostrará la información de un usuario, usuarios de emergencia, su última ubicación y un listado de sus respectivos usuarios secundarios ordenados por grupos, cada uno con su última ubicación. Si hay un usuario sin grupo asignado, aparecerá en el último parámetro "users"

HTTP Request  | Name Endpoint   |  Endpoint
--------------|-----------------|----------------------
POST          | Detail primary  | {{url}}/api/oauth/detail_primary

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | Int    | Obligatorio







# Contactos de emergencia
## Mostrar Contactos de emergencia
> Mostrar Contactos de emergencia:

```java
{
    "user_id": 1
}
```
```javascript
{
    "success": 1,
    "message": "Usuarios obtenidos con éxito",
    "data": {
            "id": 1,
            "name": "Alfa",
            "first_lastname": "Beta",
            "second_lastname": "Gama",
            "cell_phone": "5511112222",
            "job_phone": "5511112222",
            "relationship": null,
            "fk_users_id": 2,
            "created_at": "2020-02-18 20:09:42",
            "updated_at": "2020-02-18 20:09:42"
    }
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint mostrará la información de los contactos de emergencia respecto del ID de un usuario

HTTP Request  | Name Endpoint              |  Endpoint
--------------|----------------------------|----------------------
POST          | Emergency contacts         | {{url}}/api/oauth/emergency_contact

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | Int    | Obligatorio









## Crear Contacto de emergencia
> Crear Contacto de emergencia:

```java
{
    "name": "name",
    "first_lastname": "Lastname1",
    "second_lastname": "Lastname2",
    "cell_phone": "5511223344"
}
```
```javascript
{
    "success": 1,
    "message": "Contactos de emergencia creados con éxito",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint crea un nuevo contacto de emergencia

HTTP Request  | Name Endpoint              |  Endpoint
--------------|----------------------------|----------------------
POST          | Emergency contacts create  | {{url}}/api/oauth/create_emg_contacts

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
name                  | String | Obligatorio
first_lastname        | String | Obligatorio
second_lastname       | String | Obligatorio
cell_phone            | String | Obligatorio






#Grupos
## Crear grupo
> Crear grupo:

```java
{
    "user_id": 2,
    "group_name": "GroupName"
}
```
```javascript
{
    "success": 1,
    "message": "El grupo se ha creado exitosamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": null
}
{
    "success": 0,
    "message": "Falta agregar información",
    "data": null
}
{
    "success": 0,
    "message": "No tienes permisos para realizar esta operación",
    "data": null
}
{
    "success": 0,
    "message": "El grupo se ha creado exitosamente",
    "data": null
}
{
    "success": 0,
    "message": "El grupo con este nombre ya existe",
    "data": null
}
```

Este endpoint crea un nuevo grupo. Para crear grupos de CMS es obligatorio el "user_id"

HTTP Request  | Name Endpoint              |  Endpoint
--------------|----------------------------|----------------------
POST          | Groups create              | {{url}}/api/oauth/groups/create_group

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | Int    | Obligatorio (Desde CMS)
group_name            | String | Obligatorio







## Update grupo
> Update grupo:

```java
{
    "user_id": 2,
    "group_id": 2,
    "group_name": "GroupNameToUpdate"
}
```
```javascript
{
    "success": 1,
    "message": "El grupo se ha creado exitosamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": null
}
{
    "success": 0,
    "message": "Falta agregar información",
    "data": null
}
{
    "success": 0,
    "message": "No tienes permisos para realizar esta operación",
    "data": null
}
{
    "success": 0,
    "message": "No existe el grupo ",
    "data": null
}
{
    "success": 0,
    "message": "El grupo con este nombre ya existe",
    "data": null
}
```

Este endpoint crea un nuevo grupo. Para actualizar grupos de CMS es obligatorio el "user_id"

HTTP Request  | Name Endpoint              |  Endpoint
--------------|----------------------------|----------------------
POST          | Groups update              | {{url}}/api/oauth/groups/update_group

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | Int    | Obligatorio (Desde CMS)
group_id              | Int    | Obligatorio
group_name            | String | Obligatorio







## Delete grupo
> Delete grupo:

```java
{
    "user_id": 2,
    "group_id": 2,
    "delete_users": true
}
```
```javascript
{
    "success": 1,
    "message": "Se elimino el grupo correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": null
}
{
    "success": 0,
    "message": "Falta agregar información",
    "data": null
}
{
    "success": 0,
    "message": "No tienes permisos para realizar esta operación",
    "data": null
}
{
    "success": 0,
    "message": "No existe el grupo ",
    "data": null
}
```

Este endpoint elimina un grupo. Para eliminar grupos de CMS es obligatorio el "user_id"

HTTP Request  | Name Endpoint              |  Endpoint
--------------|----------------------------|----------------------
POST          | Groups Delete              | {{url}}/api/oauth/groups/delete_group

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type    | Mandatory
----------------------|---------|----------
user_id               | Int     | Obligatorio (Desde CMS)
group_id              | Int     | Obligatorio
delete_users          | Boolean | Obligatorio






## Update users group
> Update users group:

```java
{
    "user_id": 2,
    "origen_group_id": 2,
    "destination_group_id": 4
}
```
```javascript
{
    "success": 1,
    "message": "Actualización de grupo exitosa",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": null
}
{
    "success": 0,
    "message": "Falta agregar información",
    "data": null
}
{
    "success": 0,
    "message": "No existe el usuario secundario",
    "data": null
}
{
    "success": 0,
    "message": "No existe el grupo ",
    "data": null
}
{
    "success": 0,
    "message": "Falló al realizarse la operación",
    "data": null
}
```

Este endpoint actualiza a un usuario de grupo.

HTTP Request  | Name Endpoint              |  Endpoint
--------------|----------------------------|----------------------
POST          | Groups Update user         | {{url}}/api/oauth/groups/update_user_group

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type    | Mandatory
----------------------|---------|----------
user_id               | Int     | Obligatorio
origen_group_id       | Int     | Obligatorio
destination_group_id  | Int     | Obligatorio







## Delete users group
> Delete users group:

```java
{
    "user_id": 2,
    "group_id": 2
}
```
```javascript
{
    "success": 1,
    "message": "Se elimino el grupo correctamente",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": null
}
{
    "success": 0,
    "message": "Falta agregar información",
    "data": null
}
{
    "success": 0,
    "message": "No existe el usuario secundario",
    "data": null
}
{
    "success": 0,
    "message": "No existe algún ID de grupo enviado",
    "data": null
}
{
    "success": 0,
    "message": "No existe el grupo ",
    "data": null
}
{
    "success": 0,
    "message": "Falló al realizarse la operación",
    "data": null
}
```

Este endpoint elimina a un usuario de grupo.

HTTP Request  | Name Endpoint              |  Endpoint
--------------|----------------------------|----------------------
POST          | Groups Update user         | {{url}}/api/oauth/groups/delete_user_group

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type    | Mandatory
----------------------|---------|----------
user_id               | Int     | Obligatorio
group_id              | Int     | Obligatorio







#Ubicaciones
## Última ubicación
>Última ubicación:

```java
{
    "user_id": 1
}
```
```javascript
{
    "success": 1,
    "message": "Consulta de información correcta",
    "data": {
        "id": 1,
        "fk_users_id": 2,
        "latitude": "19.395965",
        "longitude": "-99.156067",
        "address": null,
        "description": null,
        "created_at": "2020-02-12 17:55:39",
        "updated_at": "2020-02-12 17:55:39"
    }
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint regresará la última ubicación registrada de un usuario respecto de su ID

HTTP Request  | Name Endpoint   |  Endpoint
--------------|-----------------|----------------------
POST          | Last ubication  | {{url}}/api/oauth/last_location

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | String | Obligatorio





## Historial de ubicaciones
>Historial de ubicaciones:

```java
{
    "user_id": 1
}
```
```javascript
{
    "success": 1,
    "message": "Consulta de información correcta",
    "data": [
        {
            "id": 1,
            "fk_users_id": 2,
            "latitude": "19.395965",
            "longitude": "-99.156067",
            "address": null,
            "description": null,
            "created_at": "2020-02-12 17:55:39",
            "updated_at": "2020-02-12 17:55:39"
        },
        {
            "id": 3,
            "fk_users_id": 2,
            "latitude": "19.395965",
            "longitude": "-99.156067",
            "address": null,
            "description": null,
            "created_at": "2020-02-12 16:55:39",
            "updated_at": "2020-02-12 17:55:39"
        },
        {
            "id": 2,
            "fk_users_id": 2,
            "latitude": "19.395965",
            "longitude": "-99.156067",
            "address": null,
            "description": null,
            "created_at": "2020-02-12 14:55:39",
            "updated_at": "2020-02-12 17:55:39"
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint regresará el historial de ubicaciones registradas de un usuario respecto de su ID

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | History ubication   | {{url}}/api/oauth/history_location

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | String | Obligatorio





## Actualizar ubicación
> Actualizar ubicación:

```java
{
    "user_id": 1,
    "latitude": "00.000000",
    "longitude": "00.00000."
}
```
```javascript

{
      "success": 1,
      "message": "Se actualizó la ubicación con éxito",
      "data": null
  }
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint actualiza la última ubicación del usuario. Además de esto, agrega al historial la anterior ubicación.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | Update ubication   | {{url}}/api/oauth/update_location

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                   | Type   | Mandatory
----------------------|--------|----------
user_id               | String | Obligatorio
latitude              | String | Obligatorio
longitude             | String | Obligatorio





# Solicitudes de ayuda App
## Solicitud SOS
> Solicitud SOS:

```java
{
    "address": "Some Address",
    "lat": "00.000000",
    "long": "00.000000",
}
```
```javascript

{
      "success": 1,
      "message": "Se actualizó la ubicación con éxito",
      "data": null
  }
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint lanza una solicitud SOS desde la aplicación para el CMS.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | Solicitud SOS       | {{url}}/api/oauth/new_alert_sos

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                | Type     | Mandatory
-------------------|----------|----------
address            | String   | Opcional
latitude           | String   | Obligatorio
longitude          | String   | Obligatorio



Además de lo anterior, este endpoint generará una notificación (Websocket) al CMS con la siguiente información del usuario que lanzó la notificación: <Enter>

<br />
<br />
```
{
   "user_id": 1, <br />
   "nombre":"magdiel juarez guerrero", <br />
   "latitude":"00.000000", <br />
   "longitude":"00.000000", <br />
   "alert_id":53 <br />
}
```

### Websocket
Key                | Type     | Mandatory
-------------------|----------|----------
user_id            | String   | Obligatorio
nombre             | String   | Obligatorio
latitude           | String   | Obligatorio
longitude          | String   | Obligatorio






## Editar estado solicitud SOS
> Editar estado solicitud SOS:


### Estatus de solicitudes SOS
ID | Estatus
---|----------------------
2  | Se emitió alerta, se atendió y se finalizó
1  | Se emitió alerta y se está atendiendo
0  | Se emitió alerta y no se ha atendido



```java
{
    "alert_id": 132,
    "status": 0
}
```
```javascript
{
    "success": 1,
    "message": "Se actualizó la solicitud móvil con éxito",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}

{
    "success": 0,
    "message": "No existe la alerta seleccionada",
    "data": []
}

```
Este endpoint edita el estatus de una solicitud SOS desde CMS.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | Alert SOS edit      | {{url}}/api/oauth/status_alert_sos

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                | Type     | Mandatory
-------------------|----------|----------
alert_id           | int      | Obligatorio
status             | Int      | Obligatorio






## Response Solicitud SOS
> Response Solicitud SOS:

```java
{
    "alert_id": 32,
    "response": 1
}
```
```javascript

{
      "success": 1,
      "message": "Se actualizó el estatus de esta alerta",
      "data": null
  }
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}

{
    "success": 0,
    "message": "Falla al actualizar el estatus de esta alerta",
    "data": []
}

{
    "success": 0,
    "message": "No existe la alerta seleccionada",
    "data": []
}
```
Este endpoint manda una solicitud SOS después de que el usuario dice que sí necesita ayuda en la app.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | Response push       | {{url}}/api/oauth/response_push

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                | Type     | Mandatory
-------------------|----------|----------
alert_id           | Int      | Obligatory
response           | Boolean  | Obligatory








## Listado solicitudes SOS
> Listado solicitude SOS:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Se envío la solicitud móvil con éxito",
    "data": [
        {
             "id": 273,
             "fk_user_id": 68,
             "fullname": "Saúl Negrete Gaytán",
             "address": "Calle Tenango 1, Lomas del Capulín, La Magdalena Contreras, 01860 Ciudad de México, CDMX, Mexico",
             "created_at": "2020-05-25T19:26:09.000000Z",
             "updated_at": "2020-05-25T19:26:09.000000Z",
             "status": 0,
             "latitude": "19.3063173",
             "longitude": "-99.2697627",
             "audio_alert": null
         },
         {
             "id": 272,
             "fk_user_id": 5,
             "fullname": "Dev Secondary ",
             "address": "Luna 9, Jardines de Cuernavaca, 62360 Cuernavaca, Mor., Mexico",
             "created_at": "2020-05-23T19:35:55.000000Z",
             "updated_at": "2020-05-23T19:35:55.000000Z",
             "status": 0,
             "latitude": "18.926920257",
             "longitude": "-99.20692127",
             "audio_alert": "https://cas-audios.s3.us-east-2.amazonaws.com/audio/1590262559-zghcA-audio.m4a"
         },
         {
             "id": 271,
             "fk_user_id": 5,
             "fullname": "Dev Secondary ",
             "address": "Luna 9, Jardines de Cuernavaca, 62360 Cuernavaca, Mor., Mexico",
             "created_at": "2020-05-23T18:50:22.000000Z",
             "updated_at": "2020-05-23T18:50:22.000000Z",
             "status": 0,
             "latitude": "18.926920257",
             "longitude": "-99.20692127",
             "audio_alert": "https://cas-audios.s3.us-east-2.amazonaws.com/audio/1590259828-j5vu1-audio.m4a"
         },
        ...
    ]
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```
Este endpoint lista todas las solicitudes SOS en el CMS.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
GET           | List SOS            | {{url}}/api/oauth/list_alert_sos

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido







# Push notifications
##Nueva push desde CMS
> Nueva push:

```java
{
    "type_alert": "A",
    "fk_user_sender": "2",
    "title": "Title",
    "description": "Some description",
    "latitude": "00.000000",
    "longitude": "00.000000",
    "address": "Some address description",
    "to_all": 1,
    "date_event": "2020-01-01 00:00:00"
}
```
```javascript
{
    "success": 1,
    "message": "Push enviada correctamente",
    "data": []
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
{
    "success": 0,
    "message": "Falló la generación de push",
    "data": []
}
```

Este endpoint enviará push notifications a los usuarios correspondientes

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | New Push            | {{url}}/api/oauth/new_push

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                | Type     | Mandatory
-------------------|----------|----------
user_id            | String   | Obligatorio
type_alert         | String   | Obligatorio
title              | String   | Opcional
description        | String   | Opcional
latitude           | String   | Obligatorio
longitude          | String   | Obligatorio
address            | String   | Opcional
to_all             | Boolean  | Obligatorio
date_event         | Datetime | Obligatory










## Push listado CMS
> Push listado:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Consulta de alertas exitosa",
    "data": [
        {
            "id": 1,
            "fk_user_sender": 2,
            "type_alert": null,
            "title": null,
            "description": null,
            "created_at": "2020-03-03 19:17:24",
            "updated_at": "2020-03-03 19:17:24",
            "latitude": null,
            "longitude": null,
            "address": null
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
{
    "success": 0,
    "message": "Falló la consulta de alertas",
    "data": []
}
```

Este endpoint listará todas las push notifications

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
GET           | Push list           | {{url}}/api/oauth/alerts

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido







## Push detail CMS
> Push detail:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Consulta de alerta exitosa",
    "data": {
        "alert": {
            "id": 1,
            "fk_user_sender": 2,
            "type_alert": "A",
            "title": "title",
            "description": "description",
            "created_at": "2020-03-03 19:17:24",
            "updated_at": "2020-03-03 19:17:24",
            "latitude": 0,
            "longitude": 0,
            "address": "address"
        },
        "detail_alert": [
            {
                "id_send_to": 1,
                "send_to": "Interphy  ",
                "status": null,
                "created_at": null,
                "updated_at": "2020-03-06T16:45:17.000000Z"
            }
        ]
    }
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
{
    "success": 0,
    "message": "Consulta de alerta fallida",
    "data": []
}
```

Este endpoint mostrará información detallada de una notificación y los usuarios a los que fué enviada.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
GET           | Push detail         | {{url}}/api/oauth/alerts/{alert_id}

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido










# Alerts APP
## Alerts list
> Alerts list:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Consulta de alertas exitosa",
    "data": [
        {
            "id": 1,
            "fk_user_sender": 2,
            "type_alert": "A",
            "title": "title",
            "description": "description",
            "created_at": "2020-03-03 19:17:24",
            "updated_at": "2020-03-03 19:17:24",
            "latitude": 0,
            "longitude": 0,
            "address": "address"
        }
    ]
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint listará las notificaciones que le hayan llegado aun usuario en la aplicación.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
GET           | Push detail         | {{url}}/api/oauth/mobile_alerts

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido





## Alert modify status
> Alert modify status:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Se actualizó la alerta móvil con éxito",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint deshabilitará una solicitud de ayuda enviada desde el móvil

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
GET           | Alert modify status | {{url}}/api/oauth/disable_mobilealert/{alert_id}

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido








# Staff
## Staff list
> Staff list:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Se actualizó la alerta móvil con éxito",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint lista el equipo de staff en el CMS.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
GET           | Staff list          | {{url}}/api/oauth/staff

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido







## Staff creation
> Staff creation:

```java
{
    "name": "Name",
    "first_lastname": "Lastname 1",
    "second_lastname": "Lastname 2",
    "email": "email@xample.com",
    "password": "123Qwe1",
    "type_user_id": 3
}
```
```javascript
{
    "success": 1,
    "message": "Creación de usuario staff exitoso",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
{
    "success": 0,
    "message": "Este correo ya ha sido registrado",
    "data": null
}
```

Este endpoint crea un nuevo usuario del equipo de staff en CMS.

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | Staff creation      | {{url}}/api/oauth/staff

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                 | Type     | Mandatory
--------------------|----------|----------
name                | String   | Obligatorio
first_lastname      | String   | Obligatorio
second_lastname     | String   | Obligatorio
email               | String   | Obligatorio
password            | String   | Obligatorio
cat_type_user_id    | Int      | Obligatorio

### Value cat_type_user_id
Refers              | Value   
--------------------|---------
Moderador           | 3
Admin               | 4   





## Staff update
> Staff update:

```java
{
    "staff_id": 1,
    "name": "Name",
    "first_lastname": "Lastname 1",
    "second_lastname": "Lastname 2",
    "email": "email@xample.com",
    "cat_type_user_id": 3
}
```
```javascript
{
    "success": 1,
    "message": "Actualización de usuario staff exitoso",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint actualiza un usuario del equipo de staff desde CMS

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
POST          | Staff update        | {{url}}/api/oauth/update_staff

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
Key                 | Type     | Mandatory
--------------------|----------|----------
staff_id            | String   | Obligatorio
name                | String   | Opcional
first_lastname      | String   | Opcional
second_lastname     | String   | Opcional
email               | String   | Opcional
password            | String   | Opcional
cat_type_user_id    | Int      | Obligatorio

### Value cat_type_user_id
Refers              | Value   
--------------------|---------
Moderador           | 3
Admin               | 4   







## Staff delete
> Staff delete:

```java
No requerido
```
```javascript
{
    "success": 1,
    "message": "Se ha eliminado el personal del staff",
    "data": null
}
```
```csharp
{
    "success": 0,
    "message": "No estás logueado",
    "data": []
}
```

Este endpoint elimina un usuario del equipo de staff desde CMS

HTTP Request  | Name Endpoint       |  Endpoint
--------------|---------------------|----------------------
DELETE        | Staff Delete        | {{url}}/api/oauth/staff/{staff_id}

### Headers
Key           | Value
--------------|----------------------------
Authorization | Bearer eyJ0eXAiOiJKV1Q...

### Body
No requerido
