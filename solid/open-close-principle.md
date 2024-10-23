---
description: Princípio do Aberto-Fechado, em pt-BR.
---

# Open Close Principle

Este postulado define o seguinte:

> Entidades de software devem ser abertas para extensão, mas fechadas para modificação.

Em outras palavras:

* **Aberta para extensão**: significa que o comportamento da classe pode ser entendido. Podemos fazer um método da classe se comportar de forma diferente conforme as mudanças exigidas pela aplicação ao qual ele pertence, ou para ir de encontro as necessidades de novas aplicações.
* **Fechadas para modificação**: o código-fonte da classe é inviolável. Ninguém tem a permissão de alterar o código-fonte original da classe para atender a novos requisitos da aplicação. O risco de alterar o código-fonte da classe é que isso pode impactar no funcionamento de outras rotinas que dependem do comportamento dessa classe.

Com exemplo, vamos considerar a seguinte classe que representa as figuras geométricas quadrado e circulo.

```python
class Square(Shape):
	
    def __init__(self, lenght):
	    super().__init__()
	    self.lenght = lenght
```

e

```python
class Circle(Shape):
	
	def __init__(self, radius):
	    super().__init__()
	    self.radius = radius
```

Também temos uma classe que calcula a área dessas figuras e retornar o resultado na tela:

```python
import math

class ShapeAreaCalculator:

	def calc_area(self, shape):
	    """Calcule area of shape"""

		area = 0

	    if isinstance(shape, Square):
		    area = shape.lenght ** 2
			
        elif isinstance(shape, Circle):
		    area = math.pi * shape.radius ** 2

        return area
```

O problema da classe `ShapeAreaCalculator`é que, cada vez que uma nova figura geométrica for adicionada, temos que adicionar um novo `if` para verificar o tipo da figura, fazendo com que o método `calc_area` fique cada vez maior. Em outras palavras, a classe `ShapeAreaCalculator` não está fechada para modificação.

Para iniciar os ajustes, vamos melhorar as classes de figuras geométricas criando uma classe base `Shape`, que irá possuir um método `area`, que será herdado por todas as figuras que herdarem essa classe:

```python
class Shape:

	def area(self):
	    pass
```

Atualizando `Square` e `Circle`:

```python
class Square(Shape):
	
	def __init__(self, lenght):
	    super().__init__()
	    self.lenght = lenght

	def area(self):
	    return self.lenght ** 2
```

e

```python
import math

class Circle(Shape):
	
	def __init__(self, radius):
	    super().__init__()
	    self.radius = radius

	def area(self):
	    return math.pi * self.radius ** 2
```

Agora, qualquer nova figura geométrica deve herdar a classe `Shape` e implementar seu próprio método `area`. As classes de figura agora estão abertas para extensão e fechadas para modificação (não será necessário alterar nenhuma delas quando uma nova figura for adicionada).

Agora, vamos corrigir o método `calc_area` de modo a deixá-lo fechado para modificação:

```python
class ShapeAreaCalculator:

	def calc_area(self, shape):
	    """Calcule area of shape"""
	    area = shape.area()
	    return area
```

Agora, o método `calc_area` está fechado para modificação. Independente do número de figuras geométricas que forem adicionadas na nossa aplicação.

### Fontes

[https://web.archive.org/web/20150415215806/http://www.objectmentor.com/resources/articles/ocp.pdf](https://web.archive.org/web/20150415215806/http://www.objectmentor.com/resources/articles/ocp.pdf)
