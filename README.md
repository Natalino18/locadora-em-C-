Como executar o projeto
1 - Clone o projeto 
2 - Execute no terminal:

<img width="1154" alt="Captura de Tela 2025-06-08 às 14 47 57" src="https://github.com/user-attachments/assets/413eab1f-7a90-44b9-9597-89b20112b6d3" />

Funcionalidades
Desenvolvi um sistema para uma locadora de filmes que utiliza uma pilha para armazenar os filmes escolhidos pelo usuário, seguindo a lógica LIFO (último a entrar, primeiro a sair). Além disso, implementei a funcionalidade de salvar o histórico dessas escolhas em um arquivo .txt. Assim, mesmo que o programa seja fechado, o usuário pode consultar o histórico dos últimos filmes alugados ao reabrir o sistema.
Os filmes ficaram dessa forma:

<img width="1153" alt="Captura de Tela 2025-06-08 às 15 10 26" src="https://github.com/user-attachments/assets/c86519ac-1302-4071-a7a4-4d7675c2486d" />

Desfazendo último aluguel
Como vocês podem ver por essa imagem, o último filme alugado pode ser desfeito facilmente. Essa funcionalidade é possível graças ao uso da estrutura de pilha, que permite remover rapidamente o item que está no topo ou seja, o filme mais recentemente alugado. Dessa forma, caso o usuário mude de ideia ou tenha cometido um erro, ele pode corrigir a ação com apenas um comando, mantendo o controle total sobre sua lista de aluguéis.

<img width="1129" alt="Captura de Tela 2025-06-08 às 15 18 24" src="https://github.com/user-attachments/assets/8c839342-d3ed-4cef-9da7-432f0cb8b1d6" />

Mostrando o histórico de aluguéis

Nesta parte do sistema, é possível visualizar todo o histórico de filmes alugados, exibindo-os do mais recente para o mais antigo. Isso é feito percorrendo a pilha de cima para baixo, mantendo a ordem em que os filmes foram adicionados. Além disso, com a integração do arquivo .txt, esse histórico é salvo automaticamente, permitindo que os dados sejam recuperados mesmo após o fechamento do programa. Além disso, como eu já deixei alguns filmes previamente registrados, é possível observar que o histórico aparece automaticamente ao iniciar o programa. Isso comprova que o arquivo .txt está funcionando corretamente, armazenando os dados mesmo após o encerramento do sistema e permitindo que o histórico seja carregado na próxima execução.

<img width="1150" alt="Captura de Tela 2025-06-08 às 15 28 15" src="https://github.com/user-attachments/assets/8ff9118d-e698-4792-9917-8cd2518da043" />


O codigo 

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 100
#define TAMANHO_TITULO 100
#define ARQUIVO "historico_filmes.txt"

typedef struct {
    char titulos[MAX][TAMANHO_TITULO];
    int topo;
} Pilha;

void inicializar(Pilha *p) {
    p->topo = -1;
}

int cheia(Pilha *p) {
    return p->topo == MAX - 1;
}

int vazia(Pilha *p) {
    return p->topo == -1;
}

void alugarFilme(Pilha *p, char titulo[]) {
    if (cheia(p)) {
        printf("Limite de filmes alugados atingido!\n");
        return;
    }

    p->topo++;
    strncpy(p->titulos[p->topo], titulo, TAMANHO_TITULO);
    printf("Filme '%s' alugado com sucesso.\n", titulo);
}

void desfazerAluguel(Pilha *p) {
    if (vazia(p)) {
        printf("Nenhum aluguel para desfazer.\n");
        return;
    }

    printf("Aluguel desfeito: %s\n", p->titulos[p->topo]);
    p->topo--;
}

void verUltimoFilme(Pilha *p) {
    if (vazia(p)) {
        printf("Nenhum filme alugado ainda.\n");
        return;
    }

    printf("Último filme alugado: %s\n", p->titulos[p->topo]);
}

void mostrarHistorico(Pilha *p) {
    if (vazia(p)) {
        printf("Nenhum histórico de aluguel encontrado.\n");
        return;
    }

    printf("\nHistórico de filmes alugados (mais recente para mais antigo):\n");
    int i = p->topo;
    while (i >= 0) {
        printf("- %s\n", p->titulos[i]);
        i--;
    }
    printf("\n");
}

void salvarHistorico(Pilha *p) {
    FILE *arq = fopen(ARQUIVO, "w");
    if (!arq) {
        printf("Erro ao abrir arquivo para salvar.\n");
        return;
    }

    for (int i = 0; i <= p->topo; i++) {
        fprintf(arq, "%s\n", p->titulos[i]);
    }

    fclose(arq);
}

void carregarHistorico(Pilha *p) {
    FILE *arq = fopen(ARQUIVO, "r");
    if (!arq) {
        return;
    }

    inicializar(p);
    char linha[TAMANHO_TITULO];
    while (fgets(linha, TAMANHO_TITULO, arq)) {
        linha[strcspn(linha, "\n")] = '\0';
        if (!cheia(p)) {
            p->topo++;
            strncpy(p->titulos[p->topo], linha, TAMANHO_TITULO);
        } else {
            break;
        }
    }

    fclose(arq);
}

int main() {
    Pilha alugueis;
    inicializar(&alugueis);
    carregarHistorico(&alugueis);

    int opcao = -1;
    char titulo[TAMANHO_TITULO];

    while (opcao != 0) {
        printf("\n=== MENU FILMES DO TEMPO ===\n");
        printf("1. Alugar filme\n");
        printf("2. Ver último filme alugado\n");
        printf("3. Desfazer último aluguel\n");
        printf("4. Mostrar histórico de aluguéis\n");
        printf("0. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);
        getchar();

        if (opcao == 1) {
            printf("Digite o título do filme: ");
            fgets(titulo, TAMANHO_TITULO, stdin);
            titulo[strcspn(titulo, "\n")] = '\0';
            alugarFilme(&alugueis, titulo);
        } else if (opcao == 2) {
            verUltimoFilme(&alugueis);
        } else if (opcao == 3) {
            desfazerAluguel(&alugueis);
        } else if (opcao == 4) {
            mostrarHistorico(&alugueis);
        } else if (opcao == 0) {
            printf("Encerrando sistema da locadora Filmes do Tempo...\n");
            salvarHistorico(&alugueis);
        } else {
            printf("Opção inválida. Tente novamente.\n");
        }
    }

    return 0;
}



