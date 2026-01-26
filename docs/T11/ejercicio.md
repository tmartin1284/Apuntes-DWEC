¡Claro! 😊 Aquí tienes la **traducción completa al español** del archivo `.md`.
He mantenido **el código intacto** y solo he traducido los textos explicativos, títulos y descripciones.

---

# Práctica Guiada – SPA de Gestión de Usuarios con React Router

## Objetivo

Construir una **Single Page Application (SPA)** usando React que:

- Utilice **React Router v7 (Modo Declarativo)**
- Consuma una **API REST personalizada construida en Python**
- Separe la lógica usando **services** y **custom hooks**
- Implemente **navegación y páginas de detalle**
- Simule **autenticación y rutas protegidas**

---

## Backend API (Proporcionado)

Ya tienes una API en Python ejecutándose localmente:

- GET `http://127.0.0.1:8000/users`

Respuesta de ejemplo:

```json
[
  {
    "id": 1,
    "name": "Vicent",
    "surname": "Foo",
    "email": "vicent@example.com"
  }
]
```

---

## Paso 1 – Crear el Proyecto React

Crea un nuevo proyecto React con TypeScript:

```bash
npm create vite@latest users-spa
cd users-spa
npm install
npm install react-router
code .
npm run dev
```

---

## Paso 2 – Estructura del Proyecto

Organiza el proyecto de la siguiente manera:

```text
src/
 ├─ pages/
 │   ├─ Home.tsx
 │   ├─ Users.tsx
 │   └─ UserDetail.tsx
 ├─ components/
 │   ├─ Navbar.tsx
 │   └─ PrivateRoute.tsx
 ├─ services/
 │   └─ usersService.ts
 ├─ hooks/
 │   └─ useUsers.ts
 ├─ context/
 │   └─ AuthContext.tsx
 ├─ App.tsx
 └─ main.tsx
```

---

## Paso 3 – Configurar React Router (Modo Declarativo)

Edita `App.tsx`:

```tsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import Users from "./pages/Users";
import UserDetail from "./pages/UserDetail";
import Navbar from "./components/Navbar";

function App() {
  return (
    <BrowserRouter>
      <Navbar />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/users" element={<Users />} />
        <Route path="/users/:id" element={<UserDetail />} />
        <Route path="*" element={<h2>Page not found</h2>} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

---

## Paso 4 – Componente de Navegación

Crea `components/Navbar.tsx`:

```tsx
import { Link } from "react-router-dom";

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link> | <Link to="/users">Users</Link>
    </nav>
  );
}

export default Navbar;
```

---

## Paso 5 – Crear el Servicio de Usuarios

Crea `services/usersService.ts`:

```ts
const API_URL = "http://127.0.0.1:8000/users";

export async function getUsers() {
  const response = await fetch(API_URL);
  if (!response.ok) {
    throw new Error("Error fetching users");
  }
  return response.json();
}
```

---

## Paso 6 – Crear un Custom Hook (`useUsers`)

Crea `hooks/useUsers.ts`:

```ts
import { useEffect, useState } from "react";
import { getUsers } from "../services/usersService";

export function useUsers() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    getUsers()
      .then(setUsers)
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  return { users, loading, error };
}
```

---

## Paso 7 – Página de Usuarios (Vista de Lista)

Crea `pages/Users.tsx`:

```tsx
import { Link } from "react-router-dom";
import { useUsers } from "../hooks/useUsers";

function Users() {
  const { users, loading, error } = useUsers();

  if (loading) return <p>Loading users...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          <Link to={`/users/${user.id}`}>
            {user.name} {user.surname}
          </Link>
        </li>
      ))}
    </ul>
  );
}

export default Users;
```

---

## Paso 8 – Página de Detalle de Usuario

Crea `pages/UserDetail.tsx`:

```tsx
import { useParams } from "react-router-dom";
import { useUsers } from "../hooks/useUsers";

function UserDetail() {
  const { id } = useParams();
  const { users } = useUsers();

  const user = users.find((u) => u.id === Number(id));

  if (!user) return <p>User not found</p>;

  return (
    <div>
      <h2>
        {user.name} {user.surname}
      </h2>
      <p>Email: {user.email}</p>
    </div>
  );
}

export default UserDetail;
```

---

## Paso 9 – (Opcional) Autenticación Falsa

Puedes extender la aplicación añadiendo:

- AuthContext
- Custom hook `useUser`
- Rutas protegidas (`PrivateRoute`)
- Página de login

Esto simula el control de acceso del mundo real.

---

## Paso 10 – Resultado Esperado

La aplicación final debería:

- Navegar sin recargar la página
- Mostrar una lista de usuarios desde tu API en Python
- Mostrar los detalles del usuario usando parámetros en la URL
- Usar correctamente services y custom hooks
- Seguir una estructura de proyecto limpia

---

## Criterios de Evaluación

- Uso correcto de React Router
- Consumo de la API desde el backend en Python
- Separación de responsabilidades (pages, services, hooks)
- Legibilidad del código
- Comportamiento correcto de una SPA

---

## Desafío Final (Opcional)

- Añadir un formulario para crear un nuevo usuario
- Añadir UI de carga y errores
- Proteger la ruta `/users` con autenticación
