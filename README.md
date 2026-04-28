# CRUD con Laravel — Laboratorio #2

**Universidad Tecnológica de Panamá**  
Facultad de Ingeniería de Sistemas Computacionales  
Licenciatura en Ingeniería de Sistemas y Computación  

| Campo | Detalle |
|-------|---------|
| Estudiante | Cristian González |
| Cédula | 8-1020-424 |
| Asignatura | Desarrollo de Software VII |
| Grupo | 1GS132 |
| Facilitador | Profesora Irina Fong |
| Semestre | Primer Semestre |

---

## Descripción

Sistema CRUD (Create, Read, Update, Delete) de gestión de productos desarrollado con el framework **Laravel**, utilizando el paquete `ibex/crud-generator` para la generación automática de controladores, vistas, modelos y rutas. El diseño del frontend fue construido con **Bootstrap** y compilado con **Vite**.

---

## Herramientas Utilizadas

| Herramienta | Descripción |
|-------------|-------------|
| Laravel v13.7.0 | Framework PHP principal |
| PHP 8.x | Lenguaje de programación |
| WAMP Server | Servidor local (Apache + MySQL + PHP) |
| MySQL / phpMyAdmin | Motor de base de datos |
| Composer | Gestor de dependencias PHP |
| Node.js / npm | Gestor de paquetes JavaScript |
| Vite v8.0.10 | Compilador de assets frontend |
| Bootstrap | Framework CSS |
| ibex/crud-generator | Generador automático de CRUD |

---

## Estructura de la Base de Datos

**Base de datos:** `CrudCR`  
**Tabla:** `products`

| Columna | Tipo | Descripción |
|---------|------|-------------|
| id | BIGINT (PK) | Identificador único |
| description | VARCHAR(191) | Descripción del producto |
| price | DOUBLE(8,2) | Precio del producto |
| stock | INT | Cantidad en inventario |
| created_at | TIMESTAMP | Fecha de creación |
| updated_at | TIMESTAMP | Fecha de actualización |

---

## Instalación y Configuración

### 1. Clonar el repositorio
```bash
git clone https://github.com/TuUsuario/crudCR.git
cd crudCR
```

### 2. Instalar dependencias PHP
```bash
composer install
```

### 3. Instalar dependencias de Node
```bash
npm install
```

### 4. Configurar el archivo de entorno
```bash
cp .env.example .env
php artisan key:generate
```

Edita el archivo `.env` con tus credenciales de base de datos:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=CrudCR
DB_USERNAME=root
DB_PASSWORD=
```

### 5. Configurar longitud de cadena (AppServiceProvider)
En `app/Providers/AppServiceProvider.php`:
```php
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

### 6. Crear la base de datos y correr migraciones
```bash
php artisan migrate
```

### 7. Compilar el frontend
```bash
npm run dev
```

### 8. Acceder al sistema
```
http://localhost/crudCR/public/products
```

---

## Estructura del Proyecto (MVC)

```
crudCR/
├── app/
│   ├── Http/
│   │   └── Controllers/
│   │       └── ProductController.php   <- Lógica CRUD
│   ├── Models/
│   │   └── Product.php                 <- Modelo Eloquent
│   └── Providers/
│       └── AppServiceProvider.php      <- Config. Schema
├── database/
│   └── migrations/
│       └── ..._create_products_table.php
├── resources/
│   └── views/
│       └── products/
│           ├── index.blade.php         <- Listado
│           ├── create.blade.php        <- Formulario crear
│           ├── edit.blade.php          <- Formulario editar
│           └── show.blade.php          <- Detalle
├── routes/
│   └── web.php                         <- Rutas del sistema
└── .env                                <- Variables de entorno
```

---

## Rutas del Sistema (REST)

| Método | URL | Acción | Descripción |
|--------|-----|--------|-------------|
| GET | `/products` | index | Listar productos |
| GET | `/products/create` | create | Formulario de creación |
| POST | `/products` | store | Guardar producto |
| GET | `/products/{id}` | show | Ver detalle |
| GET | `/products/{id}/edit` | edit | Formulario de edición |
| PUT/PATCH | `/products/{id}` | update | Actualizar producto |
| DELETE | `/products/{id}` | destroy | Eliminar producto |

Ver todas las rutas con:
```bash
php artisan route:list
```

---

## Comandos Utilizados

```bash
# Crear proyecto
laravel new crudCR

# Crear modelo y migración
php artisan make:model Product -m

# Correr migraciones
php artisan migrate

# Instalar generador de CRUD
composer require ibex/crud-generator --dev

# Publicar archivos del paquete
php artisan vendor:publish --tag=crud

# Generar CRUD
php artisan make:crud products

# Actualizar autoload
composer dump-autoload

# Instalar frontend
composer require laravel/ui
php artisan ui bootstrap
npm install
npm run dev
```

---

## Backup de Base de Datos

El archivo de respaldo de la base de datos se encuentra en la carpeta `/database/` del repositorio con el nombre `CrudCR.sql`.

Para restaurarlo:
1. Abre phpMyAdmin en `http://localhost/phpmyadmin`
2. Crea una base de datos llamada `CrudCR`
3. Selecciónala y ve a la pestaña Importar
4. Selecciona el archivo `CrudCR.sql` y haz clic en Importar
