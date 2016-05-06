# PBL-04
Código do problema 04
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<ctype.h>
 
struct dados{
	int n_cadastro;
	char posto[30];
	char data[12];
	char nome[30];
	int rg;
	int idade;
	char endereco[70];
	struct dados *proximo;
};

struct dados* inserir(struct dados *inicio, int count)
{
	struct dados *nova, *aux;
	aux = inicio;
	nova = (dados *) malloc( sizeof (dados));	
	if(nova == NULL)
		return NULL;
	else{
		fflush(stdin);
		printf("Digite o seu nome: \n");
		gets(nova->nome);
		printf("Digite a sua idade: \n");
		scanf("%d", &nova->idade);
		printf("Digite o seu RG: \n");
		scanf("%d", &nova->rg);
		printf("Digite o seu endereco: \n");
		fflush(stdin);
		gets(nova->endereco);
		printf("Digite a data atual  (dd/mm/aa): \n");
		gets(nova->data);
		printf("Digite o nome do Posto de Saude: \n");
		gets(nova->posto);
        nova->proximo = NULL;

		if(inicio == NULL){
			inicio = nova;
		}
		else{
			while(aux->proximo != NULL)
				aux = aux->proximo;
			aux->proximo = nova;		
		}
	}
	nova->n_cadastro = count;
	return inicio;
}

void por_rg(struct dados *inicio, int rg_user)
{
	struct dados *aux;
	aux = inicio;
	if(inicio == NULL)
		printf("Não existem pessoas cadastradas\n");
	else{
		while(aux != NULL){
			if(aux->rg == rg_user){
				printf("\nNumero do cadastro: %d\n", aux->n_cadastro);
				printf("Nome: ");
				puts(aux->nome);
				printf("\nIdade: %d\n", aux->idade);
				printf("RG: %d  //  %d\n", rg_user, aux->rg);
				printf("Endereco: ");
				puts(aux->endereco);
				printf("\nData do cadastro: ");
				puts(aux->data);
				printf("\nPosto de saude: ");
				puts(aux->posto);
				printf("\n");
			}
			aux = aux->proximo;
		}
	}	
}

void por_cad(struct dados *inicio, int cad)
{
	struct dados *aux;
	aux = inicio;
	if(inicio == NULL)
		printf("Não existem pessoas cadastradas\n");
	else{
		while(aux != NULL){
			if(aux->n_cadastro == cad){
				printf("Numero do cadastro: %d\n", aux->n_cadastro);
				printf("Nome: ");
				puts(aux->nome);
				printf("\nIdade: %d\n", aux->idade);
				printf("RG: %d\n",aux->rg);
				printf("Endereco: ");
				puts(aux->endereco);
				printf("\nData do cadastro: ");
				puts(aux->data);
				printf("\nPosto de saude: ");
				puts(aux->posto);
				printf("\n");
			}
			aux = aux->proximo;
		}
		
	}	
}

void por_nome(struct dados *inicio, char nome_user[])
{
	struct dados *aux;
	aux = inicio;
	if(inicio == NULL)
		printf("Não existem pessoas cadastradas\n");
	else{
		while(aux != NULL){
			if(!stricmp(aux->nome, nome_user)){
				printf("Numero do cadastro: %d\n", aux->n_cadastro);
				printf("Nome: ");
				puts(aux->nome);
				printf("\nIdade: %d\n", aux->idade);
				printf("RG: %d\n",aux->rg);
				printf("Endereco: ");
				puts(aux->endereco);
				printf("\nData do cadastro: ");
				puts(aux->data);
				printf("\nPosto de saude: ");
				puts(aux->posto);
				printf("\n");
			}
			aux = aux->proximo;	
		}
	}
}

