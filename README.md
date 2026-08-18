# linguagem.c
atividade em linguagem C (cadastrando produtos e valores)

//atividade em linguagem C (cadastrando produtos e valores)


#include <stdio.h>
#include <string.h>

#define MAX_PRODUTOS 100

// Estrutura do produto
struct Produto {
    int codigo;
    char nome[50];
    float preco;
    int estoque;
};

int main() {
    struct Produto produtos[MAX_PRODUTOS];

    int quantidadeProdutos = 0;
    int opcao;

    do {
        printf("\n===== SISTEMA DE ESTOQUE =====\n");
        printf("1 - Cadastrar produto\n");
        printf("2 - Consultar produto\n");
        printf("3 - Atualizar estoque\n");
        printf("4 - Listar produtos\n");
        printf("5 - Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {

            // CADASTRAR
            case 1:
                if (quantidadeProdutos >= MAX_PRODUTOS) {
                    printf("\nLimite de produtos atingido!\n");
                    break;
                }

                printf("\n===== CADASTRO DE PRODUTO =====\n");

                printf("Codigo: ");
                scanf("%d", &produtos[quantidadeProdutos].codigo);

                printf("Nome: ");
                scanf(" %[^\n]", produtos[quantidadeProdutos].nome);

                printf("Preco unitario: R$ ");
                scanf("%f", &produtos[quantidadeProdutos].preco);

                printf("Quantidade em estoque: ");
                scanf("%d", &produtos[quantidadeProdutos].estoque);

                quantidadeProdutos++;

                printf("\nProduto cadastrado com sucesso!\n");
                break;

            // CONSULTAR
            case 2: {
                int codigo;
                int encontrado = 0;

                printf("\n===== CONSULTA DE PRODUTO =====\n");
                printf("Digite o codigo do produto: ");
                scanf("%d", &codigo);

                for (int i = 0; i < quantidadeProdutos; i++) {

                    if (produtos[i].codigo == codigo) {

                        printf("\nProduto encontrado!\n");
                        printf("Codigo: %d\n", produtos[i].codigo);
                        printf("Nome: %s\n", produtos[i].nome);
                        printf("Preco: R$ %.2f\n", produtos[i].preco);
                        printf("Estoque: %d unidades\n",
                               produtos[i].estoque);

                        encontrado = 1;
                        break;
                    }
                }

                if (!encontrado) {
                    printf("\nProduto nao encontrado!\n");
                }

                break;
            }

            // ATUALIZAR ESTOQUE
            case 3: {
                int codigo;
                int tipo;
                int quantidade;
                int encontrado = 0;

                printf("\n===== ATUALIZACAO DE ESTOQUE =====\n");

                printf("Digite o codigo do produto: ");
                scanf("%d", &codigo);

                for (int i = 0; i < quantidadeProdutos; i++) {

                    if (produtos[i].codigo == codigo) {

                        encontrado = 1;

                        printf("\nProduto: %s\n",
                               produtos[i].nome);
                        printf("Estoque atual: %d\n",
                               produtos[i].estoque);

                        printf("\n1 - Entrada de produtos\n");
                        printf("2 - Saida de produtos\n");
                        printf("Escolha: ");
                        scanf("%d", &tipo);

                        printf("Quantidade: ");
                        scanf("%d", &quantidade);

                        if (quantidade <= 0) {
                            printf("\nQuantidade invalida!\n");
                        }
                        else if (tipo == 1) {

                            produtos[i].estoque += quantidade;

                            printf("\nEntrada realizada com sucesso!\n");
                            printf("Novo estoque: %d\n",
                                   produtos[i].estoque);
                        }
                        else if (tipo == 2) {

                            if (quantidade > produtos[i].estoque) {
                                printf("\nErro: estoque insuficiente!\n");
                            }
                            else {
                                produtos[i].estoque -= quantidade;

                                printf("\nSaida realizada com sucesso!\n");
                                printf("Novo estoque: %d\n",
                                       produtos[i].estoque);
                            }
                        }
                        else {
                            printf("\nOpcao invalida!\n");
                        }

                        break;
                    }
                }

                if (!encontrado) {
                    printf("\nProduto nao encontrado!\n");
                }

                break;
            }

            // LISTAR
            case 4:

                printf("\n===== LISTA DE PRODUTOS =====\n");

                if (quantidadeProdutos == 0) {
                    printf("Nenhum produto cadastrado.\n");
                }
                else {

                    for (int i = 0; i < quantidadeProdutos; i++) {

                        printf("\nProduto %d\n", i + 1);
                        printf("Codigo: %d\n",
                               produtos[i].codigo);
                        printf("Nome: %s\n",
                               produtos[i].nome);
                        printf("Preco: R$ %.2f\n",
                               produtos[i].preco);
                        printf("Estoque: %d unidades\n",
                               produtos[i].estoque);
                    }
                }

                break;

            // SAIR
            case 5:
                printf("\nEncerrando o programa...\n");
                break;

            default:
                printf("\nOpcao invalida! Tente novamente.\n");
        }

    } while (opcao != 5);

    return 0;
