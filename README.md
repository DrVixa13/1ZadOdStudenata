# 1ZadOdStudenata
""" Studenti """


#include <stdio.h>


struct Student
{
    int indeks;
    char ime[30];
    float ocena;
};


void quick_sort(struct Student *array, int start, int end)
{
    if (start < end){
        int i;
        int index = start;
        struct Student temp;

        for (i=start; i<end; i++)
        {
            if (array[i].ocena >= array[end].ocena)
            {
                temp = array[i];
                array[i] = array[index];
                array[index] = temp;
                index++;
            }
        }
        temp = array[index];
        array[index] = array[end];
        array[end] = temp;


        quick_sort(array, start, index-1);
        quick_sort(array, index+1, end);
    }
}





              int Search(struct Student *root, int indeks, int n) {

    int i;

    for(i=0; i<n; i++)

    {

	if(indeks == root[i].indeks)

	{

		return i;

	}



    }

    return -1;

}


int main()
{
   struct Student *ptr;
   int i, n, trazeni;
   float ocena = 0;
   printf("Unesi broj studenata: ");
   scanf("%d", &n);

   ptr=(struct Student*)malloc(n*sizeof(struct Student));

   for(i=0; i<n; ++i){
        printf("Unesi broj indeksa za %d. studenta:\n", i+1);
        scanf("%d", &(ptr+i)->indeks);
        printf("Unesi ime za %d. studenta:\n", i+1);
        scanf(" %[^\n]s", &(ptr+i)->ime);
        printf("Unesi prosecnu ocenu %d. studenta:\n", i+1);
        scanf("%f", &(ptr+i)->ocena);
        ocena = ocena +  (ptr+i)->ocena;
   }


// A) PROSECNA OCENA
    printf("\n\n");
    printf("Prosecna ocena: %f \n", ocena / n);

// B) SORTIRANI CLANOVI
    printf("\n\n");
    //selection_sort(n, ptr);
    quick_sort(ptr, 0, n-1);

   printf("Studenti sortirani po oceni:\n");
   for(i=0;i<n;++i)
       printf("%d\t%s\t%f\n",(ptr+i)->indeks, (ptr+i)->ime, (ptr+i)->ocena);

// C) PRETRAGA PO BIN STABLU - treba da se sredi
    printf("\n\n");
    printf("Potrazi studenta po broju indeksa:\n");
    scanf("%d", &trazeni);
    int p = Search(ptr, trazeni, n);
    printf("P: %d", p);
    if(p != -1)
    {
        printf("%d\t%s\t%f\n",(ptr+p)->indeks, (ptr+p)->ime, (ptr+p)->ocena);
    }
    return 0;
}

""" Bubble sort 2 dobar """

#include <stdafx.h>
#include <stdlib.h>
#include <stdio.h>
#include <vector>
#include <iostream>

using namespace std;

int pretrazivanje(int n, int a[], int br);

double srednja_vrednost(int n, int a[]);

void swap(int *xp, int *yp)
{
	int temp = *xp;
	*xp = *yp;
	*yp = temp;
}


void bubbleSort(int arr[], int n)
{
	int i, j;
	for (i = 0; i < n - 1; i++)

	for (j = 0; j < n - i - 1; j++)
	if (arr[j] > arr[j + 1])
		swap(&arr[j], &arr[j + 1]);
}


void printArray(int arr[], int size)
{
	int i;
	for (i = 0; i < size; i++)
		printf("%d ", arr[i]);
	printf("\n");
}


void main()
{
	int n = 11;
	int arr[] = { 4, 16, 18, 3, 12, 19, 22, 143, 6, 7, 15, };
	int arr_size = sizeof(arr) / sizeof(arr[0]);


	printf("Dat je niz brojeva \n");
	printArray(arr, arr_size);

	bubbleSort(arr, arr_size);

	printf("\nSortirani niz brojeva izgleda ovako \n");
	printArray(arr, arr_size);

	std::cin.get();
	{
	//srednja vrednost//
	cout << "Srednja vrednost niza je: " << srednja_vrednost(n, arr) << endl;
	std::cin.get();
	}

	//pretrazivanje//
	{
		int te;

		cout << "Unesite broj koji hocete da proverite da li se nalazi u nizu: " << endl;
		cin >> te;

		int m = pretrazivanje(n, arr, te);
		if (m == -1){
			cout << "Broj se ne nalazi u ovom nizu." << endl;
		}
		else{
			cout << "Broj " << te << " postoji i nalazi se na mestu " << m + 1 << " u nizu" << endl;
			std::cin.get();
		}
		std::cin.get();
	
	}

}