struct dados* atualiza(struct dados *inicio, int rg_user)
{
	struct dados *aux;
	aux = inicio;
	int escolha, resposta = 1;
	if(inicio == NULL)
		printf("Não existem pessoas cadastradas\n");
	else{
		while(aux != NULL){
			if(aux->rg == rg_user){
				printf("\nNumero do cadastro: %d\n", aux->n_cadastro);
				printf("Nome: ");
				puts(aux->nome);
				printf("\nIdade: %d\n", aux->idade);
				printf("RG: %d  //  %d\n", rg_user, aux->rg);
				printf("Endereco: ");
				puts(aux->endereco);
				printf("\nData do cadastro: ");
				puts(aux->data);
				printf("\nPosto de saude: ");
				puts(aux->posto);
				printf("\n\n");
				
				do{
					printf("Digite a informacao que deseja editar: \n");
					printf("(1) Nome\n");
					printf("(2) Idade\n");
					printf("(3) RG\n");
					printf("(4) Endereco\n");
					printf("(5) Data do cadastro\n");
					printf("(6) Posto de saude\n");
					scanf("%d", &escolha);
					switch(escolha){
						case 1:
							fflush(stdin);
							printf("Digite o novo nome: \n");
							gets(aux->nome);
							break;
						case 2:
							printf("Digite a nova idade: \n");
							scanf("%d", &aux->idade);
							break;	
						case 3:
							printf("Digite o novo RG: \n");
							scanf("%d", &aux->rg);
							break;
						case 4:
							printf("Digite o novo endereco: \n");
							fflush(stdin);
							gets(aux->endereco);
							break;
						case 5:
							printf("Digite a nova data (dd/mm/aa): \n");
							fflush(stdin);
							gets(aux->data);		
							break;
						case 6:
							printf("Digite o nome do novo Posto de Saude: \n");
							fflush(stdin);
							gets(aux->posto);		
					}
					printf("CADASTRO ATUALIZADO COM SUCESSO!\n");
					printf("Deseja editar mais alguma informacao? <1-SIM> <0-NAO>\n");
					scanf("%d", &resposta);
				}while(resposta != 0);
			}
			aux = aux->proximo;
		}
	}
}

struct dados* remove(struct dados *inicio, int rg_user)
{
	struct dados *aux, *p, *pont;
	aux = inicio;
	p = inicio;
	pont = inicio;
	int esc;
	if(inicio == NULL)
		printf("Não existem pessoas cadastradas\n");
	else{
		while(aux != NULL){
			if(aux->rg == rg_user){
				printf("\nNumero do cadastro: %d\n", aux->n_cadastro);
				printf("Nome: ");
				puts(aux->nome);
				printf("\n\nTem CERTEZA que deseja remover o cadastro? <1-SIM> <0-NAO>\n\n");
				scanf("%d", &esc);
				if(esc != 0){
					if(aux == inicio){
						inicio = inicio->proximo;
						free(aux);
					}
					else{
						if(aux->proximo == NULL){
							while(p->proximo != aux)
								p = p->proximo;
								p->proximo = NULL;
								free(aux);
						}
						else{
							pont = aux->proximo;
							while(p->proximo != aux)
								p = p->proximo;
							p->proximo = pont;
							free(aux);		
						}
					}
				}
			}
			aux = aux->proximo;
		}
	}
	return inicio;
}
int main()
{
	struct dados *pessoa = NULL;
	int caso, resp = 1, contador = 1;
	
	do{
		printf("#############################\n");
		printf("#   1 - Cadastrar Pessoa    #\n");
		printf("#   2 - Consultar Dados     #\n");
		printf("#   3 - Atualizar Dados     #\n");
		printf("#   4 - Remover Cadastro    #\n");
		printf("#   5 - Exibicao Especial   #\n");
		printf("#   6 - Sair                #\n");
		printf("#############################\n");
		scanf("%d", &caso);
		switch(caso){
			case 1:
				do{
					pessoa = inserir(pessoa, contador);
					if(pessoa == NULL)
						printf("Não foi possivel efetuar o cadastro\n");
					else{
					printf("\nCADASTRO EFETUADO COM SUCESSO!\n\n");
					contador++;
					printf("Deseja inserir um novo cadastro? <1-SIM> <0-NAO> \n");
					scanf("%d", &resp);		
					system("cls");
					}
				}while (resp != 0);
				break;
			case 2:
				system("cls");
				int sub;
				printf("\nQual o metodo de consulta: \n\n");
				printf("#############################\n");
				printf("#   1 - Por RG	     	    #\n");
				printf("#   2 - Por num de cadastro #\n");
				printf("#   3 - Por nome            #\n");
				printf("#############################\n");
				scanf("%d", &sub);
				switch(sub){
					case 1:
						int rg_dig;
						printf("Digite o RG: \n");
						scanf("%d", &rg_dig);				
						por_rg(pessoa, rg_dig);
						break;
					case 2:
						int cadastro;
						printf("Digite o numero de cadastro: \n");
						scanf("%d", &cadastro);
						por_cad(pessoa, cadastro);
						break;	
					case 3:
						char nome[30];
						printf("Digite seu nome: \n");
						fflush(stdin);
						gets(nome);
						por_nome(pessoa, nome);
						break;
					}
				break;
			case 3:
				int rg_dig2;
				printf("Digite o RG: \n");
				scanf("%d", &rg_dig2);				
				atualiza(pessoa, rg_dig2);				
				break;
			case 4:
				int rg_dig3;
				printf("Digite o RG: \n");
				scanf("%d", &rg_dig3);
				pessoa = remove(pessoa, rg_dig3);
				printf("\nCADASTRO REMOVIDO COM SUCESSO!\n\n");
				break;							
		}
	}while(caso != 6);
	system("pause");	
}
