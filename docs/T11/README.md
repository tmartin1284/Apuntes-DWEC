# UNIDAD 11: React – Tema 2: Construcción de una SPA Real

Este segundo y último tema se centra en convertir los conocimientos básicos de React en una **Single Page Application (SPA)** real.

El objetivo es ampliar los conceptos básicos de React añadiendo:

- Enrutamiento
- Obtención de datos
- Estado compartido
- Lógica de autenticación
- Lógica reutilizable mediante _custom hooks_

Este tema refleja cómo React se utiliza habitualmente en proyectos frontend del mundo real.

---

## 1. React Router v7 – Formas de Usar el Router

React Router v7 puede utilizarse de tres formas diferentes, dependiendo de la complejidad de la aplicación.  
Las presentamos de la más simple a la más avanzada.

En esta asignatura trabajaremos principalmente con el **Modo Declarativo**, pero es importante entender que existen otros enfoques.

---

### 1.1 Modo Declarativo (usado en este curso)

El Modo Declarativo es la forma más simple y flexible de usar React Router.  
Las rutas se definen directamente en JSX usando los componentes `<Routes>` y `<Route>`.

Este modo se centra en:

- Navegación
- Renderizado de componentes

La obtención de datos y la lógica se gestionan usando:

- `useEffect`
- services
- context
- custom hooks

#### ¿Por qué el Modo Declarativo?

- Fácil de entender
- Abstracción mínima
- Perfecto para aprender React
- Ideal para SPAs pequeñas y medianas

#### Configuración básica

```ts
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/users" element={<Users />} />
        <Route path="/users/:id" element={<UserDetail />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

### 1.2 Modo Data (visión general)

El Modo Data introduce un enfoque más estructurado.
Las rutas se definen usando objetos en lugar de JSX.

Ideas clave:

- Configuración centralizada del enrutado
- Carga de datos basada en rutas (`loader`)
- Carga automática y gestión de errores

```ts
const router = createBrowserRouter([
  {
    path: "users",
    loader: () => fetch("/api/users"),
    element: <Users />,
  },
]);
```

📌 Este modo es común en proyectos profesionales, pero introduce más complejidad.

---

### 1.3 Modo Framework (visión general)

El Modo Framework es la forma más completa y opinada de usar React Router.

Características:

- Enrutado basado en archivos
- Carga de datos integrada (`loader`)
- Mutaciones integradas (`action`)
- Convenciones fuertes

```ts
export async function loader() {
  return fetch("/api/users");
}
```

📌 Este modo se comporta como un framework completo y queda fuera del alcance de esta asignatura.

---

### 1.4 Comparación de Enfoques

| Modo           | Estilo de Enrutado | APIs de Datos | Complejidad | Uso Típico                 |
| -------------- | ------------------ | ------------- | ----------- | -------------------------- |
| Declarativo    | JSX (`<Routes>`)   | ❌ No         | Baja        | Aprendizaje, SPAs pequeñas |
| Modo Data      | Objetos de ruta    | ✅ Sí         | Media       | SPAs estructuradas         |
| Modo Framework | Basado en archivos | ✅ Sí         | Alta        | Aplicaciones grandes       |

---

## 2. Conceptos de Navegación y Rutas

### Creación del proyecto RR Declarativo

Creamos un proyecto React de la forma habitual. Elegimos el lenguaje de programación que queramos.

```bs
npm create vite@latest

