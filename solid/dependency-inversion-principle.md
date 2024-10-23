---
description: Princípio da Inversão de Dependência, em pt-BR
---

# Dependency Inversion Principle

Este princípio é definido por:

> _Dependa de abstrações e não de implementações_

De modo prático, este princípio recomenda que nossas subclasses sempre herdem de abstrações, ao invés de classes que sejam implementações de interfaces. Vamos pegar com exemplo as classes **Shape**, **Square** e **Circle**.&#x20;

<pre class="language-python"><code class="lang-python">class Shape:

    def area(self):
        raise NotImplementedError("Subclasse should implement this")
        

class Square(Shape):
	
    def __init__(self, lenght):
        super().__init__()
        self.lenght = lenght
        
    def area(self):
        return self.lenght ** 2
        

class Circle(Shape):
	
    def __init__(self, radius):
        super().__init__()
<strong>        self.radius = radius
</strong>    
    def area(self):
        return math.pi * self.radius ** 2

</code></pre>

As classes **Square** e **Circle** implementam o método _area_ da classe base **Shape**, que é uma abstração. Poderíamos fazer com que a classe **Square** fosse uma subclasse de **Circle:**

```python
class Square(Circle):
	
    def __init__(self, radius, lenght):
        super().__init__(radius)
        self.lenght = lenght
        
    def area(self):
        return self.lenght ** 2
```

Esse tipo de herança, fere o princípio da inversão de dependências, já que a classe **Circle** é uma classe concreta. Isso nos traz alguns inconvenientes:

1. Nossa classe **Square** irá possuir um atributo _radius_, que não faz sentido algum para a classe **Square**, já que o atributo representa o raio do _circulo_. Ao criar um objeto de **Square**, vamos precisar fornecer não só o comprimento dos lados do quadrado, com também um valor para _radius_, mesmo que ele nunca seja usado.
2. Temos que sobrescrever a implementação do método _area_ da classe **Circle**, já que se não fizermos isso, a classe Square irá utilizar a implementação de _area,_ presente na classe mãe **Circle**, devolvendo o valor errado do cálculo da área, já que tanto a fórmula de área e o valor do atributo _radius_ (como visto no item 1) serão incorretos.

Com base no exemplo acima, podemos concluir que sempre devemos implementar classes abstratas e interfaces o máximo possível, de modo a não herdamos comportamos e atributos já implementados.

### Fontes

[https://web.archive.org/web/20150905081103/http://www.objectmentor.com/resources/articles/dip.pdf](https://web.archive.org/web/20150905081103/http://www.objectmentor.com/resources/articles/dip.pdf)
