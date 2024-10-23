---
description: Princípio da Segregação de Interfaces, em pt-BR.
---

# Interface Segregation Principle

Este princípio define que:

> Uma classe nunca deve ser forçado a implementar  uma interface ou método que ele não utiliza&#x20;

Casos assim, normalmente ocorrem quando criamos classes ou interfaces muito genéricas com o intuito de "abraçar o mundo", ou seja, uma classe que tentar abranger todos os casos de um uso da nossa aplicação.&#x20;

Como exemplo, vamos retornar a nossa classe **Shape**.&#x20;

```python
class Shape:

    def area(self):
        raise NotImplementedError("Subclasse should implement this")
```

A classe **Shape**, é normalmente utilizada como classe base para as classes **Square** e **Circle**, figuras geométricas cujas classes implementam o método _area_.&#x20;

```python
class Square(Shape):
	
    def __init__(self, lenght):
        super().__init__()
        self.lenght = lenght
        
    def area(self):
        return self.lenght ** 2
```

```python
class Circle(Shape):
	
    def __init__(self, radius):
        super().__init__()
        self.radius = radius
    
    def area(self):
        return math.pi * self.radius ** 2
```

Agora vamos supor que desejemos tornar nossa classe **Shape** ainda mais abrangente, fazendo com que ela represente figuras geométricas 3D (cubo, esfera, etc.). Para isso, adicionamos a ela o método _volume_, responsável por calcular o volume dessas figuras.

```python
class Shape:

    def area(self):
        raise NotImplementedError("Subclasse should implement this")
    
    def volume(self):
        raise NotImplementedError("Subclasse should implement this")
```

Agora repare que com a adição do método _volume_, todas as nossas subclasses também serão _**obrigadas**_ a implementar esse método. Entretanto, não faz sentido algum as classes **Square** e **Circle** possuírem o método _volume_, já que elas representam figuras 2D (Quadrado e Círculo, respectivamente). Elas nem mesmo irão utilizar esse método. \
Ao forçarmos as classes **Square** e **Circle** implementarem o método _volume_, nós estamos desobedecendo ao **Princípio da Segregação de Interfaces.** O ideal nesse caso, seria criar uma nova classe diferente de **Shape** e fazer com que as subclasses representando figuras 3D implementem o método _volume._

```python
class Solid:
    
    def volume(self):
        raise NotImplementedError("Subclasse should implement this")
```

### Fontes

[https://web.archive.org/web/20150905081110/http://www.objectmentor.com/resources/articles/isp.pdf](https://web.archive.org/web/20150905081110/http://www.objectmentor.com/resources/articles/isp.pdf)
