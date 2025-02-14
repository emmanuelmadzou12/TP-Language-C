#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

typedef struct Node
{
    int data;
    struct Node* next;
}
Node;

typedef struct 
{
 Node* head;
}
LinkedList;
// Initialisation de la liste chainee
void initList(LinkedList* list)
{
    list->head = NULL;
}

Node* createNode(int data)
{
    Node* nouveauNode = (Node*)malloc(sizeof(Node));
    if (!nouveauNode) 
    {
        printf("Erreur d'allocation memoire !\n");
        exit(EXIT_FAILURE);
    }
    nouveauNode->data = data;
    nouveauNode->next = NULL;
    return nouveauNode;
}

// Insertion en tete
void insertAtHead(LinkedList* list, int data)
{
    Node* nouveauNode = createNode(data);
    nouveauNode->next = list->head;
    list->head = nouveauNode;
}

// Insertion en queue
void insertAtTail(LinkedList* list, int data)
{
    Node* nouveauNode = createNode(data);
    if (!list->head) {
        list->head = nouveauNode;
        return;
    }
    Node* temp = list->head;
    while (temp->next)
        temp = temp->next;
    temp->next = nouveauNode;
}
// insertion en position specifique 
void insertAtPosition(LinkedList* list, int data, int position)
{
    if (position < 0)
    {
        printf("Position invalide !\n");
        return;
    }
    if (position == 0)
    {
        insertAtHead(list, data);
        return;
    }
    Node* nouveauNode = createNode(data);
    Node* temp = list->head;
    for (int i = 0; temp && i < position - 1; i++) 
    {
        temp = temp->next;
    }
    if (!temp) {
        printf("Position hors limites !\n");
        free(nouveauNode);
        return;
    }
    nouveauNode->next = temp->next;
    temp->next = nouveauNode;
}
//suppression d'element 
void deleteNode(LinkedList* list, int key)
{
    Node* temp = list->head;
    Node* prev = NULL;
    while (temp && temp->data != key) 
    {
        prev = temp;
        temp = temp->next;
    }
    if (!temp)
    {
        printf("Element non trouve !\n");
        return;
    }
    if (!prev)
        list->head = temp->next;
    else
        prev->next = temp->next;
    free(temp);
}
//recherche d'un element
Node* recherche(LinkedList* list, int key)
{
    Node* temp = list->head;
    while(temp) 
        {
            if (temp->data == key)
                return temp;
            temp = temp->next;
        }
    return NULL;
}
// affiche le contenu de la liste 
void printfList(LinkedList* list)
{
    Node* temp = list->head;
    while (temp)
        {
         printf("%d ->", temp->data);
         temp = temp->next;
        }
    printf("NULL\n");
}
void deleteList(LinkedList* list)
{
    Node* temp = list->head;
    while (temp)
        {
         Node* next = temp->next;
         temp = next;
         free(temp);
        }
     list->head = NULL;
}

               

int main()
{
    
    return 0;
}



