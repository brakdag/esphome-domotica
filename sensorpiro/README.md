# Alarma Pirometrica.

## El objetivo:

Convertir una alarma pirométrica convencional, e integrarla a home assistant.

- No invasiva: No debe modificar el funcionamiento normal de la alarma.
- Transformación a litio.

## Especificaciones técnicas.

id_mercadolibre: MLAU173618482

Alarma Domicilio Inalámbrica Sensor Movimiento Sirena Contro

Sensor de movimiento PIR, Alarma wireless + DOS LLAVEROS Remotos.

- Uso sencillo y práctico.
- Ideal para hogar, cobertizo. cochera.
- Fácil instalación, no hay cables para conectar.
- Wireless.
- Area de barrido de 110°.
- Soporte de montaje ajustable.
- Contiene 2 llaveros a control remoto (rango 5m) y montaje en pared.
- Dispara automáticamente una alarma de más de 105DB alertando.
- Detecta movimiento de personas y animales.
- La alarma funciona con 4 pilas AA (NO INCLUIDAS).
- Los controles remotos funcionan con 3 pilas LR44 (INCLUIDA)
- Se puede utilizar también a corriente 220V con fuente de 6V (NO INCLUIDA).

## Características del producto.

```json
{
  "producto": {
    "marca": "Libercam",
    "linea": "Home Secure",
    "modelo": "LTA2019",
    "tipo_dispositivo": "Sensor",
    "cantidad_piezas": 1
  },
  "especificaciones_tecnicas": {
    "tipos_sensores": "Passive Infrared",
    "tipos_detectores": "Movimiento",
    "material": "Plástico",
    "nivel_sonido": "105 dB",
    "distancia_cobertura": "8 m"
  },
  "alimentacion": {
    "tipo_alimentacion": "Pilas",
    "tipo_pila": "AA",
    "con_bateria_respaldo": false,
    "tipo_bateria_respaldo": "4 pilas AA"
  },
  "caracteristicas": {
    "es_inmune_a_mascotas": true,
    "es_resistente_intemperie": false,
    "con_wifi": false,
    "es_inalambrico": true,
    "incluye_control_remoto": true,
    "con_discado_automatico": false,
    "con_alarma_sonora": true,
    "con_alarma_discreta": false
  },
  "configuracion_sistema": {
    "cantidad_zonas": 1,
    "cantidad_max_sensores": 1,
    "cantidad_alarmas": 1,
    "cantidad_sensores": 1,
    "cantidad_sirenas": 1
  }
}
```

## Funciones añadidas.

- Manejo sirena.
- Lectura estado sirena.
- Estado de sensor.
- Alimentación con 18650 batería litio.
- Cargador y manejador baterías de litio.

## Recopilación de información Alarma.

### Ingeniería inversa.

- Código de PCB Y16-85 (probablemente diseñado en 2016)
- Integrado: BSS00001 XY9336 (manejo de pirométrico)
- integrado 8 pines, sin código, manejo de alarma.

### Comportamiento.

- Led rojo 1: de estado este led enciende y se puede ver a través del plástico
  rojo donde se encuentra en sensor IR, es un indicador deque posee batería.
- Led verde armado de alarma: El led verde enciende cuando la alarma esta
  activada dura 20 segundos y se apaga, aun sigue encendiendo el led rojo 1.
- Led rojo 1: Alarma activada: Cuando detecta movimiento parpadea 6 veces
  y luego hace sonar la sirena manteniendo la luz roja encendida permanente.

## Control remoto.

- El control remoto tiene un único botón, ARM/DISARM.
- Led rojo que enciende únicamente cuando uno presiona el botón.
- Alimentación 3 pilas en serie LR44 AWG 0%Mg.Pb CELL.
- La placa dice NC13648 la placa tiene de un lado el emisior IR el boton y el
  led y del otro lado tiene el circuito con los componentes soldados smd.

## Modificaciones realizadas.

- Se agregó un circuito TP4056 usb C con una batería 18650 SONY y se quito,
  el jack hembra para alimentación y se retiro la caja para 4 baterías de 1.2v AA.

- Se decidió usar un ESP01s y el GPIO2, para detectar cuando la alarma o el led rojo
  se enciende por mas de 2 segundos, como señal de alarma activada.

- Se decidió conectar con una resistencia de $10k\Omega$ a la entrada del chip que
  controla el led rojo, para que se active con un estado bajo.

- Se agregó en home assistant un disparador para que envíe notificación al
  celular cuando se activa la sirena de la alarma.

- Se alimenta el esp01s directamente de la salida del TP4056, se quiso alimentar
  después del regulador de la misma placa, pero la tension resultante era de 2v.

- Se probó agregando un diodo común, para generar una caída de tension, pero es
  demasiado grande para que no encienda el esp01s.
