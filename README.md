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


## 3. Rechazo Activo a Perturbaciones Sistema No lineal

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


### 3.1. Funciones para la Acción de Control en el Caso No Lineal

En el control ADRC aplicado a sistemas no lineales, la acción de control se diseña utilizando funciones no lineales que mejoran la robustez y la capacidad de rechazo de perturbaciones. Entre estas funciones destaca la función de no linealidad tipo fal (del inglés function approaching linearity), la cual suaviza el comportamiento del controlador cerca del origen y actúa como ganancia variable, adaptándose a la magnitud del error.

Estas funciones permiten construir controladores y observadores que no requieren la linealización del sistema, haciendo posible una respuesta eficiente y estable incluso en presencia de fuertes no linealidades o perturbaciones no modeladas.

* $u_{0} = k_{1}fal(r_{1} - z_{1}, \alpha _{1}, \delta) + k_{2}fal((r_{1}\cdot - z_{2}, \alpha_{2}, \delta)$

 ![](https://github.com/MariaFernandaOrtiz-111449/Semana-Doce/blob/1e6c3b7e38f53f7b419dafaf953ef878992d0e2b/Ecuaciones.png)

 *Imagen 3. Ecuaciones parámetros ganancias del controlador*

## 4.  Rechazo Activo a Perturbaciones Sistema Lineal

SPara el sistema lineal se realiza un observador de estados en un sistema lineal extendido.

![image](https://github.com/user-attachments/assets/8d6663fa-e6c6-43e9-888f-4816edf05068)

*Imagen 4. Sistema lineal Principal y extendido*

En base al sistema definido previamente mediante el observador de estados, se halla la acción de control necesaria que está delimitada por la siguiente ecuación: 

$U_{0} = k_{1}(r\sim - z_{1})-k_{2}z_{2}$

En sistemas lineales, el Rechazo Activo de Perturbaciones (ADRC) ofrece una alternativa eficaz a los controladores clásicos como el PID, al no depender de un modelo matemático preciso. En este enfoque, se considera una planta lineal simple, y cualquier dinámica no modelada, incertidumbre o perturbación externa se agrupa como perturbación total, la cual es estimada en tiempo real mediante un observador extendido (ESO).

Una vez estimada, esta perturbación se compensa activamente con la acción de control, logrando un comportamiento deseado del sistema. En el caso lineal, el diseño del ADRC es más sencillo y directo, lo que lo convierte en una opción atractiva para aplicaciones prácticas donde se busca simplicidad, robustez y buen desempeño dinámico.

## 5. Observador de estados ADRC

El observador extendido de estados (ESO) es una parte fundamental del Rechazo Activo de Perturbaciones (ADRC). Su función principal es estimar no solo los estados internos del sistema, sino también una señal adicional que representa la perturbación total, es decir, la combinación de dinámicas no modeladas, incertidumbres del sistema y perturbaciones externas.

Este observador se actualiza en tiempo real y permite que el controlador reaccione rápidamente a cualquier cambio inesperado, rechazando activamente las perturbaciones sin requerir un modelo preciso de la planta. Gracias a esta estimación, el controlador puede compensar los efectos negativos y forzar al sistema a seguir el comportamiento deseado, incluso bajo condiciones adversas.

Para un sistema discreto con perturbaciones el diseño de la estimación de parámetros estaría dado por: 

* $X_{k+1} = A * X_{k} + B * u_{k} + F * d_{k}$

* $y_{k} = C * X_{k}$

Si durante el proceso de funcionamiento del sistema, vemos que la perturbación es constante $d(k+1) = d(k)$, se añade como variable de estado.

![image](https://github.com/user-attachments/assets/86410201-64f7-4431-8e85-f099ae02327e)

*Imagen 5. Matriz Observador de Estados*

Una vez se tenga el diseño del sistema con las perturbaciones añadidas, se puede diseñar el obseradoir de estados compensanndo el efecto de la salida mediante una pre-alimentación del sistema.

![image](https://github.com/user-attachments/assets/5cb72645-a5d9-40a1-b23d-5ebafd66ff57)

*Imagen 6. Observador de estados con Perturbaciones*

Una vez obtenido la representación de espacio de estados mediante una matriz, se construye el observador de Luenberger.

## 6. Observador de Luenberger

El Observador de Luenberger es una herramienta utilizada en sistemas lineales para estimar los estados internos de un sistema dinámico cuando no todos pueden ser medidos directamente. Se basa en un modelo matemático del sistema y en la retroalimentación del error entre la salida real y la estimada, ajustando así las estimaciones de los estados.

Su estructura combina el modelo del sistema con una ganancia de observación que permite corregir las estimaciones en función de la diferencia entre la salida medida y la estimada. Este observador es ampliamente utilizado en control clásico y moderno por su simplicidad, efectividad y bajo costo computacional.

En el diseño de este observador, se tiene el coeficinete $X^{\bigtriangleup \cdot }$ el cual es el vector asociado a los coeficientes que determinarán el polinomio de hurwitz asociado a la dinámica del error de estimación $e_{y} \sim$ definido como $e_{y} \sim = y- y^{\bigtriangleup }$

![image](https://github.com/user-attachments/assets/9310ba09-f977-4e47-9479-74be49fb3936)

*Imagen 7.Observador de Luenberger*

Al restar las ecuaciones del sistema real y del observador, se obtiene una ecuación que describe la dinámica del error de estimación. Esta dinámica está gobernada por una matriz, conocida como matriz del error, cuya estructura determina la estabilidad del observador. A partir de esta matriz, se puede obtener el polinomio característico, el cual permite analizar y ubicar los polos del observador para garantizar una convergencia rápida y estable del error hacia cero.

![image](https://github.com/user-attachments/assets/023ab6a0-9c54-4ee6-b0a8-a46de6657d08)

*Imagen 8. Ecuaciones dinámica el error*

Los coeficientes 𝜆𝜉 se eligen de manera que el polinomio característico de la dinámica del error de estimación tenga raíces en el semiplano izquierdo del plano complejo. Esto asegura que el sistema sea estable, cumpliendo con la condición de ser un polinomio de Hurwitz, lo cual garantiza que el error de estimación tienda a cero con el tiempo.

Donde 𝜀 representa la estimación de la perturbación generalizada, la cual se obtiene mediante un observador de estados. Se asume que esta perturbación puede ser aproximada por un polinomio en función del tiempo, lo que permite incluirla dentro del modelo del observador y estimarla junto con los estados del sistema.

![image](https://github.com/user-attachments/assets/6637f441-68eb-4822-a0cf-141b4ec3b3e8)

*Imagen 9. Polinomio en función del tiempo*

Suponiendo que la perturbación generalizada estimada cumple ε^(m)(t)=0, y considerando r(t) como el residuo entre la salida real y estimada, es posible diseñar un observador extendido que no solo estime las derivadas de la salida, sino también la perturbación generalizada y sus derivadas. Este enfoque permite capturar dinámicamente el efecto de perturbaciones e incertidumbres, facilitando su rechazo activo mediante la acción de control.

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