```

Dentro del componente `App` tenemos que incluir dos elementos: indicar qué componente debe renderizarse en función de la ruta, e incluir los links de navegación a estas rutas: Todo dentro del elemento BrouserRouter.

```ts
export default function App() {
  return (
    <>
 <BrowserRouter>
      <nav>
        <Link to="/">Comp</Link>
        <Link to="/comp2">Comp2</Link>
      </nav>


        <Routes>
          <Route path="/" element={<Comp />} />
          <Route path="/comp2" element={<Comp2 />} />
        </Routes>
      </BrowserRouter>
    </>
  );
}
```

### Enlaces de Navegación

```tsx
<Link to="/users">Users</Link>
```

- Evita recargas completas de página
- Mantiene el comportamiento de una SPA

### Navegación Programática

```ts
const navigate = useNavigate();
navigate("/login");
```

### Parámetros de Ruta

```ts
const { id } = useParams();
```

---

## 3. Obtención de Datos desde una API

Las aplicaciones React suelen obtener datos usando `fetch` dentro de `useEffect`.

```ts
useEffect(() => {
  async function loadUsers() {
    const response = await fetch("http://localhost:8000/users");
    const data = await response.json();
    setUsers(data);
  }

  loadUsers();
}, []);
```

---

## 4. Separar la Lógica de la API (Services)

Para mantener los componentes limpios, las llamadas a la API deben colocarse en archivos de servicio.

```ts
export async function getUsers() {
  const response = await fetch("http://localhost:8000/users");
  if (!response.ok) {
    throw new Error("Request failed");
  }
  return response.json();
}
```

---

## 5. Estado Compartido en React

Cuando varios componentes necesitan los mismos datos, el estado debe compartirse.

### Context API (Básico)

```ts
const UserContext = createContext(null);
```

El contexto suele almacenar:

- Usuario autenticado
- Estado de autenticación
- Acciones compartidas (login, logout)

---

## 6. Rutas Protegidas

Algunas rutas solo deberían ser accesibles para usuarios autenticados.

```tsx
function PrivateRoute({ children }) {
  return isAuthenticated ? children : <Navigate to="/login" />;
}
```

---

## 7. Formularios Controlados

En React, los formularios suelen ser controlados mediante estado.

```ts
const [email, setEmail] = useState("");

<input value={email} onChange={(e) => setEmail(e.target.value)} />;
```

---

## 8. Custom Hooks en React

### ¿Qué es un Custom Hook?

Un custom hook es una función JavaScript normal que:

- Empieza por `use`
- Puede usar otros hooks
- Permite reutilizar lógica

Los custom hooks nos ayudan a:

- Evitar lógica duplicada
- Mantener los componentes simples
- Separar la lógica de la interfaz de usuario

---

### Ejemplo: Hook de Autenticación `useUser`

Este hook encapsula toda la lógica de autenticación:

- login
- logout
- registro
- interacción con `UserContext`

```ts
import { useContext } from "react";
import { UserContext } from "../context/UserContext";

export function useUser() {
  const { setUsuario, setIsAuthenticated, setError } = useContext(UserContext);

  const login = async (nick, pass) => {
    try {
      const response = await fetch(
        `http://www.ies-azarquiel.es/paco/apigafas/usuario?nick=${nick}&pass=${pass}`,
      );

      if (!response.ok) {
        throw new Error("Error fetching user");
      }

      const data = await response.json();

      if (data.usuario === null) {
        setIsAuthenticated(false);
        setError("Invalid credentials");
      } else {
        setUsuario(data.usuario);
        setIsAuthenticated(true);
        setError(null);
      }
    } catch (err) {
      setError(err.message);
    }
  };

  const logout = () => {
    setUsuario(null);
    setIsAuthenticated(false);
    setError(null);
  };

  const register = async (nick, pass) => {
    try {
      const response = await fetch(
        "http://www.ies-azarquiel.es/paco/apigafas/usuario",
        {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ nick, pass }),
        },
      );

      if (!response.ok) {
        throw new Error("Registration failed");
      }

      await login(nick, pass);
    } catch (err) {
      setError(err.message);
    }
  };

  return { login, logout, register };
}
```

---

### Por Qué Este Hook es un Buen Ejemplo

- Usa `useContext`
- Centraliza la lógica de autenticación
- Mantiene los componentes limpios
- Patrón profesional realista

---

## 9. Estructura Básica del Proyecto

```text
src/
 ├─ pages/
 ├─ components/
 ├─ services/
 ├─ context/
 ├─ hooks/
 └─ App.tsx
```

---

## 10. Mini Proyecto: SPA de Gestión de Usuarios

El alumnado debería ser capaz de construir una SPA con:

- Enrutado
- Consumo de API
- Autenticación
- Rutas protegidas
- Páginas de detalle usando parámetros

---

## Notas Finales

- Este tema se centra en React práctico
- Los patrones mostrados son comunes en trabajos reales
- Proporciona una base sólida para frameworks como **Next.js**
