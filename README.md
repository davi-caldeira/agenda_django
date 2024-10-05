# Estrutura Básica e Introdução a Banco de Dados com o Django-Admin

Este guia detalhado irá conduzi-lo através dos conceitos fundamentais do Django, focando na estrutura básica, integração com banco de dados e utilização do Django Admin. Este é um recurso ideal para iniciantes que desejam compreender como o Django funciona e como começar a desenvolver aplicações web robustas com ele.

## Sumário

- [Introdução ao Django](#introdução-ao-django)
  - [O que é o Django?](#o-que-é-o-django)
  - [Instalação do Django](#instalação-do-django)
  - [Criando um Projeto Django](#criando-um-projeto-django)
- [Estrutura Básica do Django](#estrutura-básica-do-django)
  - [Arquivos e Diretórios Principais](#arquivos-e-diretórios-principais)
  - [URLs e Vistas](#urls-e-vistas)
  - [Templates](#templates)
- [Banco de Dados e Django Admin](#banco-de-dados-e-django-admin)
  - [Configuração do Banco de Dados](#configuração-do-banco-de-dados)
  - [Migrations](#migrations)
  - [Utilizando o Django Admin](#utilizando-o-django-admin)
- [Criando Tabelas com Models](#criando-tabelas-com-models)
  - [Definindo Models](#definindo-models)
  - [Registrando Models no Admin](#registrando-models-no-admin)
  - [Operações CRUD com Models](#operações-crud-com-models)
- [Próximos Passos](#próximos-passos)

---

## Introdução ao Django

### O que é o Django?

Django é um framework web de alto nível escrito em Python que segue o padrão arquitetural MVC (Model-View-Controller). Ele é projetado para facilitar o desenvolvimento rápido e pragmático de aplicações web, promovendo o reuso de código e a separação de componentes.

**Principais Características:**

- **Rapidez de Desenvolvimento:** Permite desenvolver aplicações web de forma rápida e eficiente.
- **Administração Automática:** Possui uma interface administrativa pronta para uso.
- **Segurança:** Inclui recursos integrados para lidar com segurança web.
- **Escalabilidade:** Projetado para lidar com as maiores demandas da web.

### Instalação do Django

Para instalar o Django, você precisará ter o Python instalado em sua máquina. Recomenda-se o uso de um ambiente virtual para gerenciar as dependências do projeto.

```bash
# Atualize o pip
pip install --upgrade pip

# Instale o virtualenv
pip install virtualenv

# Crie um ambiente virtual
virtualenv venv

# Ative o ambiente virtual
# No Windows:
venv\Scripts\activate
# No Linux/macOS:
source venv/bin/activate

# Instale o Django
pip install django
```

### Criando um Projeto Django

Após a instalação, você pode criar um novo projeto Django usando o comando `django-admin`:

```bash
django-admin startproject meu_projeto
cd meu_projeto
```

## Estrutura Básica do Django

### Arquivos e Diretórios Principais

Após criar um projeto, a estrutura de diretórios será semelhante a:

```
meu_projeto/
    manage.py
    meu_projeto/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

**Descrição dos Arquivos:**

- **manage.py:** Script de linha de comando para interagir com o projeto.
- **__init__.py:** Indica que o diretório é um pacote Python.
- **settings.py:** Arquivo de configuração do projeto.
- **urls.py:** Define as rotas URL para o projeto.
- **wsgi.py:** Ponto de entrada para servidores web compatíveis com WSGI.

### URLs e Vistas

As URLs são roteadas para vistas, que são funções ou classes que processam a requisição e retornam uma resposta.

**Exemplo de `urls.py`:**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

**Exemplo de `views.py`:**

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Olá, mundo!")
```

### Templates

Templates são arquivos HTML que podem utilizar a linguagem de template do Django para renderizar dados dinâmicos.

**Exemplo de Template (`home.html`):**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Página Inicial</title>
</head>
<body>
    <h1>Bem-vindo ao Meu Projeto Django!</h1>
</body>
</html>
```

**Renderizando um Template na View:**

```python
from django.shortcuts import render

def home(request):
    return render(request, 'home.html')
```

## Banco de Dados e Django Admin

### Configuração do Banco de Dados

O Django suporta vários bancos de dados, como SQLite, PostgreSQL, MySQL e Oracle. Por padrão, o Django utiliza o SQLite.

**Configuração no `settings.py`:**

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

### Migrations

Migrations são uma forma de sincronizar o estado dos models com o esquema do banco de dados.

**Criando Migrations:**

```bash
python manage.py makemigrations
```

**Aplicando Migrations:**

```bash
python manage.py migrate
```

### Utilizando o Django Admin

O Django Admin é uma interface administrativa pronta para uso que permite gerenciar os dados do seu aplicativo.

**Criando um Superusuário:**

```bash
python manage.py createsuperuser
```

**Executando o Servidor de Desenvolvimento:**

```bash
python manage.py runserver
```

Acesse o Django Admin em `http://127.0.0.1:8000/admin/` e faça login com as credenciais do superusuário.

## Criando Tabelas com Models

### Definindo Models

Models são classes Python que representam as tabelas do banco de dados.

**Exemplo de `models.py`:**

```python
from django.db import models

class Cliente(models.Model):
    nome = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    data_cadastro = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.nome
```

### Registrando Models no Admin

Para gerenciar seus models no Django Admin, você precisa registrá-los.

**Exemplo de `admin.py`:**

```python
from django.contrib import admin
from .models import Cliente

admin.site.register(Cliente)
```

### Operações CRUD com Models

**Criando um Registro:**

```python
cliente = Cliente.objects.create(nome="João Silva", email="joao@example.com")
```

**Lendo Registros:**

```python
clientes = Cliente.objects.all()
```

**Atualizando um Registro:**

```python
cliente = Cliente.objects.get(id=1)
cliente.nome = "João Souza"
cliente.save()
```

**Deletando um Registro:**

```python
cliente = Cliente.objects.get(id=1)
cliente.delete()
```

## Próximos Passos

*Espaço reservado para a continuação. Futuramente, serão adicionados mais tópicos e detalhes sobre funcionalidades avançadas do Django, como formulários, autenticação, testes e implantação em produção.*

---

*Este guia será atualizado com mais conteúdos em breve.*