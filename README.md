# 1VA

### 1

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
