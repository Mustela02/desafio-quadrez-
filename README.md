# quadrez.py

def criar_tabuleiro():
    return [[' ' for _ in range(8)] for _ in range(8)]

def exibir_tabuleiro(tab):
    print("  " + " ".join(str(i) for i in range(8)))
    for i, linha in enumerate(tab):
        print(str(i) + " " + " ".join(linha))

def mover_torre(tab, origem, destino):
    lo, co = origem
    ld, cd = destino
    if lo == ld or co == cd:
        tab[ld][cd] = 'T'
        tab[lo][co] = ' '
        return True
    return False

def mover_cavalo(tab, origem, destino):
    lo, co = origem
    ld, cd = destino
    dx = abs(ld - lo)
    dy = abs(cd - co)
    if (dx, dy) in [(2, 1), (1, 2)]:
        tab[ld][cd] = 'C'
        tab[lo][co] = ' '
        return True
    return False

def main():
    tabuleiro = criar_tabuleiro()
    tabuleiro[0][0] = 'T'  # Torre inicial
    tabuleiro[7][1] = 'C'  # Cavalo inicial

    while True:
        exibir_tabuleiro(tabuleiro)
        print("\n1. Mover Torre")
        print("2. Mover Cavalo")
        print("3. Sair")
        opcao = input("Escolha uma opção: ")

        if opcao == '1':
            origem = tuple(map(int, input("Origem (linha coluna): ").split()))
            destino = tuple(map(int, input("Destino (linha coluna): ").split()))
            if not mover_torre(tabuleiro, origem, destino):
                print("Movimento inválido para a torre!")
        elif opcao == '2':
            origem = tuple(map(int, input("Origem (linha coluna): ").split()))
            destino = tuple(map(int, input("Destino (linha coluna): ").split()))
            if not mover_cavalo(tabuleiro, origem, destino):
                print("Movimento inválido para o cavalo!")
        elif opcao == '3':
            print("Jogo encerrado.")
            break
        else:
            print("Opção inválida.")

if __name__ == "__main__":
    main()
