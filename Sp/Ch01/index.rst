=========
Conociendo Qt 5
=========

Este libro deberá proveerte un paseo a travez de los diferentes aspectos del desarrollo de aplicaciones usando la versión de Qt 5.x. Esta enfocado en la nueva tecnología de Qt Quick pero además provee información necesaria de escritura de "back-ends" de C++ y extensiones para Qt Quick.

Este capitulo provee un resumen principal de Qt 5. Muestra los diferentes modelos de aplicación disponibles para  los desarrolladores y una aplicación de ejemplo de  tal aplicacion de Qt 5 para tener una probadita de las cosas que vendrán. Adicionalmente el capitulo aspira a proveer un avance extenso del contenido de Qt 5 y como obtener contacto con los creadores de Qt 5.

Prefacio
=======

.. rubric:: Historia

Qt 4 ha evolucionado desde 2005 y ha proveido una base solida para miles de aplicaciones, e incluso para sistemas mobiles y de escritorio. El uso de patrones de usuarios de computadora ha cambiado en los ultimos años. Desde las PC's estacionarias hacia Notebooks portables y hoy en dia en computadoras mobiles. La maquina de escritorio clasica es cada vez mas reemplazada con dispositivos mobiles de pantalla basada al tacto. Con esto, los paradigmas de UX de lacomputadora clasica tambien ha estado cambiado. Donde en el pasado Windows UI domino el lugar donde mas tiempo gastamos, en estos dias lo gastamos en otras pantallas con otros lenguajes UI.

Qt 4 fue diseñado para satisfacer el mundo de las computadoras de escritorio teniendo un conjunto coherente de widgets de UI disponibles en la mayoria de las plataformas. El desafio para los usuarios de Qt ha cambiado ahora y se interesa mas en proporcionar un interfaz de usuario basado en pantallas de tacto “touch” para un interfaz de usuario mas orientado  al cliente y permitir interfaces de usuario modernos en la mayoria de los sistemas mobiles y de escritorio. Qt 4.7 inicio la introduccion de la tecnologia Qt Quick que permite a los usuarios crear un conjunto de componentes de interfaces de usuario usando simples elementos para lograr una UI completamente nueva y orientada por las demandas de los clientes.

El Enfoque de Qt 5
---------

Qt 5 es una renovación completa del sumamente exitosa entrega  de Qt 4. Con la liberación de Qt 4.8, la entrega de Qt 4 ha sido hace 7 años. Es tiempo de realizar un “toolkit” todavía mas espectacular. Qt 5 esta enfocado en los siguientes puntos:

* **Gráficas Destacadas**: Qt Quick 2 esta basado en la tecnología OpenGL (ES) usando la la implementación de escenas gráficas. La pila de gráficas recompuesta te permite un nuevo nivel de efectos gráficos combinado con una facilidad de uso nunca antes visto en este campo

* **Productividad de Diseño**: QML y Javascript son las principales actores de la creación de UI's. El modelo sera manejado por C++. La división entre Javascript y C++ permite una interacion rápida para los desarrolladores de vistas concentrados en crear interfaces de usuario fabulosas y los desarrolladores de modelos en C++ que están concentrados en la estabilidad , rendimiento y extensión en el tiempo de ejecución de la aplicación.

* **Portabilidad entre plataformas**: Con la consolidación de la Abstracción de Plataformas de Qt, es ahora posible el conectar rápida y fácilmente a Qt con un amplio rango de plataformas. Qt 5 fue estructurado a travez del concepto de “Qt Essentials and Add-ons” que permiten al desarrollador de sistemas operativos en enfocarse en los módulos esenciales y esto conduce a menores tiempos de ejecución.

* **Desarrollo Abierto**: Qt es ahora un proyecto gobernante realmente abierto organizada por `qt.io <http://qt.io>`_. El desarrollo es abierto y manejado por la comunidad.