double srednja_vrednost(int n, int a[]) {
	int zbir = 0;
	for (int i = 0; i < n; i++) {
		zbir = zbir + a[i];
	}

	return zbir / (double)n;
}

int pretrazivanje(int n, int a[], int br){
	for (int i = 0; i < n; i++){
		if (a[i] == br) return i;

	}
	return -1;
}
  
""" Merge sort 2 dobar"""
  

#include<stdlib.h>
#include<stdio.h>
#include <vector>
#include <iostream>

using namespace std;

int sekvencijalno_pretrazivanje(int n, int a[], int br);

double srednja_vrednost(int n, int a[]);

void merge(int arr[], int l, int m, int r)
{
	int i, j, k;
	int n1 = m - l + 1;
	int n2 = r - m;



	vector<int> L(n1);
	vector<int> R(n2);


	for (i = 0; i < n1; i++)
		L[i] = arr[l + i];
	for (j = 0; j < n2; j++)
		R[j] = arr[m + 1 + j];


	i = 0;
	j = 0;
	k = l;
	while (i < n1 && j < n2)
	{
		if (L[i] <= R[j])
		{
			arr[k] = L[i];
			i++;
		}
		else
		{
			arr[k] = R[j];
			j++;
		}
		k++;
	}

	while (i < n1)
	{
		arr[k] = L[i];
		i++;
		k++;
	}

	while (j < n2)
	{
		arr[k] = R[j];
		j++;
		k++;
	}
}

void mergeSort(int arr[], int l, int r)
{
	if (l < r)
	{

		int m = l + (r - l) / 2;


		mergeSort(arr, l, m);
		mergeSort(arr, m + 1, r);

		merge(arr, l, m, r);
	}
}

void printArray(int A[], int size)
{
	int i;
	for (i = 0; i < size; i++)
		printf("%d ", A[i]);
	printf("\n");
}


void main()
{
	int n = 11;
	int arr[] = { 56, 98, 23, 1, 22, 33, 6, 94, 3, 2, 34 };
	int arr_size = sizeof(arr) / sizeof(arr[0]);

	printf("Dat je niz brojeva \n");
	printArray(arr, arr_size);

	mergeSort(arr, 0, arr_size - 1);

	printf("\nSortirani niz brojeva izgleda ovako \n");
	printArray(arr, arr_size);

	//pretrazivanje//
	{
		int te;

		cout << "Unesite broj koji hocete da proverite da li se nalazi u nizu: " << endl;
		cin >> te;

		int m = sekvencijalno_pretrazivanje(n, arr, te);
		if (m == -1){
			cout << "Broj se ne nalazi u ovom nizu." << endl;
		}
		else{
			cout << "Broj " << te << " postoji i nalazi se na mestu " << m+1 << " u nizu" << endl;
		}

		cout << "Srednja vrednost niza je: " << srednja_vrednost(n, arr) << endl;
	}
	std::cin.get();

}

double srednja_vrednost(int n, int a[]) {
	int zbir = 0;
	for (int i = 0; i < n; i++) {
		zbir = zbir + a[i];
	}

	return zbir / (double)n;
}

int sekvencijalno_pretrazivanje(int n, int a[], int br){
	for (int i = 0; i < n; i++){
		if (a[i] == br) return i;

	}
	return -1;
}
  
""" Prvi zadatak """
  
#include <stdio.h>
#include <stdlib.h>

void bubble_sort(int n,int niz[]){
    int i,j,k;
    for (i=n-1;i>0; i--)
      for(j=0;j<i;j++)
         if (niz[j] > niz[j+1]){
            k=niz[j];
            niz[j]=niz[j+1];
        niz[j+1]=k;
        }
}


int srednja_vrednost(int n,int niz[])
{
    int i,suma;
    float sv;
    suma=0;
    for (i=0;i<n;i++)
        suma+=niz[i];
    sv=suma/12; 
    return sv;
}

void stampaj(int n,int niz[]){
    int i,j;
    for(i=0;i<n;i++)
        printf("%d,", niz[i]);
}



