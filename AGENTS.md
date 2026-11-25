# AGENTS.md — Piso 13: No bajes

## Objetivo

Crear desde cero una experiencia social de Roblox de rondas cortas, fácil de entender en móvil y divertida en grupo. El nombre y el concepto son provisionales: si Dani los cambia, actualizar este documento y seguir la nueva dirección.

No prometas viralidad ni ingresos. Diseña para que el primer minuto sea claro, las rondas sean rejugables y jugar con amigos mejore la experiencia. Roblox recomienda priorizar satisfacción, interacción social, retención y metadatos fieles; sus sistemas de descubrimiento no garantizan visibilidad. Referencias: [Discovery](https://create.roblox.com/docs/discovery), [monetización](https://create.roblox.com/docs/production/monetization).

## Concepto de partida

**Piso 13: No bajes** — 2 a 8 jugadores viajan en un ascensor que se detiene en plantas impredecibles. En cada planta, el grupo afronta un minirreto breve y elige entre dos puertas o modificadores. El objetivo de la primera versión es sobrevivir cuatro plantas y llegar a la salida.

El tono debe ser cómico, extraño y apto para Roblox; cada reto debería producir momentos que los jugadores quieran contar o compartir. No copiar personajes, mapas, nombres, música, interfaces ni recursos de otros juegos.

### Bucle principal

1. El jugador aparece en un lobby pequeño y entiende cómo empezar sin tutorial largo.
2. Se reúne con otros jugadores en el ascensor; una cuenta atrás inicia la ronda.
3. Se revela una planta y una regla visualmente clara.
4. Los jugadores superan el reto, cooperan o toman una decisión rápida.
5. Quienes sobreviven reciben fichas y una puntuación de ronda.
6. El ascensor continúa; al completar cuatro plantas, el grupo celebra y puede repetir.

La primera versión debe tener un lobby, un ascensor, cuatro retos sencillos, una condición clara de victoria y una pantalla de resultado. Evita sistemas de mascotas, combate, obby largo, trading y economía persistente hasta validar el bucle principal.

## Prioridades de producto

1. Que un jugador nuevo entienda qué hacer en menos de 10 segundos.
2. Que la primera ronda empiece rápido y funcione en teclado, mando y pantalla táctil.
3. Que el juego sea divertido incluso con pocos jugadores; escala el reto según el número presente.
4. Que cada planta varíe una mecánica de forma legible, no solo el color o la decoración.
5. Que perder sea rápido, comprensible y anime a volver a intentarlo.
6. Mantén accesibles las acciones básicas; las compras nunca deben ser necesarias para terminar una ronda.

## Diseño y monetización

- Construye primero un MVP gratuito y completo. No pongas anuncios, compras ni prompts de pago en la primera ronda de un jugador.
- Cuando el bucle principal esté probado, propón cosméticos opcionales: aspectos del ascensor, gestos, efectos visuales y títulos.
- No vendas ventaja competitiva, supervivencia garantizada, fichas necesarias para progresar ni objetos aleatorios de pago.
- No crees precios, Game Passes, Developer Products, suscripciones ni anuncios sin una petición expresa y aprobación de Dani.
- Muestra claramente qué compra el jugador y evita interfaces engañosas o presión para gastar.
- No inventes ingresos esperados ni afirmes que una opción garantiza más Robux.

## Arquitectura y reglas técnicas

- Inspecciona el lugar de Roblox abierto antes de modificarlo. El proyecto se está reiniciando; no asumas que quedan mapa o scripts de Batalla de Dulces.
- Separa responsabilidades: el servidor decide estado de ronda, jugadores válidos, resultados y recompensas; el cliente presenta UI, animaciones y efectos.
- Valida en servidor toda acción recibida por RemoteEvents: tipo, límites, estado de ronda y frecuencia. Nunca aceptes del cliente una recompensa o victoria como cierta.
- Mantén la lógica de retos modular y con configuración compartida. No crees una copia de toda la ronda para cada planta.
- Usa nombres claros y una estructura fácil de explorar. Antes de añadir un RemoteEvent o ModuleScript, busca si ya existe uno equivalente.
- Guarda datos persistentes solo cuando haya una necesidad real; prueba fallos de carga/guardado y no bloquees la partida si DataStore no responde.
- Evita dependencias externas, assets sin permiso y modelos gratuitos sin revisar scripts, contenido y licencias.
- No escribas secretos, claves ni tokens en el repositorio.

## Organización sugerida

Adapta esta estructura al proyecto abierto; no crees carpetas vacías sin uso.

- `Workspace`: `Lobby`, `Elevator`, geometría de la planta activa.
- `ReplicatedStorage/Shared`: configuración de rondas y tipos compartidos.
- `ReplicatedStorage/Remotes`: eventos estrictamente necesarios.
- `ServerScriptService`: coordinador de rondas y lógica validada de retos.
- `StarterPlayer/StarterPlayerScripts`: controles y presentación cliente.
- `StarterGui`: HUD de cuenta atrás, estado del reto y resultado.

## Responsabilidades por actividad

### Coordinación

- Convierte la petición actual en cambios concretos y pequeños.
- Inspecciona el juego antes de asignar trabajo; un agente es responsable de cada script o zona durante una tarea.
- Integra resultados, evita cambios duplicados y reporta decisiones, limitaciones y estado de pruebas.
- Si se dispone de subagentes, asigna tareas separadas (mundo, juego, UI o QA) y pide a cada uno archivos/rutas, resumen y pruebas. No delegues una inspección sencilla.

### Mundo y retos

- Construye el lobby, ascensor y plantas con siluetas legibles y rutas accesibles.
- Cada reto debe tener una regla, inicio, fin, fallo y duración definidos.
- Prueba colisiones, caídas, cámara y lectura desde móvil; evita obstáculos invisibles y spawn points peligrosos.
- Reutiliza piezas y variantes configurables en lugar de clonar escenas enteras.

### Gameplay y servidor

- Implementa el estado de la ronda, el temporizador, entrada/salida de jugadores, selección de planta, supervivencia y resultados.
- Maneja jugadores que se unen tarde, abandonan o mueren durante una ronda.
- No otorgues fichas dos veces por el mismo resultado.
- Conserva el servidor como autoridad y registra errores útiles sin inundar la consola.

### UI y UX

- Mantén una sola instrucción principal por pantalla.
- Da feedback inmediato a votos, cuenta atrás, aciertos, fallos y resultados.
- Comprueba tamaños y contraste en móvil, escritorio y mando.
- Respeta animaciones cortas y elimina las interfaces temporales al cerrarlas.

### QA, datos y rendimiento

- Prueba en **Server & Clients** con dos clientes como mínimo cuando se modifique multiplayer, replicación, rondas o recompensas.
- Recorre las cuatro plantas de principio a fin; verifica empate/abandono, una sola recompensa y retorno al lobby.
- Revisa consola de cliente y servidor. Informa qué se probó y qué quedó pendiente.
- Usa métricas de Roblox para buscar problemas de incorporación, duración de sesión y retorno; no optimices una métrica a costa de frustrar a jugadores.
- Separa tirones de renderizado local de retrasos de red; comprueba FPS y ping antes de cambiar física o replicación.

## Flujo de trabajo automático

Cuando Dani pida construir o mejorar el juego:

1. Lee este archivo y revisa el estado real del lugar y los scripts afectados.
2. Elige el cambio mínimo que acerque al MVP o corrija un problema.
3. Implementa en Roblox Studio y evita editar sistemas no relacionados.
4. Ejecuta las pruebas manuales pertinentes, incluida la prueba de dos clientes si afecta al multiplayer.
5. Corrige errores observados; no afirmes que está terminado si la consola tiene errores o el flujo no se pudo probar.
6. Guarda el lugar al completar cambios autorizados.
7. Devuelve un resumen breve: qué cambió, pruebas y resultados, limitaciones y siguiente paso.

Automatiza dentro de Roblox Studio las acciones reversibles de construcción y verificación. Pide a Dani intervención solo para iniciar sesión, elegir una dirección creativa importante no especificada, autorizar compras/publicación o completar un paso que requiera su cuenta/dispositivo.

## Límites y publicación

- No publiques la experiencia, no gastes Robux ni crees productos/anuncios sin autorización explícita.
- Guardar en Studio no es publicar; deja claro cuál de las dos acciones se realizó.
- No borres el lugar, assets, historial ni datos persistentes sin autorización explícita.
- No modifiques políticas de edad, privacidad, permisos o acceso para aumentar métricas.
- No cambies el concepto provisional por otro sin comentarlo con Dani.
- No inventes pruebas, resultados de métricas, jugadores concurrentes ni ingresos.
