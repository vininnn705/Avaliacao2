#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_ESTUDANTES 10
#define QTD_NOTAS 3
#define TAM_MAX_NOME 21

void ler_dados(int num_estudantes, char nomes[][TAM_MAX_NOME], float notas[][QTD_NOTAS]) {
    for (int i = 0; i < num_estudantes; i++) {
        int nome_valido = 0;
        while (!nome_valido) {
            printf("\nNome do estudante %d: ", i + 1);
            fgets(nomes[i], TAM_MAX_NOME, stdin);
            
            nomes[i][strcspn(nomes[i], "\n")] = '\0';
            
            if (strlen(nomes[i]) > 0) {
                nome_valido = 1;
            } else {
                printf("Erro: O nome não pode estar vazio!\n");
            }
            
        }

        for (int j = 0; j < QTD_NOTAS; j++) {
            float nota_temp;
            int nota_valida = 0;
            while (!nota_valida) {
                printf("Nota %d de %s: ", j + 1, nomes[i]);
                if (scanf("%f", &nota_temp) == 1 && nota_temp >= 0.0f && nota_temp <= 10.0f) {
                    notas[i][j] = nota_temp;
                    nota_valida = 1;
                } else {
                    printf("Erro: Nota inválida! O valor deve estar entre 0 e 10.\n");
                }
            }
        }
    }
}

void calcular_medias(int num_estudantes, float notas[][QTD_NOTAS], float *medias) {
    for (int i = 0; i < num_estudantes; i++) {
        float soma = 0.0f;
        for (int j = 0; j < QTD_NOTAS; j++) {
            soma += notas[i][j];
        }
        medias[i] = soma / QTD_NOTAS; 
    }
}

void exibir_resultados(int num_estudantes, char nomes[][TAM_MAX_NOME], float notas[][QTD_NOTAS], float *medias) {
    float soma_geral = 0.0f;
    float maior_media = 0.0f;

    printf("\n--- BOLETIM DA TURMA ---\n");
    printf("Nome                 | N1    | N2    | N3    | Média | Situação\n");
    
    for (int i = 0; i < num_estudantes; i++) {
        soma_geral += medias[i];
        if (medias[i] > maior_media) {
            maior_media = medias[i];
        }

        char situacao[20];
        if (medias[i] >= 6.0f) {
            strcpy(situacao, "atingiu a meta");
        } else {
            strcpy(situacao, "abaixo da meta");
        }

        printf("%-20s | %5.2f | %5.2f | %5.2f | %5.2f | %s\n", 
               nomes[i], notas[i][0], notas[i][1], notas[i][2], medias[i], situacao);
    }

    float media_geral = soma_geral / num_estudantes;
    printf("\nMédia geral da turma: %.2f\n", media_geral);

    printf("O(s) estudante(s) com a(s) maior(es) média(s) foi(foram): ");
    for (int i = 0; i < num_estudantes; i++) {            
        printf("\n");
        if (medias[i] == maior_media) {
            printf("%s\n", nomes[i]);
        }
    }
}

int main() {
    int num_estudantes = 0;

    printf("--- SISTEMA DE NOTAS ---\n");
    
    while (num_estudantes < 1 || num_estudantes > MAX_ESTUDANTES) {
        printf("Informe a quantidade de estudantes (1 a %d): ", MAX_ESTUDANTES);
        if (scanf("%d", &num_estudantes) != 1) {
            int c;
            while ((c = getchar()) != '\n' && c != EOF);
            continue;
        }
    }

    char nomes[MAX_ESTUDANTES][TAM_MAX_NOME];
    float notas[MAX_ESTUDANTES][QTD_NOTAS];

    float *medias = (float *)calloc(num_estudantes, sizeof(float));
    
    if (medias == NULL) {
        printf("Erro na alocação de memória!\n");
        return 1;
    }

    ler_dados(num_estudantes, nomes, notas);
    calcular_medias(num_estudantes, notas, medias);
    exibir_resultados(num_estudantes, nomes, notas, medias);

    free(medias);
    
    return 0;
}
