---
description: Princípio de Substituíção de Liskov, em pt-BR.
---

# Liskov Substitution Principle

Este princípio define que:

> Funções que usam ponteiros ou referências para a classe base devem ser capazes de usar objetos de classes derivadas sem conhecê-las.

Em outras palavras, se **S** é um subtipo de **T**, então os objetos do tipo **T** podem ser substituídos pelos objetos do tipo **S** sem a necessidade de qualquer alteração no código da aplicação.&#x20;

Como exemplo, podemos considerar a classe **Shape**, que representa uma figura geométrica.

```python
class Shape:

    def area(self):
        raise NotImplementedError("Subclasse should implement this")
```

Toda classe que herdar a classe **Shape**, deve também implementar o método _area_. Caso uma subclasse não o implemente, o método da classe **Shape** será chamado e teremos a exceção _NotImplementedError_.

Seguindo com exemplo, vamos supor que tenhamos a seguinte classe, que recebe a classe **Shape** e suas subclasses e invoca o método _area_.

```python
class ShapeAreaCalculator:

    def calc_area(self, shape):
        """Calcule area of shape"""
        return shape.area()

```

Podemos substituir o parâmetro _shape_, por qualquer objetos das subclasses de **Shape**, que o método _calc\_area_ irá funcionar, desde que a subclasse ao qual esse objeto pertence tenha implementado o método _area_.

### Fontes:

[https://web.archive.org/web/20150905081111/http://www.objectmentor.com/resources/articles/lsp.pdf](https://web.archive.org/web/20150905081111/http://www.objectmentor.com/resources/articles/lsp.pdf)
