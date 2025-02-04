# **APÉNDICE B Aprendiendo TypeScript para React**

Esta guía te introduce a los conceptos esenciales de TypeScript para usarlo eficazmente con React, con una breve explicación de **alias de tipo** e **interfaces**, y cuándo usar cada uno.

---

## 1. **¿Qué es TypeScript?**

TypeScript es un superconjunto de JavaScript que agrega **tipado estático**. Ayuda a detectar errores durante el desarrollo y hace que tu código sea más predecible y fácil de mantener.

Características clave:

- Tipado estático
- Interfaces y tipos para definir estructuras de datos
- Mejora en herramientas y autocompletado de código

---

## 2. **Configurar TypeScript en un proyecto de React**

1. Crea un proyecto de React:

   ```bash
   npx create-react-app my-app --template typescript
   ```

2. Agrega TypeScript a un proyecto de React existente:

   ```bash
   npm install typescript @types/react @types/react-dom
   ```

   Luego, crea un archivo `tsconfig.json` con `npx tsc --init`.

---

## 3. **Conceptos básicos de TypeScript**

### 3.1 Tipos

#### Primitivos

```typescript
const count: number = 5;
const username: string = "John";
const isLoggedIn: boolean = true;
```

#### Arreglos

```typescript
const numbers: number[] = [1, 2, 3];
const names: string[] = ["Alice", "Bob"];
```

#### Objetos

```typescript
const user: { id: number; name: string } = {
  id: 1,
  name: "Alice",
};
```

#### Tipos de unión

```typescript
let result: string | number;
result = "Success";
result = 42;
```

---

## 4. **Alias de tipo vs Interfaces**

### ¿Qué es un alias de tipo?

Un **alias de tipo** es una forma de definir un nombre de tipo personalizado para cualquier tipo en TypeScript. Puede describir:

- Primitivos
- Objetos
- Uniones
- Tuplas
- Funciones

```typescript
type User = {
  id: number;
  name: string;
};

type Status = "active" | "inactive";
type Coordinates = [number, number];
type Callback = (message: string) => void;
```

---

### ¿Qué es una interfaz?

Una **interfaz** está diseñada específicamente para describir la estructura de un objeto. Se puede **extender** o **fusionar**, lo que la hace ideal para definir estructuras de objetos reutilizables.

```typescript
interface User {
  id: number;
  name: string;
}

interface Admin extends User {
  permissions: string[];
}
```

---

### ¿Cuándo usar cada uno?

| Caso de uso                              | Alias de tipo                       | Interfaz                                 |
| ---------------------------------------- | ----------------------------------- | ---------------------------------------- |
| **Definir primitivos, uniones o tuplas** | ✅                                  | ❌                                       |
| **Describir estructuras de objetos**     | ✅                                  | ✅                                       |
| **Extender o fusionar tipos**            | Limitado (usar intersecciones: `&`) | ✅ (`extends` o fusión de declaraciones) |

---

## 5. **TypeScript con React**

### Componentes funcionales con props simples

```typescript
import React from "react";

type Props = {
  title: string;
};

const Header: React.FC<Props> = ({ title }) => {
  return <h1>{title}</h1>;
};

export default Header;
```

---

### Props con estructuras de datos complejas

#### Ejemplo: Arreglo de objetos como props

Cuando una prop es un arreglo de objetos, puedes usar un alias de tipo o una interfaz para definir su estructura.

```typescript
type Item = {
  id: number;
  name: string;
};

type ListProps = {
  items: Item[];
};

const ItemList: React.FC<ListProps> = ({ items }) => {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
};

export default ItemList;
```

---

### Estado con estructuras de datos complejas

#### Ejemplo: Estado con un arreglo de objetos

```typescript
import React, { useState } from "react";

type Task = {
  id: number;
  description: string;
  completed: boolean;
};

const TaskManager: React.FC = () => {
  const [tasks, setTasks] = useState<Task[]>([
    { id: 1, description: "Aprender TypeScript", completed: false },
    { id: 2, description: "Construir una app con React", completed: true },
  ]);

  const toggleTask = (id: number) => {
    setTasks((prevTasks) =>
      prevTasks.map((task) =>
        task.id === id ? { ...task, completed: !task.completed } : task
      )
    );
  };

  return (
    <ul>
      {tasks.map((task) => (
        <li key={task.id}>
          <span
            style={{ textDecoration: task.completed ? "line-through" : "none" }}
          >
            {task.description}
          </span>
          <button onClick={() => toggleTask(task.id)}>
            {task.completed ? "Deshacer" : "Completar"}
          </button>
        </li>
      ))}
    </ul>
  );
};

export default TaskManager;
```

---

### Props con objetos anidados

#### Ejemplo: Objetos anidados en props

```typescript
type Address = {
  street: string;
  city: string;
  postalCode: string;
};

type User = {
  id: number;
  name: string;
  address: Address;
};

type UserCardProps = {
  user: User;
};

const UserCard: React.FC<UserCardProps> = ({ user }) => {
  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.address.street}</p>
      <p>
        {user.address.city}, {user.address.postalCode}
      </p>
    </div>
  );
};

export default UserCard;
```

---

## 6. **Resumen**

- Usa **alias de tipo** para definir **primitivos**, **uniones**, **tuplas** o **tipos de funciones**.
- Usa **interfaces** para definir **estructuras de objetos**, especialmente cuando necesites **extensibilidad** o **fusión de declaraciones**.
- Para props y estados con **estructuras de datos complejas**, define tipos/interfaces reutilizables para mantener claridad y consistencia.

Al combinar estos conceptos, puedes manejar props y estado en React de manera efectiva mientras aprovechas la potencia de TypeScript. 🚀
