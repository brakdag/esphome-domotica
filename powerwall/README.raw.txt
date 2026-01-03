Quiero hacer un archivo readme bastante profesional, siguiendo los estandards
digamos de google microsoft o empresas importantes.
La idea es organizar todas estas ideas que he obtenido viendo videos y investigando
sobre como funcionan los powerwalls en internet, generalmente de españa y europa powerwalls caseros todos con celdas 18650,pude ver que ponian 14 filas de baterias, que colocaban despues
en serie, y usaban diferentes equipos pero eran todas celdas recicladas, probablemente
equipos de inversiòn, costosos, pero ahorraban en las baterias, o sea en inversor no escatimaban
costos pero si en las baterias, no se porque.
En fin de lo que pude ver, las cosas mas importantes, usaban un testeador, opus bt-c3000, de los
que tambien que hacen lo mismos en algunos paises de centroamerica, pero no pude ver cual, pero mas precario, tambien modulos de descarga, o sea lo que se hace es medir al voltaje que llegan cargado al maximo, tambien se descargan con una resistencia, que mide la capacidad de descarga en mAh, tambien vi que midiendo con diferentes aparatos dan resultados disntinos o muy dispares, por ejemplo 1420 con un aparato y 1550mAh con otro aparato, calculo que serà por la suma de errores.
Tambièn vi el modo de agrupar las celdas, individual o de a 4 en paralelo, pero a su vez despues todo un bloque vertical en paralelo.

Lo más pro que vi fue un desarme de bateria o powerwall de tesla, y es muy distinto, las celdas se colocan como en un relleno de goma, y van lo mas juntas posibles, evitando hacerlo tan espacioso como la gente DIYers, ademas de todo encerrado en un bloque de chapa, como para que no salgan gases o analizar si hay gases, me parecio todo mas hermetico, ademas usan como un pegamento parece para evitar el movimiento, no se como las conectan porque no se ven soldaduras en la bateria de tesla.

Me gustaría que me vayas ordenando las ideas.

Con respecto a los test de descarga, no se si el calculo se hace a una tensión equivalente, por ejemplo 3.7v, o si se va tomando la corriente de descarga y se suma cada segundo una especie de integración directa sin importar a la tension que se descarga, porque no es lo mismo 1A a 4.2V que a 3V. El ampere a 4.2V tiene mayor Wh, que es lo que se almacena en la bateria energía, pero
no conozco como son las curvas de tensión de descarga de las baterías de litio, asique debería buscar y agregar información de esas curvas.

El objetivo de interiorizarme en el tema baterias, es para poder elegir las mejores, o ver cuales
comprar ya recicladas.
En argentina, recuerdo haber comprado baterias usadas por 40 pesos, un lote de 15 baterias, o sea
eran un monton, pero parece que la gente las empezò a reciclar y aumentò la demanda, y el precio
hoy en dia de las baterias usadas, no esta para nada tentador. Al parecer hay personas que las desarman, las prueban y las venden separadas. No investigue si se puede comprar desde china
en argentina, directamente o el mercado internacional, ( al parecer como compran en españa)

Si vi una pagina secondlifestorage.com, donde uno puede buscar con el codigo de las baterias 
usadas, y le da todas las especificaciones tecnicas, que no siempre son igual en distintas baterias, hay baterias buenas y otras no tanto.

Principalmente las baterias se cargan con el integrado tp4056, es para celda individual, tendria
que buscar las specs bien detallado, se alimenta con 5V, que tiene cualquier cargador
de celular y el usb mini o el c. Depende del modelo, tiene dos pines donde se conecta la bateria
B+ y B-, reciclar los BMS, modulos de carga de baterias de notebooks, es muy complejo, se recomienda tirarlos y comprar un bms, para powerwall se compran bms de marca, porque son varias celdas 14, pero intuyo que dentro deben tener bms chinos.

Se recomienda siempre conectar baterias del mismo voltaje, conectar baterias de distinto voltaje
puede generar diferencia de potencial y altas corrientes y calor, a pesar de esto, baterias del mismo voltaja y la misma capacidad, para no generar diferencia de potencial en la descarga. Igualmente la bateria que se descarga antes, se vuelve a cargar con la de la otra bateria, lo que produce una circulacion extra, y digamos mas calor. La perdida en esta carga esta dada por la resistencia interna y la corriente que circule.

En general mis necesidades son 1000wh, que consumo en la noche, consumo de la heladera 200wh %50 ciclo encendito, tv 80w 4hs, y el consumo stand-by 40wh. 