# Parse de URL

## Enunciado

Implemente `parse_url`. A função recebe uma URL e devolve um `ParsedURL` com protocolo, domínio, caminho e parâmetros de query.

```python
url = "https://api.exemplo.com/v1/users?id=10&active=true"

print(parse_url(url))
# protocol: https, domain: api.exemplo.com, path: /v1/users, query_params: {'id': '10', 'active': 'true'}
```

Sem caminho, `path` fica vazio. Sem query string, `query_params` fica um dicionário vazio.

## Código entregue no live coding

```python
class ParsedURL:
    def __init__(self, protocol: str, domain: str, path: str, query_params: Dict[str, str]):
        self.protocol = protocol
        self.domain = domain
        self.path = path
        self.query_params = query_params

    def __str__(self):
        return (
            f"protocol: {self.protocol}, "
            f"domain: {self.domain}, "
            f"path: {self.path}, "
            f"query_params: {self.query_params}"
        )


def parse_url(url: str) -> ParsedURL:
    pass
```

## Código melhorado

```python
from typing import Dict


class ParsedURL:
    def __init__(self, protocol: str, domain: str, path: str, query_params: Dict[str, str]):
        self.protocol = protocol
        self.domain = domain
        self.path = path
        self.query_params = query_params

    def __str__(self):
        return (
            f"protocol: {self.protocol}, "
            f"domain: {self.domain}, "
            f"path: {self.path}, "
            f"query_params: {self.query_params}"
        )


def parse_url(url: str) -> ParsedURL:
    protocol, remaining_url = url.split("://", 1)
    query_string = ""
    if "?" in remaining_url:
        remaining_url, query_string = remaining_url.split("?", 1)
    slash_index = remaining_url.find("/")
    if slash_index == -1:
        domain = remaining_url
        path = ""
    else:
        domain = remaining_url[:slash_index]
        path = remaining_url[slash_index:]
    query_params = {}
    if query_string:
        for pair in query_string.split("&"):
            key, value = pair.split("=", 1)
            query_params[key] = value
    return ParsedURL(protocol, domain, path, query_params)
```
