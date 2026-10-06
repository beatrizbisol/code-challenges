# Parse de URL

## Enunciado

Implemente `parse_url`. A função recebe uma URL e devolve um `ParsedURL` com protocolo, domínio, caminho e parâmetros de query.

Sem caminho, `path` fica vazio. Sem query string, `query_params` fica um dicionário vazio.

```python
if __name__ == "__main__":
    print(parse_url("https://api.charterup.com/v1/buses?city=Austin&capacity=50"))
    print(parse_url("http://example.com/path"))
    print(parse_url("https://example.engineering"))
    print(parse_url("https://example.com?key=value"))
    print(parse_url("https://example.com/path/to/resource?a=1&b=2&c="))
```

## Código entregue no live coding

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
    protocol, remaining_url = url.split("://")
    print(protocol)
    print(remaining_url)
    query_params = {}
    if remaining_url.find("?") == -1:
        pass
    else:
        remaining_url, query_params = remaining_url.split("?")
    print(query_params)
    if remaining_url.find("/") == -1:
        if remaining_url.split("?") == -1:
            domain = remaining_url
        else:
            domain = remaining_url.split("?")[0]
    else:
        domain = remaining_url.split("/")[0]
    print(domain)
    position_s = remaining_url.find("/")
    # position_i = remaining_url.find("?")
    path = ""
    if position_s == -1:
        pass
    else:
        path = remaining_url[position_s:]
    print(path)
    query_params = dict()
    return ParsedURL(protocol, domain, path, query_params)

# split function
# txt = "hello, my name is Peter, I am 26 years old"

# x = txt.split(", ") # delimeter

# print(x) # ["hello", "my name is Peter", "I am 26 years old"]

# string.find("?") # position of string or -1 if not found

# substring
# url = "http://example.com/path"
# print(url[7:]) = "example.com/path"
if __name__ == "__main__":
    print(parse_url("https://api.charterup.com/v1/buses?city=Austin&capacity=50"))
    print(parse_url("http://example.com/path"))
    print(parse_url("https://example.engineering"))
    print(parse_url("https://example.com?key=value"))
    print(parse_url("https://example.com/path/to/resource?a=1&b=2&c="))
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
