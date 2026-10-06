# Melhorar tipos do dicionário

Melhore o código abaixo.

A saída esperada é:

```text
age NUMBER, name STRING, address STRING
```

```python
entrada = {"age": 30, "name": "jose", "address": "sp"}

output = 'age NUMBER, name STRING, address STRING'

output = ''
for k, v in entrada.items():
    if isinstance(v, int):
        tipo = "NUMBER"
    if isinstance(v, str):
        tipo = "STRING"
    print(k, tipo)
    output += f'{k} {tipo}, '

print(output)
```
