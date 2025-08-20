# ⚡ ALU de 32 Bits – Nand2Tetris

Implementación de una **ALU de 32 bits** desarrollada en lenguaje **HDL** y ejecutada en el software **Nand2Tetris**.  

---

## 🖥️ Entorno de desarrollo

- **Sistemas operativos:** 
   * Fedora Workstation 42
   * Manjaro Linux 25.0.7

- **Software:** [Nand2Tetris](https://www.nand2tetris.org/)  

---

## ▶️ Ejecución del programa

1. Ir al directorio de herramientas del simulador:

   ```bash
   cd nand2tetris/tools
   bash HardwareSimulator.sh
   ```
2. Dentro del simulador, cargar el chip ALU32 ubicado en la carpeta `proyecto/2`

## 📋 Descripción detallada del diseño 
Nuestra solución a la problemática planteada consiste en utilizar dos ALUs de 16 bits con el
método ADD16 modificado. Cada ALU contará con una entrada adicional a las habituales: el
Carry-in.

El procedimiento inicia dividiendo las entradas numéricas en bloques de 16 bits: la parte
inferior se envía a la primera ALU y la parte superior a la segunda. Esto permite realizar las
operaciones correspondientes respetando las banderas definidas por el usuario.
La nueva entrada Carry-in cumple un papel clave. En la primera ALU, este valor se inicializa
en 0, ya que aún no se ha efectuado ninguna operación. En la segunda ALU, en cambio, es
esencial ingresar el Carry15 generado en el método ADD16 modificado, lo cual asegura la
correcta propagación de datos entre ambas unidades.

Cada ALU genera su respectiva señal zr, y ambas se combinan mediante una operación AND
para determinar si el resultado total es 0. Por su parte, la señal ng se obtiene del bit más
significativo de la salida (posición 31).

Finalmente, el método ADD16 modificado introduce dos cambios fundamentales. Primero, la
operación inicial ya no se realiza con un HalfAdder, sino con un FullAdder, considerando el
carry-in, la entrada x y la entrada y. Segundo, se añade una nueva salida denominada
carryFinal, la cual se utiliza como entrada en el carry-in de la siguiente ALU o como señal de
overflow en la ALU final.
