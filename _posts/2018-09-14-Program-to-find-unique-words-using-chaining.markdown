---
layout: post
title:  "Program to find unique words using chaining"
date:   2018-09-14 16:33:42 +0530
categories: program chaining
---
Suppose we are given N words, find out the unique words, count the unique words

Input

N = 5

abc
abc
bca
def
qwerty

Output:
(Not in order)

abc
bca
def
qwerty

4

``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Node
{
	char word[50];
	struct Node *next;
};

// Hashing function => sum of letters (index 0 to 25) mod 10
// abc = ( 0 + 1 + 2 ) % mod 10  returns 3
int hashCode(char word[])
{
	int wlen = strlen(word), sum = 0;
	for (int i = 0; i < wlen; i++)
	{
		sum += word[i] - 'a';
	}

	return sum % 10;
}

struct Node *createNode(char word[])
{
	struct Node *new_node = (struct Node *)malloc(sizeof(struct Node));
	strcpy(new_node->word, word);
	new_node->next = NULL;
	return new_node;
}

void createHash(char word[], struct Node *ht[])
{
	int hashIndex = hashCode(word);
	if (ht[hashIndex] == NULL)
		ht[hashIndex] = createNode(word);
	else
	{
		struct Node *t = ht[hashIndex];
		while (t)
		{
			if (!strcmp(t->word, word))
				return;
			t = t->next;
		}
		struct Node *temp = ht[hashIndex];
		ht[hashIndex] = createNode(word);
		ht[hashIndex]->next = temp;
	}
}
//Printing Linked list
void printLL(struct Node *head)
{
	struct Node *temp = head;
	while (temp)
	{
		printf("%s -> ", temp->word);
		temp = temp->next;
	}
	printf("NULL");
}

//Printing the node content
void printLLContent(struct Node *head)
{
	struct Node *temp = head;
	while (temp)
	{
		printf("%s ", temp->word);
		temp = temp->next;
	}
}

//Printing the hashTable
void printTable(struct Node *ht[])
{
	printf("\nPrinting Table(Chaining) : \nMemory\tLinkedList\n");
	for (int i = 0; i < 10; i++)
	{
		printf("%p ", ht[i]);
		printLL(ht[i]);
		printf("\n");
	}
}
//Printing the Unique words in hashTable
void printUnique(struct Node *ht[])
{
	printf("\nPrinting Unique words : \n");
	for (int i = 0; i < 10; i++)
	{
		printLLContent(ht[i]);
	}
}

//Counting the nodes in Linked list
int countList(struct Node *head)
{
	struct Node *temp = head;
	int countL = 0;
	while (temp)
	{
		countL++;
		temp = temp->next;
	}

	return countL;
}

void countUnique(struct Node *ht[])
{
	int count = 0;
	for (int i = 0; i < 10; i++)
	{
		count += countList(ht[i]);
	}
	printf("\nNumber of Unique words : %d\n", count);
}

int main()
{
	int n;
	printf("Enter no of words : \n");
	scanf("%d", &n);
	//Hash Table
	//Array of pointers to structure of size 10
	//All are NULL initially
	struct Node *hashTable[10] = {NULL};

	for (int i = 0; i < n; i++)
	{
		char word[50];
		scanf("%s", word);
		createHash(word, hashTable);
	}

	printTable(hashTable);
	printUnique(hashTable);
	countUnique(hashTable);
}

```

<pre>
Output:

Enter no of words : 
10
abc
def
abc
def
qwerty
hello
hi
hello 
samehash
hashsame

Printing Table(Chaining) : 
Memory	LinkedList
(nil) NULL
(nil) NULL
0x558e62f59b20 qwerty -> def -> NULL
0x558e62f59a80 abc -> NULL
(nil) NULL
0x558e62f59bc0 hi -> NULL
0x558e62f59c60 hashsame -> samehash -> NULL
0x558e62f59b70 hello -> NULL
(nil) NULL
(nil) NULL

Printing Unique words : 
qwerty def abc hi hashsame samehash hello 
Number of Unique words : 7

</pre>