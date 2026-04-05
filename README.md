* 🏦 PJL BANK – Sistema Bancário Simples com Flask

* Descrição do nosso Projeto

O PJL BANK é um sistema bancário simples desenvolvido com Python, Flask e SQLAlchemy.
Ele permite cadastrar clientes 

O sistema possui uma página principal:

* Home→ formulário para cadastrar clientes

O projeto utiliza "SQLite" como banco de dados local.

---

* Tecnologias Utilizadas

* Python
* Flask
* Flask-SQLAlchemy
* HTML5
* CSS3
* SQLite

---

* Estrutura do Projeto


PJL_BANK

 app.py
 site.db

 templates
      
       index.html
      


* Explicação

| Arquivo                  | Função                              |
| ------------------------ | ----------------------------------- |
| *app.py*               | Arquivo principal do servidor Flask |
| *site.db*              | Banco de dados SQLite               |
| *templates/index.html*| Página de cadastro de clientes      |

---

* Configuração do Flask

No início do "app.py", o Flask e o SQLAlchemy são configurados:

python
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///site.db'
db = SQLAlchemy(app)


* Explicação

* "Flask(_name_) "→ cria a aplicação web
* "SQLALCHEMY_DATABASE_URI"→ define o banco SQLite
* "SQLAlchemy(app)" → conecta o Flask ao banco

---

* Etapa 1 – Criação do Modelo do Banco

A classe "Dados_Cadastrais" representa a tabela do banco.

python
class Dados_Cadastrais(db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    cpf = db.Column(db.String(11), nullable=False)
    nome = db.Column(db.String(255), nullable=False)
    rua = db.Column(db.String(255), nullable=False)
    cidade = db.Column(db.String(255), nullable=False)
    estado = db.Column(db.String(255), nullable=False)


* (Campos da tabela )

| Campo  | Tipo    | Descrição           |
| ------ | ------- | ------------------- |
| id     | Integer | Identificador único |
| cpf    | String  | CPF do cliente      |
| nome   | String  | Nome do cliente     |
| rua    | String  | Rua do endereço     |
| cidade | String  | Cidade              |
| estado | String  | Estado              |

--

* Etapa 2 – Página Inicial (Home)

A rota "/home" mostra o formulário de cadastro.

python
@app.route("/home")
def home():
    return render_template("index.html")


A página "index.html" contém o formulário para cadastro de clientes.

Campos do formulário:

* CPF
* Nome
* Rua
* Cidade
* Estado

O formulário envia os dados para a rota:


/cadastrar


---

*  Etapa 3– Cadastro de Cliente

A rota "/cadastrar" recebe os dados enviados pelo formulário.

python
@app.route("/cadastrar", methods=["POST"])
def cadastrar():


* Processo de cadastro

. Recebe os dados do formulário
. Verifica se todos os campos estão preenchidos
. Cria um objeto cliente
. Salva no banco de dados

Exemplo:

python
novo_cliente = Dados_Cadastrais(
    cpf=cpf,
    nome=nome,
    rua=rua,
    cidade=cidade,
    estado=estado
)


Depois os dados são salvos com:

python
db.session.add(novo_cliente)
db.session.commit()


-------------------

 Como Executar o Projeto

 1. Instalar dependências


pip install flask
pip install flask_sqlalchemy


---

2. Executar o projeto


python app.py


---

* 3 Acessar no navegador

Página de cadastro:


http://127.0.0.1:5000/home


----------------------

* Banco de Dados

O banco "site.db" será criado automaticamente quando o sistema rodar pela primeira vez.

python
with app.app_context():
    db.create_all()

-------------------------

* Autores
Luciano de Oliveira Tavares Filho
Pedro Henrique Gervásio Rodrigues
Júlio César Batista Silva

Projeto desenvolvido para fins de estudo utilizando *Flask + SQLAlchemy.
