# Misterio-no-museu

# Variaveis globais
ContagemDeTentativas = 0
OpcaoDeEntradaEscolhida = "nenhuma"

# Sub programas
# Histórias e mensagens
def story():
    print("Você vê um cofre em uma sala escura parcialmente bloqueado por uma viga...\n")

# Subtrai as tentativas
def sub(x):
    newValue = x - 1
    print("Senha incorreta.\nTentativas restantes: %d" % (newValue))
    return newValue

# Continuar o jogo
def continuarJogo():
    opcaoDeContinuar = input("\nGame over\n\nDeseja jogar novamente? (SIM - NAO): ")
    if opcaoDeContinuar == "SIM":
        return 1
    else:
        return 0

# Verifica se o numero eh float
def isfloat(x):
    verificacao = 0
    if "." in x:
        length = len(x)
        for i in range(length):
            if x[i] == ".":
                continue
            elif str.isdigit(x[i]) == 0 and i == 0:
                verificacao = 0
                break
            elif str.isdigit(x[i]) == 1:
                verificacao = 1
            else:
                verificacao = 0

    if verificacao == 1:
        return 1
    else:
        return 0

# Função com o desafio da opção frente
def DesafioFrente(A,B,C):
    if 294 % A == 0 and 294 / A == B and B / A == C:
                return 1
    else:
        return 0

# Função com desafio da opção servico
def desafioServico(A,B):
    if A % B == 0 and B % 2 != 0 and A + B > 50:
        return 1
    else:
        return 0

# Função com o desafio da opção telhado
def desafioTelhado(X,Y,Z):
    if X + Y > Z and X + Z > Y and Y + Z > X:
        return 1
    else:
        return 0

# Opção frente
def Frente():

    tentativas = 3
    controlEntradaValores = 1
    while controlEntradaValores:
        valoresDigitados = input("\nDigite três números, sendo dois inteiros e um decimal.\nResposta: ").split()

        # Verifica se o usuario digitou a quantidade certa de numeros e se são digitos
        if len(valoresDigitados) != 3:
            print("Entradas insuficientes.")

        # Verifica se os numeros estão requerida
        elif str.isdigit(valoresDigitados[0]) == 1 and str.isdigit(valoresDigitados[1]) == 1 and isfloat(valoresDigitados[2]) == 1:
            A = int(valoresDigitados[0])
            B = int(valoresDigitados[1])
            C = float(valoresDigitados[2])

            if DesafioFrente(A, B, C) == 1:
                global ContagemDeTentativas
                ContagemDeTentativas = tentativas
                return 1
            else:
                tentativas = sub(tentativas)
                if tentativas == 0:
                    return 0
        else:
            print("Entrada inválida! Use o formato: número_inteiro número_inteiro número_decimal")

# Opção serviço
def servico():

    tentativas = 3
    controlEntradaValores = 1
    while controlEntradaValores:
        valoresDigitados = input("\nDigite dois números inteiros.\nResposta: ").split()

        # Verifica se o usuario digitou a quantidade certa de numeros
        if len(valoresDigitados) != 2:
                print("Entradas insuficientes.")

        # Verifica se os numeros digitados são inteiros
        elif str.isdigit(valoresDigitados[0]) == 1 and str.isdigit(valoresDigitados[1]) == 1:
            A = int(valoresDigitados[0])
            B = int(valoresDigitados[1])
            if desafioServico(A,B) == 1:
                global ContagemDeTentativas
                ContagemDeTentativas = tentativas
                return 1
            else:
                tentativas = sub(tentativas)
                if tentativas == 0:
                    return 0
        else:
            print("Entrada inválida! Use o formato: número_inteiro número_inteiro")

# Opção telhado
def telhado():

    tentativas = 3
    controlEntradaValores = 1
    while controlEntradaValores:
        valoresDigitados = input("\nDigite três números decimais.\nResposta: ").split()

        # Verifica se o usuario digitou a quantidade certa de numeros
        if len(valoresDigitados) != 3:
            print("Entradas insuficientes.")

        # Verifica se os valores são decimais e se são diferentes
        elif isfloat(valoresDigitados[0]) == 1 and isfloat(valoresDigitados[1]) == 1 and isfloat(valoresDigitados[2]) == 1:
            if valoresDigitados[0] != valoresDigitados[1] or valoresDigitados[0] != valoresDigitados[2] or valoresDigitados[1] != valoresDigitados[2]:
                X = float(valoresDigitados[0])
                Y = float(valoresDigitados[1])
                Z = float(valoresDigitados[2])
                if desafioTelhado(X,Y,Z) == 1:
                    global ContagemDeTentativas
                    ContagemDeTentativas = tentativas
                    return 1
                else:
                    tentativas = sub(tentativas)
                    if tentativas == 0:
                        return 0
            else:
                tentativas = sub(tentativas)
                if tentativas == 0:
                    return 0
        else:
            print("Entrada inválida! Use o formato: número_float número_float número_float")

