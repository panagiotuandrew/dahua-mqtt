<h1 align="center">Dahua MQTT</h1>
<p align="center">
  <a href="https://docs.docker.com/compose/">
    <img src="https://img.shields.io/badge/docker%20compose-0e4df2" alt="Docker Compose">
  </a>
</p>

> [!IMPORTANT]
> This docker compose file has been only tested with the Dahua VTO2000A, and may not work with other models.

Dahua MQTT publishes ring presses from Dahua Intercoms as MQTT events.

# Environment Variables

-  ```VTO_BASE_URL```: Your VTO's IP address
-  ```VTO_USER```: Your VTO's username
-  ```VTO_PASS```: Your VTO's password
-  ```MQTT_URL```: Your MQTT broker's URL, use ``mqtt://localhost`` if on the same device
-  ```MQTT_TOPIC```: Your preffered MQTT topic
