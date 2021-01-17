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

//A ideia é que tenha uma matriz base que mantenha registro da matriz do jogador 1 e 2 ao mesmo tempo
//Ela terá valor 0 até que alguem escolha se escolherem o mesmo não tem problema ela irá aumentar de 1 em 1 a cada escolha
//Ou seja se ambos escolherem essa celula terá valor 2 e se escolhido atingirá ambos
//por algum motivo está executando o i = 2 e i = 3 duas vezes ou tres vezes por algum motivo

int main(){
    srand(time(NULL));
    int celulab[11][11], celula1[11][11], celula2[11][11], linha, coluna, verificador = 0, de = 0;

    //inicializo a matriz base pra todos os valores serem 0 e assim poder armazenar a quantidade de embarcações em cada celula
    for(int i = 0; i < 11; i++){
        for(int j = 0; j < 11; j++){
            celulab[i][j] = 0;
            celula1[i][j] = 0;
            celula2[i][j] = 0;
            }
        }

    //posições do jogador 1
    // o mais complexo aqui são as condições para poder colocar a embarcação
    for(int i = 0; i < 4; i++){
        if(i == 0){
            linha = rand() % 11;
            coluna = rand() % 11;

            //o celulab recebe++ para facilitar quando for a vez do jogador2
            //quando o jogador 2 aumentar o numero irá dizer quantas embarcacoes ocupam a celula
            celulab[linha][coluna]++;
            celula1[linha][coluna] = 1;


        }else if(i == 1){
            for(int j = 0; j < 2; j++){
                if(j == 0){
                    linha = rand() % 11;
                    coluna = rand() % 11;
                    if(celula1[linha][coluna] == 1){
                        j--;
                    }else{
                        celula1[linha][coluna] = 1;
                        celulab[linha][coluna]++;
                    }
                }else{
                    de = rand() % 2;


                    if(verificador == 0 && coluna > 0){
                        celula1[linha][coluna - 1] = 1;
                        celulab[linha][coluna - 1]++;
                    }else if(verificador == 1 && coluna < 10){
                        celula1[linha][coluna + 1] = 1;
                        celulab[linha][coluna + 1]++;
                    }else{
                        j--;
                        }
                    }
                }
        }else if(i == 2){
            for(int j = 0; j < 2; j++){
                linha = rand() % 11;
                coluna = rand() % 11;


                if( (celula1[linha][coluna] != 1 && celula1[linha + 1][coluna + 1] != 1) && (linha > 0 && coluna < 10)){
                    celulab[linha][coluna]++;
                    celulab[linha - 1][coluna + 1]++;
                    celula1[linha][coluna] = 1;
                    celula1[linha - 1][coluna + 1] = 1;
                }else{
                    j--;
                }
            }
        }else if(i == 3){
            for(int j = 0; j < 2; j++){
                linha = rand() % 11;
                coluna = rand() % 11;

                if( (celula1[linha][coluna] != 1 && celula1[linha + 1][coluna + 1] != 1) && (linha < 10 && coluna < 10)){
                    celulab[linha][coluna]++;
                    celulab[linha + 1][coluna + 1]++;
                    celula1[linha][coluna] = 1;
                    celula1[linha + 1][coluna + 1] = 1;
                }else{
                    j--;
                }
            }
        }
    }

    for(int i = 0; i < 11; i++){
        for(int j = 0; j < 11; j++){
            printf("%i ", celula1[i][j]);
        }
        printf("\n");
    }
}


//basta dar ctrl c ctrl v no codigo acima para o jogador 2 e mudando a variavel celula1 por celula2
//apos isso crie uma parte do codigo para guardar os pontos do jogador 1 e do jogador 2  e um codigo onde de uma loopada para
//ler as posições explodidas e levando em consideração os pontos

```
