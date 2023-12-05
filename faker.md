# Criando Dados Fictícios com a Biblioteca Faker em Python

<div align='justify'>
  
## Introdução
No projeto a seguir, exploraremos como criar dados fictícios de clientes, produtos e vendas usando a biblioteca Faker em Python. Essa prática é útil para desenvolver conjuntos de dados para análise exploratória, testes e simulações.

## Instalando a Biblioteca
Antes de começar, certifique-se de instalar a biblioteca Faker utilizando o seguinte comando:

```
!pip install Faker
from faker import Faker
import random

fake = Faker()
```

## Gerando Dados de Clientes
Vamos começar criando dados fictícios para clientes. A função gerar_fake_cliente utiliza métodos da biblioteca Faker para gerar nomes, telefones, idades, gêneros, e localizações fictícias. Vamos destacar os principais pontos dessa função:
```
def gerar_fake_cliente():
    nome = fake.name()
    telefone = fake.phone_number()
    idade = fake.random_int(min=18, max=90)
    # ...
    genero = fake.random_element(elements=('M', 'F', 'F'))
    localizacao = fake.random_element(elements=('Belo Horizonte', 'Rio de Janeiro', 'São Paulo', 'Salvador', 'Curitiba'))
    # ...
    return id_cliente_atual, nome, idade, genero, telefone, localizacao
```
Note que usamos fake.random_element para escolher aleatoriamente gêneros e localizações. A função também lida com a idade, garantindo que, se a idade for superior a 65, há uma chance de reduzi-la, tornando os dados mais realistas.

## Gerando Dados de Produtos
A próxima etapa é criar dados fictícios para produtos. A função gerar_fake_produto gera tipos, categorias, tamanhos e preços fictícios. Destacamos a geração do preço:
```
def gerar_fake_produto():
    # ...
    preco_produto = fake.random_int(min=49, max=300, step=3)
    # ...
    return id_produto_atual, tipo_produto, categoria_produto, tamanho_produto, preco_produto
```
Aqui, usamos fake.random_int para gerar preços no intervalo desejado.

## Gerando Dados de Vendas
Finalmente, vamos gerar dados fictícios para vendas. A função gerar_fake_venda cria datas, quantidades e valores fictícios. Destacamos a geração da quantidade:

```
def gerar_fake_venda(id_cliente, id_produto):
    # ...
    quantidade = random.randint(1, 10)
    if quantidade and random.random() > 0.80:
        quantidade = random.randint(1, 5)
    # ...
    return id_cliente, id_produto, quantidade, date_venda.strftime('%d-%m-%Y')
```
A função ajusta aleatoriamente a quantidade vendida, tornando alguns valores mais prováveis do que outros.

## Criando Arquivos CSV
Finalmente, o código cria arquivos CSV contendo os dados gerados para clientes, produtos e vendas.
#### Clientes
```
with open('dados_clientes.csv','w',newline='') as csvfile_cliente:
  writer_cliente = csv.writer(csvfile_cliente)
  writer_cliente.writerow(['id_cliente', 'nome', 'idade', 'genero', 'telefone', 'localizacao'])
  for _ in range(3000):
    clientes = gerar_fake_cliente()
    writer_cliente.writerow(clientes)

print("Arquivo 'dados_cliente.csv' gerado com sucesso.")
```
#### Produtos
```
with open('dados_produtos.csv','w',newline='') as csvfile_produto:
  writer_produto = csv.writer(csvfile_produto)
  writer_produto.writerow(['id_produto', 'tipo_produto', 'categoria_produto', 'tamanho_produto', 'preco_produto'])
  for _ in range(500):
    produtos = gerar_fake_produto()
    writer_produto.writerow(produtos)

print("Arquivo 'dados_produtos.csv' gerado com sucesso.")
```  

#### Vendas

```    
with open('dados_vendas.csv','w',newline='') as csvfile_vendas:
  writer_pedido = csv.writer(csvfile_vendas)
  writer_pedido.writerow(['id_cliente', 'id_produto', 'quantidade_vendida', 'valor_venda'])
  for _ in range(5000):
    id_cliente_atual = fake.random_int(min=1, max=3000)
    id_produto_atual = fake.random_int(min=1, max=500)
    vendas = gerar_fake_venda(id_cliente_atual, id_produto_atual)
    writer_pedido.writerow(vendas)

print("Arquivo 'dados_vendas.csv' gerado com sucesso.")"
```
## Conclusão
Neste projeto, exploramos a geração de dados fictícios usando a biblioteca Faker em Python. As funções criadas demonstram como gerar dados realistas e variados para análise exploratória. Este projeto é uma ótima oportunidade para praticar habilidades em Python, além de proporcionar a experiência valiosa de trabalhar com conjuntos de dados fictícios.

</div>

##

> [!NOTE]
> Você pode acessar o código completo [aqui](fake_data.ipynb)
