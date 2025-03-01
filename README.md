# projeto-3
import random

class BatalhaNaval:
    def __init__(self, tamanho=5):
        self.tamanho = tamanho
        self.tabuleiro = [['~' for _ in range(tamanho)] for _ in range(tamanho)]
        self.navios = []
        self.colocar_navios()
    
    def colocar_navios(self, quantidade=3):
        """Posiciona os navios aleatoriamente no tabuleiro"""
        while len(self.navios) < quantidade:
            x, y = random.randint(0, self.tamanho - 1), random.randint(0, self.tamanho - 1)
            if (x, y) not in self.navios:
                self.navios.append((x, y))
    
    def mostrar_tabuleiro(self, revelar=False):
        """Exibe o tabuleiro, ocultando os navios caso revelar=False"""
        for i in range(self.tamanho):
            linha = ''
            for j in range(self.tamanho):
                if (i, j) in self.navios and revelar:
                    linha += 'N '
                else:
                    linha += f'{self.tabuleiro[i][j]} '
            print(linha)
        print()
    
    def atirar(self, x, y):
        """Realiza um ataque na posição escolhida"""
        if (x, y) in self.navios:
            print("🔥 Acertou um navio!")
            self.tabuleiro[x][y] = 'X'
            self.navios.remove((x, y))
        else:
            print("💦 Errou!")
            self.tabuleiro[x][y] = 'O'
    
    def jogo_terminou(self):
        """Verifica se todos os navios foram destruídos"""
        return len(self.navios) == 0

# Exemplo de uso
jogo = BatalhaNaval()

print("Bem-vindo ao Batalha Naval!")
while not jogo.jogo_terminou():
    jogo.mostrar_tabuleiro()
    try:
        x = int(input("Informe a linha: "))
        y = int(input("Informe a coluna: "))
        if 0 <= x < jogo.tamanho and 0 <= y < jogo.tamanho:
            jogo.atirar(x, y)
        else:
            print("Coordenadas fora do tabuleiro!")
    except ValueError:
        print("Entrada inválida! Digite números inteiros.")

print("🎉 Parabéns! Você destruiu todos os navios!")
jogo.mostrar_tabuleiro(revelar=True)