int main()
{   
    
    int n=12,i;
    int niz[12]={134,6,8,12,23,19,12,343,16,194,23,12};
    int traz_broj;
    float as;
    bubble_sort(n,niz);
    as=srednja_vrednost(n,niz);
    stampaj(n,niz);
    printf("\nSrednja vrednost je %f\n",as);
    printf("Unesi trazeni broj:\n");
    scanf("%d",&traz_broj);
    for (i=0;i<n;i++){
        if (niz[i]==traz_broj)
            printf("Indeks trazenog broja nakon sortiranja je %d",i);}
            

    return 0;
}

""" Quic sort dobar """

#include <stdafx.h>
#include <stdlib.h>
#include <stdio.h>
#include <vector>
#include <iostream>

using namespace std;

int pretrazivanje(int n, int a[], int br);

double srednja_vrednost(int n, int a[]);

void swap(int* a, int* b)
{
	int t = *a;
	*a = *b;
	*b = t;
}


int partition(int arr[], int low, int high)
{
	int pivot = arr[high];    
	int i = (low - 1);  
	for (int j = low; j <= high - 1; j++)
	{
		if (arr[j] <= pivot)
		{
			i++;    
			swap(&arr[i], &arr[j]);
		}
	}
	swap(&arr[i + 1], &arr[high]);
	return (i + 1);
}

void quickSort(int arr[], int low, int high)
{
	if (low < high)
	{
		int pi = partition(arr, low, high);
		quickSort(arr, low, pi - 1);
		quickSort(arr, pi + 1, high);
	}
}


void printArray(int arr[], int size)
{
	int i;
	for (i = 0; i < size; i++)
		printf("%d ", arr[i]);
	printf("\n");
}


void main()
{
	int n = 10;
	int arr[] = { 56, 98, 2, 3, 9, 1125, 343, 4, 94, 34 };
	int arr_size = sizeof(arr) / sizeof(arr[0]);


	printf("Dat je niz brojeva \n");
	printArray(arr, arr_size);

	quickSort(arr, 0, arr_size-1);

	printf("\nSortirani niz brojeva izgleda ovako \n");
	printArray(arr, arr_size);

	std::cin.get();
	{
	//srednja vrednost//
	cout << "Srednja vrednost niza je: " << srednja_vrednost(n, arr) << endl;
	std::cin.get();
	}

	//pretrazivanje//
	{
		int te;

		cout << "Unesite broj koji hocete da proverite da li se nalazi u nizu: " << endl;
		cin >> te;

		int m = pretrazivanje(n, arr, te);
		if (m == -1){
			cout << "Broj se ne nalazi u ovom nizu." << endl;
		}
		else{
			cout << "Broj " << te << " postoji i nalazi se na mestu " << m + 1 << " u nizu" << endl;
			std::cin.get();
		}
		std::cin.get();
	
	}

}

double srednja_vrednost(int n, int a[]) {
	int zbir = 0;
	for (int i = 0; i < n; i++) {
		zbir = zbir + a[i];
	}

	return zbir / (double)n;
}

int pretrazivanje(int n, int a[], int br){
	for (int i = 0; i < n; i++){
		if (a[i] == br) return i;

	}
	return -1;
}
  
""" Studenti dobar 2"""
  
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>

//Tip podatka "Student" koji se sastoji od broja indeka(int), imena(char[30]) i prosecne ocene(float)
struct Student{
	int brIndeksa;
	char ime[30];
	float prosecnaOcena;
};

//Metoda koja racuna prosecnu ocenu iz niza
float prosecnaOcena(struct Student *niz, int n){
	float proOcena = 0;

	for (int i = 0; i<n; i++){
		proOcena += niz[i].prosecnaOcena;
	}
	proOcena /= n;
	return proOcena;
}


//Metoda za brzo sortiranje
void quicksort(struct Student *niz, int first, int last){
	int pivot, j, i;
	Student temp;

	if (first<last){
		pivot = first;
		i = first;
		j = last;

		while (i<j){
			while (niz[i].prosecnaOcena >= niz[pivot].prosecnaOcena&&i<last)
				i++;
			while (niz[j].prosecnaOcena<niz[pivot].prosecnaOcena)
				j--;
			if (i<j){
				temp = niz[i];
				niz[i] = niz[j];
				niz[j] = temp;
			}
		}

		temp = niz[pivot];
		niz[pivot] = niz[j];
		niz[j] = temp;
		quicksort(niz, first, j - 1);
		quicksort(niz, j + 1, last);

	}
}


//Definisanje tipa stablo
struct bin_stablo {
	Student data;
	struct bin_stablo * right, *left;
};
typedef struct bin_stablo cvor;

