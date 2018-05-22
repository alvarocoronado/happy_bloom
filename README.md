PASOS PARA DEJAR FUNCIONANDO EN MQTT AWS UN SENSOR DE TEMPERATURA

1) Instalar AWS CLI // MOS TOOL (Cesanta Mongoose) // Github
2) descomprimir el rar en GitHub/sensor_mqtt
3) Configurar el YML con el tópico de publicación y el mqtt:server:

  - ["mqtt.pub", "s", "/sbs/devicedata/chao", {title: "Publish topic"}]
  - ["mqtt.sub", "s", "/request", {title: "Subscribe topic"}]
  - ["mqtt.server", "apazm8p6pm7gy.iot.us-west-2.amazonaws.com:8883"]

	El server es: <accountnumber>.iot.<your-certificate's region>.amazonaws.com:8883
  
4) mos build --arch esp8266
5) mos flash
6) mos wifi RN40gtd rosarionorte40
7) mos aws-iot-setup --aws-region us-west-2 --aws-iot-policy ElPrimeroPolicy
8) En IoT core ir a test, suscribirse al topico y comprobar que llegan los mensajes.

-----------------------------------------------------------------------

CREAR UNA REGLA QUE SE GATILLA CON CADA MENSAJE

1) Se crea desde IoT core.
2) Dentro del IoT core en Act se crean las reglas.
3) Se da un nombre a la regla, y en Attribute: *. En topic filter la gerarquía del topico MQTT donde publicas.
4) Set one or more actions.
5) Por ejemplo para gatillar el envio de mails, se agrega la regla SNS.
6) Para setear el mail a quien se envian los mensajes debes ingresar a AWS -> SNS -> Topics y creas un topico.
7) Al seleccionar el topico se configuran las acciones. Hay que darle a "Create a suscription" y en el protocolo "email". Como "endpoint" el mail del usuario. Luego debes confirmar via mail.

-------------------------------------------------------------------------


