# Login & menu
O código a seguir foi desenvolvido por mim com o objetivo de criar uma interace de login para determinar entre o menu de colaborador e o menu de administrador.

This code was projected by me to create a login interface to alternate between colaborator's and administrator's menu.

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void limparTela()
{
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif
}

int main()
{
    int op, cargo, cargoarq, op2;
    char senha[50], nome[50], senhaconf[50], nomearq[50], senhaarq[50];
    FILE *arqlogin;

    do
    {
        limparTela();
        printf("----REGISTRO----");
        printf("\n1- Cadastro;");
        printf("\n2- Login;");
        printf("\n0- Sair.");
        printf("\n\nEscolha uma opcao: ");
        scanf("%d", &op);
        getchar();

        switch (op)
        {
        case 0:
            printf("Saindo...\n");
            return 0;

        case 1:
            limparTela();
            printf("----CADASTRO----\n");

            do
            {
                limparTela();
                printf("Escolha o cargo:\n");
                printf("1- Colaborador;\n");
                printf("2- Admin.\n");
                printf("\nDigite sua escolha: ");
                scanf("%d", &cargo);
                getchar();

                if (cargo != 1 && cargo != 2)
                {
                    limparTela();
                    printf("Opcao invalida.\n\n");
                    printf("Pressione Enter para tentar novamente...");
                    getchar();
                }
            }
            while (cargo != 1 && cargo != 2);

            do
            {
                limparTela();
                printf("----CADASTRO----\n");

                printf("Digite seu nome de usuario: ");
                fgets(nome, sizeof(nome), stdin);
                nome[strcspn(nome, "\n")] = '\0';

                printf("Digite sua senha: ");
                fgets(senha, sizeof(senha), stdin);
                senha[strcspn(senha, "\n")] = '\0';

                printf("Confirme sua senha: ");
                fgets(senhaconf, sizeof(senhaconf), stdin);
                senhaconf[strcspn(senhaconf, "\n")] = '\0';

                if (strcmp(senha, senhaconf) != 0)
                {
                    limparTela();
                    printf("As senhas nao coincidem.\n\n");
                    printf("Pressione Enter para tentar novamente...");
                    getchar();
                }
            }
            while (strcmp(senha, senhaconf) != 0);

            arqlogin = fopen("dados.txt", "a");
            if (arqlogin == NULL)
            {
                printf("Erro ao abrir o arquivo.\n");
                return 1;
            }

            fprintf(arqlogin, "%s,%s,%d\n", nome, senha, cargo);
            fclose(arqlogin);

            printf("Cadastro realizado com sucesso!\n");
            break;

        case 2:
            arqlogin = fopen("dados.txt", "r");
            if (arqlogin == NULL)
            {
                limparTela();
                printf("Erro ao abrir o arquivo. Talvez você precise se cadastrar primeiro.\n\n");
                printf("Pressione ENTER para tentar novamente...");
                getchar();
                break;
            }

            int login_success = 0;

            do
            {
                int login_success = 0;
                limparTela();
                printf("----LOGIN----\n");

                printf("Digite seu nome de usuário: ");
                fgets(nome, sizeof(nome), stdin);
                nome[strcspn(nome, "\n")] = '\0';
                fflush(stdin);

                printf("Digite sua senha: ");
                fgets(senha, sizeof(senha), stdin);
                senha[strcspn(senha, "\n")] = '\0';
                fflush(stdin);

                while (fscanf(arqlogin, "%49[^,],%49[^,],%d\n", nomearq, senhaarq, &cargoarq) != EOF)
                {
                    if (strcmp(nome, nomearq) == 0 && strcmp(senha, senhaarq) == 0)
                    {
                        login_success = 1;
                        break;
                    }
                }

                if (login_success == 1)
                {
                    do
                    {
                        limparTela();
                        printf("Logado como: %s (%s)\n\n", nomearq, (cargoarq == 1) ? "Colaborador" : "Administrador");
                        printf("---MENU---\n");
                        printf("1- Cadastro de lotes\n");
                        printf("2- Listagem de lotes\n");
                        printf("3- Salvar dados de lotes\n");
                        printf("4- Listar tarefas\n");
                        if (cargoarq == 2) {
                            printf("5- Criar nova tarefa\n");
                            printf("6- Exibir ICA (Índice de Conversão Alimentar)\n");
                            printf("7- Média de Lucro\n");
                            printf("8- Testar Peso Ideal para Venda\n");
                        }
                        printf("0- Deslogar/Sair\n\n");

                        printf("Selecione uma opção: ");
                        scanf("%d", &op2);
                        getchar();

                        switch (op2)
                        {
                        case 1:
                            cadastrarLote(animais, &quantidadeAnimais);
                            getchar();
                            break;
                        case 2:
                            listarLotes(animais, quantidadeAnimais);
                            getchar();
                            break;
                        case 3:
                            salvarDados(animais, quantidadeAnimais);
                            getchar();
                            break;
                        case 4:
                            listarTarefas();
                            getchar();
                            break;
                        case 5:
                            if (cargoarq == 2) {
                                criarTarefa();
                                getchar();
                            }
                            break;
                        case 6:
                            if (cargoarq == 2) {
                                printf("Índice de Conversão Alimentar (ICA): %.2f\n",
                                       ICA(gastoTotalRacao, ganhoTotal));
                                getchar();
                            }
                            break;
                        case 7:
                            if (cargoarq == 2) {
                                printf("Média de Lucro: %.2f\n",
                                       mediaLucro(ganhoTotal, gastoTotalRacao));
                                getchar();
                            }
                            break;
                        case 8:
                            if (cargoarq == 2) {
                                float peso, custo, preco;
                                printf("Digite o peso atual (kg): ");
                                scanf("%f", &peso);
                                printf("Digite o custo por kg: ");
                                scanf("%f", &custo);
                                printf("Digite o preço de venda por kg: ");
                                scanf("%f", &preco);
                                if (testePesoIdeal(peso, custo, preco) == 0) {
                                    printf("Peso ideal para venda.\n");
                                } else {
                                    printf("Peso insuficiente para venda.\n");
                                }
                                getchar();
                            }
                            break;
                        case 0:
                            printf("Deslogando...\n");
                            break;
                        default:
                            limparTela();
                            printf("Opção inválida! Tente novamente.\n\n");
                            printf("Pressione ENTER para tentar novamente.");
                            getchar();
                        }
                    } while (op2 != 0);
                }
                else
                {
                    limparTela();
                    printf("Usuário ou senha incorretos.\n\n");
                    printf("Pressione Enter para tentar novamente...");
                    getchar();
                }
            } while (login_success != 1);

            fclose(arqlogin);

            break;
        default:
            limparTela();
            printf("Opcao invalida.\n");
            printf("\nPressione Enter para tentar novamente...");
            getchar();
            break;
        }
    }
    while (op != 0);

    return 0;
}
```

Para maior aprofundamento sobre cada opção dos menus, verifique os outros arquivos.

To learn more about each option of the menu, please take a look on the other archives.
