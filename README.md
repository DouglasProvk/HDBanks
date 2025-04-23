# HDBanks
Simples "Sistema Bancário em C++"

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <locale.h> // bilbioteca de localização
#include <time.h>
 
// Globals
char login_user[100]; // usuario para logar
char login_pass[100]; // senha para logar
 
char read_user[100]; // login que usuario digitou
char read_pass[100]; // senha que o usuario digitou
 
// Prototipos (funções declaradas abaixo do MAIN())
void header();
 
 
void main(void)
{
	setlocale(LC_ALL, "PTBR"); // seta config de localização para PTBR (moeda, acentos etc...)
 
	int option = 0; // Guardara opções que o usuario escolher no menu
 
	while(option != 3)
	{
		header("MENU - BANK SYSTEM"); // mostra header estilizado
 
		printf("1. Cadastro\n");
		printf("2. Login\n");
		printf("3. Sair\n");
		printf("Digite a opcao: ");
 
		scanf("%i", &option); // aguarda o usuario digitar uma das opcoes do menu (Ler na variavel option)
 
		switch(option)
		{
			case 1:
				system("cls");
				header("CADASTRO - BANK SYSTEM");
				printf("Login para cadastro: ");
				scanf("%s", login_user);
				printf("Senha para cadastro: ");
				scanf("%s", login_pass);
			break;
 
			case 2:
				system("cls");
				header("LOGIN - BANK SYSTEM");
				printf("Login: ");
				scanf("%s", read_user);
				printf("Senha: ");
				scanf("%s", read_pass);
 
				if(strcmp(read_user, login_user) == 0 && strcmp(read_pass, login_pass) == 0)
				{
					printf("Logado com sucesso!\n");
					system("cls");
 
					// Titulo da Area de "usuario logado"
					char strTitleLogged[254] = "BANK SYSTEM - ";
 
					// Concatena com nome do usuario
					strcat(strTitleLogged, read_user);
 
					// Saldo da conta do usuario
					float balance = 0.0f;
 
					// opções do menu do usuario
					int option_user = 0;
					while(option_user != 4)
					{
						header(strTitleLogged); // mostra Cabeçalho personalizado
						// Menu
						printf("\nData :%s  |  Hora:%s\n",__DATE__,__TIME__);//data e hora en tempo real
						printf("1. Ver Saldo\n");
						printf("2. Sacar\n");
						printf("3. Depositar\n");
						printf("4. Sair\n");
						printf("Escolha uma opcoes: ");
						scanf("%i", &option_user); // Ler opções
 
						switch(option_user){
							case 1:
								system("cls");
								printf("Saldo atual: %1.f\n", balance); // mostra saldo
								break;
 
							case 2:
								system("cls");
								float cash_out; // Guardara valor a ser sacado
								printf("Valor a ser sacado: ");
								scanf("%f", &cash_out);
 
								if(cash_out <= balance) // sacar somente se houver saldo
								{
									system("cls");
									balance -= cash_out;
									printf("Saque realizado com sucesso.\n");
								}else
								{
									system("cls");
									printf("Valor especificado maior que o saldo Disponivel em conta.\n");
								}
								break;
							case 3:
								system("cls");
								float deposit = 0.0f;
								printf("Valor do Deposito: ");
								scanf("%f", &deposit);
 
								if(deposit > 0) // valor do Depósito obrigatoriamente maior que zero
								{
									balance += deposit;
									printf("Deposito realizado com sucesso.\n");
								}else
								{
									printf("Valor especificado e menor ou igual a zero. Repita a operacao!\n");
								}
								break;
						}
					}
				}else
				{
					printf("Falha :_(\n");
				}
			break;
		}// fim switch
 
	}// fim while
}// fim main
 
/*
   Mostra um Cabeçalho personalizado
*/
void header(char title[254])
{
	printf("==============[%s]==============\n\n", title);
}
