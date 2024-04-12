# Desenvolvendo-sua-Primeira-API-com-FastAPI-Python-e-Docker
**Desafio de Projeto**

Neste projeto, aprenderemos a criar uma poderosa **API assíncrona** para uma competição de crossfit usando o framework **FastAPI**. O objetivo é construir um aplicativo web moderno e eficiente que possa lidar com operações simultâneas de maneira escalável.

Aqui estão as instruções para o projeto:

1. **Adicionar query parameters nos endpoints:**
    - Para o endpoint de atleta, adicione os seguintes parâmetros de consulta:
        - Nome
        - CPF

2. **Customizar o retorno dos endpoints:**
    - No endpoint que obtém todos os atletas, retorne as seguintes informações:
        - Nome do atleta
        - Centro de treinamento
        - Categoria

3. **Manipular exceção de integridade dos dados:**
    - Se ocorrer um erro de integridade (por exemplo, se já existir um atleta cadastrado com o mesmo CPF), trate a exceção `sqlalchemy.exc.IntegrityError` e retorne a seguinte mensagem:
        - "Já existe um atleta cadastrado com o CPF: x"
        - Use o código de status HTTP 303 para indicar redirecionamento.

4. **Adicionar paginação:**
    - Utilize a biblioteca `fastapi-pagination` para adicionar paginação aos resultados.
    - Implemente os parâmetros `limit` e `offset` para controlar a quantidade de resultados retornados.

Para configurar o **FastAPI** para o seu projeto, siga os passos abaixo:

1. **Instalação do FastAPI:**
    - Certifique-se de ter o Python instalado em sua máquina.
    - Abra um terminal ou prompt de comando e execute o seguinte comando para instalar o FastAPI:
        ```
        pip install fastapi
        ```

2. **Crie um arquivo principal para a sua aplicação:**
    - Crie um arquivo chamado `main.py` (ou outro nome de sua escolha) para iniciar sua aplicação.
    - Importe o FastAPI e crie uma instância da aplicação:
        ```python
        from fastapi import FastAPI

        app = FastAPI()
        ```

3. **Defina os endpoints:**
    - Crie rotas (endpoints) para as diferentes funcionalidades da sua API. Por exemplo:
        ```python
        @app.get("/")
        def read_root():
            return {"message": "Bem-vindo à API da competição de crossfit!"}
        ```

4. **Adicione query parameters nos endpoints:**
    - Para adicionar parâmetros de consulta (query parameters), você pode fazer o seguinte:
        ```python
        @app.get("/atletas/")
        def get_atletas(nome: str = None, cpf: str = None):
            # Lógica para buscar atletas com base nos parâmetros de consulta
            # Retorne os resultados conforme especificado nas instruções
            return {"nome": nome, "cpf": cpf}
        ```

5. **Customize o retorno dos endpoints:**
    - No endpoint que obtém todos os atletas, você pode retornar os dados desejados:
        ```python
        @app.get("/atletas/")
        def get_all_atletas():
            # Lógica para buscar todos os atletas
            # Retorne os dados conforme especificado nas instruções
            return {"nome": "Nome do Atleta", "centro_treinamento": "Nome do Centro", "categoria": "Categoria"}
        ```

6. **Manipule exceções de integridade dos dados:**
    - Para tratar a exceção `sqlalchemy.exc.IntegrityError`, você pode fazer o seguinte:
        ```python
        from sqlalchemy.exc import IntegrityError
        from fastapi import HTTPException

        @app.exception_handler(IntegrityError)
        async def integrity_error_handler(request, exc):
            # Lógica para tratar a exceção de integridade
            # Retorne a mensagem e o código de status 303
            raise HTTPException(status_code=303, detail=f"Já existe um atleta cadastrado com o CPF: {exc.params['cpf']}")
        ```

7. **Adicione paginação:**
    - Utilize a biblioteca `fastapi-pagination` para adicionar paginação aos resultados.
    - Consulte a documentação da biblioteca para saber como configurar a paginação com os parâmetros `limit` e `offset`.

Devemos sempre adaptar esses exemplos conforme a estrutura do seu projeto e as tabelas do banco de dados.

https://github.com/digitalinnovationone/workout_api
