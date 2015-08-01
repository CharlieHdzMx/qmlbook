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

Qt 5 Introduction
=================


Qt Quick
--------

Qt Quick is the umbrella term for the user interface technology used in Qt 5. Qt Quick itself is a collection of several technologies:

* QML - Markup language for user interfaces
* JavaScript - The dynamic scripting language
* Qt C++ - The highly portable enhanced c++ library

.. image:: assets/qt5_overview.png


Similar to HTML, QML is a markup language. It is composed of tags called elements in Qt Quick enclosed in curly brackets ``Item {}``. It was designed from the ground up for the creation of user interfaces, speed and easier reading for developers. The user interface can be enhanced using JavaScript code. Qt Quick is easily extendable with your own native functionality using Qt C++. In short the declarative UI is called the front-end and the native parts are called the back-end. This allows you to separate the computing intensive and native operation of your application from the user interface part.

In a typical project the front-end is developed in QML/JavaScript and the back-end code, which interfaces with the system and does the heavy lifting is developed using Qt C++. This allows a natural split between the more design oriented developers and the functional developers. Typically the back-end is tested using Qt own unit testing framework and exported for the front-end developers to be used.


Digesting an User Interface
---------------------------

Let's create a simple user interface using Qt Quick, which showcases some aspects of the QML language. At the end we will have a paper windmill with rotating blades.


.. image:: assets/scene.png
    :scale: 50%


We start with an empty document called ``main.qml``. All QML files will have the ending ``.qml``. As a markup language (like HTML) a QML document needs to have one and only one root element, which in our case is the ``Image`` element with a width and height based on the background image geometry:

.. code-block:: qml

    import QtQuick 2.3

    Image {
        id: root
        source: "images/background.png"
    }

As QML does not make any restriction which element type is the root element we use an ``Image`` element with the source property set to our background image as the root element.


.. image:: src/showcase/images/background.png


.. note::

    Each element has properties, e.g. a image has a ``width``, ``height`` but also other properties like a ``source`` property.  The size of the image element is automatically deducted from the image size. Otherwise we would need to set the ``width`` and ``height`` property to some useful pixel values.

    The most standard elements are located in the ``QtQuick`` module which we include in the first line with the import statement.

    The ``id`` special property is optional and contains an identifier to reference this element later in other places in the document. Important: An ``id`` property cannot be changed after it has been set and it cannot be set during runtime. Using ``root`` as the id for the root-element is just a habit by the author and makes referencing the top-most element predictable in larger QML documents.

The foreground elements pole and pin wheel of our user interface are placed as separate images.

.. image:: src/showcase/images/pole.png
.. image:: src/showcase/images/pinwheel.png

The pole needs to be placed in the horizontal center of the background towards the bottom. And the pinwheel can be placed in the center of the background.

Normally your user interface will be composed of many different element types and not only image elements like in this example.


.. code-block:: qml

  Image {
      id: root
      ...
      Image {
          id: pole
          anchors.horizontalCenter: parent.horizontalCenter
          anchors.bottom: parent.bottom
          source: "images/pole.png"
      }

      Image {
          id: wheel
          anchors.centerIn: parent
          source: "images/pinwheel.png"
      }
      ...
  }



To place the pin wheel at the central location we use a complex property called ``anchor``. Anchoring allows you to specify geometric relations between parent and sibling objects. E.g. Place me in the center of another element ( ``anchors.centerIn: parent`` ). There are left, right, top, bottom, centerIn, fill, verticalCenter and horizontalCenter relations on both ends. Sure they need to match, it does not make sense to anchor my left side to the top side of an element.

So we set the pinwheel to be centered in the parent our background.

.. note::

    Sometime you will need to make small adjustments on the exact centering. This would be possible with ``anchors.horizontalCenterOffset`` or with ``anchors.verticalCenterOffset``. Similar adjustments properties are also available to all the other anchors. Please consult the documentation for a full list of anchors properties.

.. note::

    Placing an image as a child element of our root element (the ``Image`` element) shows an important concept of a declarative language. You describe the user interface in the order of layers and grouping, where the topmost layer (our rectangle) is drawn first and the child layers are drawn on top of it in the local coordinate system of the containing element.

To make the showcase a little bit more interesting, we would like to make the scene interactive. The idea is to rotate the wheel when the user pressed the mouse somewhere in the scene.