# Função referente a segunda etapa
def segundaEtapa():

    print("Você pode escolher dois itens desde que sejam diferentes.")
    controlLoop = 1
    while controlLoop:
        ItensEscolhidos = input("Itens disponíveis: (lanterna, chave e corda).\nEscolhas: ").split()

        # Verifica se o usuario digitou a quantidade certa de numeros
        if len(ItensEscolhidos) != 2:
            print("Itens insuficientes.")
        else:
            # Verifica se os itens eh um dos disponíveis
            verific = 0
            for i in range(len(ItensEscolhidos)):
                if ItensEscolhidos[i] in ["lanterna", "chave", "corda"]:
                    verific = 1
                else:
                    print("Item(ns) errado(s)")
                    verific = 0
                    break
            if verific == 1 and ItensEscolhidos[0] != ItensEscolhidos[1]:

                # Verifica se o jogador escolheu a combinação certa de itens de acordo com a entrada escolhida
                if OpcaoDeEntradaEscolhida == "frente":
                    checkItensFrente = 0
                    for i in range(len(ItensEscolhidos)):
                        if ItensEscolhidos[i] in ["lanterna", "chave"]:
                            checkItensFrente = 1
                        else:
                            checkItensFrente = 0
                            break
                    if checkItensFrente == 1:
                        return 1
                    else:
                        return 0
                elif OpcaoDeEntradaEscolhida == "servico":
                    checkItensServico = 0
                    for i in range(len(ItensEscolhidos)):
                        if ItensEscolhidos[i] in ["chave", "corda"]:
                            checkItensServico = 1
                        else:
                            checkItensServico = 0
                            break
                    if checkItensServico == 1:
                        return 1
                    else:
                        return 0
                elif OpcaoDeEntradaEscolhida == "telhado":
                    checkItensTelhado = 0
                    for i in range(len(ItensEscolhidos)):
                        if ItensEscolhidos[i] in ["lanterna", "corda"]:
                            checkItensTelhado = 1
                        else:
                            checkItensTelhado = 0
                            break
                    if checkItensTelhado == 1:
                        return 1
                    else:
                        return 0


# Função principal
def main():

    control = 1
    while control:
        print("\nMistério no Museu\n")

        # Verifica se a entrada escolhida pelo jogador eh uma das disponiveis.
        controlEntrada = 1
        while controlEntrada:
            entrada = input("Escolha uma forma de entrada no museu: (frente, servico ou telhado).\nEscolha: ")
            if entrada in ["frente", "servico", "telhado"]:
                global OpcaoDeEntradaEscolhida
                OpcaoDeEntradaEscolhida = entrada
                controlEntrada = 0

        # Primeira opção de entrada no museu (frente)
        if entrada == "frente":
            if Frente() == 1:
                print("\nPrimeira etapa concluida\n")
                story()
                if segundaEtapa() == 1:
                    if ContagemDeTentativas == 3:
                        print("\nExcelente supremo")
                        control = continuarJogo()
                    elif ContagemDeTentativas == 2:
                        print("\nExcelente")
                        control = continuarJogo()
                    elif ContagemDeTentativas == 1:
                        print("\nNeutro")
                        control = continuarJogo()
                else:
                    print("\nVocê fez barulho demais...\nFinal ruim")
                    control = continuarJogo()

            else:
                control = continuarJogo()

        # Segunda opção de entrada no museu (servico)
        elif entrada == "servico":
            if servico() == 1:
                print("\nPrimeira etapa concluida\n")
                story()
                if segundaEtapa() == 1:
                    if ContagemDeTentativas == 3:
                        print("\nPerfeito supremo")
                        control = continuarJogo()
                    elif ContagemDeTentativas == 2:
                        print("\nPerfeito")
                        control = continuarJogo()
                    elif ContagemDeTentativas == 1:
                        print("\nNeutro")
                        control = continuarJogo()
                else:
                    print("\nVocê fez barulho demais...\nFinal ruim")
                    control = continuarJogo()

            else:
                control = continuarJogo()

        # Terceira opção de entrada no museu (telhado)
        elif entrada == "telhado":
            if telhado() == 1:
                print("\nPrimeira etapa concluida\n")
                story()
                if segundaEtapa() == 1:
                    if ContagemDeTentativas == 3:
                        print("\nNinja supremo")
                        control = continuarJogo()
                    elif ContagemDeTentativas == 2:
                        print("\nNinja")
                        control = continuarJogo()
                    elif ContagemDeTentativas == 1:
                        print("\nNeutro")
                        control = continuarJogo()
                else:
                    print("\nVocê fez barulho demais...\nFinal ruim")
                    control = continuarJogo()
            else:
                control = continuarJogo()

# Programa completo
main()



