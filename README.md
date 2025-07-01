# 🧪 Trabajo Práctico Complementario: Implementación de Búsqueda por Nombre

## 📚 Descripción del Proyecto

Este proyecto es una aplicación **CRUD de productos con MongoDB, Express, React y Node.js (MERN stack)**. Inicialmente permitía crear, leer, actualizar y eliminar productos desde una base de datos.

En esta entrega se agregó una **nueva funcionalidad de búsqueda de productos por nombre**, integrando el frontend y backend mediante una consulta dinámica y parcial.

---

## 🛠️ Tecnologías utilizadas

- **Backend:**

  - Node.js
  - Express.js
  - MongoDB + Mongoose
  - dotenv

- **Frontend:**

  - React.js
  - Vite
  - JavaScript
  - Fetch API
  - Context API (para manejo de sesión de usuario)

---

## 🚀 ¿Cómo ejecutar el proyecto?

### Backend (API)

1. Clonar el repositorio.

2. Ir a la carpeta del backend:

```bash
cd backend
```

3. Instalar dependencias:

```bash
npm install
```

4. Crear un archivo `.env` siguiendo el ejemplo de `.env.example`. Variables necesarias:

```
MONGODB_URI=mongodb://localhost:27017/tu_basededatos
PORT=3000
```

5. Iniciar el servidor:

```bash
npm run dev
```

---

### Frontend (React + Vite)

1. Ir a la carpeta del frontend:

```bash
cd frontend
```

2. Instalar dependencias:

```bash
npm install
```

3. Crear un archivo `.env` siguiendo el ejemplo de `.env.example`. Variables necesarias:

```
VITE_API_URL=http://localhost:3000
```

4. Iniciar el servidor de desarrollo:

```bash
npm run dev
```

---

## 🌟 Nueva funcionalidad agregada: Búsqueda por Nombre

### ✅ ¿En qué consiste la mejora?

Ahora, desde el **frontend**, el usuario puede ingresar un texto de búsqueda y la aplicación devuelve **todos los productos cuyo nombre contenga ese texto**, sin importar mayúsculas o minúsculas.

---

### 💻 ¿Cómo funciona internamente?

#### Backend (API):

Se modificó el controlador `getAllProducts` para permitir buscar por nombre de manera parcial:

```typescript
const { name } = req.query;

let products;

if (name && typeof name === "string" && name.trim() !== "") {
  products = await Product.find({
    name: { $regex: name, $options: "i" },
  });
} else {
  products = await Product.find();
}
```

Esto permite buscar productos que contengan el texto ingresado en cualquier parte del nombre (búsqueda parcial, insensible a mayúsculas/minúsculas).

---

#### Frontend (React):

Se agregó un **input de búsqueda** y se actualizó la función `fetchingProducts` para enviar el parámetro `name` al backend mediante **query params**:

```javascript
const searchValue = { name: value }
const params = new URLSearchParams(searchValue).toString();
const response = await fetch(`${apiUrl}/api/products?${params}`, {
  method: "GET",
});
```

Cada vez que el usuario escribe, se hace una petición GET con el término buscado.

---

## 💻 Ejemplo de uso

1. El usuario abre la app y ve el listado completo de productos.

2. En el campo de búsqueda escribe:

```
"camisa"
```

3. La aplicación muestra solo los productos cuyos nombres incluyan la palabra "camisa", como:

- Camisa Blanca
- Camisa de Jean
- Camisa Roja

4. La búsqueda ignora diferencias entre mayúsculas y minúsculas.

---

## 🔐 Variables de entorno necesarias

### Backend: `.env.example`

```
MONGODB_URI=mongodb://localhost:27017/tu_basededatos
PORT=3000
```

### Frontend: `.env.example`

```
VITE_API_URL=http://localhost:3000
```

---

## Creado por Herrera Franco
