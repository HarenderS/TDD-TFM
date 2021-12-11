# TDD-TFM

## TDD
Es una metodología de desarrollo cuyo objetivo es crear primero las pruebas y luego escribir el software. Sus siglas en Inglés son: Test Driven Development y en español significa: Desarrollo guiado por pruebas.

Este concepto no es nada nuevo, fue a finales de los años 80 cuando se comenzó a utilizar esta metodología de desarrollo.

El test-driven development se orienta según los resultados de los casos de prueba definidos por los desarrolladores. Su estructura cíclica garantiza que el código se transmita al sistema productivo únicamente cuando se hayan cumplido todos los requisitos del software. En otras palabras, los elementos del código se refactorizan y se vuelven a poner a prueba en tantas veces como sea necesario, hasta que el test ya no dé errores. Esta estrategia permite enriquecer el software poco a poco con nuevas funciones, redactando nuevo código fuente tras cada test superado. Por este motivo, el TDD se considera un modelo incremental de desarrollo de software.

Para el uso del TDD se deben combinar 2 metodologías: Test-first development (escribir las pruebas primero) y Refactoring (refactorización de código). Para esto, se usa un ciclo de desarrollo que consta de 3 partes principales:
- La prueba debe fallar. (Red: Muchas herramientas muestran los fallos de las pruebas en rojo)
- La prueba debe pasar. (Green: Al igual que lo anterior, las herramientas muestran las pruebas que pasan en verde)
- Se debe mejorar el código. (Refactoring)

Complicaciones que puede haber:
- Hay que pensar en lo que se quiere conseguir con el código y en cómo protegerlo para que no se rompa (probarlo).
-	Tiene una curva de aprendizaje muy pronunciada. Es necesario aprender los principios y patrones de diseño para crear un código limpio y cómo refactorizarlo para mantenerlo así.
-	El código se defiende. El código existente que no está bajo prueba te pilla entre la espada y la pared. Necesita refactorizarlo para ponerlo bajo prueba y necesitas pruebas para refactorizarlo.

Los errores más comunes:
- No seguir el enfoque de «primero la prueba».
- No refactorizar todo el tiempo.
- Escribir más de una prueba a la vez.
- No ejecutar las pruebas con frecuencia, perdiendo la retroalimentación temprana de las mismas.
- Escribir pruebas que son lentas. Todo el conjunto debería completarse en minutos o incluso en segundos.
- Escribir pruebas sin aserciones.
- No escribir el codigo minimo (suficiente para aprobar el test creado no mas).

## Inside-Out

La escuela clásica (Inside-Out) se distingue por centrarse en la verificación del estado de los objetos, siendo por ello imprescindible que el contexto de los test siempre deba estar formado por `objetos reales`, configurados previamente. Para la correcta generación de estos contextos se pueden crear clases que nos ayuden.
La existencia previa de estos `objetos reales`, implica que el diseño de nuestra solución irá creciendo poco a poco desde la base hasta la funcionalidad final. De ahí el sobrenombre de técnica Inside-out. 

Aunque todos los desarrolladores deben tener en cuenta el panorama general, Inside Out TDD permite que el desarrollador se concentre en una cosa a la vez. Cada entidad (es decir, un módulo individual o una clase única) se crea hasta que se construye toda la aplicación. En cierto sentido, las entidades individuales podrían considerarse inútiles hasta que trabajen juntas, y conectar el sistema en una etapa tardía puede constituir un riesgo mayor. Por otro lado, centrarse en una entidad a la vez ayuda a paralelizar el trabajo de desarrollo dentro de un equipo.

Tomando el juego Tic-Tac-Toe como ejemplo, una solución podría incluir al menos tres entidades: un tablero, las notificaciones y un juego.

Usando el enfoque Inside Out, el tablero y las notificaciones se pueden identificar fácilmente como independientes, mientras que el juego integra las entidades en todo el sistema.

