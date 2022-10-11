![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | Vue.js WikiCountries

## Introducción

Después de pasar demasiado tiempo en GitHub, has encontrado un [conjunto de datos JSON de países](https://ih-countries-api.herokuapp.com/countries) y has decidido utilizarlo para crear tu Wikipedia de países.

<p align="center">
  <img src="https://education-team-2020.s3.eu-west-1.amazonaws.com/web-dev/labs/lab-wiki-countries-1.gif" alt="Example - Finished LAB"/>
</p>

## Configuración

- Haz un fork de este repo
- Clona este repositorio
- Abre el LAB y empieza:

  ```bash
  $ cd lab-vue-wiki-countries-es
  $ yarn
  $ yarn start
  ```

## La presentación

- Al terminar, ejecuta los siguientes comandos:

  ```bash
  git add .
  git commit -m "done"
  git push origin main
  ```

- Crea un Pull Request para que tus TAs puedan comprobar tu trabajo.

## Cómo empezar

Limpia el componente `App.vue` para que tenga la siguiente estructura dentro de las etiquetas de la plantilla

```vue
<!-- src/App.js -->
<template>
  <div class="app">
  </div>
</template>
```

<br/>

## Instrucciones

### Iteración 0 | Instalación del vue Router

Recuerda instalar el vue Router:

```shell
$ yarn add vue-router
```

Y configurar el router en su archivo `src/router/index.js`:

```js
// src/router.js
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    path: '/',
    name: 'countries',
    component: () => import(/* webpackChunkName: 'list' */ '../views/CountriesList.vue'),
    children: [
      {
        path: ':code',
        name: 'details',
        component: () => import(/* webpackChunkName: 'details' */ '../views/CountriesDetails.vue')
      },
    ]
  }
];

const router = createRouter({
  history: createWebHistory('/'),
  routes,
  scrollBehavior() {
    document.getElementById('app').scrollIntoView();
  }
});

export default router;
```
## Instrucciones

### Iteración 1.1 | Crear componentes

En esta iteración, nos centraremos en el diseño general. Antes de empezar, dentro de la carpeta `src`, crea la carpeta `components`. Allí crearás al menos el componente:

- `Navbar`: Muestra la barra de navegación básica con el nombre LAB

A continuación, Dentro de la carpeta `src`, crea la carpeta `views`. Allí crearás al menos las vistas:

- `CountriesList`: Muestra la lista de enlaces con los nombres de los países. Cada enlace debe ser un `router-link` que utilizaremos para *enviar* el código del país`(alpha3Code`) a través de la URL.

- `CountryDetails`: Es el componente que renderizaremos a través de la `router` de `vue-router` y que *recibirá* el código del país (`alpha3Code`) a través de la URL.

  En realidad es el id del país (ejemplo: `/ESP` para España, `/FRA` para Francia).

Para ayudarte con la estructura de los componentes, te hemos dado un ejemplo de página dentro de `example.html`.

Si quieres darle estilo puedes cómo abordamos el estilo con [Bulma](https://bulma.io/) en el `example.html`.

### Iteración 1.2 | Componente Navbar

La forma más sencilla de definir un componente en vue es escribir una función JavaScript, también conocida como componente de función. La barra de navegación debería mostrar el título *LAB - WikiCountries*.

### Iteración 1.3 | Componente CountriesList

Este componente debe mostrar una lista de `router-link` que se utilizan para activar el cambio de URL del navegador. Al hacer clic en un componente `router-link` se activará la `router` correspondiente mostrando el componente de detalles del país.

### Iteración 1.4 | Componente CountryDetails y configuración `del router-view`

Ahora que nuestra lista de países está lista, debemos crear la página `CountryDetails`. `CountryDetails` muestra los detalles del país según el enlace que hemos pulsado. Este componente debe ser mostrado/renderizado dinámicamente con el `<router-vue />`.

```vue
<!-- Example -->

<router-view>
```

Los componentes renderizados con Vue.js pueden leer la consulta con `useRoute()`. Podemos utilizarlo para obtener la información procedente de la barra URL del navegador, por ejemplo, el código `alpha3Code` del país.

**NOTA:** Para la imagen pequeña de la bandera, se puede utilizar el `alpha2Code` en minúsculas e incrustarlo en la URL como se muestra a continuación:

- Francia: <https://flagpedia.net/data/flags/icon/72x54/fr.png>
- Alemania: https: [//flagpedia.net/data/flags/icon/72x54/de.png](https://flagpedia.net/data/flags/icon/72x54/de.png)
- Brasil: https: [//flagpedia.net/data/flags/icon/72x54/br.png](https://flagpedia.net/data/flags/icon/72x54/br.png)
- etc.

----

### Iteración 2 | Enlazarlo todo

Una vez creados los componentes, la estructura de los elementos que su `App.vue` va a renderizar debería ser algo parecido a esto:

```html
<div class="app">
  <Navbar />
  <div>
    <CountriesList :countries="countries" />
    <router-view>
  </div>
</div>
```

----

### Iteración 3 | Establecer el estado cuando el componente se monta

Nuestra aplicación `App.vue` debería tirar de `countries` en el método vue data, manteniendo los datos procedentes del archivo `src/assets/countries.json`.

----

### Iteración 4 | Bono | Obtener los datos de los países desde una API

En lugar de confiar en los datos estáticos procedentes de un archivo `json`, vamos a hacer algo más interesante y obtener los datos de una API real.

Hagamos una petición `GET` a la URL <https://ih-countries-api.herokuapp.com/countries> y utilicemos los datos devueltos en la respuesta como lista de países. Puedes usar `fetch` o `axios` para hacer la petición.

Deberías usar el hook `onMounted()` para establecer el hook lifcycle que se ejecuta sólo una vez y hace una petición a la API. La petición debe ocurrir a primera hora cuando se cargue la aplicación, por lo tanto piensa cuándo y desde dónde debemos hacer la petición a la API.

----

### Iteración 5 | Bono | Obtener los datos de un país desde una API

Usando el hook `onMounted()`  configure el componente `CountriesDetails`. Debería hacer una petición a la API RestCountries y obtener los datos del país en cuestión. Puede construir el endpoint de la petición utilizando el `alpha3Code` del país. Ejemplo:

- Estados Unidos: <https://ih-countries-api.herokuapp.com/countries/USA>
- Japón: https: [//ih-countries-api.herokuapp.com/countries/JPN](https://ih-countries-api.herokuapp.com/countries/JPN)
- India: https: [//ih-countries-api.herokuapp.com/countries/IND](https://ih-countries-api.herokuapp.com/countries/IND)

El efecto debe ejecutarse después del renderizado inicial y cada vez que el parámetro de la URL con el `alpha3Code` cambie.

<br/>

¡Feliz codificación! :heart: