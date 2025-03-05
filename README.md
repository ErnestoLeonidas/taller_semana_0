# Taller de HTML: Creación de una Lista de Tareas

## 📌 Introducción

HTML **no es programar**. Programar es hacer que los datos sean procesados dinámicamente, mientras que HTML solo estructura el contenido.

## 📖 ¿Qué es HTML?

HTML (*HyperText Markup Language*) es un lenguaje utilizado para crear y estructurar páginas web. Se basa en **etiquetas y atributos** para indicar cómo mostrar los elementos en una página. Con HTML puedes crear:

✅ Secciones  
✅ Párrafos  
✅ Enlaces  
✅ Listas  
✅ Imágenes  
✅ Tablas de datos  

Sin embargo, **HTML no es un lenguaje de programación** porque no permite:

❌ Uso de variables  
❌ Control de flujo (*condiciones, bucles, funciones*)  
❌ Manipulación de datos  

## 🚀 Proyecto: To-Do List con HTML, CSS y JavaScript

Vamos a construir una **Lista de Tareas** usando HTML para la estructura, CSS para el diseño y JavaScript para la interacción.

---

## 🏗 Paso 1: Crear el Esqueleto HTML

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
</head>
<body>
    <!-- Contenedor principal -->
    <div id="app">
        <h2>Lista de Tareas</h2>
        <!-- Input para escribir una nueva tarea -->
        <input type="text" id="nuevaTarea" placeholder="Agregar tarea">
        <button id="agregarBtn">Agregar</button>
        <!-- Lista de tareas -->
        <ul id="listaTareas"></ul>
    </div>
</body>
</html>
```

🔹 **Tip:** Puedes escribir `html:5` y presionar `Tab` en VS Code para autocompletar la estructura.  
🔹 **Tip:** Usa **Live Server** en VS Code para visualizar los cambios en tiempo real.

---

## 🎨 Paso 2: Aplicar Estilos con CSS

```css
body {
    font-family: Arial, sans-serif;
    max-width: 400px;
    margin: 20px auto;
    text-align: center;
}

/* Contenedor del input y botón */
.input-container {
    display: flex;
    gap: 10px;
    justify-content: center;
}

/* Estilo del input */
input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 20px;
    background-color: #f0f0f0;
    color: #333;
    outline: none;
    width: 100%;
}

/* Estilo del botón */
button {
    padding: 10px;
    border: none;
    border-radius: 20px;
    background-color: #28a745;
    color: white;
    cursor: pointer;
    transition: background 0.3s ease;
}

/* Cambio de color al pasar el mouse */
button:hover {
    background-color: #218838;
}
```

🔹 **Tip:** Los estilos deben ir dentro de `<style></style>` en el `<head>` o en un archivo `.css` externo.

---

## 🎯 Paso 3: Agregar Interactividad con JavaScript y Vue.js

```html
<script>
const { createApp, reactive } = Vue;

createApp({
    setup() {
        // Estado reactivo
        const state = reactive({
            nuevaTarea: '',
            tareas: []
        });

        // Agregar una tarea
        const agregarTarea = () => {
            if (state.nuevaTarea.trim() !== '') {
                state.tareas.push({ texto: state.nuevaTarea.trim(), completada: false });
                state.nuevaTarea = ''; // Limpiar el input
            }
        };

        // Eliminar una tarea
        const eliminarTarea = (index) => {
            state.tareas.splice(index, 1);
        };

        return { state, agregarTarea, eliminarTarea };
    }
}).mount("#app");
</script>
```

**Modificación del HTML para integrar Vue.js:**

```html
<!-- Contenedor del input y botón -->
<div class="input-container">
    <input v-model="state.nuevaTarea" @keyup.enter="agregarTarea" placeholder="Agregar tarea">
    <button @click="agregarTarea">Agregar</button>
</div>

<!-- Lista de tareas -->
<ul>
    <li v-for="(tarea, index) in state.tareas" :key="index">
        <div class="task-content">
            <input type="checkbox" v-model="tarea.completada">
            <span :class="{ completada: tarea.completada }">{{ tarea.texto }}</span>
        </div>
        <button class="eliminar" @click="eliminarTarea(index)">X</button>
    </li>
</ul>
```

---

## 🎨 Paso 4: Mejorar el Diseño con CSS

```css
/* Lista de tareas */
ul {
    list-style-type: none;
    padding: 0;
}

/* Estilo de cada tarea */
li {
    background: #f4f4f4;
    padding: 10px;
    margin: 5px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 10px;
}

/* Alineación del checkbox y el texto */
.task-content {
    display: flex;
    align-items: center;
    gap: 10px;
}

/* Estilo para tareas completadas */
.completada {
    text-decoration: line-through;
    color: gray;
}

/* Botón de eliminar */
.eliminar {
    background: red;
    color: white;
    border: none;
    padding: 5px;
    cursor: pointer;
    border-radius: 5px;
}
```

---

## 🎉 ¡Listo! 🚀

Con estos pasos, hemos creado una lista de tareas dinámica utilizando **HTML, CSS y Vue.js**. ¡Prueba el código y personalízalo a tu gusto!

📢 **¿Cómo ejecutar el proyecto?**
1. Guarda el archivo como `todo.html`.
2. Usa **Live Server** en VS Code o abre el archivo `todo.html` en tu navegador.
3. ¡Empieza a gestionar tus tareas de manera interactiva!

📢 **¿Tienes ideas para mejorar el proyecto?** ¡Abre un issue o haz un pull request en el repositorio!

## 🏆 Desafío: Separar los archivos y ejecutar el programa sin modificaciones

Actualmente, todo el código está dentro de un solo archivo HTML. Tu tarea es **separarlo en tres archivos** y asegurarte de que el programa funcione igual sin sufrir cambios:

1. **Crear un archivo `todo.html`** y mover la estructura HTML ahí.
2. **Crear un archivo `style.css`** y enlazarlo correctamente desde el HTML.
3. **Crear un archivo `script.js`** y enlazarlo en el HTML para que la lógica de la lista de tareas siga funcionando.

🔹 **Pistas:**
- Usa la etiqueta `<link>` en el `<head>` para conectar `style.css`.
- Usa `<script src="script.js"></script>` antes de cerrar `</body>` en `todo.html`.
- No modifiques la funcionalidad, solo separa los archivos.

¡Súbelo a tu repositorio y prueba que sigue funcionando! 🚀


---
✨ **BIENVENIDOS A DUOC** ✨  
