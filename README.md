# Caixa de Supermercado
Nosso trabalho será um simulador de caixa de supermercado, como Bahamas, onde o funcionário poderá realizar cadastro de mercadoria, com nome, código, quantidade, preço,  consultar estoque, modificar estoque, modificar o preço da mercadoria, fazer o controle de caixa como caixa atual, consular caixa e realizar a venda para o cliente.
# Projeto_Caixa_de_Supermercado

|Nome do campo|tipo| Descrição|
|-------------|----|----------|
|cadastrar | inteiro  |Constará no menu de opçoes e fará o cadastro de um novo produto|
|alterarEstoque|inteiro|Constará no menu e alterará a quantidade em estoque|
|modificarPreco|Real|Constará no menu e modificará o preço do produto|
|venda|Real|Constará no menu e mostrará o valor total de venda|
|listaProduto|inteiro|Constará no menu e mostrará os produtos no estoque|
|consultarSaldo|Real|Constará no menu e mostrará o valor existente no caixa|
|codigo|Inteiro|Código do produto|
|nome|Cadeia de caracteres|Nome do produto|
|quantidade|Inteiro|Quantidade de produtos|
|preco|Real|Valor do produto|
|caixaAtual|Real|Valor disponivel no caixa|

##  Grupo:

ADRIELY AVELINO DE CASTRO

EMERSON SOUZA DA SILVA

SAULO FURTADO NUNES

#include<stdio.h>
#include<stdlib.h>
#include<locale.h>

/*
Equipe: Saulo F Nunes, Adriely , Emerson
Disciplina: Linguagem de programacao 1

 */

//CONSTANTE PARA CONTROLAR QUANTIDADE DE DADOS
#define QTREG 30


//ESTRUTURA UTILIZADA PARA CADASTRAR PRODUTOS

typedef struct {
    int codigo;
    char nome[30];
    int quantidade;
    float preco;
} REGPRODUTO;

//CRIA VARIAVEL DO TIPO regproduto
REGPRODUTO produto[QTREG];

//VARIAVEIS GLOBAIS
float caixaAtual = 800.00;

//CABECALHO DAS FUNCOES QUE SERAO USADAS

//CABECALHO DA FUNCAO INSERIR UM PRODUTO NO ESTOQUE
int cadastrar();

//CABECALHO DA FUNCAO AUMENTAR O ESTOQUE DE UM PRODUTO
void alterarEstoque(int pCodgio, int pQuantidade);

//CABECALHO DA FUNÇÃO MODIFICAR O PRECO DE UM PRODUTO
void modificarPreco(int pCodigo, float pPreco);

//CABECALHO DA FUNÇÃO REALIZAR VENDA
float venda();

//CABECALHO DA FUNCAO CONSULTAR O ESTOQUE DOS PRODUTOS
void listaProduto(int pQtProduto);

//CABECALHO DA FUNCAO CONSULTAR O SALDO DO CAIXA
void consultarSaldo();

int main(void) {

    int op = 0;

    setlocale(LC_ALL, "Portuguese");

    while (op != 7) {
        printf("\n\n\t* Aividade Prof Joventino - Equipe Saulo, Adriely e Emerson *\n\n\n");
        printf("\n\n\t*  Super Mercado - Sistema de gerenciamento de mercadoria 2020 *\n\n\n");
        printf("MENU\n\n1 - Cadastrar Produto\n2 - Atualizar Estoque\n3 - Alterar preco produto");
        printf("\n4 - Realizar venda\n5 - Consultar estoque\n6 - Consultar saldo do caixa\n7 - Sair\n");
        fflush(stdout);
        scanf("%d", &op);
        fflush(stdin);
        system("cls");

        switch (op) {
            int qtProduto;
            float lucro;
            case 1://OPCAO CADASTRAR PRODUTO
                qtProduto = cadastrar();
                break;
            case 2:
            {//OPCAO ATUALIZAR ESTOQUE
                int pCodigo, pQuantidade;
                printf("Digite o codigo do produto que deseja atualizar o estoque:");
                fflush(stdout);
                scanf("%d", &pCodigo);
                fflush(stdin);
                printf("Deseja alterar quantidade do produto: %s - quantidade: %d \n", produto[pCodigo].nome, produto[pCodigo].quantidade);
                printf("Nova quantidade:");
                fflush(stdout);
                scanf("%d", &pQuantidade);
                fflush(stdin);
                system("pause");
                alterarEstoque(pCodigo, pQuantidade);
            }
                break;
            case 3:
            {//OPCAO ALTERAR PRECO DO PRODUTO
                int pCodigo;
                float pPreco;
                printf("Digite o codigo do produto que deseja modificar o preco:");
                fflush(stdout);
                scanf("%d", &pCodigo);
                fflush(stdin);
                printf("Deseja modificar o preco do produto: %s - preco: %0.2f \n", produto[pCodigo].nome, produto[pCodigo].preco);
                printf("Novo preco:");
                fflush(stdout);
                scanf("%f", &pPreco);
                fflush(stdin);
                system("pause");
                modificarPreco(pCodigo, pPreco);
            }
                break;
            case 4://OPCAO DE REALIZAR VENDA
                lucro = venda();
                caixaAtual = caixaAtual + lucro;
                break;
            case 5://OPCAO DE LISTAR PRODUTOS
                listaProduto(qtProduto);
                break;
            case 6://CONSULTAR SALDO NO CAIXA
                consultarSaldo();
                break;
            case 7://OPCAO SAIR DO PROGRAMA
                break;
            default:// EXIBE MENSAGEM DE OPCAO INVALIDA CASO DIGITE UM NUMERO QUE NAO TENHA NO MENU
                printf("Opcao invalida");
                fflush(stdout);
                break;

        }
    }


    system("pause");
    return 0;

}

