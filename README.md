# Quiz Ingenieria Web
## Documentacion:
En este archivo quiz.html implementa una página web que consulta usuarios desde
la API https://randomuser.me.

## Los cambios realizados fueron:

1. Se agregó un filtro para que la API únicamente devuelva usuarios hombres
   utilizando el parámetro ?gender=male en la URL de la consulta.

2. Se añadió un contador que muestra cuántos usuarios han sido consultados
   cada vez que se presiona el botón.

3. Se agregó lógica para cambiar el borde de la foto dependiendo del género.
   En este caso, como solo se consultan hombres, el borde se vuelve azul.

## Version Final de el codigo:
```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Taller Progra Web</title>
<style>

body{
    font-family: Arial;
}

/* Esta es la tarjeta principal donde se muestran los datos del usuario */
.card {
    width: 300px;
    padding: 20px;
    border: 2px solid black;
    text-align: center;
    margin: 100px auto;
    box-shadow: 4px 4px 10px gray;
}

/* Este es el contenedor de la foto del usuario */
.foto {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background-color: #ddd;
    overflow: hidden;
    margin: auto;
    border: 5px solid white;
}

/* Este es el botón para cargar otro usuario */
button{
    padding: 10px;
    margin-top: 10px;
    cursor: pointer;
}

</style>
</head>

<body>

<div class="card">

    <div class="foto" id="foto-container"></div>

    <h2 id="nombre">Nombre Aquí</h2>
    <p id="email">Email Aquí</p>

    <button id="btn-cargar">Cambiar Usuario</button>

    <p id="contador">Usuarios consultados: 0</p>

</div>

<script>

/*
La función que se va a ejecutar cuando se presiona el botón cambiar usuario es:
- Consulta la API de RandomUser filtrando únicamente hombres
- Muestra el nombre, email y foto del usuario en el HTML
- Aumenta el contador de usuarios consultados.
*/

let contador = 0;

const boton = document.getElementById('btn-cargar');

boton.addEventListener('click', async () => {

    try {

        /* Se llama a la API para filtar solo hombres */
        const respuesta = await fetch("https://randomuser.me/api/?gender=male");

        /* Convierte la respuesta a formato JSON */
        const datos = await respuesta.json();

        /* Se obtiene el primer usuario del resultado */
        const usuario = datos.results[0];

        /* Muestra el nombre y email del usuario */
        document.getElementById('nombre').innerText = usuario.name.first;
        document.getElementById('email').innerText = usuario.email;

        /* Muestra la foto del usuario */
        document.getElementById('foto-container').innerHTML =
        `<img src="${usuario.picture.large}" width="100">`;

        /* Cambia el borde de la foto a azul */
        const foto = document.getElementById("foto-container");
        foto.style.border = "5px solid blue";

        /* Aumenta el contador de usuarios consultados */
        contador++;

        document.getElementById("contador").innerText =
        `Usuarios consultados: ${contador}`;

    } catch (error) {

        console.error("Algo salió mal:", error);

    }

});

</script>

</body>
</html>
```
