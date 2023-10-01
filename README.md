# Puzzle1
Código Puzzle 1 para leer una tarjeta NFC con la RPi
En primer lugar, importamos los módulos necesarios para poder trabajar:
•	“board” nos permite interactuar con los pines de la RPi
•	“busio” permite configurar y gestionar la comunicación I2C
•	“adafruit_pn532.i2c” importa la clase PN532_I2C del que utilizaremos para interactuar con el lector NFC a través de la comunicación I2C
Siguiendo la estructura presentada en el documento del Puzzle1, definimos la clase “RfidReader”, esta constará de dos métodos principalmente:
•	El método “__init__” será el encargado de iniciar la comunicación I2C utilizando los pines anteriormente mencionados SCL y SDA (para llamarlos utilizamos “board.SCL” y “board.SDA”). Luego creamos la instancia PN532_I2C para interactuar con el lector NFC especificando la dirección obtenida anteriormente 0x24. Finalmente configuramos el lector NFC para leer las tarjetas MIFARE, utilizando “self.pn532.SAM_configuration()”
•	El método “read_uid” permite la detección y lectura del UID, que es identificador único de las tarjetas NFC. Dentro de este método tendremos:
o	Esperamos a que se detecte una tarjeta NFC utilizando “uid = self.pn532.read_passive_target(timeout=15.0)”
o	Si detectamos una tarjeta, su UID se almacena en la variable “uid_hex”
o	Retornaremos el UID en formato hexadecimal si detectamos una tarjeta NFC. Si no detectamos ninguna tarjeta durante el tiempo de espera, devolvemos un mensaje. 
Por último, verificaremos si el código se está ejecutando con la condición “if __name__” == “__main__”. Esto permitirá que el código dentro del bloque se ejecute solo cuando el archivo se ejecuta directamente y no cuando se importa el módulo. Es importante tener esto en cuenta para el futuro, cuando deberemos utilizar todo lo trabajado en el puzzle1 llamándolo desde otro programa.
Crearemos una instancia de la clase RfidReader llamada rfid.
Usamos el método “read_uid” en la instancia rfid para detectar y leer el UID de una tarjeta NFC. El resultado se almacenará en la variable uid.
Imprimimos el UID por consola.
En resumen, esta clase “RfidReader” tiene la funcionalidad necesaria para interactuar con el lector NFC PN532 a través de la comunicación I2C. Al crear una instancia de esta clase y llamar a su método “read_uid” podemos obtener el UID de la tarjeta NFC detectada. 
