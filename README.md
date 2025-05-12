# Apuntes_Semana Doce
Apuntes control de movimiento - Tercer Corte - Doceava Semana

# Control de Movimiento (Rechazo Activo a Perturbaciones)

**Introducción al Rechazo Activo de Perturbaciones**

En los sistemas de control, uno de los principales desafíos es mantener el desempeño deseado ante la presencia de perturbaciones externas o internas que pueden afectar negativamente el comportamiento del sistema. El rechazo de perturbaciones es, por tanto, un aspecto fundamental para garantizar la estabilidad, precisión y robustez del control.

Tradicionalmente, los controladores PID han sido ampliamente utilizados debido a su simplicidad y efectividad en una gran variedad de aplicaciones. Sin embargo, su rendimiento puede verse comprometido cuando el sistema se enfrenta a perturbaciones no modeladas o cuando el modelo de la planta no está bien definido. En este contexto, surge el Control por Rechazo Activo de Perturbaciones (ADRC, por sus siglas en inglés: Active Disturbance Rejection Control) como una alternativa poderosa al PID.

El ADRC propone una estrategia innovadora basada en la estimación activa de perturbaciones para luego rechazarlas en tiempo real, minimizando su impacto en el sistema. Esta técnica reduce significativamente la dependencia de un modelo preciso de la planta y compensa de manera efectiva las debilidades de los controladores convencionales, mejorando así la robustez del sistema frente a incertidumbres y variaciones externas.

## 1. ADCR

Durante el proceso de desistimar las pertubaciones, el sistema utiliza una ley de control, la cual indica el resultado de realizar la estimación de una función no lineal del error utilizando un observador de estados extendido no lineal.

El uso de este observador de estados nos permite estimar las dinámicas desconocidas del sistema como las pertubaciones que afectarán la entrada en el proceso de funcionamiento. La ventaja de este sistema sobre otros es que se puede controlar sistemas de distinta naturaleza y complejidad sin necesidad de tener un modelo preciso previamente definido.

Durante el año 2014 Gao destaca 3 características sobre el funcionamiento ADRC:

* No es indispensable contar con un modelo detallado del proceso que se desea controlar. Al principio, basta con conocer el orden del sistema y una estimación del valor de su ganancia. Esta ganancia se refiere al parámetro que define la proporción entre la señal de control aplicada y la derivada de orden n de la salida del sistema.

* El control por rechazo activo de perturbaciones (ADRC) se basa en la estimación de una señal que representa tanto las incertidumbres del modelo como las perturbaciones externas. Aunque en teoría de control estos conceptos suelen tratarse por separado, el ADRC los unifica bajo el término de perturbación total. Esta perturbación total es observada en tiempo real y contrarrestada mediante la acción de control, evitando así que su efecto se refleje en la salida del sistema y mejorando significativamente la robustez frente a variaciones y factores no modelados.

* El ADRC busca que el sistema real se comporte de forma similar a una planta nominal, lo cual simplifica el diseño del controlador y permite lograr un desempeño deseado sin depender de un modelo preciso.

## 2. Componentes de un ADRC

Para que el sistema funcione de una manera eficiente debe contener ciertos componentes  programables para la identificación del sistema y parámetros del mismo.

* Generador de trayectorias

* Observador de estado extendido

* Controlador proporcional por retroalimentación de estados

