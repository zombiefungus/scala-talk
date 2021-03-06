![LOGO](https://github.com/zombiefungus/scala-talk/raw/master/assets/images/scala-logo.png)

Programación Orientada a Objetos

<span class="red">+</span>

Programación Funcional

---

##¿Por qué crear Scala?

+++

####<span class="dgray">Idea</span>
###<span class="orange">Mejorar</span> Java
###sin <span class="orange">conflictuar</span> con este

+++

####<span class="dgray">Cómo</span>
###Abordando <span class="orange">críticas</span> a Java
###Manteniendo <span class="orange">interoperabilidad</span>

<span class="paren">[ Java Bitecode -> JVM ]</span>

<span class="paren">[ Uso de librerías sin distinción ]</span>

---
####Lo mejor de dos mundos
### <span class="orange">Objetos</span>

<span class="paren">[ Reutilización de código, Encapsulamiento, ... ]</span>

### <span class="orange">Funcional</span>

<span class="paren">[ Inmutabilidad, Mónadas, Inferencia de tipos, Pattern matching, ... ]</span>

---
#### <span class="red">¿Quién lo usa?</span>

<img src="https://cdn4.iconfinder.com/data/icons/social-messaging-ui-color-shapes-2-free/128/social-linkedin-square2-128.png"
     alt="LinkedIn" height="100">
<img src="https://edubloxtutor.com/wp-content/uploads/2016/11/twitter-3-xxl.png"
     alt="Twitter" height="100">
<img src="https://www.shareicon.net/data/128x128/2016/07/16/796802_logo_512x512.png"
     alt="Foursquare" height="100">
<img src="https://img.clipartfest.com/41febf049d705f818380e1f03ed4e091_free-icons-clipart-netflix_256-256.png"
     alt="Netflix" height="100">

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/Tumblr.svg/256px-Tumblr.svg.png"
     alt="Tumblr" height="100">
<img src="http://riga.esn.lv/sites/default/files/partners/images/airbnb.png"
     alt="AirBnB" height="100">
<img src="http://icons.iconarchive.com/icons/danleech/simple/256/meetup-icon.png"
     alt="Meetup" height="100">
<img src="http://www.omavahti.fi/wp-content/uploads/2015/02/sony-logo-slogan.png" alt="Sony" height="100">

---
#### <span class="red">Herramientas en Scala</span>

<img src="https://svbtleusercontent.com/ivdemz9z9lsm6g_small.png"
     alt="Spark" height="100">
<img src="https://svn.apache.org/repos/asf/kafka/site/logos/originals/png/WIDE%20-%20Black%20on%20Transparent.png"
     alt="Kafka" height="100">

<img src="https://upload.wikimedia.org/wikipedia/commons/5/50/Samza_Logo.png"
     alt="Samza" height="100">
<img src="https://upload.wikimedia.org/wikipedia/en/thumb/5/5e/Akka_toolkit_logo.svg/1280px-Akka_toolkit_logo.svg.png"
     alt="Akka" height="100">

---

###Hola Mundo

<span class="red">Compilado</span>
```scala
object HelloWorld extends App {
println("Hello, World!")
}
```
<span class="red">Interpretado</span>
```scala
println("Hello, World!")
```

---
##Features

---
###Fuerte sistema de tipado <span class="red">estático</span>

+++

Un ejemplo en <span class="dgray">Python</span>

```python
def foo(x):
return x*3
```

Qué tipo de dato recibe?

Qué tipo de dato retorna?

+++

- `foo(4)` ->  `12` |
- `foo(True)` -> `3` |
- `foo(False)` ->  `0` |
- `foo("what?!")` ->  `"what?!what?!what?!"` |
- `foo({'one':'uno'})` -> `unsupported operand type(s) for *: 'dict' and 'int'` |

---

###<span class="red">Inferencia</span> de tipos

+++

Esto es obvio

```java
int num = 14;
```

Esto también

```
String str = "DAHH, soy un String!!"
```

+++

Esto requiere más esfuerzo

```java
private int tres() { return 3; }
...
int mi3 = tres();
```

Pero <span class="red">es posible</span>

Y Scala lo hace

+++

Es decir:
- Type-safe &#10003;
- <span>Código más <span class="red">legible</span> &#10003;</span> |
- <span>Código <span class="dgray">menos repetitivo</span> &#10003; </span> |

---
###Tipos de datos <span class="red">inmutables</span>

+++

&#9745; Thread-safe

&#9745; Eficiencia |

&#9745; Visibilidad != Mutabilidad (Encapsulamiento) |

+++

Por ejemplo

`scala.collections.Map`

`scala.collections.mutable.HashMap`

`scala.collections.immutable.HashMap`

Estructuras de alto nivel <span class="red">más eficientes</span>

+++

declaración de variables no re-asignables

```scala
val x = "hola"
var y = ">.<"
```
---
###<span class="red">Sobrecarga</span> de operadores

+++

Por qué este resultado

```java
...
("Hola"+"Mundo").equals("HolaMundo")
...
```

Mientras que este no compila?
```java
int a[] = {1,2,3};
int b[] = {4,5};
a = a + b;
```

+++

Porque `+` está <span class="red">sobrecargado</span> para Strings (cool)

¿Cómo lo hago para listas? (u otros)

<span class="dgray">Sorry, noup</span>

+++

En Scala es posible

#### operador = método

tiene algunas implicaciones interesantes

<span class="paren">[ más en un momento ]</span>

---
###Relajación de Sintaxis

+++

<span class="paren">[ recordemos ]</span>

####<span class="red">operador = método</span>

entonces, por ejemplo

+++

Este código

```scala
1 + 2
```

Es equivalente a

```scala
1.+(2)
```

+++

Esto implica que

```scala
class X {
	def foo(x:Int):String = {
		"oli :)"
	}
}

val x = new X()
x.foo(3)
```

+++

Se puede escribir como


```scala
class X {
	def foo(x:Int):String = {
		"oli :)"
	}
}

val x = new X()
x foo 3
```

+++

También es posible cambiar <span class="dgray">paréntesis</span>

por <span class="red">corchetes</span> en las llamadas de los métodos

```scala
1.+(2)
```
es lo mismo que

```scala
1.+{2}
```

y que

```scala
1 + {
	2
}
```

+++

####Pero.. ¿para qué?

Los métodos lucen como <span class="red">keywords</span>

```scala
    object Lunar extends Baysick {
      def main(args:Array[String]) = {
        10 PRINT "Welcome to Baysick Lunar Lander v0.0.1"
        20 LET ('dist := 100)
        30 LET ('v := 1)
        40 LET ('fuel := 1000)
        50 LET ('mass := 1000)
    
        60 PRINT "You are a in control of a lunar lander."
        70 PRINT "You are drifting towards the surface of the 
moon."
        80 PRINT "Each turn you must decide how much fuel to burn."
        90 PRINT "To accelerate enter a positive number, to 
decelerate a negative"
    
        100 PRINT "Distance " % 'dist % "km, " % "Velocity " % 'v % 
"km/s, " % "Fuel " % 'fuel
        110 INPUT 'burn
        120 IF ABS('burn) <= 'fuel THEN 150
        130 PRINT "You don't have that much fuel"
        140 GOTO 100
        150 LET ('v := 'v + 'burn * 10 / ('fuel + 'mass))
        160 LET ('fuel := 'fuel - ABS('burn))
        170 LET ('dist := 'dist - 'v)
        180 IF 'dist > 0 THEN 100
        190 PRINT "You have hit the surface"
        200 IF 'v < 3 THEN 240
        210 PRINT "Hit surface too fast (" % 'v % ")km/s"
        220 PRINT "You Crashed!"
        230 GOTO 250
        240 PRINT "Well done"
    
        250 END
    
        RUN
      }
    }
```
---
###`for` como <span class="red">generadores</span>

+++

Las iteraciones pueden retornar valores

Si usan la keyword <span class="red">yield</span>

```scala
val g = for {i <- 'a' to 'z' if (i >= 'm')} yield i
```


---
###Otras ventajas

+++

####Evaluación perezosa

Las ventajas que ya conocemos

Ej: Streams infinitos

+++

####Programación de alto orden

- El poder de pasar funciones por parámetros
- Retornar funciones como parámetros|
- <span class="red">Clausuras</span>|

+++
<span class="red">Clausuras</span>

Funciones que viajan con un ambiente

+++

####Creación de métodos asociativos a derecha

Esto ya lo conocemos

Qué significa `1|2|3|nil` ?

+++

<span class="red">No</span> significa `((1|2)|3)|nil`

En realidad es `1|(2|(3|nil)))`
+++

Se pueden crear si el nombre del método termina en `:`

+++

Muchas más

- Funciones anónimas|
- Parámetros opcionales|
- Pattern Matching|
- Destructuración|
- Mónadas|

---
