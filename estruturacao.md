# Estruturação do código
Código final estruturado pelo [Paulo Otávio](https://github.com/Paulo-if).
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <locale.h>
#include "cadastrodelotes.h"  // Certifique-se de incluir a header corretamente
#include "listartarefas.h"
#include "criartarefas.h"
#include "funcoesAP2.h"
#include "cadastroRacao.h"


#define MAX_ANIMAIS 100
#define MAX_TAREFA 256

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

    setlocale(LC_ALL, "Portuguese");

    int op, cargo, cargoarq, op2, ub, voltarMenu;
    char senha[50], nome[50], senhaconf[50], nomearq[50], senhaarq[50];
    FILE *arqlogin;

    Animal animais[MAX_ANIMAIS];  // Declarando a variável animais
    int quantidadeAnimais = 0;  // Inicializando a quantidade de animais
    float ganhoTotal = 0.0, gastoTotalRacao = 0;
    int numeroDeVendas = 0, quantidadeDeComprasDeRacao = 0;

    do
    {
        limparTela();
        printf("                ##++      ..##..                mmmmmmmm            mmmm                            \n");
        printf("            ++--                ##            mmmm  ::mm            mm++                            \n");
        printf("          @@  ####          ++##..##        --mm        --mm    mm  mmmmmmmm++  mmmmmm--++mmmmmm    \n");
        printf("          ..####              @@    ##      mmmm        --mm    mm  mmmm  mmmm  mm  mmmm  mmmmmm    \n");
        printf("        ##    ##              ..  ##..        mmmm    mm  mm++mmmm  mmmm  mmmm++mmmm      mm        \n");
        printf("        ..  ##..  @@########  ##  ..  ##      mmmmmmmmmm  --mmmm    mmmmmmmmmm  mmmmmmmm  mm        \n");
        printf("            --  ##MMMMMMMMMMMM  ##    ##          ::      ..mmmm                  ..                \n");
        printf("      MM  mm######MMMMMMMMMMMM######  ##                  mmmm                                      \n");
        printf("      ++  ##mm##@@####MMMM##MM##mm##--##        mmmmmm                                                \n");
        printf("              @@@@MMMMMMMMMMMM##      ##      mmmmmmmmmm                                              \n");
        printf("        ##    ::##MMMMMMMMMMMM##              mm          mmmmmm  mmmm  mm  ::mm                     \n");
        printf("        mm      ##@@########MMMM    ##      ++mm        mmmm  mmmmmmmm  mm  ::mm                     \n");
        printf("          ##      ############    --          mm++      mmmm  mmmm++mm  mm++mmmm                     \n");
        printf("            ##    ##@@@@@@@@    mm            mmmmmmmmmm..mmmmmm::  mmmm  mmmm                       \n");
        printf("              MM##  ......  ..##                  mm::      ++        ..                             \n");
        printf("                    ######--                                                                         \n");
        printf("\n");
        printf("----REGISTRO----");
        printf("\n1- Cadastro;");
        printf("\n2- Login;");
        printf("\n0- Sair.");
        printf("\n\nEscolha uma opção: ");
        scanf("%d", &op);
        getchar();

        switch (op)
        {
        case 0:
            printf("Saindo...\n");
            break;

        case 1:
            limparTela();
            printf("                ##++      ..##..                mmmmmmmm            mmmm                            \n");
            printf("            ++--                ##            mmmm  ::mm            mm++                            \n");
            printf("          @@  ####          ++##..##        --mm        --mm    mm  mmmmmmmm++  mmmmmm--++mmmmmm    \n");
            printf("          ..####              @@    ##      mmmm        --mm    mm  mmmm  mmmm  mm  mmmm  mmmmmm    \n");
            printf("        ##    ##              ..  ##..        mmmm    mm  mm++mmmm  mmmm  mmmm++mmmm      mm        \n");
            printf("        ..  ##..  @@########  ##  ..  ##      mmmmmmmmmm  --mmmm    mmmmmmmmmm  mmmmmmmm  mm        \n");
            printf("            --  ##MMMMMMMMMMMM  ##    ##          ::      ..mmmm                  ..                \n");
            printf("      MM  mm######MMMMMMMMMMMM######  ##                  mmmm                                      \n");
            printf("      ++  ##mm##@@####MMMM##MM##mm##--##        mmmmmm                                                \n");
            printf("              @@@@MMMMMMMMMMMM##      ##      mmmmmmmmmm                                              \n");
            printf("        ##    ::##MMMMMMMMMMMM##              mm          mmmmmm  mmmm  mm  ::mm                     \n");
            printf("        mm      ##@@########MMMM    ##      ++mm        mmmm  mmmmmmmm  mm  ::mm                     \n");
            printf("          ##      ############    --          mm++      mmmm  mmmm++mm  mm++mmmm                     \n");
            printf("            ##    ##@@@@@@@@    mm            mmmmmmmmmm..mmmmmm::  mmmm  mmmm                       \n");
            printf("              MM##  ......  ..##                  mm::      ++        ..                             \n");
            printf("                    ######--                                                                         \n");

            printf("----CADASTRO----\n");

            do
            {

                printf("Escolha o cargo:\n");
                printf("1- Colaborador;\n");
                printf("2- Admin.\n");
                printf("0- Se deseja retornar ao menu\n");
                printf("\nDigite sua escolha: ");
                scanf("%d", &cargo);
                getchar();

                if (cargo != 1 && cargo != 2 && cargo != 0)
                {
                    limparTela();
                    printf("Opção inválida.\n\n");
                    printf("Pressione Enter para tentar novamente...");
                    getchar();
                }
            }
            while (cargo != 1 && cargo != 2 && cargo != 0);

            do
            {
                if(cargo == 0){
                    break;
                }

                limparTela();
                printf("                ##++      ..##..                mmmmmmmm            mmmm                            \n");
                printf("            ++--                ##            mmmm  ::mm            mm++                            \n");
                printf("          @@  ####          ++##..##        --mm        --mm    mm  mmmmmmmm++  mmmmmm--++mmmmmm    \n");
                printf("          ..####              @@    ##      mmmm        --mm    mm  mmmm  mmmm  mm  mmmm  mmmmmm    \n");
                printf("        ##    ##              ..  ##..        mmmm    mm  mm++mmmm  mmmm  mmmm++mmmm      mm        \n");
                printf("        ..  ##..  @@########  ##  ..  ##      mmmmmmmmmm  --mmmm    mmmmmmmmmm  mmmmmmmm  mm        \n");
                printf("            --  ##MMMMMMMMMMMM  ##    ##          ::      ..mmmm                  ..                \n");
                printf("      MM  mm######MMMMMMMMMMMM######  ##                  mmmm                                      \n");
                printf("      ++  ##mm##@@####MMMM##MM##mm##--##        mmmmmm                                                \n");
                printf("              @@@@MMMMMMMMMMMM##      ##      mmmmmmmmmm                                              \n");
                printf("        ##    ::##MMMMMMMMMMMM##              mm          mmmmmm  mmmm  mm  ::mm                     \n");
                printf("        mm      ##@@########MMMM    ##      ++mm        mmmm  mmmmmmmm  mm  ::mm                     \n");
                printf("          ##      ############    --          mm++      mmmm  mmmm++mm  mm++mmmm                     \n");
                printf("            ##    ##@@@@@@@@    mm            mmmmmmmmmm..mmmmmm::  mmmm  mmmm                       \n");
                printf("              MM##  ......  ..##                  mm::      ++        ..                             \n");
                printf("                    ######--                                                                         \n");
                printf("\n");
                printf("----CADASTRO----\n");

                printf("Digite seu nome de usuário: ");
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
                    printf("As senhas não coincidem.\n\n");
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

            int login_success = 0; // Variável de controle para login

            while (login_success != 1) // Loop infinito até o login ser bem-sucedido
            {
                limparTela();
                printf("                ##++      ..##..                mmmmmmmm            mmmm                            \n");
                printf("            ++--                ##            mmmm  ::mm            mm++                            \n");
                printf("          @@  ####          ++##..##        --mm        --mm    mm  mmmmmmmm++  mmmmmm--++mmmmmm    \n");
                printf("          ..####              @@    ##      mmmm        --mm    mm  mmmm  mmmm  mm  mmmm  mmmmmm    \n");
                printf("        ##    ##              ..  ##..        mmmm    mm  mm++mmmm  mmmm  mmmm++mmmm      mm        \n");
                printf("        ..  ##..  @@########  ##  ..  ##      mmmmmmmmmm  --mmmm    mmmmmmmmmm  mmmmmmmm  mm        \n");
                printf("            --  ##MMMMMMMMMMMM  ##    ##          ::      ..mmmm                  ..                \n");
                printf("      MM  mm######MMMMMMMMMMMM######  ##                  mmmm                                      \n");
                printf("      ++  ##mm##@@####MMMM##MM##mm##--##        mmmmmm                                                \n");
                printf("              @@@@MMMMMMMMMMMM##      ##      mmmmmmmmmm                                              \n");
                printf("        ##    ::##MMMMMMMMMMMM##              mm          mmmmmm  mmmm  mm  ::mm                     \n");
                printf("        mm      ##@@########MMMM    ##      ++mm        mmmm  mmmmmmmm  mm  ::mm                     \n");
                printf("          ##      ############    --          mm++      mmmm  mmmm++mm  mm++mmmm                     \n");
                printf("            ##    ##@@@@@@@@    mm            mmmmmmmmmm..mmmmmm::  mmmm  mmmm                       \n");
                printf("              MM##  ......  ..##                  mm::      ++        ..                             \n");
                printf("                    ######--                                                                         \n");
                printf("\n");
                printf("----LOGIN----\n");

                printf("Deseja retornar ao menu? Digite 0, caso contrário digite 1\n");
                scanf("%d", &voltarMenu);

                if(voltarMenu == 0){
                    break;
                }


                getchar();
                limparTela();
                printf("                ##++      ..##..                mmmmmmmm            mmmm                            \n");
                printf("            ++--                ##            mmmm  ::mm            mm++                            \n");
                printf("          @@  ####          ++##..##        --mm        --mm    mm  mmmmmmmm++  mmmmmm--++mmmmmm    \n");
                printf("          ..####              @@    ##      mmmm        --mm    mm  mmmm  mmmm  mm  mmmm  mmmmmm    \n");
                printf("        ##    ##              ..  ##..        mmmm    mm  mm++mmmm  mmmm  mmmm++mmmm      mm        \n");
                printf("        ..  ##..  @@########  ##  ..  ##      mmmmmmmmmm  --mmmm    mmmmmmmmmm  mmmmmmmm  mm        \n");
                printf("            --  ##MMMMMMMMMMMM  ##    ##          ::      ..mmmm                  ..                \n");
                printf("      MM  mm######MMMMMMMMMMMM######  ##                  mmmm                                      \n");
                printf("      ++  ##mm##@@####MMMM##MM##mm##--##        mmmmmm                                                \n");
                printf("              @@@@MMMMMMMMMMMM##      ##      mmmmmmmmmm                                              \n");
                printf("        ##    ::##MMMMMMMMMMMM##              mm          mmmmmm  mmmm  mm  ::mm                     \n");
                printf("        mm      ##@@########MMMM    ##      ++mm        mmmm  mmmmmmmm  mm  ::mm                     \n");
                printf("          ##      ############    --          mm++      mmmm  mmmm++mm  mm++mmmm                     \n");
                printf("            ##    ##@@@@@@@@    mm            mmmmmmmmmm..mmmmmm::  mmmm  mmmm                       \n");
                printf("              MM##  ......  ..##                  mm::      ++        ..                             \n");
                printf("                    ######--                                                                         \n");
                printf("\n");
                printf("----LOGIN----\n");

                printf("Digite seu nome de usuário: ");
                fgets(nome, sizeof(nome), stdin);
                nome[strcspn(nome, "\n")] = '\0';  // Remover o '\n' no final da string
                fflush(stdin);

                printf("Digite sua senha: ");
                fgets(senha, sizeof(senha), stdin);
                senha[strcspn(senha, "\n")] = '\0';  // Remover o '\n' no final da string
                fflush(stdin);

                // Percorrer o arquivo e verificar se o login é correto
                int encontrado = 0;
                while (fscanf(arqlogin, "%49[^,],%49[^,],%d\n", nomearq, senhaarq, &cargoarq) != EOF)
                {
                    if (strcmp(nome, nomearq) == 0 && strcmp(senha, senhaarq) == 0)
                    {
                        login_success = 1;  // Login bem-sucedido
                        encontrado = 1;
                        break;
                    }
                }

                if (encontrado==1)
                {
                    // Login bem-sucedido, seguir para o menu
                    do
                    {
                        limparTela();
                        printf("                ##++      ..##..                mmmmmmmm            mmmm                            \n");
                        printf("            ++--                ##            mmmm  ::mm            mm++                            \n");
                        printf("          @@  ####          ++##..##        --mm        --mm    mm  mmmmmmmm++  mmmmmm--++mmmmmm    \n");
                        printf("          ..####              @@    ##      mmmm        --mm    mm  mmmm  mmmm  mm  mmmm  mmmmmm    \n");
                        printf("        ##    ##              ..  ##..        mmmm    mm  mm++mmmm  mmmm  mmmm++mmmm      mm        \n");
                        printf("        ..  ##..  @@########  ##  ..  ##      mmmmmmmmmm  --mmmm    mmmmmmmmmm  mmmmmmmm  mm        \n");
                        printf("            --  ##MMMMMMMMMMMM  ##    ##          ::      ..mmmm                  ..                \n");
                        printf("      MM  mm######MMMMMMMMMMMM######  ##                  mmmm                                      \n");
                        printf("      ++  ##mm##@@####MMMM##MM##mm##--##        mmmmmm                                                \n");
                        printf("              @@@@MMMMMMMMMMMM##      ##      mmmmmmmmmm                                              \n");
                        printf("        ##    ::##MMMMMMMMMMMM##              mm          mmmmmm  mmmm  mm  ::mm                     \n");
                        printf("        mm      ##@@########MMMM    ##      ++mm        mmmm  mmmmmmmm  mm  ::mm                     \n");
                        printf("          ##      ############    --          mm++      mmmm  mmmm++mm  mm++mmmm                     \n");
                        printf("            ##    ##@@@@@@@@    mm            mmmmmmmmmm..mmmmmm::  mmmm  mmmm                       \n");
                        printf("              MM##  ......  ..##                  mm::      ++        ..                             \n");
                        printf("                    ######--                                                                         \n");
                        printf("\n");
                        printf("Logado como: %s (%s)\n\n", nomearq, (cargoarq == 1) ? "Colaborador" : "Administrador");
                        printf("---MENU---\n");
                        printf("1- Cadastro de lotes\n");
                        printf("2- Listagem de lotes\n");
                        printf("3- Salvar dados de lotes\n");
                        printf("4- Listar tarefas\n");
                        if (cargoarq == 2)
                        {
                            printf("5- Criar nova tarefa\n");
                            printf("6- Exibir ICA (Índice de Conversão Alimentar)\n");
                            printf("7- Média de Lucro\n");
                            printf("8- Testar Peso Ideal para Venda\n");
                            printf("9- Cadastrar dados mensais\n");
                        }
                        printf("0- Deslogar/Sair\n\n");
                        printf("Selecione uma opção: ");
                        scanf("%d", &op2);
                        getchar();

                        switch (op2)
                        {
                        case 1:
                            printf("Quantos lotes serão cadastrados: ");
                            scanf("%d", &quantidadeAnimais);
                            cadastrarLote(animais, &quantidadeAnimais);
                            getchar();
                            break;
                        case 2:
                            listarLotes(animais, &quantidadeAnimais);
                            getchar();
                            break;
                        case 3:
                            salvarDados(animais, &quantidadeAnimais);
                            getchar();
                            break;
                        case 4:
                            listarTarefas();
                            getchar();
                            break;
                        case 5:
                            if (cargoarq == 2)
                            {
                                criarTarefa();
                                getchar();
                            }
                            break;
                        case 6:
                            if (cargoarq == 2)
                            {
                                float ganhoPeso;
                                printf("Digite o ganho de peso por animal ao mês: ");
                                scanf("%f", &ganhoPeso);
                                printf("Digite a quantidade de consumo de ração por animal ao mês: ");
                                scanf("%f", &gastoTotalRacao);
                                getchar();
                                printf("Índice de Conversão Alimentar (ICA): %.2lf\n", ICA(gastoTotalRacao, ganhoPeso));
                                getchar();
                            }
                            break;
                        case 7:
                            if (cargoarq == 2)
                            {
                                printf("Digite o ganho total com as vendas: ");
                                scanf("%f", &ganhoTotal);
                                printf("Digite o gasto total de manutenção do gado: ");
                                scanf("%f", &gastoTotalRacao);
                                getchar();
                                printf("Média de Lucro: %.2lf R$\n", mediaLucro(ganhoTotal, gastoTotalRacao));
                                printf("Pressione enter para retornar ao menu...\n");
                                getchar();
                            }
                            break;
                        case 8:
                            if (cargoarq == 2)
                            {
                                float peso, custo, preco;
                                printf("Digite o peso atual (kg): ");
                                scanf("%f", &peso);
                                printf("Digite o custo por kg: ");
                                scanf("%f", &custo);
                                printf("Digite o preço de venda por kg: ");
                                scanf("%f", &preco);
                                getchar();
                                if (testePesoIdeal(peso, custo, preco) == 0)
                                {
                                    printf("Peso ideal para venda.\n");
                                }
                                else
                                {
                                    printf("Peso insuficiente para venda.\n");
                                }
                                getchar();
                            }
                            break;
                        case 9:  // Nova opção para registrar compras de ração e vendas de lote
                            if (cargoarq == 2)
                            {
                                int op3;
                                // Exemplo de opção para registro e consulta de dados de ração
                                limparTela();
                                printf("                ##++      ..##..                mmmmmmmm            mmmm                            \n");
                                printf("            ++--                ##            mmmm  ::mm            mm++                            \n");
                                printf("          @@  ####          ++##..##        --mm        --mm    mm  mmmmmmmm++  mmmmmm--++mmmmmm    \n");
                                printf("          ..####              @@    ##      mmmm        --mm    mm  mmmm  mmmm  mm  mmmm  mmmmmm    \n");
                                printf("        ##    ##              ..  ##..        mmmm    mm  mm++mmmm  mmmm  mmmm++mmmm      mm        \n");
                                printf("        ..  ##..  @@########  ##  ..  ##      mmmmmmmmmm  --mmmm    mmmmmmmmmm  mmmmmmmm  mm        \n");
                                printf("            --  ##MMMMMMMMMMMM  ##    ##          ::      ..mmmm                  ..                \n");
                                printf("      MM  mm######MMMMMMMMMMMM######  ##                  mmmm                                      \n");
                                printf("      ++  ##mm##@@####MMMM##MM##mm##--##        mmmmmm                                                \n");
                                printf("              @@@@MMMMMMMMMMMM##      ##      mmmmmmmmmm                                              \n");
                                printf("        ##    ::##MMMMMMMMMMMM##              mm          mmmmmm  mmmm  mm  ::mm                     \n");
                                printf("        mm      ##@@########MMMM    ##      ++mm        mmmm  mmmmmmmm  mm  ::mm                     \n");
                                printf("          ##      ############    --          mm++      mmmm  mmmm++mm  mm++mmmm                     \n");
                                printf("            ##    ##@@@@@@@@    mm            mmmmmmmmmm..mmmmmm::  mmmm  mmmm                       \n");
                                printf("              MM##  ......  ..##                  mm::      ++        ..                             \n");
                                printf("                    ######--                                                                         \n");
                                printf("\n");
                                printf("--- Gestão de Ração e Vendas ---\n");
                                printf("1 - Registrar dados de ração\n");
                                printf("2 - Exibir dados registrados\n");
                                printf("0 - Voltar ao menu principal\n");
                                printf("Escolha uma opção: ");
                                scanf("%d", &op3);
                                getchar();

                                switch(op3){
                                    case 1:
                                        registrarDadosUsuario1();
                                        getchar();
                                    break;

                                    case 2:
                                        lerarquivo();
                                        getchar();
                                    break;
                                }
                            }
                        case 0:
                            printf("Deslogando...\n");
                            break;
                        default:
                            limparTela();
                            printf("Opção inválida! Tente novamente.\n\n");
                            printf("Pressione ENTER para tentar novamente.");
                            getchar();
                        }
                    }
                    while (op2 != 0);
                }
                else if(encontrado != 1)
                {
                    limparTela();
                    printf("Usuário ou senha incorretos.\n\n");
                    printf("Pressione Enter para tentar novamente...");
                    getchar();
                }

                // Reposicionar o ponteiro do arquivo para o começo após ler todas as entradas
                fseek(arqlogin, 0, SEEK_SET);
            }

            fclose(arqlogin);
            break;


        default:
            limparTela();
            printf("Opção inválida.\n");
            printf("\nPressione Enter para tentar novamente...");
            getchar();
            break;
        }
    }
    while (op != 0);

    return 0;
}
```

![image](https://github.com/user-attachments/assets/1513a3fd-9503-49d0-9b3c-135954673c42)

