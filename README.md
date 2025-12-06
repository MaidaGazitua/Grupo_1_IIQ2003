# Grupo_1_IIQ2003
Caracterización del perfil de temperatura en paredes residenciales en Santiago de Chile, considerando materiales de cambio de fase (PCM), con el objetivo de evaluar su efectividad en el aislamiento térmico.

## Descripción general del proyecto

El proyecto permite caracterizar el perfil de temperatura en paredes residenciales en Santiago de Chile, el cual está gobernado por conducción de calor a través de su espesor. Se centra en un geopolímero de concreto (GPC) con material microencapsulado de cambio de fase (MPCM). A partir de ello, busca evaluar su efectividad en el aislamiento térmico considerando las variaciones en la capacidad calorífica del material con la temperatura.

La principal problemática que aborda el proyecto es el alto consumo energético, emisiones de dióxido de carbono e ineficiencia en el aislamiento térmico. En Chile, el sector residencial representa cerca del 15% del consumo total de energía y el 5% de las emisiones nacionales de dióxido de carbono, siendo la calefacción la principal fuente de consumo (Ministerio de Energía, 2019a). Como consecuencia, una mejora en el área permitirá incrementar la eficiencia energética y reducir la contaminación, lo cual beneficiará a las futuras generaciones (Ministerio de Energía, 2019b). A su vez, se estima que más del 60% de las viviendas carece de aislación térmica adecuada, lo que incrementa la vulnerabilidad energética de los hogares y los expone a condiciones extremas de frío y calor, contaminación intradomiciliaria y altos costos de calefacción (CIPER Chile, 2022). Como consecuencia, disminuye considerablemente la calidad de vida de las personas. 

En Chile, existe una importante problemática para mantener condiciones térmicas adecuadas dentro del hogar debido a la baja calidad constructiva y la ausencia de aislación. Miles de familias deben destinar una proporción significativa de sus ingresos a calefacción para alcanzar temperaturas mínimas de confort, sin lograrlo en muchos casos. Esta situación que genera un círculo de desigualdad, donde familias quedan expuestas a enfermedades respiratorias y contaminación intradomiciliaria, enfrentando altos costos energéticos que afectan su presupuesto mensual (Amigo Jorquera et al., 2019). En este contexto, mejorar el aislamiento térmico de muros y techos puede reducir la demanda energética hasta en un 40%, mejorando el bienestar y salud de las familias (Universidad Central de Chile, 2020). 

La carencia de un buen aislamiento térmico ha impulsado al Estado a implementar proyectos relacionados con la sustentabilidad, respondiendo a la urgencia de optimizar el uso energético y reducir el impacto económico y ambiental del país. Uno de ellos es la actualización de la reglamentación térmica en la Ordenanza General de Urbanismo y Construcciones (OGUC), que incorpora exigencias para las infraestructuras de establecimientos educacionales y de salud. El Ministerio de Vivienda y Urbanismo presenta una serie de beneficios de este cambio: permitirá mantener una temperatura cómoda, mejorar calidad del aire interior, evitar patologías constructivas por condensación, reducir el uso de leña, disminuir las emisiones de material particulado y contribuir al ahorro en calefacción (MINVU, 2024). Esto confirma la pertinencia del proyecto frente a las necesidades del país, el que se plantea como una contribución al esfuerzo de mejorar la calidad de vida de los habitantes y proteger el medio ambiente. 

## Explicación breve del sistema modelado

El proyecto permite caracterizar el perfil de temperatura en paredes residenciales en Santiago de Chile, el cual está gobernado por conducción de calor a través de su espesor. Esta condición nos permite modelar el problema de forma unidimensional, dado que las variaciones laterales de temperatura son despreciables en comparación al gradiente dominante en el eje normal a la superficie. Esta aproximación es aceptable en geometrías donde una dimensión es significativamente menor que las otras, ya que la conducción se concentra casi exclusivamente en la dirección reducida (Cengel, 2002). A la vez, se plantea un modelo transiente que incluye las variaciones en las condiciones ambientales a lo largo del día, tanto de temperatura exterior como de radiación.

Luego, se definieron los principales fenómenos de transporte involucrados. De forma más relevante, se debe considerar la transferencia de calor por conducción a lo largo del espesor de la pared. A la vez, existe transferencia de calor por convección natural, tanto hacia el interior como el exterior de la vivienda. Para el interior, se consideró una temperatura constante de 21°C. Para el exterior, se consideró una variación temporal senoidal de temperatura durante el verano. Por último, se debe incluir el calor absorbido por radiación solar, asumiendo una variación senoidal a lo largo del día.

Para modelar el sistema, se consideraron 4 supuestos relevantes. En primer lugar, la transferencia de calor a través de la pared es unidimensional en el eje x. Además, no hay ninguna fuente de generación de energía dentro de la pared. A la vez, el aislante dentro de la pared está distribuido de forma homogénea y es isotrópico. Finalmente, la densidad y conductividad térmica del material son constantes. A continuación, se presenta un esquema del sistema.

![Esquema transferencia de calor en pared residencial](Figuras/Esquema.png)

## Descripción del método numérico utilizado

A partir de los supuestos realizados, se pudo modelar el problema mediante la ecuación de conservación de energía:

$$\rho c_p \left( \frac{\partial T}{\partial t} + v_x \frac{\partial T}{\partial x} + v_y \frac{\partial T}{\partial y} + v_z \frac{\partial T}{\partial z} \right) = k \left( \frac{\partial^2 T}{\partial x^2} + \frac{\partial^2 T}{\partial y^2} + \frac{\partial^2 T}{\partial z^2} \right) + \mu\phi_v$$

