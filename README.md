1. Escriba la diferencia entre Vue y Nuxt.

-La diferencia es que Vue es para hacer una SPA(Single Page Aplication) y NUXT es para hacer una SSR(Server SIde Rendering), una aplicacion del lado del servidor, aprate te da una estructura mas relevante para hacer proyectos ya que es un framework y vue es una libreria de UI.

2. ¿Cómo logra una plataforma ̈X ̈ escribir código en ES6/ES7 (javascript más reciente)
   que sea reconocido por el navegador?

   Logra a travez de Babel, que es un compilador de javascript. Convierte lo ultimo de javascript a javascipt antiguo para dar soporte a todo.

3. ¿Qué significan las siglas SSR en función del frontend?

Significa Server Side Rendering, sirve para hacer Render del lado del servidor, por eso la mejor opcion es Nuxt en vez de Vue en este caso, tambien sirve para el SEO.

4. ¿Tienes conocimientos en TypeScript? Si tu respuesta es sí, explica cómo lo has usado
   y si lo usas en Vue y/o Nuxt.
   ** Sí
   ** No

   No tengo conocimiento en Typescript por ahora.

5. Describa su proceso de creación de urls en Nuxt que sean accesibles por el navegador.
   Ejemplo: Si se necesitarán la urls dominio.com/categorias/detalle/categoria-uno,
   dominio.com/categorias/detalle/categoria-dos, ¿cómo las configuraría en Nuxt?

   crearia una carpeta categorias en la carpeta pages, dentro de la misma una carpeta detalles, dentro un componente llamado categoria-uno y dentro de la carpeta deltalle otro componnte categoria-dos.
   en el caso de que las categorias sean de mañera dinamica crearia el componente categoria-[id].
