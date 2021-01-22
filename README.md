# 1VA

### 1

1: Você comprou um jogo da memória com 16 peças para jogar contra um amigo. As regras do jogo são
simples: inicialmente o jogador 1 levanta uma pedra e em seguida levanta a segunda. Se as duas forem iguais, elas são
retiradas do jogo, o jogador1 ganha 1 ponto e passa para a vez para o jogador 2. Caso elas sejam diferentes, passa
para a vez do jogador2. Informe quem foi o vencedor ou se houve empate.

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(){
    srand(time(NULL));
    int matriz[4][4], verificador = 0, valores[16] = {1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7, 8, 8}, x = 0, j = 0;

    //algoritmo de preenchimento da matriz maneira aleatoria
    for(int i = 0; i < 4; i++){
        while(j < 4){
            x = rand() % 16;
            if(valores[x] != 0){
                matriz[i][j] = valores[x];
                valores[x] = 0;
                j++;
            }
        }
        j = 0;
    }


    for(int i = 0; i < 4; i++){
        for(int j = 0; j < 4; j++){
            printf("%i ", matriz[i][j]);
        }
        printf("\n");
    }


    printf("\n\n");

    int jogador1 = 0, jogador2 = 0, l1 = 0, c1 = 0, l2 = 0, c2 = 0;


    while(jogador1 + jogador2 < 8 ){
        printf("\n");
         for(int i = 0; i < 4; i++){
            for(int k = 0; k < 4; k++){
                if(matriz[i][k] != 0){
                    printf("x ");
                }else{
                    printf("0 ");
                }
            }
            printf("\n");
        }



        printf("\nJogador 1 digite a primeira celula desejada\n");
        scanf("%i %i", &l1, &c1);
        printf("\nJogador 1 Digite a segunda celula desejada\n");
        scanf("%i %i", &l2, &c2);
        if( (l1 != l2 || c1 != c2)){
        //interface para facilitar a vizualização

        if(matriz[l1][c1] == matriz[l2][c2] && matriz[l1][c1] != 0){
            jogador1++;
            matriz[l1][c1] = 0;
            matriz[l2][c2] = 0;
            printf("\nPosicoes retiradas: %i %i e %i %i\n\n", l1, c1, l2, c2);
            printf("Pontuacao jogador 1: %i\n\n", jogador1);
         }else{
            printf("\nVez passada\n\n");}
        }else{
            printf("\nVez passada\n\n");
        }

        for(int i = 0; i < 4; i++){
                for(int k = 0; k < 4; k++){
                    if(matriz[i][k] != 0){
                        printf("x ");
                    }else{
                        printf("0 ");
                    }
                }
                printf("\n");
            }


            printf("\nJogador 2 digite a primeira celula desejada\n");
            scanf("%i %i", &l1, &c1);
            printf("\nJogador 2 Digite a segunda celula desejada\n");
            scanf("%i %i", &l2, &c2);

            if( l1 != l2 || c1 != c2){

                if(matriz[l1][c1] == matriz[l2][c2] && matriz[l1][c1] != 0){
                    jogador2++;
                    matriz[l1][c1] = 0;
                    matriz[l2][c2] = 0;
                    printf("\nPosicoes retiradas: %i %i e %i %i\n", l1, c1, l2, c2);
                    printf("Pontuacao do jogador 2: %i", jogador2);
                }else{
                    printf("\nVez passada\n\n");}
            }else{
                printf("\nVez passada\n\n");
            }
    }


    if(jogador1 > jogador2){
        printf("O vencedor é o jogador 1");
    }else if(jogador2 > jogador1){
        printf("O vencedor é o jogadro 2");
    }else{
        printf("Empate");
    }
return 0;
}

