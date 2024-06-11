# README

## Proyecto de Hacking Ético con Aircrack-ng

Este repositorio contiene scripts y herramientas utilizados en nuestro curso de hacking ético en la escuela. En un entorno controlado, los estudiantes aprenden a auditar la seguridad de redes inalámbricas utilizando la suite de herramientas `aircrack-ng`. 

### Objetivo

El objetivo de este proyecto es proporcionar a los estudiantes una comprensión práctica de las técnicas de hacking ético, específicamente en la auditoría de redes inalámbricas. Los estudiantes aprenderán a capturar tráfico de red, buscar contraseñas de puntos de acceso (AP) y realizar ataques de desautenticación.

### Herramientas Utilizadas

- **Aircrack-ng**: Una suite de herramientas para auditoría de redes inalámbricas. Incluye `airodump-ng`, `aireplay-ng`, `aircrack-ng`, entre otras.

### Requisitos

- Un sistema operativo basado en Linux (recomendado: Ubuntu, Kali Linux).
- Una tarjeta de red inalámbrica compatible con el modo monitor.
- Aircrack-ng instalado (puedes instalarlo con `sudo apt-get install aircrack-ng`).

### Instalación

1. Clona este repositorio por  medio de https o SSH:
    ```sh
    git clone git@github.com:luisjuarez099/Une-Hacks.git
    ```
    ```sh
    https://github.com/luisjuarez099/Une-Hacks.git
    ```
    
2. Navega al directorio del proyecto:
    ```sh
    cd Une-Hacks/
    ```

### Uso

#### 1. Captura de tráfico y búsqueda de contraseñas

1. **Poner la tarjeta de red en modo monitor**:
    ```sh
    sudo airmon-ng start <nombre_interfaz>
    ```
    capturar y mostrar información sobre las redes inalámbricas en tu área
     ```sh
       airodump-ng wlp0s20f3mon
     ```
3. **Capturar el tráfico de una red específica**:
    ```sh
    sudo airodump-ng -c <canal> -w <nombre_archivo> --bssid <MAC_AP> <interfaz_monitor>
    ```
    Ejemplo:
    ```sh
    sudo airodump-ng -c 1 -w captura -d 50:4E:DC:38:C2:60 wlp0s20f3mon
    ```

4. **Buscar la contraseña del AP**:
    Una vez que hayas capturado suficiente tráfico, puedes intentar descifrar la contraseña:
    ```sh
    sudo aircrack-ng -w <ruta_diccionario> <archivo_captura>
    ```
    Ejemplo:
    ```sh
    sudo aircrack-ng -w /usr/share/wordlists/rockyou.txt captura-01.cap
    ```

#### 2. Ataque de Desautenticación

1. **Lanzar un ataque de desautenticación**:
    ```sh
    sudo aireplay-ng --deauth <número_de_paquetes> -a <MAC_AP> <interfaz_monitor>
    ```
    Ejemplo:
    ```sh
    sudo aireplay-ng --deauth 0 -a 50:4E:DC:38:C2:60 wlp0s20f3mon
    ```

### Notas Importantes

- **Entorno Controlado**: Todos los ejercicios y prácticas deben realizarse en un entorno controlado y con el consentimiento expreso de los propietarios de la red. El uso indebido de estas técnicas fuera de un entorno autorizado es ilegal y antiético.
- **Propósito Educativo**: Este proyecto está destinado únicamente a fines educativos y para la mejora de la seguridad de redes propias.

### Contribuciones

Las contribuciones son bienvenidas. Por favor, abre un issue o crea un pull request para discutir cambios importantes antes de enviarlos.

### Licencia

Este proyecto está licenciado bajo la MIT License. Consulta el archivo `LICENSE` para más detalles.

---

**Contacto**

Para cualquier duda o consulta, puedes contactar al instructor del curso o abrir un issue en este repositorio.

---

¡Gracias por participar en este proyecto de hacking ético y mejorar la seguridad de nuestras redes!