El desarrollador se puede centrar primero en las entidades independientes, creando los test y las funcionalidades de esas entidades. Todas las funcionalidades de las entidades independientes van a funcionar perfectamente ya no requieren ningun tipo de interacciones con alguna otra entidad. Con esto, el desarrollador está abordando una pieza aislada de funcionalidad a la vez. Pero cuando se trata del Juego, que es el nivel superior, todas las piezas deben estar juntas, con las entidades individuales interactuando entre sí.

Debido a que Inside Out TDD se enfoca inicialmente en las entidades individuales del sistema, el riesgo de que estas entidades no interactúen correctamente entre sí se lleva a una etapa posterior. Si las entidades no se comunican como se esperaba, se volverá a trabajar.

Esto demuestra que cuando se usa Inside Out TDD, no se requiere una comprensión completa del diseño del sistema al principio. Solo es necesario identificar una entidad para comenzar. Los detalles internos de esa entidad surgen mediante el uso de pruebas unitarias específicas, lo que lleva a un diseño que se adhiere bien al Principio de Responsabilidad Única (SRP). En la etapa inicial, no siempre está claro qué comportamiento debe exponerse en una entidad. Esto podría dar como resultado que se exponga más o menos comportamiento de lo necesario.

Con Inside Out, si hay un grupo de entidades que expresan un comportamiento, como el Juego, las pruebas unitarias pueden abarcar más de una entidad (ya que también se están utilizando el Tablero y las notificaciones). Esto significa que las entidades colaboradoras se pueden reemplazar sin cambiar la prueba, proporcionando un marco para una refactorización segura.


|                                             Lo bueno                           |                                             Lo malo                                          |
|                                            -----------                         |                                          -----------                                         |
| Un camino muy claro y fácil para comenzar, conociendo su capa de comunicación de backend, puede comenzar con la capa de red genérica (si es necesario), aplicar TDD y también respuestas API de stub desde el principio.                                       | En algún lugar entre los casos de uso y la vista, comenzará a detectar e intentar resolver                                                                                            las diferencias en los conceptos que provienen de la lógica de dominio y la vista (UX).      |
| Complejidad incremental, fácil de seguir.                                      |  Muchas veces los cambios serán muy profundos, muchas veces también habrá que cambiar los                                                                                              conceptos completos. Cuando se hagan cambios en el nivel inferior, requerirán un montón de cambios                                                                                    de interfaces hasta la parte superior, lo que inducirá muchos cambios horizontales dolorosos en la                                                                                    misma capa.                                                                                   |
| Puede probar la integración desde las primeras etapas de desarrollo            | Dado que la capa subyacente siempre estará preparada, probada y funcionando, no siempre creará                                                                                        simulacros para ellos, manteniendo así la capacidad de prueba separada de cualquier componente                                                                                        adicional más alta, lo que afectará especialmente y el tipo de prueba de comportamiento potencial                                                                                      de los mismos. Como consecuencia, es posible que deba depurar todas las capas en lugar de detectar                                                                                    un problema en la real.                                                                       |
|                                                                                |La implementación oscilante de los cambios hacia abajo y hacia arriba podría alterar seriamente el                                                                                        cronograma de entrega y los costos esperados.                                               |
|                                                                                |Cada viaje de refactorización hacia abajo y hacia atrás reducirá involuntariamente la calidad del                                                                                       código.                                                                                       |
|                                                                                |Probablemente terminará con un código que no será necesario en absoluto (YAGNI).                |
		
		
## Outside-In

La escuela de Londres (Outside-In) toma un enfoque distinto, centrándose en verificar que el comportamiento de los objetos es el esperado. Dado que este el objetivo final, verificar las correctas interacciones entre objetos, y no el estado en sí mismo de los objetos, mediante este enfoque podremos ahorrarnos todo el trabajo con los objetos reales (creación y mantenimiento) sustituyéndolos por dobles de test.