```

### 2

O jogo batalha naval é extremamente conhecido e viciante. Trata-se da disputa entre dois jogadores, onde o objetivo de cada jogador é destruir as navegações inimigas. Cada jogador tem a informação das suas embarcações, desconhecendo a posição das navegações inimigas. Cada jogador visualiza a posição de suas embarcações através de uma grade. 
Exemplo de visualização de cada jogador: 

Este jogo apresenta 4 tipos de navegações: 
 A embarcação que ocupa uma célula da grade. 
 A embarcação que ocupa duas células de forma horizontal. 
 A embarcação que ocupa duas células, sendo que uma célula localizada na parte superior direita. 


 A embarcação que ocupa duas células, sendo que uma célula localizada na parte superior esquerda. 
Funcionamento do jogo 
Inicialmente, cada jogador começa com uma embarcação de cada tipo posicionadas aleatoriamente na grade, ou seja, cada jogador possui 4 embarcações cada um, sendo 1 embarcação de cada tipo. 
IMPORTANTE: As embarcações não podem ser posicionadas de forma sobreposta! 
Uma vez que cada jogador sabe a posição de suas próprias embarcações, o jogo começa com o jogador 1 escolhendo uma célula do tabuleiro para realizar um bombardeio. Caso a célula escolhida tenha uma embarcação inimiga, a embarcação deve ser destruída (removida da grade do adversário, mesmo que esta embarcação seja de 2 células) e a vez passa para o jogador 2. Caso contrário, se a célula escolhida não for uma embarcação, a vez passa para o jogador 2 da mesma forma. Caso contrário, se a célula escolhida for uma embarcação do próprio jogador, esta embarcação deve ser destruída (removida de sua grade), passando a vez para o jogador 2. Este processo se repete para o jogador 2 e assim sucessivamente. 
O jogo termina quando um dos jogadores não possuir mais embarcações. O jogo deve informar o vencedor. 
OBS: O jogador escolhe uma célula do tabuleiro para realizar um bombardeio. Caso a célula escolhida tenha uma embarcação inimiga, a embarcação deve ser destruída (removida da grade do adversário, mesmo que esta embarcação seja de 2 células). Caso contrário, se a célula escolhida não for uma embarcação, não acontece nada. Caso contrário, se a célula escolhida for uma embarcação do próprio jogador, esta embarcação deve ser destruída (removida de sua grade). Imprima uma mensagem informando qual dos cenários aconteceu: 
1- “Embarcação inimiga destruída!” 
2- “Não houve destruição.” 
3- “Erro. Própria navegação destruída!

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main(){
    srand(time(NULL));
    int celulab[10][10], celula1[10][10], celula2[10][10], linha = 0, coluna = 0, j = 0, vidaP1 = 7, vidaP2 = 7;

    for(int i = 0; i < 10; i++){
        for(int j = 0; j < 10; j++){
            celulab[i][j] = 0;
            celula1[i][j] = 0;
            celula2[i][j] = 0;
        }
    }

    //decidir se a segunda embarcação fica virado para direita ou esquerda
    int direitaEsquerda = rand() % 2;

    j = 0;
    //algoritmo de preenchimento da matriz do jogador 1
    for(int i = 0; i < 4; i++){
        if(i == 0) {
            linha = rand() % 10;
            coluna = rand() % 10;

            celula1[linha][coluna] = 1;
            celulab[linha][coluna]++;
        }else if(i == 1){
            while(j < 1) {
                linha = rand() % 10;
                coluna = rand() % 10;

                if( (celulab[linha][coluna] < 1 && direitaEsquerda == 0) && (coluna < 9) ) {
                    celulab[linha][coluna]++;
                    celulab[linha][coluna + 1]++;
                    celula1[linha][coluna] = 1;
                    celula1[linha][coluna + 1] = 1;
                    j++;
                }else if( (celulab[linha][coluna] < 1 && direitaEsquerda == 1) && (coluna > 0) ) {
                    celulab[linha][coluna]++;
                    celulab[linha][coluna - 1]++;
                    celula1[linha][coluna] = 1;
                    celula1[linha][coluna - 1] = 1;
                    j++;
                }
            }
        }else if(i == 2){
            j = 0;
            while(j < 1){
                linha = rand()%10;
                coluna = rand()%10;
                if( (celulab[linha][coluna] < 1 && celulab[linha - 1][coluna + 1] < 1) && (linha > 0 && coluna < 9) ){
                    celulab[linha][coluna]++;
                    celulab[linha - 1][coluna + 1]++;
                    celula1[linha][coluna] = 1;
                    celula1[linha - 1][coluna + 1] = 1;
                    j++;
                }
            }
        }else if(i == 3){
            j = 0;
            while(j < 1){
                linha = rand()%10;
                coluna = rand()%10;
                if( (celulab[linha][coluna] < 1 && celulab[linha - 1][coluna - 1] < 1) && (linha > 0 && coluna > 0)){
                    celulab[linha][coluna]++;
                    celulab[linha - 1][coluna - 1]++;
                    celula1[linha][coluna] = 1;
                    celula1[linha - 1][coluna - 1] = 1;
                    j++;
                }
            }
        }
    }

    // parte do jogador 2

    direitaEsquerda = rand() % 2;
    j = 0;

    for(int i = 0; i < 4; i++){
        if(i == 0) {
            linha = rand() % 10;
            coluna = rand() % 10;

            celula2[linha][coluna] = 1;
            celulab[linha][coluna]++;
        }else if(i == 1){
            while(j < 1) {
                linha = rand() % 10;
                coluna = rand() % 10;

                if((celulab[linha][coluna] < 2 && direitaEsquerda == 0 ) && (coluna < 9)){
                    celulab[linha][coluna]++;
                    celulab[linha][coluna + 1]++;
                    celula2[linha][coluna] = 1;
                    celula2[linha][coluna + 1] = 1;
                    j++;
                }else if((celulab[linha][coluna] < 2 && direitaEsquerda == 1) && (coluna > 0)){
                    celulab[linha][coluna]++;
                    celulab[linha][coluna - 1]++;
                    celula2[linha][coluna] = 1;
                    celula2[linha][coluna - 1] = 1;
                    j++;
                }
            }
        }else if(i == 2){
            j = 0;
            while(j < 1){
                linha = rand()%10;
                coluna = rand()%10;
                if((celulab[linha][coluna] < 2 && celulab[linha - 1][coluna + 1] < 2) && (linha > 0 && coluna < 9)){
                    celulab[linha][coluna]++;
                    celulab[linha - 1][coluna + 1]++;
                    celula2[linha][coluna] = 1;
                    celula2[linha - 1][coluna + 1] = 1;
                    j++;
                }
            }
        }else if(i == 3){
            j = 0;
            while(j < 1){
                linha = rand()%10;
                coluna = rand()%10;
                if((celulab[linha][coluna] < 2 && celulab[linha - 1][coluna - 1] < 2) && (linha > 0 && coluna > 0)){
                    celulab[linha][coluna]++;
                    celulab[linha - 1][coluna - 1]++;
                    celula2[linha][coluna] = 1;
                    celula2[linha - 1][coluna - 1] = 1;
                    j++;
                }
            }
        }
    }
    //mapa do jogador 1
    for(int i = 0; i < 10; i++){
        for(int j = 0; j < 10; j++){
            printf("%i ", celula1[i][j]);
        }
        printf("\n");
    }

    printf("\n\n");
    //mapa do jogador 2
    for(int i = 0; i < 10; i++){
        for(int j = 0; j < 10; j++){
            printf("%i ", celula2[i][j]);
        }
        printf("\n");
    }

    while(vidaP1 != 0 && vidaP2 != 0){
        printf("Jogador 1 digite a linha e coluna para atacar\n\n");
        scanf("%i %i", &linha, &coluna);
        if(celula2[linha][coluna] == 1){
            if(celula1[linha][coluna] == 1){
                printf("Embarcacao inimiga destruida!\n\n");
                printf("Erro. Propria navegação destruida!\n\n");
                celula1[linha][coluna] = celula2[linha][coluna] = celulab[linha][coluna] = 0;
                vidaP1--;
                vidaP2--;
                    if(vidaP1 == 0 || vidaP2 == 0){
                        break;
                    }
            }else{
                printf("Embarcação inimiga destruida!\n\n");
                celula2[linha][coluna] = 0;
                celulab[linha][coluna]--;
                vidaP2--;
                if(vidaP2 == 0){
                    break;
                }
            }
        }else{
            printf("Não houve destruicao\n\n");
        }
        printf("Jogadro 2 digite a linha e coluna para atacar\n\n");
        scanf("%i %i", &linha, &coluna);
        if(celula1[linha][coluna] == 1){
            if(celula2[linha][coluna] == 1){
                printf("Embarcacao inimiga destruída!\n\n");
                printf("Erro. Propria navegação destruída!\n\n");
                celula1[linha][coluna] = celula2[linha][coluna] = celulab[linha][coluna] = 0;
                vidaP1--;
                vidaP2--;
                if(vidaP1 == 0 || vidaP2 == 0){
                    break;
                }
            }else{
                printf("Embarcação inimiga destruída!\n\n");
                celula1[linha][coluna] = 0;
                celulab[linha][coluna]--;
                vidaP1--;
                if(vidaP1 == 0){
                    break;
                }
            }
        }else{
            printf("Não houve destruição\n\n");
        }
    }

    if(vidaP1 == 0){
        printf("\nO vencedor eh o jogador 2");
    }else{
        printf("\nO vencedor eh o jogador 1");
    }
return 0;
}
```

