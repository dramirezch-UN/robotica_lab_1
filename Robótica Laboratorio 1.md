# Robótica Laboratorio 1

## Herramienta

El diseño de la herramienta se basó en el datasheet de robot ABB IRB140, desde el cual se consiguieron las dimensiones de la placa de montaje para poder transportarlas al diseño en Inventor.
![plano_datasheet](https://i.imgur.com/uOdeqDb.jpg)

El objetivo principal en el diseño de la herramienta fue asegurar que el eje z del plano de montaje y el eje z de la herramienta no estuvieran alienados. Para poder evitar problemas de singularidad en futuros laboratorios. También se tuvo en cuenta las limitaciones de la fabricación por impresión 3D. Por lo cual, se imprimió de manera modular para ensamblar las piezas como la herramienta final.

![inventor](https://i.imgur.com/RCDXKkv.png)


Se utilizó un tubo de PVC de 1/2 para recibir el marcador, aunque debido a un error por no tener en cuenta las tolerancias de fabricación se tuvo que cortar en la parte inferior para poderlo insertar. Se usó un resorte compensar la curvatura e imperfecciones del tablero.

A partir de este diseño se realizó una versión que simula el tubo de PVC junto con el marcador dentro de este para poder tener un modelo fidedigno con el cual trabajar en Robot Studio.

![inventor_herramienta_final](https://i.imgur.com/SFDi1mr.png)



Tras imprimir las piezas diseñadas y comprar los demás materiales, se ensambló la herramienta que sostiene al marcador. Se realizaron unos pequeños ajustes para facilitar su uso:

1. Al tener la herramienta ensamblada nos dimos cuenta de que era probable que el marcador se saliera de su sitio, ya que no estaba amarrado al tubo de PVC. Por esto, el primer ajuste que se hizo fue agregar cinta que conectara al marcador con el tubo de tal forma que no fuera posible que el marcador se saliera, pero que la cinta permitiera el movimiento del marcador hacia adentro del tubo.
2. Nos dimos cuenta de que los agujeros para los tornillos M6 eran muy pequeños. Por esto, tuvimos que ampliarlos. 

![herramienta](https://i.imgur.com/ISQIKxP.png)


Con estas modificaciones, la herramienta pudo ser montada en el robot sin más complicaciones.

![herramienta_calibracion](https://i.imgur.com/2NW6fYt.png)

Para calibrar la herramienta en el robot, se realizó el proceso de llevarlo a un punto 3 veces desde posiciones iniciales distintas.

![herramienta_guardada](https://i.imgur.com/Pn6pkbs.png)

## Programación en Robot Studio
El primer paso a seguir, una vez calibrada la herramienta, fue la de realizar la programación en Robot Studio de la rutina a seguir por el IRB 140. 

Lo primero, fue exportar la herramienta modelada en Inventor a Robot Studio, donde gracias a este procedimiento, fue mucho más fácil la definición del TCP y su precisión a la hora de escribir en la realidad.

![Herramienta en simulador](https://i.imgur.com/BH8aVwi.jpg)

Una vez realizada la respectiva configuración de la herramienta con su alineación, se procedió a exportar las guía para definir los puntos de las letras y poder programar las trayectorias. Como con la herramienta, las letras se diseñaron en Inventor y se exporta a Robot Studio como un objeto. Con el objeto exportado, se le ubicó a una distancia apta para que el brazo alcanzara a llegar sin problema. Se ubicó a x=500 y=100 z=0. 

Con la ubicación definida, se procedió a establecer los puntos en las letras para programar las trayectorias. En donde existen curvas, se marcaban 3 puntos para definir dos trayectorias y que se pudiese generar la curva deseada. Para las trayectorias rectas solo se definían dos puntos. También fue necesario generar puntos para llevar al robot desde el home hasta las letras, para así evitar que 2 o más articulaciones quedaran lineales una respecto a la otra. También fue necesario establecer puntos por encima del plano de escritura para levantar que el brazo hiciera un trazo continuo entre letra y letra. Es de aclarar que todos los puntos deben de invertirse para que la herramienta pueda "atacarlos" correctamente.

![Trayectoria externa de la O](https://i.imgur.com/DBbc0Ns.png)


Con ello definido, se crearon un total de 7 Paths como trayectorias, donde cada dos Paths representarían a una letra, sin contar el primero, que se considera como el acercamiento inicial. Con esto configurado, se procedió a realizar pruebas en el simulador, donde se obtuvieron resultados satisfactorios.

![Foto del simulador en uso](https://i.imgur.com/lXuoBcl.png)

Por último, se realizó la validación en otra posición desplazando el workobject, arrojando resultados satisfactorios. Se realiza la exportación a RAPID y se lleva al laboratorio.



## Programa
Teniendo el código en Rapid listo para ser usado, se cargó este código al robot y se realizó una primera prueba sin montar la herramienta.

En este punto nos dimos cuenta de que faltaba una instrucción al final del programa, la de volver al home. Por lo que se editó el código en RAPID desde el flex pendant para agregar esto.

Se volvió a ejecutar el programa sin la herramienta y tras verificar que el resultado obtenido era el esperado, se montó la herramienta y se realizó una segunda prueba. Para esta prueba, se tomó la precaución de que la herramienta no tocara el tablero. Esto se consiguió cambiando la ubicación z del work object.

Tras esto, se empezó a bajar la ubicación en z del work object hasta que la herramienta tocara el tablero. Desafortunadamente, la ubicación escogida en el tablero no era plana.

![robot_2_mal](https://i.imgur.com/aWshK5P.png)

Por esto, se realizó el mismo proceso en el otro robot y se obtuvieron los resultados esperados:

![ubicacion_1](https://i.imgur.com/shD18hM.jpg)

Luego, para cumplir el requisito de escribir en otra ubicación, se cambiaron las coordenadas del work object y se volvió a correr el programa.

![ubicacion_2](https://i.imgur.com/24dtJwD.png)