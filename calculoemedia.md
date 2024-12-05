# Cálculo de lucro, gasto, e ICA
Biblioteca desenvolvida pelo [Luís Felipe](https://github.com/Schneiderss) com o intuito de armazenar as funções responsáveis por efetuar os cálculos dentro do código
```C
#ifndef FUNCOESAP2_H_INCLUDED
#define FUNCOESAP2_H_INCLUDED
double mediaGanho(float ganhoTotal, int numeroDeVendas) {
    return ganhoTotal / numeroDeVendas;
}
//printf("%.2lf", mediaGanho(asd, ki));


double mediaGastoAlimentacao(int numeroAnimais, float precoRacao, int numeroComprasRacao) {

    return precoRacao * numeroComprasRacao / numeroAnimais;
}

double mediaLucro(float ganhoTotal, float gastoTotal) {
    return ganhoTotal - gastoTotal;
}

double ICA(float consumoDeRacao, float ganhoPeso) {
    return consumoDeRacao / ganhoPeso;

    // precoRacao * numerocompraracao == gastototalracao
}


/**
 * Testa se o peso do animal é ideal para venda.
 * @param peso - Peso atual do animal.
 * @param gastoPorKgBoi - Custo para criar o boi por kg.
 * @param precoVendaKgBoi - Preço de venda por kg.
 * @return 0 se o peso é ideal, 1 caso contrário.
 */
int testePesoIdeal(float peso, float gastoPorKgBoi, float precoVendaKgBoi) {
    if (peso * precoVendaKgBoi >= 1.3 * gastoPorKgBoi*peso) {
        return 0; // Peso ideal para venda
    } else {
        return 1; // Não está no peso ideal
    }
}



#endif // FUNCOESAP2_H_INCLUDED
```
