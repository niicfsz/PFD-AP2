# Dados de lotes e criação de tarefas
Bibliotecas desenvolvidas pelo [Lucas](https://github.com/LucasFreitas1307) com o intuito de gerenciar os lotes, e criar e administrar tarefas pelo FILE.

## Cadastro de lotes
```C
#ifndef CADASTRODELOTES_H_INCLUDED
#define CADASTRODELOTES_H_INCLUDED

#define MAX_ANIMAIS 100  // Definindo o limite de animais por lote
#define MAX_TAREFA 256

// Definindo a estrutura Animal
typedef struct {
    int lote, numeroAnimais, idadeMeses;
    float pesoAtual, ganhoPesoIdeal;
    char sexo[30];
    float consumoAlimento; // Consumo de alimento
    float custoAlimentacao; // Custo de alimentação
}Animal;

// Função para cadastrar lote
void cadastrarLote(Animal animais[], int *quantidade) {
    if (*quantidade >= MAX_ANIMAIS) {
        printf("Limite de lotes cadastrados atingido!\n");
    }
    else{
        for(int i; i<(*quantidade); i++){
            printf("\nCadastro de lote:\n");
            printf("Digite o número do lote: ");
            scanf("%d", &animais[i].lote);
            printf("Digite o número de animais: ");
            scanf("%d", &animais[i].numeroAnimais);
            printf("Digite o peso atual (kg): ");
            scanf("%f", &animais[i].pesoAtual);
            printf("Digite o sexo dos animais: ");
            scanf("%s", animais[i].sexo);
            printf("Digite a idade média dos animais (meses): ");
            scanf("%d", &animais[i].idadeMeses);
            printf("Digite o ganho de peso ideal (kg): ");
            scanf("%f", &animais[i].ganhoPesoIdeal);
            printf("Digite o consumo de alimento por animal (kg): ");
            scanf("%f", &animais[i].consumoAlimento);
            printf("Digite o custo da alimentação por animal (R$): ");
            scanf("%f", &animais[i].custoAlimentacao);
        }

        printf("Lote cadastrado com sucesso!\n");
    }
}

// Função para listar os lotes
void listarLotes(Animal animais[], int *quantidade) {
    printf("\n--- Lotes Cadastrados ---\n");
    for (int i=0; i<(*quantidade); i++) {
        printf("Lote %d: %d animais, Peso Médio: %.2f kg, Sexo: %s, Idade Média: %d meses\n",
               animais[i].lote,
               animais[i].numeroAnimais,
               animais[i].pesoAtual,
               animais[i].sexo,
               animais[i].idadeMeses);
    }
    printf("-----------------------------\n");
}

// Função para salvar dados em arquivo
void salvarDados(Animal animais[], int quantidade) {
    FILE *arquivo = fopen("dados_animais.txt", "w");
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo para salvar.\n");
    }

    for (int i = 0; i < quantidade; i++) {
        fprintf(arquivo, "Lote: %d, Animais: %d, Peso: %.2f, Sexo: %s, Idade: %d meses, Ganho Ideal: %.2f kg, Consumo Alimento: %.2f kg, Custo Alimentacao: R$%.2f\n",
                animais[i].lote,
                animais[i].numeroAnimais,
                animais[i].pesoAtual,
                animais[i].sexo,
                animais[i].idadeMeses,
                animais[i].ganhoPesoIdeal,
                animais[i].consumoAlimento,
                animais[i].custoAlimentacao);
    }

    fclose(arquivo);
    printf("Dados salvos com sucesso!\n");
}

#endif // CADASTRODELOTES_H_INCLUDED
```

## Registro de ração utilizada
```C
#ifndef CADASTRORACAO_H_INCLUDED
#define CADASTRORACAO_H_INCLUDED

// Estrutura para armazenar os dados de ração e vendas
typedef struct
{
    int numeroComprasRacao, numeroVendasLote;
    float precoRacao, precoPelaVenda;

} CadastroRacao;


void salvarDadosRacao(CadastroRacao dados1)
{

    FILE *arquivo = fopen("racao_vendas.txt", "a"); // Abre o arquivo no modo append
    if (arquivo == NULL)
    {
        perror("Erro ao abrir o arquivo para salvar dados");
        getchar();
        return;
    }


// Salva os dados da estrutura no arquivo
    fprintf(arquivo, "%d %.2f %d %.2f\n", dados1.numeroComprasRacao, dados1.precoRacao, dados1.numeroVendasLote, dados1.precoPelaVenda);

    fclose(arquivo);
    printf("Dados salvos com sucesso.\n");
}

void lerarquivo()
{

    FILE *arquivo = fopen("racao_vendas.txt", "r");
    if (arquivo == NULL)
    {
        perror("Erro ao abrir o arquivo para salvar dados");
        getchar();
        return;
    }

    int ncra, nvla;
    float pra, pva;

    while (fscanf(arquivo, "%d %f %d %f\n", &ncra, &pra, &nvla, &pva) != EOF)
    {
        printf("Quantidade de ração comprada: %d\nPreço das rações: %.2f\nQuantidade de vendas do lote: %d\nPreço de venda do lote: %.2f", ncra, pra, nvla, pva);
    }

}



// Função para capturar os dados do usuário
void registrarDadosUsuario1()
{
    CadastroRacao dados;

    // Capturando o número de compras de ração
    printf("Digite o número de compras de ração realizadas: ");
    scanf("%d", &dados.numeroComprasRacao);

    // Capturando o preço da ração
    printf("Digite o preço da ração (por kg ou por unidade): ");
    scanf("%f", &dados.precoRacao);

    // Capturando o número de vendas de lote
    printf("Digite o número de vendas de lote realizadas: ");
    scanf("%d", &dados.numeroVendasLote);

    printf("Digite o valor arrecadado com a venda: ");
    scanf("%f", &dados.precoPelaVenda);

    // Salvar os dados no arquivo
    salvarDadosRacao(dados);
}

#endif // CADASTRORACAO_H_INCLUDED
```
## Criação, listagem
### Criação
```C
#ifndef CRIARTAREFAS_H_INCLUDED
#define CRIARTAREFAS_H_INCLUDED
#define MAX_TAREFA 256

void criarTarefa() {
    FILE *arquivo = fopen("tarefas.txt", "a");
    if (arquivo == NULL) {
        printf("Erro ao abrir o arquivo!\n");
        return 0;
    }

    char tarefa[MAX_TAREFA];
    printf("Digite a descrição da tarefa (max %d caracteres): ", MAX_TAREFA );
    fgets(tarefa, MAX_TAREFA, stdin);
    tarefa[strcspn(tarefa, "\n")] = '\0'; // Remover o '\n' do final

    fprintf(arquivo, "%s\n", tarefa);
    fclose(arquivo);
    printf("Tarefa salva com sucesso!\n");
}


#endif // CRIARTAREFAS_H_INCLUDED
```

### Listagem
```C
#ifndef LISTARTAREFAS_H_INCLUDED
#define LISTARTAREFAS_H_INCLUDED
#define MAX_TAREFA 256

void listarTarefas()
{
    FILE *arquivo = fopen("tarefas.txt", "r");
    if (arquivo == NULL)
    {
        printf("Nenhuma tarefa encontrada!\n");
    }

    char tarefa[MAX_TAREFA];

    printf("Tarefas:\n");
    printf("-----------------------------\n\n");

    while (fgets(tarefa, MAX_TAREFA, arquivo))
    {
        printf("- %s", tarefa);
    }
    printf("\n-----------------------------\n");

    fclose(arquivo);
}


#endif // LISTARTAREFAS_H_INCLUDED
```