### 3

 O jogo The Maze Runner trata-se da disputa entre dois jogadores, onde o objetivo de cada jogador é chegar ao ‘fim’ vivo. Inicialmente, cada jogador lança dois dados, o jogador que obtiver a maior soma dos valores dos dois dados começa (considere dados com valores de 1 a 6). 
-Os dois jogadores começam na célula ‘início’. 
-Os dois jogadores começam com vida = 10 pontos. A pontuação máxima da vida é 10 pontos não podendo ser ultrapassado. -Os dois jogadores podem estar na mesma célula ao mesmo tempo. 
Uma vez definido o jogador que inicia, este jogador lança 1 (um) dado e o seu valor determina o número de células a serem percorridas. Após a jogador do primeiro jogador, o segundo jogador faz o mesmo processo. Implemente todo o funcionamento do jogo. 
O tabuleiro apresenta células de diferentes cores, onde cada cor representa uma ação sobre o jogador: 

onde não há ação sobre o jogador A célula vermelha penaliza o jogador em 3 pontos de vida 
A célula verde recupera 1 ponto de vida do jogador 
A célula amarela aprisiona o jogador por um turno sem jogar 
A célula azul permite que o jogador jogue novamente 
A célula preta faz o jogador voltar para o início (desconsidere as células de início e fim) 
A célula branca representa um espaço neutro

