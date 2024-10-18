import random

print("                      MENU")
print("- "*25)
print("Escolha a opção desejada:")
print("1 - Cadastrar contato")
print("2 - Consultar contato(s)")
print("3 - Remover contato")
print("4 - Sair")


lista_contatos = []
id_global = 3109628

def cadastrar_contato(id):

    while True:
        nome = input("Insira o nome: ")
        if len(nome) > 50:
            print("Nome excedeu a quantidade de caracteres. Abrevie o nome do meio")
        else:
            break
    while True:
        atividade = input("Digite seu ramo de atividade: ")
        if len(atividade) > 50:
            print("Atividade excedeu quantidade máxima de caracteres. Abrevie!")
        else:
            break
    while True:
        telefone = input("Digite seu telefone para contato: ")
        if len(telefone) != 7:
            print("Digite um telefone válido, com 9 números")
        else:
            break
    id = str(random.randint(1000000, 9999999))

    contato = {
        "id": id,
        "nome": nome,
        "atividade": atividade,
        "telefone": telefone
    }
    lista_contatos.append(contato.copy())
    print(f"Contato cadastrado com sucesso! ID cadastrado {id}")

def consultar_contatos():
    while True:
        opcao = input("Qual opcao desejada: 1 - Consultar todos, 2 - Consultar por id, 3 - Consultar por setor, 4 - Retornar ao Menu)")
        if opcao == "1":
            for contato in lista_contatos:
                print(contato)
        elif opcao == "2":
            subopcao = input("Digite o ID desejado: ")
            if len(subopcao) != 7:
                print("ID inválido! Digite um Id com 7 números!")
                return
            for contato in lista_contatos:
                if contato["id"] == subopcao:
                    print(contato)
                else:
                    print("Id nao encontrado!")
                    return
        elif opcao == "3":
            atividade_buscada = input("Digite o ramo de atividade: ")
            contatos_encontrados = [contato for contato in lista_contatos if contato["atividade"] == atividade_buscada]
            if contatos_encontrados:
                for contato in contatos_encontrados:
                    print(contato)
                return

        elif opcao =="4":
            break


def remover_contato():
    while True:
        contato_buscado = input("Digite o ID do contato a ser removido: ")
        if len(contato_buscado) != 7:
            print("ID inválido! Digite o ID com 7 números.")
            return

        removedor = [contato for contato in lista_contatos if contato["id"] == contato_buscado]

        if not removedor:
            print("ID não encontrado! Digite um ID válido: ")
            return
        else:
            lista_contatos.remove(removedor[0])  # Remove apenas o primeiro contato encontrado
            print("Contato removido com sucesso!")
            return

while True:
    opcao = input("Digite a opção do menu: 1 - Cadastrar contato, 2 - Consultar contato, 3 - Remover contato, 4 - Sair: ")
    if opcao == "4":
        break
    elif opcao == "1":
        cadastrar_contato(id)
    elif opcao == "2":
        consultar_contatos()
    elif opcao == "3":
        remover_contato()
