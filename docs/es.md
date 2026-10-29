# Cthangover: Murakami — una línea argumental del juego principal

Este mod añade a Cthangover una línea argumental: algo ronda el pueblo, y seguir su rastro lleva a un encuentro con Murakami. Trae los escenarios de ese encuentro, a Murakami como personaje con su retrato y su repertorio de expresiones, una misión en el diario y combates. Forma parte del juego Cthangover y necesita la historia base (`cthangover_game`) para funcionar.

Esta página describe cómo se engancha la línea al juego y cómo empieza; lo que ocurre después se lo deja al jugador.

## Cómo empieza

Cuando Marao llega a la entrada del pueblo, un gruñido llega desde la oscuridad y el jugador elige entre volver a casa o revisar el callejón:

![La entrada del pueblo de noche: el texto «[Un gruñido sordo llegó desde la oscuridad]» con las respuestas Volver a casa y Revisar el callejón.](assets/growl.jpg)

Revisar el callejón inicia la misión **Encuentro con Murakami**, y su primera entrada aparece en el diario:

![El diario con la misión activa Encuentro con Murakami y la entrada «Me encontré con un lobo salvaje en la ciudad; intentaba entrar en una casa cerrada».](assets/journal.jpg)

## Cómo se engancha a la historia base

El mod no cambia ningún archivo del juego base. Añade escenarios a las escenas existentes, y el juego elige cuál representar por su prioridad y condición:

```scenario
scene: town_entry
priority: 10
condition: MeetingMurakamiQuest.notHasTag("wolf_battle")
```

- El escenario de apertura pertenece a la escena `town_entry` con prioridad 10, así que se elige sobre los escenarios ordinarios del pueblo mientras se cumpla su condición.
- Cada paso siguiente de la línea es otro escenario de `town_entry` con prioridad mayor (20, 30) cuya condición mira las etiquetas de la misión `MeetingMurakamiQuest`. El último paso se juega en la casa (`home_vestibule`).
- Los combates arrancan con `battle.init` sobre el sistema de combate de la plataforma; el desenlace se escribe de vuelta como etiqueta de la misión, así el siguiente escenario sabe qué pasó.
- Cuando la línea termina, sus condiciones dejan de cumplirse y el pueblo vuelve a representar sus escenarios ordinarios.

Qué incluye el mod:

- `scenarios/murakami/meeting/` — los cuatro escenarios del encuentro;
- `quests/quests.json` — la misión con tres entradas de diario;
- `characters/player/murakami.json` — Murakami como personaje, con su imagen;
- `avatars/murakami/` — sus expresiones para los diálogos;
- los fondos del encuentro en `backgrounds/town/meetingmurakami/`;
- textos en siete idiomas en `locale/`.

## Cómo desactivarlo

Se puede dejar la línea fuera de la colección del juego: el pueblo entonces representa solo sus propios escenarios y la misión nunca aparece.

## Problemas conocidos

- Dos expresiones de Marao que usan estos escenarios, `marao/what` y `marao/relax`, no existen en el juego, así que esas líneas no muestran retrato. El validador las marca como `REF_NOT_FOUND`.
