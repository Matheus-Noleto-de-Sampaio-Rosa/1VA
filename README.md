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



    int jogador1 = 0, jogador2 = 0, l1 = 0, c1 = 0, l2 = 0, c2 = 0;


    while((jogador1 + jogador2 < 8) && (jogador1 < 4 && jogador2 < 4)){
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
         }else{
            printf("\nVez passada\n");}
        }else{
            printf("\nVez passada\n");
        }

        for(int i = 0; i < 4; i++){
                for(int k = 0; k < 4; k++){
                    if(matriz[i][k] != 0){
                        printf("x");
                    }else{
                        printf("0");
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
                }else{
                    printf("\nVez passada\n");}
            }else{
                printf("\nVez passada\n");
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