Siendo este el caso, podremos empezar por la funcionalidad final que se necesita, implementando poco a poco toda la estructura que dé soporte a dicha funcionalidad. Por esto, esta técnica recibe el nombre de Outside-in, en este caso, desarrollando las funcionalidades desde el exterior hacia dentro.

Outside In TDD se presta bien a tener una ruta definible a través del sistema desde el principio, incluso si algunas partes están inicialmente codificadas.

Las pruebas se basan en escenarios solicitados por el usuario y las entidades están conectadas desde el principio. Esto permite que surja una API fluida y la integración se demuestra desde el inicio del desarrollo.

Al enfocarse en un flujo completo a través del sistema desde el principio, se requiere conocimiento de cómo las diferentes partes del sistema interactúan entre sí. A medida que emergen las entidades, se mockean, lo que permite que sus detalles se difieran hasta más tarde. Este enfoque significa que el desarrollador necesita saber cómo probar las interacciones desde el principio, ya sea a través de un marco de simulación o escribiendo sus propios dobles de prueba. Luego, el desarrollador retrocederá, proporcionando la implementación real de las entidades falsificadas o simuladas a través de nuevas pruebas unitarias.

Al usar Outside In TDD, el desarrollador necesita algún conocimiento previo de cómo se comunicarán las entidades en el sistema. El enfoque suele estar en cómo interactúan las entidades más que en sus detalles internos, de ahí el uso de pruebas de aceptación de alto nivel. En el exterior, las soluciones a menudo aplican la Ley de Deméter: nunca se crea una nueva entidad sin que la entidad primaria pregunte qué quiere de ella. Esto se adhiere bien al principio "Diga, no pregunte", y da como resultado que el estado solo se exponga si lo requieren otras entidades. 
Los detalles de implementación del diseño están en las pruebas. Un cambio de diseño generalmente da como resultado que las pruebas también se modifiquen. Esto puede agregar más riesgo o requerir más confianza para implementarlo.

También es importante remarcar el uso de la técnica del doble bucle:
- Comenzaremos por un test de aceptación que falle en el bucle externo, lo que nos guiará al bucle interno.
- En el bucle interno, que representa la metodología de trabajo TDD («Red-Green-Refactor»), implementaremos la lógica de nuestra solución.
- Realizaremos las iteraciones necesarias de este bucle interno hasta conseguir pasar el test de aceptación.

|                                             Lo bueno                           |                                             Lo malo                                         |
|                                            -----------                         |                                          -----------                                        |
| Comenzará con los requisitos del usuario, es decir, desde el inicio del Producto, desde cómo debería funcionar la aplicación.                                                                                                                                        | No hay forma de que los eventuales cambios en cualquier capa se puedan evitar por completo. |
| Al bajar las capas, siempre podrá simular una conexión suelta hacia abajo, manteniendo así cada capa en una forma perfectamente comprobable y preservando un alto nivel de    modularidad, lo que significa capacidad de mantenimiento y capacidad de cambio a nivel de componente.                                                                                                                                                                   | Aunque bajar las capas requiere bastante tiempo, un desarrollador aún tendrá que hacer una                                                                                            evaluación de los requisitos del usuario en comparación con las API existentes e inducir cambios                                                                                      potenciales si es necesario.                                                                 |
|	TDD será tan fluido como con el enfoque Inside-Out, pero además podrá aplicar BDD completo de todas las capas desde el principio.                                                                                                                                     | Problema de actulizar el doble cuando cambia el comportamiento de la clase del doble.       |
|  Con cada paso de desarrollo hacia la API, verá más fácil y rápido si es necesario un cambio. Esto le da más tiempo a la API para ser adaptada (o reemplazada por otra generalmente de Middleware) y el cambio de API no requerirá ningún cambio en el código como lo hace con Inside-Out.
En consecuencia, no habrá muchos cambios oscilantes hacia arriba y hacia abajo de las capas.
La API se puede adaptar a las necesidades del producto y no al revés.             |                                                                                              
		
