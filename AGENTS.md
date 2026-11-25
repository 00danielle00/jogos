# AGENTS.md — Batalla de Dulces

## Propósito del proyecto

Experiencia de Roblox de estilo obby y combate en una arena de dulces. El proyecto combina recorrido, lobby seguro, combate con caramelos y una interfaz de bienvenida y reglas.

Estas instrucciones orientan a cualquier agente que trabaje en el proyecto. Si el usuario da una indicación distinta, prevalece la indicación del usuario.

## Antes de cambiar algo

1. Comprueba el estado actual del lugar y lee los scripts relacionados con la tarea.
2. Identifica si el cambio afecta al cliente, al servidor o a ambos.
3. Conserva los nombres y rutas existentes cuando sea posible; evita duplicar sistemas.
4. Haz cambios acotados y explica qué scripts, objetos o zonas modificaste.
5. No publiques la experiencia. Guardar en Studio no equivale a publicar.

## Responsabilidades por tipo de tarea

### Nivel y entorno

- Trabaja en `Workspace` y en los objetos visuales o físicos del mapa.
- Mantén transiciones transitables entre obby, puente y arena; comprueba colisiones y puntos donde el personaje pueda atascarse.
- Conserva el tema pastel de dulces y no añadas decoración que bloquee el recorrido o la cámara.
- Al tocar puentes o plataformas, comprueba el recorrido desde ambos sentidos y que no haya huecos, solapamientos ni piezas móviles inestables.

### Combate y reglas de juego

- El servidor es la autoridad para validar disparos, cooldowns, impactos, daño, zonas seguras y reapariciones.
- El remoto de disparo existente es `ReplicatedStorage.Remotes.LanzarCaramelo`. Valida tipo y magnitud de la dirección, posición del jugador y cooldown en el servidor.
- Reglas actuales del combate: 100 de vida, 10 de daño por impacto, cooldown de 0,6 s.
- Lobby: centro aproximado `(0, 50, 0)`, radio 48 studs. Arena: centro aproximado `(0, 50, -160)`, radio 54 studs; altura de combate entre Y=40 e Y=80.
- No permitas daño en el lobby ni daño al propio jugador. Evita que un proyectil dañe más de una vez.
- Comprueba tanto un impacto válido en la arena como un disparo que no debe hacer daño en la zona segura.

### Interfaz y experiencia del jugador

- Mantén la bienvenida breve y las reglas visibles al entrar en la arena hasta que el jugador las cierre.
- Conserva una composición centrada y proporcionada, con tipografía legible en escritorio y móvil.
- No añadas franjas decorativas superiores que sobresalgan del panel o permanezcan durante la animación de cierre.
- Toda interfaz temporal debe ocultar o destruir sus elementos al cerrar; comprueba el final de las animaciones.
- Mantén coherentes colores, botones, mensajes del arma y el estilo pastel del mapa.

### Diagnóstico, pruebas y rendimiento

- Para cambios de combate o replicación, usa **Server & Clients** con dos clientes.
- Comprueba que ambos jugadores aparecen, se ven mover y pueden probar el flujo completo.
- Para daño: confirma que la vida del objetivo baja exactamente 10 por impacto en la arena. En el lobby, la vida no debe bajar.
- Revisa la consola de servidor y cliente después de probar. Informa de errores y de los casos que no se pudieron verificar.
- Distingue tirones de renderizado en Studio de problemas de replicación: revisa FPS y ping y, si hace falta, confirma con dos dispositivos o clientes reales.
- Evita crear pruebas que alteren el lugar persistente; elimina muñecos, proyectiles y objetos temporales al terminar.

## Colaboración entre agentes

- Divide el trabajo por componente: mapa, combate, interfaz o diagnóstico. Asigna un único responsable por script u objeto para evitar ediciones simultáneas.
- Cada agente debe devolver: hallazgo, cambio realizado (si hubo), archivos/rutas afectados y pruebas ejecutadas con resultado.
- El agente coordinador integra los cambios, resuelve conflictos, comprueba la consola y comunica al usuario cualquier limitación.
- No delegues una tarea si una inspección breve basta.

## Límites de los cambios

- No cambies mecánicas, valores de daño, nombres de remotos, límites de arena ni puntos de reaparición sin una razón clara y una comprobación del efecto.
- No reemplaces scripts completos para corregir un detalle localizado.
- No afirmes que una función está probada si solo se leyó el código o se vio aparecer un proyectil.
- No publiques, compartas ni envíes mensajes externos en nombre del usuario.


