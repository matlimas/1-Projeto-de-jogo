#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define NUM_CAIXAS 5
#define NUM_JOGADORES 2

char *nomes[] = {"Neymar", "Cristiano", "Jaderson", "Kadu", "Eduardo", "Vinicius", "Raphinha"};

void perguntaEResposta() {
    char resposta;
    int acertos = 0;
    
    const char* pergunta[5] = {
        "Qual time de futebol tem mais titulos no mundo? \n(a)Barcelona \n(b)Clube do Remo \n(c)Real Madrid \n(d)Paysandu \nResposta: ",
        "Quem foi considerada a Redentora do Brasil? \n(a) Princesa Isabel \n(b) Maria da Penha \n(c)Marta \n(d)Tarsila do Amaral \nResposta: ",
        "Quem e o homem de ferro? \n(a)Bruce Wayne \n(b)Tony Stark \n(c)Steve Rogers \n(d)Bruce Banner \nResposta: ",
        "Quanto e 1+1? \n(a)4 \n(b)2 \n(c)3 \n(d)5 \nResposta: ",
        "Quanto e 6*6? \n(a)22 \n(b)24 \n(c)12 \n(d)36 \nResposta: "
    };
    
    const char respostasCorretas[5] = {'c', 'a', 'b', 'b', 'd'};
    const char* respostasCorretasTexto[5] = {
        "Real Madrid", "Princesa Isabel", "Tony Stark", "2", "36"
    };
    
    for(int i = 0; i < 5; i++) {
        printf("%s", pergunta[i]);
        scanf(" %c", &resposta);
        
        if(resposta == respostasCorretas[i]) {
            printf("Resposta correta. \n");
            acertos++;
        } else {
            printf("Resposta incorreta. A resposta correta e: %s\n", respostasCorretasTexto[i]);
        }
    }
    
    printf("Voce acertou %d de 5 perguntas!\n", acertos);
    
    char jogarNovamente;
    printf("Quer jogar novamente? (s/n):");
    scanf(" %c", &jogarNovamente);
    if(jogarNovamente == 's' || jogarNovamente == 'S') {
        perguntaEResposta();
    } else {
        printf("Voltando ao menu principal...\n");
    }
}

void cobraNaCaixa() {
    int cobra, botao, escolha, jogador;
    srand(time(NULL));
    
    printf("Escolha dois jogadores (1-7): ");
    int p1, p2;
    scanf("%d %d", &p1, &p2);
    p1--;
    p2--;
    char *jogadores[] = {nomes[p1], nomes[p2]};
    
    jogador = rand() % NUM_JOGADORES;
    printf("%s comeca o jogo!\n", jogadores[jogador]);
    
    cobra = rand() % NUM_CAIXAS;
    botao = rand() % NUM_CAIXAS;
    while (botao == cobra) botao = rand() % NUM_CAIXAS;
    
    while (1) {
        printf("%s, escolha uma caixa (1-%d): ", jogadores[jogador], NUM_CAIXAS);
        scanf("%d", &escolha);
        
        if (escolha - 1 == cobra) {
            printf("Voce encontrou a cobra! %s perdeu!\n", jogadores[jogador]);
            break;
        } else if (escolha - 1 == botao) {
            printf("Voce encontrou o botao! %s venceu!\n", jogadores[jogador]);
            break;
        }
        printf("Caixa vazia! Proximo jogador.\n");
        jogador = (jogador + 1) % NUM_JOGADORES;
    }
    char jogarNovamente;
    printf("Quer jogar novamente? (s/n):");
    scanf(" %c", &jogarNovamente);
    if(jogarNovamente == 's' || jogarNovamente == 'S') {
        cobraNaCaixa();
    } else {
        printf("Voltando ao menu principal...\n");
    }
}

void exibirMenu() {
    printf("Menu Principal \n");
    printf("1. Pergunta e Resposta\n");
    printf("2. Cobra na Caixa!\n");
    printf("3. Sair\n");
    printf("Escolha um jogo: ");
}

int main() {
    int escolha;
    do {
        exibirMenu();
        scanf("%d", &escolha);
        
        switch (escolha) {
            case 1:
                perguntaEResposta();
                break;
            case 2:
                cobraNaCaixa();
                break;
            case 3:
                printf("Saindo do programa...\n");
                break;
            default:
                printf("Opcao invalida. Tente novamente.\n");
        }
    } while (escolha != 3);
    
    return 0;
}
