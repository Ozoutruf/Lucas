# Projeto do curso de Ti ebac Atualizado
Cartório 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <locale.h>

void registro() {
    char cpf[40], nome[40], sobrenome[40], cargo[40], arquivo[50];
    
    printf("Digite o CPF a ser cadastrado: ");
    scanf("%s", cpf);
    
    strcpy(arquivo, cpf);
    strcat(arquivo, ".txt");

    printf("Digite o nome: ");
    scanf("%s", nome);

    printf("Digite o sobrenome: ");
    scanf("%s", sobrenome);

    printf("Digite o cargo: ");
    scanf("%s", cargo);

    FILE *file = fopen(arquivo, "w");
    if (file == NULL) {
        printf("Erro ao criar o arquivo!\n");
        return;
    }

    fprintf(file, "%s,%s,%s,%s", cpf, nome, sobrenome, cargo);
    fclose(file);
    printf("Cadastro realizado com sucesso!\n");
    system("pause");
}

void consulta() {
    setlocale(LC_ALL, "Portuguese");

    char cpf[40], arquivo[50], conteudo[200];
    printf("Digite o CPF a ser consultado: ");
    scanf("%s", cpf);

    strcpy(arquivo, cpf);
    strcat(arquivo, ".txt");

    FILE *file = fopen(arquivo, "r");
    if (file == NULL) {
        printf("Usuário não encontrado.\n");
    } else {
        printf("\nInformações do usuário:\n");
        while (fgets(conteudo, sizeof(conteudo), file) != NULL) {
            printf("%s\n", conteudo);
        }
        fclose(file);
    }

    system("pause");
}

void deletar() {
    char cpf[40], arquivo[50];
    printf("Digite o CPF do usuário a ser deletado: ");
    scanf("%s", cpf);

    strcpy(arquivo, cpf);
    strcat(arquivo, ".txt");

    FILE *file = fopen(arquivo, "r");
    if (file == NULL) {
        printf("Usuário não encontrado.\n");
    } else {
        fclose(file);
        if (remove(arquivo) == 0) {
            printf("Usuário deletado com sucesso!\n");
        } else {
            printf("Erro ao deletar o arquivo.\n");
        }
    }

    system("pause");
}

int main() {
    setlocale(LC_ALL, "Portuguese");

    int opcao;
    char senha[20];

    printf("### Cartório da EBAC ###\n");
    printf("Login de administrador\n");
    printf("Digite a senha: ");
    scanf("%s", senha);

    if (strcmp(senha, "admin") == 0) {
        while (1) {
            system("cls");
            printf("### Menu Principal ###\n");
            printf("1 - Registrar nome\n");
            printf("2 - Consultar nome\n");
            printf("3 - Deletar nome\n");
            printf("4 - Sair\n");
            printf("Escolha uma opção: ");
            scanf("%d", &opcao);

            system("cls");

            switch (opcao) {
                case 1:
                    registro();
                    break;
                case 2:
                    consulta();
                    break;
                case 3:
                    deletar();
                    break;
                case 4:
                    printf("Encerrando o sistema...\n");
                    return 0;
                default:
                    printf("Opção inválida!\n");
                    system("pause");
            }
        }
    } else {
        printf("Senha incorreta!\n");
    }

    return 0;
}
