---
layout: post
title:  "Program to find successive unique words using hashing (chaining)"
date:   2018-09-14 16:55:42 +0530
categories: program chaining
---

``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
    
struct Node
{
	char word[50];
	struct Node *next;
};

// Hashing function => sum of power of letters (index 0 to 25) with their position mod 10
// abc = ( 0^1 + 1^2 + 2^3 ) % mod 10  returns 9
int hashCode(char word[])
{
	int wlen = strlen(word), sum = 0;
	for (int i = 0; i < wlen; i++)
	{
		int t = word[i] - 'a';
		sum += pow(t, i+1);
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

/*
	Start from the second word and insert into hashIndex of previous word if it is NULL return 1
	and if it is not NULL, search in the linked list. If word is found return 0
	otherwise return 1 
	*/
int createHash(char firstWord[], char secondWord[], struct Node *ht[])
{
	int hashIndex = hashCode(firstWord);
	if (ht[hashIndex] == NULL)
	{
		ht[hashIndex] = createNode(secondWord);
		return 1;
	}
	else
	{
		struct Node *t = ht[hashIndex];
		while (t)
		{
			//if present return 0
			if (!strcmp(t->word, secondWord))
				return 0;
			t = t->next;
		}
		//if it is not present insert into hashTable
		struct Node *temp = ht[hashIndex];
		ht[hashIndex] = createNode(secondWord);
		ht[hashIndex]->next = temp;
	}
	return 1;
}

void printTable(struct Node *ht[])
{
	for (int i = 0; i < 10; i++)
	{
		printf("%p\n", ht[i]);
	}
}

int main()
{
	int n;
	scanf("%d", &n);
	struct Node *hashTable[10] = {NULL};
	int count = 0;
	char word[n][50];
	for (int i = 0; i < n; i++)
	{
		scanf("%s", word[i]);
	}

	for (int i = 1; i < n; i++)
	{
		count += createHash(word[i - 1], word[i], hashTable);
	}

	printf("%d", count);
	//printTable(hashTable);
}
```

<pre>
Input:

5
abc
def
abc
def
qwerty

Output:
3 
(abc,def), (def, abc), (def,qwerty)

(abc, def) is repeated so we won't count it
</pre>