//CORPO DA FUNCAO

//FUNCAO INSERIR UM PRODUTO NO ESTOQUE

int cadastrar() {
    char opSub;
    int cont = 0, qtProdutoCad = 0;
    //float compra;
    do {
        produto[cont].codigo = cont;
        fflush(stdin);
        printf("Digite o nome do produto:");
        fflush(stdout);
        gets(produto[cont].nome);
        fflush(stdin);
        printf("Digite a quantidade:");
        fflush(stdout);
        scanf("%d", &produto[cont].quantidade);
        fflush(stdin);
        printf("Digite o preco:");
        fflush(stdout);
        scanf("%f", &produto[cont].preco);
        fflush(stdin);
        caixaAtual = caixaAtual - produto[cont].preco;
        qtProdutoCad = qtProdutoCad + cont;
        cont++;


        printf("Deseja cadastrar um novo produto sim(s) ou nao(n)?");
        fflush(stdout);
        scanf("%c", &opSub);
        fflush(stdin);
    } while (opSub == 's' || opSub == 'S');
    return qtProdutoCad;
}

//FUNCAO AUMENTAR O ESTOQUE DE UM PRODUTO

void alterarEstoque(int pCodigo, int pQuantidade) {
    produto[pCodigo].quantidade = pQuantidade;
}

//FUNCAO MODIFICAR O PRECO DE UM PRODUTO

void modificarPreco(int pCodigo, float pPreco) {
    produto[pCodigo].preco = pPreco;
}

//FUNCAO REALIZA VENDA

float venda() {
    int pCodigo, qtd;
    float lucro = 0;
    char a;
    do{
        printf("Informe o codigo do produto: ");
        fflush(stdout);
        scanf("%d", &pCodigo);
        fflush(stdin);
        if (produto[pCodigo].quantidade < 0) {

            printf("Produto indisponivel\n");
            fflush(stdout);
        } else {
            printf("Informe a quantidade: ");
            fflush(stdout);
            scanf("%d", &qtd);
            fflush(stdin);
            printf("\tProduto: %s - \tQtdade: %d - \tPreco: %1.2f - \tSubTotal: %1.2f\n",
                    produto[pCodigo].nome, qtd, produto[pCodigo].preco, produto[pCodigo].preco * qtd);
            fflush(stdout);
            lucro += produto[pCodigo].preco * qtd;
            produto[pCodigo].quantidade -= qtd;
        }
        printf("Informar novo item para a venda? (s/n) ");
        fflush(stdout);
        scanf("%c", &a);
    } while (a != 'n');


    printf("\t\t\t Total: %1.2f", lucro);
    fflush(stdout);
    return lucro;
}

//FUNCAO CONSULTAR SALDO

void consultarSaldo() {
    printf("Saldo atual em caixa: %1.2f", caixaAtual);
    fflush(stdout);
}

//FUNCAO CONSULTAR O ESTOQUE DOS PRODUTOS

void listaProduto(int pQtProduto) {
    int i, qtProduto;
    qtProduto = pQtProduto;
    for (i = 0; i < qtProduto; i++) {
        printf("\tCodigo - %d \tNome - %s \tQuantidade - %d \n", produto[i].codigo, produto[i].nome, produto[i].quantidade);
    }
    fflush(stdout);
}

