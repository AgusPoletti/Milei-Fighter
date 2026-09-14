# Experiencias y correcciones aplicadas

## 1) Bug de colisiones con enemigos "lejanos"

### Síntoma
El jugador moría aunque los enemigos parecían estar lejos en pantalla.

### Causa original
La lógica de colisión estaba usando cajas de colisión genéricas y demasiado pequeñas para los objetos reales del juego. La función `hit(a, b)` comparaba solo coordenadas centrales con anchos/altos default, en vez de usar los tamaños reales de los sprites renderizados.

### Corrección aplicada
- Se aumentaron los tamaños de hitbox del jugador y de los enemigos para que coincidan mejor con el sprite visible.
- Se ajustó la función `hit(a, b)` para usar dimensiones explícitas con un cálculo más consistente.
- Se volvió a revisar la lógica de player/enemy para que la detección sea más fiel a lo que se ve en pantalla.

## 2) Bug de colisiones invisibles / objetos extra que provocaban daño

### Síntoma
Con la visualización de hitboxes activada, el jugador seguía siendo golpeado por objetos que no parecían estar colisionando visualmente.

### Causa original
Había una segunda fuente de daño: enemigos que salían de la pantalla eran eliminados con una penalización de vida (`lives--`) en lugar de solo removerse del array.

### Corrección aplicada
- Se eliminó la pérdida de vida al salir de pantalla.
- Ahora los enemigos fuera de pantalla simplemente se remueven sin descontar una vida.

## 3) Modo de debug para hitboxes

### Síntoma
Necesitábamos una forma rápida de ver qué estaba triggerando las colisiones.

### Causa original
No existía una herramienta visual para inspeccionar hitboxes en tiempo real.

### Corrección aplicada
- Se agregó un toggle con la tecla `T` para activar/desactivar el modo debug de colisiones.
- Cuando está activo, se dibujan cajas rectangulares alrededor del jugador, los enemigos y los proyectiles para facilitar la depuración.

## 4) Verificación final

### Qué se validó
- La lógica del script se comprobó con una validación de sintaxis JavaScript.
- La comprobación final dio resultado positivo:
  - `JS syntax OK`

## Resumen

Estos cambios apuntaron a dos objetivos principales:
1. Corregir los falsos positivos de colisión.
2. Dejar una forma práctica de depurar hitboxes en juego.

Si en el futuro aparecen más errores de colisión, el flujo recomendado es:
- activar `T` para ver hitboxes,
- identificar qué entidad está disparando daño,
- ajustar el tamaño o la condición de colisión según corresponda.
