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

$$
\rho c_p \left( \frac{\partial T}{\partial t} 
+ v_x \frac{\partial T}{\partial x}
+ v_y \frac{\partial T}{\partial y}
+ v_z \frac{\partial T}{\partial z} \right)
= k \left(
\frac{\partial^2 T}{\partial x^2}
+ \frac{\partial^2 T}{\partial y^2}
+ \frac{\partial^2 T}{\partial z^2}
\right)
+ \psi_b
$$



Se consideró que las velocidades en todos los ejes son 0, ya que se está modelando un sólido. Además, solo nos interesa el transporte transiente en la dirección x. Por lo tanto, el sistema se simplifica a a siguiente ecuación:

$$
\rho c_p \frac{\partial T}{\partial t}
= k \frac{\partial^2 T}{\partial x^2}
$$


Para resolver el sistema, se utilizarán dos métodos numéricos acoplados. En primer lugar, se implementará el método forward time centred space (FTCS) para resolver el sistema. En cada iteración, se debe realizar una serie de iteraciones
sobre punto fijo para poder construir una matriz de coeficientes constante. 


## Instrucciones para ejecutar el código
## Gráficos generados