![](https://github.com/MariaFernandaOrtiz-111449/Semana-Doce/blob/03f9ebe2b21b3c40e13901f090c58441aeba6d6b/Componentes%20ADRC.png)

*Imagen 1. Compontentes ADRC*


**Rechazo Activo a Perturbaciones Sistema No lineal**

En el control de sistemas no lineales, uno de los mayores desafíos es lidiar con la complejidad del modelo y la presencia de perturbaciones externas o dinámicas internas no modeladas. A diferencia de los sistemas lineales, donde existen métodos bien establecidos para el diseño de controladores, los sistemas no lineales requieren enfoques más flexibles y robustos.

En este contexto, el Rechazo Activo de Perturbaciones (ADRC) surge como una alternativa eficaz que no depende de un modelo matemático exacto del sistema. En lugar de eso, el ADRC se enfoca en estimar y compensar en tiempo real una señal denominada perturbación total, que engloba tanto incertidumbres internas como perturbaciones externas. Esto permite que el sistema real se comporte como una planta nominal más sencilla, facilitando así el diseño del controlador, incluso en presencia de no linealidades.

$ÿ = -a_{1}y\cdot --a_{0} + bu$

La identificación del sistema en espacio de estados estaría dado de la siguiente manera:

* $X_{1}\cdot = X_{2}$

* $X_{2}\cdot = -a_{0}X_{1} -a_{1}X_{2} +bu +w$

* $y=X_{1}$

En base a la identificación del sistema suponemos que la función del sistema esta dado por la ecuación:

* $f= -a_{0}X_{1} -a_{1}X_{2} +(b-b_{0})u +w$

Sustituyendo la función del sistema en espacio de estados obtendremos el siguiente parámetro:

* $X_{1}\cdot = X_{2}$

* $X_{2}\cdot = f +b_{0}u$

* $y=X_{1}$

Al obtener el sistema en espacio de estados se obtiene que F es la variable desconocida y se le asigna un estado:

* $X_{1}\cdot = X_{2}$

* $X_{2}\cdot = X_{3} +b_{0}u$

* $X_{3}\cdot = h$

* $y=X_{1}$

![](https://github.com/MariaFernandaOrtiz-111449/Semana-Doce/blob/36e779fc961ac85343fa1080678cede0f9b1ab02/Observador%20de%20estados%20extendido.png)

*Imagen 2. Observador de estados extendido para NADRC*

Una vez que se realiza el proceso en el espacio de estados, obtenemos la función del sistema controlado y libre de perturbaciones con un comportamiento integrador.

* $X_{1}\cdot = X_{2}$

* $X_{2}\cdot = u_{0}$

* $y = X_{1}$


## 3. Funciones para la Acción de Control en el Caso No Lineal

En el control ADRC aplicado a sistemas no lineales, la acción de control se diseña utilizando funciones no lineales que mejoran la robustez y la capacidad de rechazo de perturbaciones. Entre estas funciones destaca la función de no linealidad tipo fal (del inglés function approaching linearity), la cual suaviza el comportamiento del controlador cerca del origen y actúa como ganancia variable, adaptándose a la magnitud del error.

Estas funciones permiten construir controladores y observadores que no requieren la linealización del sistema, haciendo posible una respuesta eficiente y estable incluso en presencia de fuertes no linealidades o perturbaciones no modeladas.

* $u_{0} = k_{1}fal(r_{1} - z_{1}, \alpha _{1}, \delta) + k_{2}fal((r_{1}\cdot - z_{2}, \alpha_{2}, \delta)$

 ![]()

### 3.1. Eficiencia

La eficiencia en el control de movimiento se refiere a la capacidad de un sistema para transformar la energía en movimiento preciso y efectivo, minimizando pérdidas y optimizando el desempeño.

**Factores Clave en la Eficiencia**

*Transmisión de Energía*

* Usar mecanismos de transmisión eficientes, como engranajes de alta precisión o correas síncronas con baja fricción.

* Minimizar pérdidas por rozamiento y holguras en acoplamientos mecánicos.

*Control del Torque y la Velocidad*

* Implementar controladores PID o algoritmos avanzados para ajustar dinámicamente el torque y la velocidad.

* Asegurar una relación de inercia adecuada entre el motor y la carga para mejorar la respuesta del sistema.

*Reducción de Pérdidas Energéticas*

* Seleccionar motores y accionamientos con alta eficiencia.

* Evitar sobrecargas y diseñar el sistema para operar dentro del rango óptimo de eficiencia del motor.

*Optimización del Perfil de Movimiento*

* Usar aceleraciones y desaceleraciones suaves para evitar picos de corriente y desgaste mecánico.

* Aplicar técnicas como interpolación y control de trayectoria para mejorar la precisión y reducir vibraciones.

*Selección de Sensores y Realimentación*

* Implementar sensores de alta resolución para mejorar la precisión y estabilidad del control.

* Utilizar sistemas de retroalimentación en tiempo real para corregir desviaciones y mejorar la eficiencia del sistema.
  
### 3.2. Inercia Total

Es la suma de todas las inercias reflejadas al eje del motor. Incluye la inercia del propio motor, la inercia de la carga y la de los elementos de transmisión, ajustadas según la relación de transmisión. Se expresa mediante la fórmula general:

$$J{total} = J{motor} + J{transmisión} + J{carga} {reflejada}$$

Donde:

* $J{motor}$: Es la inercia del rotor del motor.

* $J{transmision}$: Es la inercia de engranajes, poleas, correas, etc.

*$J{carga reflejada}$: ​Es la inercia de la carga ajustada a la referencia del motor, calculada como:

$$J{carga}{reflejada} : J{carga} * N^{2}$$

Donde N está dado por la relación de transmisión.

$N: \frac{W_{motor}}{W_{carga}}$

**Importancia del Cálculo de la Inercia Total**
* *Afecta la respuesta dinámica: Una inercia elevada requiere mayor torque para acelerar y desacelerar.*
* *Influye en la selección del motor: Un desbalance entre la inercia del motor y la carga puede afectar la estabilidad y eficiencia del sistema.*
* *Optimiza el control de movimiento: Una inercia total bien calculada permite un control más preciso y eficiente del sistema.*
  
### 3.3. Relación de Inercia

Es un parámetro clave en el diseño de sistemas de control de movimiento, ya que indica el equilibrio dinámico entre el motor y la carga. Se define como la razón entre la inercia reflejada de la carga y la inercia del rotor del motor

Relación de Inercia: $$\frac{J{carga} {reflejada}}{J_{motor}}$$

**Donde:**
* $J{carga} {reflejada}: J_{carga} * N^{2}$ (si hay una transmisión con relación N)
* $J_{motor}$ es la inercia del motor

**Práctica de la relación de Inercia**

En la práctica, la relación de inercia entre la carga y el motor es un aspecto clave para lograr un sistema de movimiento eficiente y confiable. Esta relación influye directamente en el comportamiento dinámico del sistema, así como en la selección del motor y la transmisión. Dependiendo del tipo de aplicación y sus exigencias, se pueden presentar distintos escenarios que vale la pena considerar:

* *Relación de inercia baja (rango de 1 a 2)*: Es adecuada para aplicaciones que requieren movimientos rápidos, con frecuentes arranques y paradas. No obstante, puede implicar el uso de un motor sobredimensionado, lo cual aumenta los costos y reduce la eficiencia energética.

* *Relación de inercia alta (mayor a 10):* Se emplea en situaciones donde no se necesita una alta dinámica, como en movimientos lentos o constantes. Aunque puede reducir el tamaño del motor, también conlleva riesgos como una baja eficiencia del sistema o torque insuficiente para cumplir con la tarea.

Por ello, elegir correctamente la relación de inercia según la aplicación es esencial para optimizar el rendimiento y evitar problemas en el diseño de sistemas de control de movimiento.
Un sensores un dispositivo que detecta cambios en una magnitud física o química, como temperatura, presión o luz, y los convierte en señales eléctricas para su procesamiento. Se usa en diversos sistemas para monitoreo y automatización.


## 4. Concepto Transmisión Polea-Correa

El sistema de transmisión por polea y correa es un mecanismo ampliamente utilizado para transferir movimiento y potencia entre dos ejes separados. Este tipo de transmisión se basa en el uso de una correa flexible que conecta dos poleas: una motriz (conectada al motor) y otra conducida (conectada a la carga). Al girar la polea motriz, la correa transmite ese movimiento a la polea conducida, permitiendo modificar la velocidad y el torque de salida según el diámetro de las poleas involucradas.

Entre sus ventajas destacan la simplicidad mecánica, el bajo costo, el funcionamiento silencioso y la capacidad de absorber vibraciones. Además, permite transmisiones a distancia y cierta flexibilidad en la alineación de los ejes. Sin embargo, también presenta desventajas como el posible deslizamiento de la correa, la necesidad de mantenimiento periódico (ajuste de tensión y reemplazo de la correa) y una eficiencia menor comparada con sistemas más rígidos como engranajes.

**Puntos claves:**

* *Relación de transmisión:* Se determina por el cociente entre los diámetros de las poleas. Esto permite adaptar la velocidad y el torque entre el motor y la carga.

* *Tensión adecuada:* Es fundamental mantener la correa con la tensión correcta para evitar deslizamientos y asegurar una transmisión eficiente y duradera.

### 4.1. Relación de Transmisión

La relación de transmisión en un sistema de polea-correa indica cómo se modifica la velocidad de rotación entre la polea motriz (la que transmite el movimiento) y la polea conducida (la que recibe el movimiento). Esta relación depende directamente del tamaño de las poleas, y se calcula como:

Relación de transmisión (i) = $$\frac {Diámetro de la polea conducida}{Diámetro de la polea motriz}$$

Este valor también puede expresarse usando las velocidades de rotación:

$$i: \frac{Velocidad de la polea motriz}{Velocidad de la polea conducida}$$

### 4.2. Inercia Reflejada

En un sistema de polea-correa, la inercia reflejada se refiere a cómo la inercia de la carga (conectada a la polea conducida) se “ve” desde el motor (polea motriz), tomando en cuenta la relación de transmisión. Este concepto es clave en el diseño de sistemas de control de movimiento, ya que afecta directamente la respuesta dinámica del motor.

La inercia reflejada $J_{ref}$ al eje del motor se obtiene mediante la siguiente fórmula:

$$J_{ref}: \frac{J_{carga}}{i^{2}}$$

Donde:
* $J_{carga}$ es la inercia real de la carga.
* 𝑖
i es la relación de transmisión (diámetro polea conducida / diámetro polea motriz).

### 4.3. Torque de Carga

El torque de carga en un sistema de transmisión por polea-correa es el torque que debe entregar el motor para mover la carga conectada a la polea conducida. Este torque depende de la relación de transmisión, el tipo de carga y la eficiencia del sistema.

**Relación entre torque del motor y torque de la carga:**

$$T{motor}: \frac{T_{carga}}{i*n}$$

Donde:

* $T{motor}$ es el torque que debe generar el motor
* $T_{carga}$ es el torque requerido por la carga
* $i$ es la relación de transmisión (diámetro polea conducida / diámetro polea motriz)
* $n$ es la eficiencia del sistema (entre 0 y 1)

## 5. Ejercicios

### Una carga tiene una inercia de 0.05 kg·m² y se conecta a un motor a través de una relación de transmisión de 4:1.
* Calcula la inercia reflejada al motor.

$$J_{r}=\frac{J_{L}}{N^{2}}$$

$J_{r}=\frac{0.05}{4^{2}}$

$J_{r}=\frac{0.05}{16}$

$J_{r}=0.003125 Kg*m^{2}$

* Si el torque requerido por la carga es de 2 Nm, ¿cuánto torque reflejado sentirá el motor?

$$T_{r}= \frac{T_{L}}{N}$$

$T_{r}=\frac{2}{4}$

$T_{r}=0.5 Nm$


### Un motor eléctrico proporciona un torque constante de 3 Nm a una velocidad de 1500 rpm.

* Calcular la potencia mecánica entregada por el motor en watts.

$$P=T*\omega$$

$T=3 Nm$

$\omega = 2\pi * \frac{rpm}{60}$

$\omega=2\pi* \frac{1500}{60}$

$\omega=2\pi * 25$

$\omega = 157.08 rad/s$

$P=3*157,08$

$P=471,24 W$

### Un sistema de transmisión tiene una eficiencia del 85%. Si el motor entrega una potencia de 500 W:

*  Calcular la potencia útil disponible en la carga.

$$P_{util}=\eta*P_{entrada}$$

$P_{util}=0.85*500$

$P_{util}= 425 W$

## 6. Conclusiones

* El diseño correcto de sistemas de transmisión mecánica (engranajes, correas, cadenas) es esencial para garantizar eficiencia, precisión, seguridad y durabilidad en sistemas automatizados y mecatrónicos.
* Una correcta elección del motor y su relación con la transmisión y la carga permite alcanzar un funcionamiento óptimo. Esto requiere asegurar el torque necesario, una relación de inercia adecuada y el cumplimiento de criterios como el costo, precisión y tiempos de ciclo.
* La inercia y el torque reflejados al eje del motor deben calcularse para anticipar el esfuerzo que el motor debe realizar. Esto es vital para evitar sobrecargas, mejorar el rendimiento dinámico y permitir un control más preciso.
* La relación entre engranajes afecta directamente la velocidad y el torque transmitido. Además, mantener alta eficiencia en el sistema minimiza pérdidas energéticas, mejora la vida útil del equipo y reduce el consumo energético.
* La relación define el equilibrio entre la inercia de la carga y la del motor. Mantenerla en rangos adecuados asegura un control estable y eficiente. Una mala relación puede llevar a inestabilidad, sobreesfuerzo del motor o pérdida de precisión.

## 7. Referencias

* Mecatrónica Integrada (2023). Motores eléctricos: Torque, potencia y eficiencia. Universidad Cooperativa de Colombia – Facultad de Ingeniería Mecatrónica. Material de estudio.

* González, J. (2019). Principios de máquinas eléctricas y transformadores. McGraw-Hill.

* Universidad Nacional de Colombia (2022). Laboratorio de máquinas eléctricas: prácticas con motores de inducción y corriente continua. Facultad de Ingeniería Eléctrica.

* Universidad Cooperativa de Colombia – Facultad de Ingeniería Mecatrónica. (2023). Motores eléctricos: Torque, potencia y eficiencia. Material de estudio interno.