Se consideró que las velocidades en todos los ejes son 0, ya que se está modelando un sólido. Además, solo nos interesa el transporte transiente en la dirección x. Por lo tanto, el sistema se simplifica a a siguiente ecuación:

$$
\rho c_p \frac{\partial T}{\partial t}
= k \frac{\partial^2 T}{\partial x^2}
$$

Considerando que la capacidad calorífica varía con la temperatura, se puede modelar mediante las siguientes ecuaciones, considerando que su temperatura de fusión (Tm) es igual a 23,7°C:

$$
C_p(T) =
\begin{cases}
C_{p0}+h\cdot \dfrac{w_l^{2 m_l}}
{w_l^2+(2^{\frac{1}{m_l}}-1)\cdot (2T-2T_m)^2}, & T \le T_m \\
C_{p0}+h\cdot \dfrac{w_r^{2 m_r}}
{w_r^2+(2^{\frac{1}{m_r}}-1)\cdot (2T-2T_m)^2}, & T > T_m
\end{cases}
$$

Además, se planteó 1 condición inicial y 2 condiciones de borde. La condición inicial considera que la temperatura en el tiempo 0 es conocida. La primera condición de borde considera la transferencia de calor por convección hacia el interior de la vivienda, considerando que esta mantiene una temperatura constante de 21°C. La segunda condición de borde considera la transferencia de calor por convección hacia el exterior de la vivienda, así como por radiación. Para este caso, se considera que tanto la temperatura exterior como radiación solar varían de forma senoidal a lo largo del día:

$$
\text{1) Condición inicial: } \quad T(x, t=0) = T_0
$$

$$
\text{2) Convección borde 1:} \quad
-k \frac{\partial T(x=0)}{\partial x} = h_1 \left( T_\infty^{\text{interior}} - T(x=0) \right)
$$

$$
\text{3) Condición borde 2:} \quad
-k \frac{\partial T(x=\delta)}{\partial x}= h_2 \left( T(x=\delta) - T_\infty^{\text{exterior}}(t) \right)- \alpha q''_{solar}(t)
$$

donde $T_\infty^{\text{exterior}(t)}$ y $q''_{solar}(t)$ son funciones senoidales en función del tiempo:

$$
T_\infty^{\text{exterior}(t)}= \frac{T_{\max} + T_{\min}}{2}+ \frac{T_{\max} - T_{\min}}{2}\sin\left( \frac{\pi}{43200} t - \frac{2\pi}{3} \right)
$$

$$
q''_{solar}(t) = 
\begin{cases}
0, & 21{:}00 \le t \le 5{:}00 \\
q_{s,\max} \, \sin\left( \frac{\pi}{57600}\, t - \frac{5\pi}{16} \right),
& 5{:}00 < t < 21{:}00
\end{cases}
$$

Luego, se puede discretizar la ecuación diferencial y las condiciones de borde. Para la ecuación diferencial, se considera una aproximación hacia adelante de primer orden para la derivada temporal, y una aproximación central de segundo orden para la derivada espacial. Para la condición inicial, se reemplaza en el nodo de tiempo 0. Para la condición de borde 1, se usa una aproximación hacia adelante de segundo orden. Para la condición de borde 2, se usa una aproximación hacia atrás de segundo orden. A continuación, se muestra la forma en que se despeja la discretización de la ecuación diferencial.

$$
\rho\ c_p\\frac{T_i^{j+1} - T_i^{j}}{\Delta t}=k\frac{T_{i+1}^{j} - 2T_i^{j} + T_{i-1}^{j}}{\Delta x^2}
$$

$$
\frac{\rho\ c_pT_i^{j+1}}{\Delta t} = \frac{\rho\ c_pT_i^{j}}{\Delta t}+k\frac{T_{i+1}^{j} - 2T_i^{j} + T_{i-1}^{j}}{\Delta x^2}
$$

$$
T_i^{j+1} = T_i^{j} + \Delta t \frac{k}{\rho c_p\Delta x^2} (\{T_{i+1}^{j} - 2T_i^{j} + T_{i-1}^{j} \}) 
$$

Luego, las condición inicial queda:

$$
\quad T_i^{j=0} = T_0
$$

La condición de borde 1 se simplifica:

$$
k \cdot \frac{3T_i^j - 4T_{i+1}^{j} + T_{i+2}^{j}}{2\Delta x} = h_1 \left( T_\infty^{\text{interior}} - T_i^j \right)
$$

$$
T_i^j = \frac{k}{3k + 2h_1\Delta x} \left( 4T_{i+1}^{j} - T_{i+2}^{j} \right) + \frac{h_1 \cdot T_\infty^{\text{interior}} 2\Delta x}{3k + 2h_1\Delta x}
$$

Finalmente, la condición de borde 2 se simplifica:

$$
k \cdot \frac{-3T_i^j + 4T_{i-1}^{j} - T_{i-2}^{j}}{2\Delta x} = h_2 \left( T_i^j - T_\infty^{\text{exterior}} \right) -\alpha q_{solar}
$$

$$
T_i^j = \frac{1}{-\frac{3}{2\Delta x}-h_2}\left(\frac{k}{2\Delta x} \left(- 4T_{i-1}^{j} + T_{i-2}^{j} \right) - h_2 T_\infty^{\text{exterior}} -\alpha q_{solar}\right)
$$

Para resolver el sistema, se utilizarán dos métodos numéricos acoplados. En primer lugar, se implementará el método forward time centred space (FTCS) para resolver el sistema. En cada iteración, se debe realizar una serie de iteraciones
sobre punto fijo para poder construir una matriz de coeficientes constante. 

DESCRIBIR A DETALLE

## Instrucciones para ejecutar el código

REVISAR CODIGO

## Gráficos generados

COPIAR Y PEGAR
