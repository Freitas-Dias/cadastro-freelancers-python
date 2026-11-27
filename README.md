# Aplicação de Cadastro de Freelancers (Versão Beta)

Projeto desenvolvido para a atividade **MAPA** da disciplina **Linguagem de Programação** do curso de **Ciência de Dados e Análise do Comportamento (UniCesumar)**.

## 📋 1. Contextualização e Objetivo

O projeto consiste em uma aplicação de linha de comando (CLI) desenvolvida em Python para o cadastro e a listagem de até **5 freelancers**. Cada registro armazena um código identificador único (`cod`), nome, e-mail, linguagem de programação principal e valor por hora trabalhada.

---

## 💻 2. Código-Fonte Completo e Documentado

O código abaixo apresenta a implementação original completamente documentada com explicações sobre estruturas de dados (`list` e `dict`), funções auxiliares, controle de fluxo e tratamento de entradas (disponível também no arquivo [`mapa.py`](./mapa.py)).

```python
# ==============================================================================
# ATIVIDADE: MAPA - LINGUAGEM DE PROGRAMAÇÃO - 54_2026
# PROJETO: Aplicação de Cadastro de Freelancers (Versão Beta)
# OBJETIVO: Permitir o cadastro (até 5 registros) e a listagem de profissionais
#           utilizando listas, dicionários, funções e estruturas de repetição.
# CURSO: Ciência de Dados e Análise do Comportamento
# UNIVERSIDADE: UniCesumar
# ALUNO: Ricardo Freitas
# ==============================================================================

# 1. ESTRUTURA DE ARMAZENAMENTO GLOBAL
# Cria uma lista vazia que funcionará como o "banco de dados" em memória.
# Cada posição desta lista armazenará um dicionário representando um freelancer.
lista = []

# 2. DEFINIÇÃO DAS FUNÇÕES AUXILIARES

# A função imprime percorre todos os dicionários armazenados na 'lista' e exibe
# os dados formatados de cada freelancer cadastrado.
# O laço 'for' acessa um dicionário por vez dentro da lista.
def imprime():
    for freelancer in lista:
        print("*** Código do freelancer:", freelancer["cod"])
        print("Nome:", freelancer["nome"])
        print("E-mail:", freelancer["email"])
        print("Linguagem:", freelancer["linguagem"])
        print("Preço por hora (R$):", freelancer["valor"])
        print("-----------")

# A função menu exibe o cabeçalho e as opções de navegação disponíveis para o
# usuário. Não recebe parâmetros e não retorna valores; apenas imprime na tela.
def menu():
    print("----------- FREELANCERS - VERSÃO BETA -----------")
    print("1 - Digite 1 para inserir novo cadastro de freelancer;")
    print("2 - Digite 2 para mostrar freelancers cadastrados;")
    print("0 - Digite 0 para encerrar.")

# 3. VARIÁVEIS DE CONTROLE DO FLUXO

# 'cont' gera um identificador único (ID) sequencial iniciando em 0 (0, 1, 2, 3, 4).
cont = 0

# 'op' armazena a escolha do usuário no menu. Inicia com -1 (valor diferente de 0)
# para garantir que o programa entre no laço 'while' pela primeira vez.
op = -1

# 4. LOOP PRINCIPAL DA APLICAÇÃO
# Mantém o programa em execução contínua até que o usuário digite 0 para sair.
while op != 0:
    menu()             # Chama a função que desenha o menu na tela
    op = int(input())  # Lê a opção digitada e converte de texto (str) para inteiro

    # --- OPÇÃO 1: CADASTRAR NOVO FREELANCER ---
    if op == 1:
        if len(lista) < 5:   # Verifica se a lista ainda tem menos de 5 cadastros
            freelancer = {}  # Cria um dicionário vazio p/ agrupar os dados do novo cadastro

            # Preenche as chaves do dicionário com o ID automático e as entradas do usuário
            freelancer["cod"] = cont
            freelancer["nome"] = input("Insira o nome do freelancer:\n")
            freelancer["email"] = input("Insira o e-mail do freelancer:\n")
            freelancer["linguagem"] = input("Insira principal linguagem de programação do freelancer:\n")
            # Converte o texto p/ número decimal (float), exigindo ponto (ex: 120.00)
            freelancer["valor"] = float(input("Insira preço do freelancer por hora trabalhada:\n"))

            # Adiciona o dicionário preenchido ao final da lista principal
            lista.append(freelancer)
            # Incrementa o contador para que o próximo freelancer receba o próximo código
            cont += 1

        # Caso len(lista) já seja igual a 5, impede novos cadastros
        else:
            print("Lista de freelancers lotada!")
        # Pausa a execução para o usuário ler o resultado antes de reexibir o menu
        input("Pressione Enter para continuar...")

    # --- OPÇÃO 2: LISTAR FREELANCERS CADASTRADOS ---
    elif op == 2:
        # 'if not lista:' verifica se a lista está vazia (equivale a len(lista) == 0)
        if not lista:
            print("Lista de freelancers vazia!")
        else:
            # Se houver pelo menos 1 cadastro, chama a função de exibição
            imprime()
        input("Pressione Enter para continuar...")

    # --- VALIDAÇÃO DE OPÇÃO INVÁLIDA ---
    # Se 'op' não for 1, nem 2 e nem 0, informa que o comando não existe
    elif op != 0:
        print("Erro: opção inválida!")
        input("Pressione Enter para continuar...")