```c
```

### 4

 The Walking Dead é uma febre mundial. Esta série de zumbis despertou o seu interesse para o desenvolvimento de um jogo de sobrevivência. Neste jogo, existem zumbis, obstáculos (pedras, árvores, carros parados,...) e Rick, o personagem principal. O objetivo de Rick é encontrar a única saída existente em meio a uma horda de zumbis e obstáculos espalhados no cenário. 
Nesta questão, você deve desenvolver 1 estágio deste jogo, respeitando as seguintes instruções: 
1-O Cenário possui 100 metros quadrados. 
2-Rick acorda atordoado em algum lugar aleatório no cenário, com uma arma sem balas. 
3-Existem 15 zumbis espalhados aleatoriamente pelo cenário. 
4-Os obstáculos estão em toda parte. São ao todo 4 carros, 7 árvores e 8 pedras distribuídas aleatoriamente. 
5-No cenário existe uma única saída, também definida aleatoriamente. Se ela estiver bloqueada por obstáculos, Rick não tem saída e morrerá. Caso contrário, se Rick alcançar a saída, o jogo é encerrado. 
6-Rick possui 4 movimentações possíveis: cima, baixo, esquerda e direita. Embora a vida de Rick esteja complicada, existem 4 balas espalhadas no cenário. Se Rick se movimentar e tiver uma bala naquela posição, Rick carregará a arma imediatamente. 
7-Se Rick tentar se mover para uma região em que há um obstáculo, ele permanece onde está e não se movimenta. Caso ele se movimente para uma região em que há um zumbi, existem duas possibilidades: se Rick estiver com a arma descarregada, ele é atacado e morre; caso contrário, Rick usa a bala no zumbi. 
8-Obstáculos são estáticos, não se movimentam. 
9-Zumbis possuem 4 movimentações possíveis: cima, baixo, esquerda e direita. Os zumbis que estão a 3 metros quadrados de Rick passam a persegui-lo. Os que estão mais distantes, ficam parados. 
10-Toda vez que Rick realizar um movimento no cenário, a posição dos zumbis próximos deve ser atualizada. Implemente o jogo e informe a situação de Rick: morreu ou fugiu.

### 5

Walter White é um professor de química em uma escola, mas costuma fazer hora extra com Jesse Pinkman em um novo negócio. Na escola, Walter precisa pegar 4 produtos químicos (1,2,3,4) para a fabricação da sua solução. Esses produtos encontram-se em uma sala de 25 m2. Nesta sala, o itens são organizados da seguinte forma: 


Walter só pode pegar 1 item de cada produto, para que a escola não dê conta. Caso ele pegue mais de um item do mesmo produto, ele é preso e o jogo termina. Após pegar os itens necessários, Walter deve sair pela porta pela qual entrou. Se tentar sair pela porta sem ter pego todos os 4 itens, uma mensagem deverá ser exibida para lembrá-lo de pegar. Ao sair da porta, Walter encontra-se no estacionamento, devendo pegar o seu carro (5) e dirigir-se à saída da escola. Se Walter tentar pegar outro carro, deve ser exibida uma mensagem informando que o carro não é dele. 

No mapa, existem 4 letras, E (é a saída da escola por onde Walter está saindo com o carro), P é a polícia (você deve evitar passar por lá, se não, você tem 50% de chance de ser preso, ou 50% de ser liberado e perder os produtos), J é a casa de Jesse (você deve se deslocar até lá e pegá-lo). Finalmente, S é a saída (você deve acessá-la após pegar Jesse e estar com todos os itens). Caso tente pegar a saída sem Jesse e os produtos, uma mensagem deve ser mostrada para lembrá-lo. Ao chegar na saída com Jesse e os itens, Walter finalmente inicia a produção (informar se produção normal ou dobrada) e o jogo é encerrado. Caso chegue à saída e não tenha produtos, e os produtos não existem mais no cenário, deve ser informado que não haverá trabalho hoje e o jogo é encerrado!

```c
```
