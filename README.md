//============================================================================
// Name        : QuickSelect.cpp
// Author      : Filipe
// Version     :
// Copyright   : Your copyright notice
// Description : Hello World in C++, Ansi-style
//============================================================================

#include <iostream>
#include <cstdlib>

using namespace std;

// realiza a troca entre dois elementos
void troca(int v[], int i, int j) {
	int aux = v[i];
	v[i] = v[j];
	v[j] = aux;
}

// retorna o índice do pivot (mesma função do quicksort)
int particiona(int v[], int inicio, int fim) {
	int pivot, pivot_indice, i;

	// o pivot é sempre o último elemento
	pivot = v[fim];

	pivot_indice = inicio;

	for (i = inicio; i < fim; i++) {
		// verifica se o elemento é <= ao pivot
		if (v[i] <= pivot) {
			troca(v, i, pivot_indice);
			pivot_indice++;
		}
	}

	// troca o pivot
	troca(v, pivot_indice, fim);

	return pivot_indice;
}

// retorna o k-ésimo menor elemento de um vor não ordenado
int seleciona(int v[], int inicio, int fim, int k) {
	int indice_pivot = particiona(v, inicio, fim);

	if (indice_pivot == (k - 1))
		return v[indice_pivot];
	else if (indice_pivot > (k - 1))
		return seleciona(v, inicio, indice_pivot - 1, k);

	return seleciona(v, indice_pivot + 1, fim, k);
}

int main(int argc, char *argv[]) {
	int* v = new int[2]; //Meu array onde sera adicionado valores
	int v_size = 2; // Tamanho do meu array
	int contador = 0; // Conta quantos valores foram adicionados
	int entrada; // Valor inserido

	while (cin >> entrada) {
		//Leio da entrada enquanto receber inteiros

		if (contador == v_size) {
			//Overflow
			int *novoVetor = new int[v_size * 2];

			for (int i = 0; i < v_size; i++) {
				novoVetor[i] = v[i];
			}
			v_size *= 2;

			v = novoVetor;
		}

		//Adiciono o valor ao vetor
		v[contador] = entrada;
		contador++;
	}

	int k = atoi(argv[2]);

	cout << seleciona(v, 0, contador-1, k+1) <<endl;

	return 0;
}
