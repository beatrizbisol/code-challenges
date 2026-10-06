# Tipos de um JSON

## Enunciado

Trabalhe o input para que o resultado seja o output.

```python
entrada = {"age": 30, "name": "jose", "address": "sp"}

output = 'age NUMBER, name STRING, address STRING'
```

## Código entregue no live coding

```python
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

## Código melhorado

```python
TIPOS = {
    int: "NUMBER",
    str: "STRING",
}
entrada = {"age": 30, "name": "jose", "address": "sp"}
output = ", ".join(
    f"{chave} {TIPOS[type(valor)]}"
    for chave, valor in entrada.items()
)
print(output)
```