//Metoda za ubacivanje studenata u stablu
void ubaci(cvor ** drvo, Student val)
{
	cvor *temp = NULL;
	if (!(*drvo))
	{
		temp = (cvor *)malloc(sizeof(cvor));
		temp->left = temp->right = NULL;
		temp->data = val;
		*drvo = temp;
		return;
	}

	if (val.brIndeksa < (*drvo)->data.brIndeksa)
	{
		ubaci(&(*drvo)->left, val);
	}
	else if (val.brIndeksa >(*drvo)->data.brIndeksa)
	{
		ubaci(&(*drvo)->right, val);
	}

}

//Metoda za pretragu studenta po stablu
cvor* pretraga(cvor ** drvo, int val)
{
	if (!(*drvo))
	{
		return NULL;
	}

	if (val < (*drvo)->data.brIndeksa)
	{
		pretraga(&((*drvo)->left), val);
	}
	else if (val >(*drvo)->data.brIndeksa)
	{
		pretraga(&((*drvo)->right), val);
	}
	else if (val == (*drvo)->data.brIndeksa)
	{
		return *drvo;
	}
}


//Glavni program
void main(){

	//Deklaracija promenljivih koje se unose sa tastature
	char ponavljanje = 'p';
	char slovo;
	int a = 0;
	char b[30] = "";
	float c = 0;
	int indeksPretraga;

	//Deklaracija podatka tipa "Student",niza i stabla
	Student student;
	struct Student *nizA;
	cvor *root;
	cvor *tmp;

	//Deklaracija promenljive tipa "int" koja se unosi sa tastature i pretstavlja ukupan broj studenata
	int brSt;
	printf("Unesi broj studenata: ");
	scanf("%d", &brSt);

	//Inicijalizacija dimenzije niza
	nizA = (Student*)malloc(sizeof(struct Student)*brSt);

	//Unosenje podataka
	for (int i = 0; i<brSt; i++){
		printf("\n\nStudent %d\n\n", i + 1);
		printf("\nUnesi broj indeksa: ");
		scanf("%d", &student.brIndeksa);
		printf("\nUnesi ime studenta: ");
		scanf("%s", &student.ime);
		printf("\nUnesi prosecnu ocenu: ");
		scanf("%f", &student.prosecnaOcena);

		nizA[i] = student;
	}
	printf("\n\n_________________________________________");

	//Stampanje unetog niza na ekranu
	printf("\n\nUneti su studenti:\n");
	for (int i = 0; i<brSt; i++){
		printf("\nBroj indeksa: %d, ime: %s, prosecna ocena: %.2f\n", nizA[i].brIndeksa, nizA[i].ime, nizA[i].prosecnaOcena);
	}

	//Stampanje prosecne ocene zaokruzene na dve decimale
	printf("\n\n_________________________________________");
	printf("\n\nProsecna ocena je: %.2f", prosecnaOcena(nizA, brSt));

	//Kreiranje stabla sa unetim studentima
	root = NULL;
	for (int i = 0; i<brSt; i++){
		ubaci(&root, nizA[i]);
	}

	//Sortiranje niza
	quicksort(nizA, 0, brSt - 1);

	//Stampanje sortiranog niza
	printf("\n_________________________________________");
	printf("\n\n\nSortiran niz: \n");
	for (int i = 0; i<brSt; i++){
		printf("\nBroj indeksa: %d, ime: %s, prosecna ocena: %.2f\n", nizA[i].brIndeksa, nizA[i].ime, nizA[i].prosecnaOcena);
	}
	printf("\n\n_________________________________________");

	//Unosenje broja indeksa i njegova pretraga u stablu
	while (ponavljanje == 'p' || ponavljanje == 'P'){
		printf("\n\n\nUnesi indeks za pretrazivanje: ");
		scanf("%d", &indeksPretraga);
		tmp = pretraga(&root, indeksPretraga);
		if (tmp)
		{
			printf("\nTrazeni student je: %s, sa prosecnom ocenom: %.2f\n\n", tmp->data.ime, tmp->data.prosecnaOcena);
		}
		else
		{
			printf("\nTrazeni student nije pronadjen.\n\n");
		}

		printf("\nZa ponovnu pretragu unesi slovo 'p' i pretisni enter: ");
		slovo = getchar();
		ponavljanje = getchar();

	}
}

                       
                       
