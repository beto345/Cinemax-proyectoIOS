Díaz Castellanos Alejandro Isaías
Vazquez Enriquez Alberto

Flujo:

Inicio -> Lista de Películas -> Detalle
Detalle -> Descripción de película -> Agregar a favoritos
Buscar -> Resultado de Búsqueda -> Detalle
Favoritos -> Mis Favoritos -> Detalle -> Quitar favoritos

<img width="636" height="277" alt="Captura de pantalla 2026-09-21 a la(s) 4 24 19 p m" src="https://github.com/user-attachments/assets/3ff134cb-d560-4367-9a6d-ea1cc4dc07dd" />


1. ¿Qué problema aborda nuestro proyecto y quién es el usuario?
Cinemax termina con el problema de descubrir, buscar y guardar películas rápidamente desde tu celular, sin tener que recordar títulos ni entrar en sitios pesados. Usa el catálogo de TMDB para mostrar portada, título e info básica, permite buscar, ver detalle (sinopsis y fecha de estreno) y marcar favoritas guardadas localmente. El usuario es un cinéfilo con iPhone que quiere “explorar y encontrar sus películas favoritas” (como dice la pantalla de inicio) y tener una lista personal a mano.

2. ¿Qué es el MVP y por qué deberíamos limitar el alcance?
El MVP (Producto Mínimo Viable) es la versión más pequeña de la app que ya resuelve de punta a punta el problema completo. El MVP obligatorio según la diapositiva es: lista de películas desde TMDB, búsqueda con resultados y manejo de “sin resultados”, detalle (poster, título, sinopsis, estreno), agregar/quitar favoritas con persistencia local, estados de loading, error, vacío y favoritos vacíos. Se limita el alcance porque el tiempo y el equipo son finitos: es mejor entregar tres flujos completos y estables (Inicio > Lista > Detalle; Inicio > Búsqueda > Resultados > Detalle; Inicio > Favoritos > Guardada > Detalle) que muchas funcionalidades a medias. Un alcance acotado permite priorizar, probar pronto y agregar extras (reseñas, calificaciones, login real) sólo cuando lo esencial funcione.

3 SwiftUI funciona bajo un paradigma declarativo. ¿Qué significa esto?
Lo que describimos es qué debe verse según el estado, no cómo construirlo paso a paso. En vez de crear un botón, agregarlo a la vista y actualizarlo manualmente cuando cambien los datos (imperativo, como UIKit), escribimos algo como Text(pelicula.titulo) y if favoritos.isEmpty { EmptyView }; cuando el estado cambia, SwiftUI recalcula y redibuja la interfaz por nosotros.

4 En SwiftUI, View es el tipo base para representar la interfaz de usuario. Cada vista es un valor que describe lo que debe mostrar. Cuando se actualiza el estado de una vista, SwiftUI vuelve a invocar el cuerpo del struct, lo que genera un nuevo árbol de vistas. Luego, SwiftUI compara este nuevo árbol con el anterior y aplica solo los cambios necesarios para actualizar la pantalla.
View es el protocolo que representa cualquier pieza de interfaz: un texto, una imagen, una tarjeta de película o una pantalla completa completa. Cualquier estructura que utilice View describe parte de la interfaz de usuario, y puede anidarse dentro de otras vistas, del mismo modo que las tarjetas “Favoritos” se muestran repetidas dentro de la cuadrícula del diseño.

5 ¿Para qué sirve body?
El cuerpo es la única propiedad obligatoria del protocolo View. Return the content of the view, i.e., the description of what must be drawn. Cada vez que cambia un estado del que depende (@State, @Binding, @ObservedObject, etc.) SwiftUI lo vuelve a evaluar.

6. ¿Que son los modifiers?
Son métodos que se encadenan a una vista para cambiar su apariencia o comportamiento, y devuelven una nueva vista: .font(.title), .padding(), .foregroundColor(.gray), .cornerRadius(12), .onTapGesture { }. Así, por ejemplo, el botón morado “Agregar a favoritos” del diseño, se conseguiría con .background(.purple).foregroundColor(.white).clipShape(Capsule()). El orden de aplicación es importante.

7. ¿Para qué se usa Preview?
#Preview (o PreviewProvider) muestra la vista en el canvas de Xcode en tiempo real, sin compilar y sin ejecutar la app completa en el simulador. Permite iterar rápidamente el diseño, probar la vista con datos de ejemplo y en distintos dispositivos, tamaños de texto o modo oscuro. Es perfecto para poder reproducir las pantallas del Figma antes de conectar TMDB.

8. ¿Cuál es la diferencia entre VStack, HStack y ZStack?

VStack: apila verticalmente sus hijos (poster arriba, título y descripción abajo, como en cada tarjeta de favoritos).
HStack: los acomoda horizontalmente (miniatura a la izquierda y título/descripción a la derecha, como en los renglones de “Section title”).
ZStack: se coloca uno encima del otro en profundidad (por ejemplo un texto o un icono de corazón sobre el poster, o un fondo detrás del contenido).

9. ¿Para qué usamos datos locales en esta fase?
Eso se debe a que, queremos construir y validar la interfaz y la navegación sin depender de la red, la API key de TMDB, ni del manejo de errores y asincronía. Con un mock de películas podemos ver las pantallas en Preview, avanzar en paralelo mientras otros preparan la capa de red y aislar errores: si algo falla, sabemos que es la vista y no la conexión. Más adelante se cambia la fuente local por el servicio de TMDB sin cambiar las vistas.

10. ¿Por qué es importante mantener el proyecto en un estado compilable y hacer commits identificables?
Un proyecto que siempre compila asegura que cualquier miembro pueda descargar la rama y trabajar o mostrar la app en cualquier momento; un build roto impide al equipo entero seguir adelante. Los commits pequeños y con mensajes claros (“Agrega pantalla de detalle con sinopsis”, “Persistencia local de favoritos”) permiten saber quién hizo qué, revisar cambios, revertir un error puntual sin perder lo demás y evidenciar el avance ante el profesor. Esa es la base para trabajar con Git de forma colaborativa.

VoiceOver: 

Pantalla de Inicio:
POSTER DE LA PELICULA
TITULO DE LA PELICULA 
BOTONES INFERIORES (BUSQUEDA, FAVORITOS Y CUENTA) 

Pantalla de Detalle de la película:
TITULO DE LA PELICULA
CALIFICACION DE LA PELICULA 
BOTON DE AGREGAR A FAVORITOS 
SINOPSIS DE LA PELICULA 
PELICULAS SIMILARES (DESPLEGABLE) 
[TITULO DE LA PELICULA 
BOTONES INFERIORES (BUSQUEDA, FAVORITOS Y CUENTA)]

Pantalla de búsqueda: 
BUSCAR
ANTERIOR
CANCELAR
DETALLE DE BUSQUEDA

Pantalla de favoritos
MIS FAVORITOS
POSTER 
TITULO DE LA PELICULA
BOTON PARA ELIMINAR DE FAVORITOS



