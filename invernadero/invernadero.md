# Invernadero controlado por Arduino

## Motivación  

Hemos reciclado una vieja maqueta que teníamos por el laboratorio de Ciencias para construir un pequeño invernadero dotado de los siguientes elementos:

- Sensor de dióxido de carbono.
- Sensor de temperatura y humedad ambiental DHT11
- Sensor de humedad de la tierra
- Ventilador, que  nos permite la extracción y renovación del aire.  

---

## Componentes del montaje  

Se han utilizado los siguientes componentes electrónicos:
- [Placa Keyestudio UNO](KS0001_KEYESTUDIO.pdf)
- [Sensor de temperatura y humedad DHT11](DHT11-Technical-Data-Sheet-Translated-Version-1143054.pdf)
- [Display LCD I2C](I2C_1602_LCD_datasheet.pdf)
- [Sensor de humedad de la tierra KS0049](sensor-de-humedad-de-suelo-fc28.pdf)
- [Sensor de CO<sub>2</sub>](mh-z19b-co2-ver1_0_datasheet.pdf)
- Cables Dupont



## Modelos en 3D de las piezas  

Ha habido que fabricar algunas piezas con la impresora 3D para conseguir ensamblar las dos partes de vidrio de las que se compone el invernadero, así como para sostener la placa Arduino y todo el cableado.  

- **Unión de las dos partes del invernadero:**  
Esta pieza permite sujetar las dos estructuras fabricadas en vidrio, dejando un pequeño hueco para la entrada de aire.

![Pieza Auxiliar](img/PiezaAux.png "Pieza auxiliar para cerrar el invernadero")  
[Descarga el archivo .stl](InvernaderoAux.stl)  



Así mismo, se ha diseñado una pieza para sostener todo el cableado, la placa Arduino y el display.  

- **Unidad de presentación**:  


![Pieza 1](img/PiezaInvernaderoCaja1.png "Unidad de presentación: pieza 1")  
[Descarga el archivo .stl](InvernaderoCaja1.stl)  


![Pieza 2](img/PiezaInvernaderoCaja2.png "Unidad de presentación: pieza 2")  
  

![Pieza 3](img/PiezaInvernaderoCaja3.png "Unidad de presentación: pieza 3")  
[Descarga el archivo .stl de las piezas 2 y 3](InvernaderoCaja2y3.stl)

## Imágenes 
![Componentes varios](img/Componentes.jpg "Componentes del montaje")  
![Impresión de pieza](img/ImpresionPiezas.jpg "Unidad de presentación: pieza 1")  


### Unidad de presentación

![Presentación 1](img/PiezaInvernadero1.jpg "Unidad de presentación")  
![Presentación 2](img/PiezaInvernadero2.jpg "Unidad de presentación")  
![Presentación 3](img/PiezaInvernadero3.jpg "Unidad de presentación")  

### Sensores de humedad del suelo  
![Sensores de humedad del suelo](img/SensoresHumedadSuelo.jpg "Unidad de presentación")  


### Ventilador
![Ventilador huecos](img/VentiladorHuecos.jpg "Huecos del ventilador")  
![Ventilador pruebas](img/VentiladorPrueba.jpg "Pruebas de funcionamiento del ventilador")  
![Ventilador](img/VentiladorInstalado.jpg "Ventilador instalado")  







## Código

Puedes consultar el código en [este enlace](codigo.md).

## Vídeo


[![Haz clic para ver el vídeo](https://img.youtube.com/vi/9--anr8eSh8/0.jpg)](https://www.youtube.com/watch?v=9--anr8eSh8)


[VOLVER](https://angelmicelti.github.io/VilladiegoSTEAM/)
