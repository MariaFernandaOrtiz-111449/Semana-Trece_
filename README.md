# Apuntes_Semana Trece
Apuntes control de movimiento - Tercer Corte - Treceava Semana

Tomás Santiago Sánchez Barrera & María Fernanda Ortíz Velandia & Andrés Felipe Arteaga Escalante

# Indice


# 1. Control de Movimiento (Rechazo Activo a Perturbaciones)

**1.1 Introducción al Rechazo Activo de Perturbaciones**

En los sistemas de control, uno de los principales desafíos es mantener el desempeño deseado ante la presencia de perturbaciones externas o internas que pueden afectar negativamente el comportamiento del sistema. El rechazo de perturbaciones es, por tanto, un aspecto fundamental para garantizar la estabilidad, precisión y robustez del control.

💡Ejemplo 1: Control de temperatura de un horno

Situación: De repente, alguien abre la puerta del horno y entra aire frío, causando una perturbación que reduce la temperatura interna.

Solución: El controlador PID detecta la caída de temperatura, aumenta la potencia del calefactor para compensar el enfriamiento y luego la reduce gradualmente al recuperar los 200 °C, manteniendo así la estabilidad y precisión del sistema.

![image](https://github.com/user-attachments/assets/787c9709-0829-49e7-bf8a-8bae20653be9)

Imagen 1. Ejemplo 1

Tradicionalmente, los controladores PID han sido ampliamente utilizados debido a su simplicidad y efectividad en una gran variedad de aplicaciones. Sin embargo, su rendimiento puede verse comprometido cuando el sistema se enfrenta a perturbaciones no modeladas o cuando el modelo de la planta no está bien definido. En este contexto, surge el Control por Rechazo Activo de Perturbaciones (ADRC, por sus siglas en inglés: Active Disturbance Rejection Control) como una alternativa poderosa al PID.

El ADRC propone una estrategia innovadora basada en la estimación activa de perturbaciones para luego rechazarlas en tiempo real, minimizando su impacto en el sistema. Esta técnica reduce significativamente la dependencia de un modelo preciso de la planta y compensa de manera efectiva las debilidades de los controladores convencionales, mejorando así la robustez del sistema frente a incertidumbres y variaciones externas.

💡Ejemplo 2: Plataforma de estabilización de cámara en un dron

Situación: Un dron en vuelo debe mantener su cámara estable frente a vibraciones del motor, ráfagas de viento o movimientos bruscos. Estas perturbaciones son difíciles de modelar con precisión.

🚫 Limitación del PID: El controlador PID puede no reaccionar a tiempo o sobreactuar ante estas perturbaciones rápidas, ya que no conoce ni anticipa la fuente del error.

✅ Ventaja del ADRC: El ADRC estima activamente las perturbaciones (vibraciones, viento) en tiempo real y ajusta el control para contrarrestarlas, manteniendo la cámara estable sin necesidad de un modelo exacto del dron o su entorno.

![image](https://github.com/user-attachments/assets/19b97883-db93-4c8f-9f4d-22683170f575)

Imagen 2. Ejemplo 2

## 2. Conceptos Básicos

* Perturbaciones y modelo: ADRC funciona bien incluso si el modelo del sistema es inexacto y hay perturbaciones desconocidas.

* Estado extendido: Incluye las perturbaciones como parte del sistema para poder observarlas y controlarlas.

* ESO (Observador de Estado Extendido): Estima en tiempo real los estados del sistema y las perturbaciones que lo afectan.

* Ley de control: Usa las estimaciones del ESO para corregir el sistema y rechazar perturbaciones activamente.

* Robustez y simplicidad: Es robusto frente a incertidumbre y fácil de ajustar con pocos parámetros.

## 3. ADCR

Durante el proceso de desistimar las pertubaciones, el sistema utiliza una ley de control, la cual indica el resultado de realizar la estimación de una función no lineal del error utilizando un observador de estados extendido no lineal.

![image](https://github.com/user-attachments/assets/88a979db-32cf-43d3-ac1e-59860ff5c885)

Imagen 3. Modelo del sistema.

El uso de este observador de estados nos permite estimar las dinámicas desconocidas del sistema como las pertubaciones que afectarán la entrada en el proceso de funcionamiento. La ventaja de este sistema sobre otros es que se puede controlar sistemas de distinta naturaleza y complejidad sin necesidad de tener un modelo preciso previamente definido.


Durante el año 2014 Gao destaca 3 características sobre el funcionamiento ADRC:

* No es indispensable contar con un modelo detallado del proceso que se desea controlar. Al principio, basta con conocer el orden del sistema y una estimación del valor de su ganancia. Esta ganancia se refiere al parámetro que define la proporción entre la señal de control aplicada y la derivada de orden n de la salida del sistema.

* El control por rechazo activo de perturbaciones (ADRC) se basa en la estimación de una señal que representa tanto las incertidumbres del modelo como las perturbaciones externas. Aunque en teoría de control estos conceptos suelen tratarse por separado, el ADRC los unifica bajo el término de perturbación total. Esta perturbación total es observada en tiempo real y contrarrestada mediante la acción de control, evitando así que su efecto se refleje en la salida del sistema y mejorando significativamente la robustez frente a variaciones y factores no modelados.

* El ADRC busca que el sistema real se comporte de forma similar a una planta nominal, lo cual simplifica el diseño del controlador y permite lograr un desempeño deseado sin depender de un modelo preciso.

## 4. Componentes de un ADRC

Para que el sistema funcione de una manera eficiente debe contener ciertos componentes  programables para la identificación del sistema y parámetros del mismo.

* Generador de trayectorias

* Observador de estado extendido

* Controlador proporcional por retroalimentación de estados

![image](https://github.com/user-attachments/assets/303c6b13-59a9-4a94-b5fe-151142c98d67)

*Imagen 4. Compontentes ADRC*

💡Ejemplo 3: Control de Posición de un Motor DC

### Sistema:
* Planta: Motor DC con fricción y carga variable.

* Objetivo: Controlar la posición angular del eje.

### Implementación ADRC:
* TD: Suaviza la señal de referencia angular $\theta _{ref}$ y obtiene su derivada (velocidad deseada).

* ESO: Estima la velocidad real del motor y la perturbación total (fricción + carga variable).

* NLSEF: Calcula la corriente de control al motor compensando el error de posición y perturbaciones estimadas.

🧠 Resultado: El motor sigue la referencia sin importar los cambios de carga o fricción.

![image](https://github.com/user-attachments/assets/d03b18c7-0740-4f63-afa7-79e6e58ffb64)

*Imagen 5. Control de Posición de un Motor DC*


💡Ejemplo 4: Plataforma Inclinable (Gimbal)

### Sistema:

* Planta: Plataforma 2DOF para mantener una cámara estable.

* Objetivo: Controlar el ángulo en pitch y roll frente a perturbaciones (movimiento del dron, viento).

### Implementación ADRC:

* TD: Suaviza los ángulos deseados para la cámara.

* ESO: Estima los ángulos actuales y perturbaciones (movimiento externo, vibración).

* NLSEF: Genera señales PWM para los servos que corrigen la posición.

🧠 Resultado: La cámara se mantiene estable a pesar de los movimientos del dron.

![image](https://github.com/user-attachments/assets/77dfb797-d3fe-49a1-8488-04bf3545fb03)

*Imagen 6. Plataforma Inclinable*

## 5. Rechazo Activo a Perturbaciones Sistema No lineal

En el control de sistemas no lineales, uno de los mayores desafíos es lidiar con la complejidad del modelo y la presencia de perturbaciones externas o dinámicas internas no modeladas. A diferencia de los sistemas lineales, donde existen métodos bien establecidos para el diseño de controladores, los sistemas no lineales requieren enfoques más flexibles y robustos.

En este contexto, el Rechazo Activo de Perturbaciones (ADRC) surge como una alternativa eficaz que no depende de un modelo matemático exacto del sistema. En lugar de eso, el ADRC se enfoca en estimar y compensar en tiempo real una señal denominada perturbación total, que engloba tanto incertidumbres internas como perturbaciones externas. Esto permite que el sistema real se comporte como una planta nominal más sencilla, facilitando así el diseño del controlador, incluso en presencia de no linealidades.

![image](https://github.com/user-attachments/assets/bcc5cacd-f495-4a07-9a5e-2c55b2482d7f)

*Imagen 7. Rechazo de perturbaciones internas y externas mediante ADRC*

A continuación realizaremos la identificación de parámetros en base al análisis de ecuaciones dieferenciales del sistema como se observa a continuación:

$ÿ = -a_{1}y\cdot -a_{0}y + bu$

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


*Imagen 8. Observador de estados extendido para NADRC*

El sistema en lazo extendido nos dará los parámetros en el espacio Z aplicando la transformada Z, como resultado se obtienen las siguientes fórmulas:

* $Z_{1}\cdot  = Z_{2} -\beta _{1}\gamma _{1}(\epsilon)$

* $Z_{2}\cdot = Z_{3} + b_{0}u - \beta _{2}\gamma _{2}(\epsilon)$

* $Z_{3}\cdot = - \beta _{3}\gamma _{3}(\epsilon)$

* $\epsilon = Z_{1} - y$

Los parámetros de u están dados por la siguiente ecuación:

$U = \frac{u_{0} - Z_{3}}{b_{0}}$

Una vez que se realiza el proceso en el espacio de estados, obtenemos la función del sistema controlado y libre de perturbaciones con un comportamiento integrador.

* $X_{1}\cdot = X_{2}$

* $X_{2}\cdot = u_{0}$

* $y = X_{1}$


### 3.1. Funciones para la Acción de Control en el Caso No Lineal

En el control ADRC aplicado a sistemas no lineales, la acción de control se diseña utilizando funciones no lineales que mejoran la robustez y la capacidad de rechazo de perturbaciones. Entre estas funciones destaca la función de no linealidad tipo fal (del inglés function approaching linearity), la cual suaviza el comportamiento del controlador cerca del origen y actúa como ganancia variable, adaptándose a la magnitud del error.

Estas funciones permiten construir controladores y observadores que no requieren la linealización del sistema, haciendo posible una respuesta eficiente y estable incluso en presencia de fuertes no linealidades o perturbaciones no modeladas.

* $u_{0} = k_{1}fal(r_{1}-Z_{1}, \vartheta _{1}, \delta)$

  $+k_{2}fal(r_{1} \cdot - Z_{2}, \vartheta _{2}, \delta)$

Para hallar los parámetros de ganancias del sistema del observador y del controlador se debe tener encuenta los siguientes casos en base a la función $fal(e^{\sim }, \vartheta _{i}, \delta)$:

**Caso 1**

* $\frac{e^{\sim }}{\delta ^{1} -\vartheta _{i}}$  ,   $|X|\leq \delta$

**Caso 2**

* $|e^{\sim }| sign(e^{\sim }),   |X|>\delta$

## 4.  Rechazo Activo a Perturbaciones Sistema Lineal

Para el sistema lineal se realiza un observador de estados para la función aplicando transformada Z:

* $Z_{1} \cdot = Z_{2} + L_{1}e$

* $Z_{2} \cdot = Z_{3} + b_{0}u + L_{2}e$

* $Z_{3} \cdot = L_{3}e$

* $e= y - Z_{1}$

Frente a este modelo se realiza la extención de modelo para que nos de como resultado:

* $X_{1} \cdot = X_{2}$

* $X_{2} \cdot = X_{3} + b_{0}u$

* $Z_{3} \cdot = h$

* $y = X_{1}$

En base al sistema definido previamente mediante el observador de estados, se halla la acción de control necesaria que está delimitada por la siguiente ecuación: 

$U_{0} = k_{1}(r\sim - z_{1})-k_{2}z_{2}$

En sistemas lineales, el Rechazo Activo de Perturbaciones (ADRC) ofrece una alternativa eficaz a los controladores clásicos como el PID, al no depender de un modelo matemático preciso. En este enfoque, se considera una planta lineal simple, y cualquier dinámica no modelada, incertidumbre o perturbación externa se agrupa como perturbación total, la cual es estimada en tiempo real mediante un observador extendido (ESO).

![image](https://github.com/user-attachments/assets/8d52a0a1-2699-4b4e-bffb-47e4ef81a62f)

*Imagen 9. Comparación ADRC y PID*

Una vez estimada, esta perturbación se compensa activamente con la acción de control, logrando un comportamiento deseado del sistema. En el caso lineal, el diseño del ADRC es más sencillo y directo, lo que lo convierte en una opción atractiva para aplicaciones prácticas donde se busca simplicidad, robustez y buen desempeño dinámico.

## 5. Observador de estados ADRC

El observador extendido de estados (ESO) es una parte fundamental del Rechazo Activo de Perturbaciones (ADRC). Su función principal es estimar no solo los estados internos del sistema, sino también una señal adicional que representa la perturbación total, es decir, la combinación de dinámicas no modeladas, incertidumbres del sistema y perturbaciones externas.

Este observador se actualiza en tiempo real y permite que el controlador reaccione rápidamente a cualquier cambio inesperado, rechazando activamente las perturbaciones sin requerir un modelo preciso de la planta. Gracias a esta estimación, el controlador puede compensar los efectos negativos y forzar al sistema a seguir el comportamiento deseado, incluso bajo condiciones adversas.

Frente al desarrollo del observador de estados planteamos la fórmula inicial de estado para el desarrollo del análisis matemático:

$X_{k+1} = AX_{k} + Bu_{k}$

Con base al análisis de la ecuación de estados desarrollamos la ecuación de Observador:

$X_{k+1}^{\wedge} = AX_{k}^{\wedge} + Bu + L(y_{k} - X_{k}^{\wedge})$

![image](https://github.com/user-attachments/assets/54e9d6e3-2fdd-454b-9735-67a590628d43)

*Imagen 10. Observador de Estados*

Para un sistema discreto con perturbaciones el diseño de la estimación de parámetros estaría dado por: 

* $X_{k+1} = A * X_{k} + B * u_{k} + F * d_{k}$

* $y_{k} = C * X_{k}$

Si durante el proceso de funcionamiento del sistema, vemos que la perturbación es constante $d(k+1) = d(k)$, se añade como variable de estado.

$$Faltante diapositiva 18$$

Una vez se tenga el diseño del sistema con las perturbaciones añadidas, se puede diseñar el obseradoir de estados compensanndo el efecto de la salida mediante una pre-alimentación del sistema.

$$FAltante diapositiva 19$$

Una vez obtenido la representación de espacio de estados mediante una matriz, se construye el observador de Luenberger.

$$Faltante diapositiva 20$$

## 6. Observador de Luenberger

El Observador de Luenberger es una herramienta utilizada en sistemas lineales para estimar los estados internos de un sistema dinámico cuando no todos pueden ser medidos directamente. Se basa en un modelo matemático del sistema y en la retroalimentación del error entre la salida real y la estimada, ajustando así las estimaciones de los estados.

![image](https://github.com/user-attachments/assets/853ca022-0859-4ff8-bf79-434464528794)

*Imagen 11. Observador de Luenberger*

Su estructura combina el modelo del sistema con una ganancia de observación que permite corregir las estimaciones en función de la diferencia entre la salida medida y la estimada. Este observador es ampliamente utilizado en control clásico y moderno por su simplicidad, efectividad y bajo costo computacional.

En el diseño de este observador, se tiene el coeficinete $X^{\bigtriangleup \cdot }$ el cual es el vector asociado a los coeficientes que determinarán el polinomio de hurwitz asociado a la dinámica del error de estimación $e_{y} \sim$ definido como $e_{y} \sim = y- y^{\bigtriangleup }$

*Faltante diapositiva 21*

Al restar las ecuaciones del sistema real y del observador, se obtiene una ecuación que describe la dinámica del error de estimación. Esta dinámica está gobernada por una matriz, conocida como matriz del error, cuya estructura determina la estabilidad del observador. A partir de esta matriz, se puede obtener el polinomio característico, el cual permite analizar y ubicar los polos del observador para garantizar una convergencia rápida y estable del error hacia cero.

$(e_{y}^{\sim })^{n+m}+ \lambda_{n+m-1}(e_{y}^{\sim })^{n+m-1} + \lambda_{n+m-2}(e_{y}^{\sim })^{n+m-2} + ... + \lambda_{2}(e_{y}^{\sim })^{2} + \lambda_{1}e_{y}^{\sim \cdot } + \lambda_{0}e_{y}^{\sim } = \epsilon ^{(m)} (t)$


$p(s)=s^{n+m} + \lambda_{n+m-1}s^{n+m-1} + \lambda_{n+m-2}s^{n+m-2} + ... + \lambda_{2}s^{2} + \lambda_{1}s + \lambda_{0}$

Los coeficientes 𝜆𝜉 se eligen de manera que el polinomio característico de la dinámica del error de estimación tenga raíces en el semiplano izquierdo del plano complejo. Esto asegura que el sistema sea estable, cumpliendo con la condición de ser un polinomio de Hurwitz, lo cual garantiza que el error de estimación tienda a cero con el tiempo.

Donde 𝜀 representa la estimación de la perturbación generalizada, la cual se obtiene mediante un observador de estados. Se asume que esta perturbación puede ser aproximada por un polinomio en función del tiempo, lo que permite incluirla dentro del modelo del observador y estimarla junto con los estados del sistema.

$\zeta(t) = K_{0} + K_{1}t + K_{2}t^{2} + ... + k_{m}t^{m} +r(t)$

Suponiendo que la perturbación generalizada estimada cumple ε^(m)(t)=0, y considerando r(t) como el residuo entre la salida real y estimada, es posible diseñar un observador extendido que no solo estime las derivadas de la salida, sino también la perturbación generalizada y sus derivadas. Este enfoque permite capturar dinámicamente el efecto de perturbaciones e incertidumbres, facilitando su rechazo activo mediante la acción de control.

## 7. Conclusiones


## 8. Referencias
