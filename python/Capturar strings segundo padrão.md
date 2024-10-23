#regex #python #snippet

Utilizamos `regex` para realizar a busca do conteudo da string dentro de delimitadores, no caso, colchetes.

Exemplo:

```python
text = 'PRODUTO [033338] [1023]'
```

Devemos extrair o código entre colchetes: `033338`.

Utilizamos a expressão regular:

```regex
\[([0-9]+?)\]
```

Que busca uma ou mais ocorrencias dos digitos de `0` a `9` entre colchetes.

```python
import re

text = 'PRODUTO [033338] [1023]'

# Retorna uma lista de ocorrecias do padrao
codigos = re.findall('\[([0-9]+?)\]', text)

for cod in codigos:
	print(cod)

# Saida:
# [033338]
# [1023]
