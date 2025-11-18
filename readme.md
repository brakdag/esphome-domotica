# Proyecto de Domótica y Automatización del Hogar con ESPHome

![ESPHome](https://img.shields.io/badge/Plataforma-ESPHome-blue?style=for-the-badge&logo=esphome)
![Home Assistant](https://img.shields.io/badge/Integración-Home%20Assistant-blue?style=for-the-badge&logo=home-assistant)
Repositorio personal de configuraciones para ESPHome. El objetivo es documentar, versionar y compartir la lógica de automatizaciones realizadas.

## Proyectos Incluidos

Este repositorio contiene las configuraciones YAML para varios dispositivos y sistemas:

* **⚡ Gestión de Energía (Inyección 0):**
    * **Descripción:** Configuración para monitorear el consumo de la red con shelly em gen3 y la generación de un sistema solar microinversor HOYMILES MI 1200, implementando una lógica de Inyección Cero.
    * **Hardware:** AhoyDTU,Hoymiles MI-1200, Shelly EM Gen3.
    * **Archivo:** `inyeccion-cero/Inyeccion0.yaml`

* **💧 Automatización de Termotanque:**
    * **Descripción:** Convierte un termotanque eléctrico estándar en un dispositivo inteligente. Permite el control de encendido/apagado por zondeo de potencia.

    * **Hardware:** ESP01s, Relé ESP01s V1.0, .
    * **Archivo:** `termotanque/termo.yaml`

* **🔔 Automatización de Timbre:**
    * **Descripción:** Un esp8299 Wemos D1  detecta la pulsación del timbre existente (sin reemplazarlo) y envía una notificación instantánea a Home Assistant, que luego la reenvía a dispositivos móviles.
    * **Hardware:** ESP8266 (Wemos D1 Mini), Parlante Piezoeléctrico.
    * **Archivo:** `timbre/timbre.yaml`

---

## Estructura del Repositorio

El proyecto se organiza en directorios, donde cada uno representa un dispositivo o una función lógica:

```

.
├── inyeccion-cero/
│   └── inyeccion0/inyeccion0.yaml
├── termotanque/
│   └── termo\termotanque.yaml
├── timbre/
│   └── timbre\timbre.yaml
│
├── .gitignore         \<-- Asegura que los secretos no se suban
├── secrets.yaml       \<-- (Local) Archivo de credenciales. NO INCLUIDO EN GIT.
└── README.md          \<-- Este archivo

````

---

## Instalación y Uso

Para utilizar estas configuraciones, necesitarás [ESPHome](https://esphome.io/guides/getting_started.html) (ya sea como *add-on* de Home Assistant o como herramienta de línea de comandos `pip`).

1.  **Clonar el repositorio:**
    ```bash
    git clone [https://github.com/tu-usuario/tu-repositorio.git](https://github.com/tu-usuario/tu-repositorio.git)
    cd tu-repositorio
    ```

2.  **Crear archivo de secretos:**
    Crea un archivo `secrets.yaml` en la raíz del proyecto. (Ver sección de Seguridad).

3.  **Compilar y Flashear:**
    Navega al directorio del proyecto y ejecuta ESPHome (reemplaza `archivo.yaml` con el deseado):
    ```bash
    # Ejemplo para el termotanque
    esphome run termotanque/termo_cocina.yaml
    ```
    O simplemente adopta los archivos desde el Dashboard de ESPHome.

---

## 🔒 ¡IMPORTANTE! Gestión de Credenciales

Este repositorio está diseñado para ser compartido de forma segura.

> **No encontrarás ninguna contraseña o clave de API en los archivos `.yaml`.**
>
> Toda la información sensible (credenciales de Wi-Fi, contraseñas de OTA, claves de API de Home Assistant, etc.) se gestiona exclusivamente a través de un archivo `secrets.yaml`.
>
> Este archivo **está listado en el `.gitignore`** y nunca debe ser subido a GitHub.

Para que estos códigos funcionen, debes crear tu propio archivo `secrets.yaml` en el directorio raíz con un formato similar al siguiente:

**`secrets.yaml` (EJEMPLO - NO COMPARTIR ESTE ARCHIVO)**
```yaml
# Credenciales de Red
wifi_ssid: "ElNombreDeTuRed"
wifi_password: "TuPasswordDeWiFi"
static_ip: "192.168.1.100" # IP estática para un dispositivo (opcional)

# Seguridad de ESPHome
ota_password: "UnaClaveSeguraParaActualizacionesOTA"
api_encryption_key: "UnaLlaveLargaParaLaAPIDeHomeAssistant"

# Credenciales de Servicios (si los usas)
# mqtt_broker: "192.168.1.50"
# mqtt_user: "usuario_mqtt"
# mqtt_pass: "pass_mqtt"
````
