# Atividade - Explorando o cache de HTTP em aplicações REST
Nesta atividade foi elaborarado um tutorial utilizando Python + Flask por Michele Ramos e João Pires

## instalar o Flask
`pip install Flask`

## Aplicação Flask:

- Criar uma aplicação Flask básica com um endpoint que retorna dados de teste

**O resultado será:**

```
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api/data')
def get_data():
    data = {
        "message": "Esta é uma resposta de teste."
    }
    return jsonify(data)

if __name__ == '__main__':
    app.run(debug=True)
```

## Implementando o CACHE

- para esta implementação será necessário instalar a biblioteca Flask-Caching

`pip install Flask-Caching`

- atualize o arquivo para:
```
from flask import Flask, jsonify
from flask_caching import Cache

app = Flask(__name__)

cache = Cache(app, config={'CACHE_TYPE': 'simple'})

@app.route('/api/data')
@cache.cached(timeout=60)
def get_data():
    data = {
        "message": "Esta é uma resposta de teste."
    }
    return jsonify(data)

if __name__ == '__main__':
    app.run(debug=True)
```

## Testando a aplicação:

- execute o arquivo
- e acesse o endpoint http://127.0.0.1:5000/api/data

## Limitações e Benefícios

- O cache pode ocupar memória e por isso optamos por incluir um timeOut para evitar problemas de excesso de memória
- O Cache reduz o tempo de resposta das requisições, pois os dados são recuperados do cache.