We use the ``MouseArea`` element and make it as big as our root element.

.. code-block:: qml

    Image {
        id: root
        ...
        MouseArea {
            anchors.fill: parent
            onClicked: wheel.rotation += 90
        }
        ...
    }

The mouse area emit signals when a user clicks inside it covered area. You can hook onto this signal overriding the ``onClicked`` function. In this case the reference the wheel image and change its rotation by +90 degree.

.. note::

    This works for every signal, the naming is ``on`` + ``SignalName`` in title cases. Also all properties emit a signal when their value changed. The naming is:

        ``on`` + ``PropertyName`` + ``Changed``

    If a ``width`` property is changing you can observe it with ``onWidthChanged: print(width)`` for example.

Now the wheel will rotate, but it is still not fluid yet. The rotation property changes immediately. What we would like that the property changes by 90 degree over time. Now animations come into play. An animation defines how a property change is distributed over a duration. To enable this we use an animation type called property behavior. The ``Behaviour`` does specify an animation for a defined property for every change applied to that property. In short every time the property changes, the animation is run. This is only one of several ways of declaring an animation in QML.

.. code-block:: qml

    Image {
        id: root
        Image {
            id: wheel
            Behavior on rotation {
                NumberAnimation {
                    duration: 250
                }
            }
        }
    }

Now whenever the property rotation of the wheel changes it will be animated using a ``NumberAnimation`` with a duration of 250 ms. So each 90 degree turn will take 250 ms.

.. image:: assets/scene2.png
    :scale: 50%

.. note:: You will not actually see the wheel blurred. This is just to indicate the rotation. But a blurred wheel is in the assets folder. Maybe you want to try to use that.


Now the wheel looks already much better. I hope this has given you a short idea of how Qt Quick programming works.

Qt Building Blocks
==================

Qt 5 consists of a large amount of modules. A module in general is a library for the developer to use. Some modules are mandatory for a Qt enabled platform. They form a set called *Qt Essentials Modules*. Many modules are optional and form the *Qt Add-On Modules*. It's expected that the majority of developers will not have the need to use them, but it's good to know them as they provide invaluable solutions to common challenges.

Qt Modules
---------------------

The Qt Essentials modules are mandatory for a Qt enabled platform. They offer the foundation to develop a modern Qt 5 Application using Qt Quick 2.

.. rubric:: Core-Essential Modules

The minimal set of Qt 5 modules to start QML programming.

.. list-table::
    :widths: 20 80
    :header-rows: 1

    *   - Module
        - Description
    *   - Qt Core
        - Core non-graphical classes used by other modules
    *   - Qt GUI
        - Base classes for graphical user interface (GUI) components. Includes OpenGL.
    *   - Qt Multimedia
        - Classes for audio, video, radio and camera functionality.
    *   - Qt Network
        - Classes to make network programming easier and more portable.
    *   - Qt QML
        - Classes for QML and JavaScript languages.
    *   - Qt Quick
        -  declarative framework for building highly dynamic applications with custom user interfaces.
    *   - Qt SQL
        - Classes for database integration using SQL.
    *   - Qt Test
        - Classes for unit testing Qt applications and libraries.
    *   - Qt WebKit
        - Classes for a WebKit2 based implementation and a new QML API. See also Qt WebKit Widgets in the add-on modules.
    *   - Qt WebKit Widgets
        - WebKit1 and QWidget-based classes from Qt 4.
    *   - Qt Widgets
        - Classes to extend Qt GUI with C++ widgets.


.. digraph:: essentials

    QtGui -> QtCore
    QtNetwork ->QtCore
    QtMultimedia ->QtGui
    QtQml -> QtCore
    QtQuick -> QtQml
    QtSql -> QtCore


.. rubric:: Qt Addon Modules

Besides the essential modules, Qt offers additional modules for software developers, which are not part of the release. Here is a short list of add-on modules available.

* Qt 3D - A set of APIs to make 3D graphics programming easy and declarative.
* Qt Bluetooth - C++ and QML APIs for platforms using Bluetooth wireless technology.
* Qt Contacts - C++ and QML APIs for accessing addressbooks / contact databases
* Qt Location - Provides location positioning, mapping, navigation and place search via QML and C++ interfaces. NMEA backend for positioning
* Qt Organizer - C++ and QML APIs for accessing organizer events (todos, events, etc.)
* Qt P
