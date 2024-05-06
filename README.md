# Ex-12-IMPLEMENTATION OF HEAP STORAGE ALLOCATION STRATEGY
# NAME:Bharathi priyan T
# REGISTER NUMBER:212221040028
# Date :24.04.2024

# Aim :
To write a program to implement heap storage allocation strategy.
# ALGORITHM
1. Start the program.
2. Define a function create( ) to create a list of allocated node. This function returns a pointer to head of list.
3. Define a function display(node) to display the list of allocated nodes.
4. Define a function search(node,key) to search for the element in list.
5. Define a function insert(node) to insert element into the list.
6. Define a function get_prev(node,value) to look for the previous element in the list.
7. Define a function delete() to remove an element from the list.
8. Stop the program.
# PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>

#define TRUE 1
#define FALSE 0

typedef struct Heap {
    int data;
    struct Heap *next;
} node;

// Function prototypes
node *create();
void display(node *);
node *search(node *, int);
node *insert(node *);
void dele(node **);
node *get_node();
node *insert_head(node *);
node *insert_last(node *);
void insert_after(node *);

// Function definitions
void dele(node **head) {
    int key;
    node *temp = *head;
    node *prev = NULL;

    if (temp == NULL) {
        printf("\nThe list is empty\n");
        return;
    }

    printf("\nEnter the element you want to delete: ");
    scanf("%d", &key);

    temp = search(*head, key);
    if (temp != NULL) {
        prev = *head;

        if (prev->data == key) {
            *head = temp->next;
            free(temp);
        } else {
            while (prev->next != NULL && prev->next->data != key)
                prev = prev->next;

            if (prev->next != NULL) {
                temp = prev->next;
                prev->next = temp->next;
                free(temp);
            } else
                printf("\nThe element is not found in the list\n");
        }
    }
}

node *get_node() {
    node *temp = (node *)malloc(sizeof(node));
    if (temp == NULL) {
        printf("\nMemory allocation failed\n");
        exit(1);
    }
    temp->next = NULL;
    return temp;
}

node *create() {
    node *temp, *New, *head = NULL;
    int val;
    char ans = 'y';
    int flag = TRUE;

    do {
        printf("\nEnter the element: ");
        scanf("%d", &val);

        New = get_node();
        if (New == NULL) {
            printf("\nMemory allocation failed\n");
            exit(1);
        }

        New->data = val;
        New->next = NULL;

        if (flag == TRUE) {
            head = New;
            temp = head;
            flag = FALSE;
        } else {
            temp->next = New;
            temp = New;
        }

        printf("\nDo you want to enter more elements? (y/n): ");
        scanf(" %c", &ans);
    } while (ans == 'y' || ans == 'Y');

    printf("\nThe list is created\n");
    return head;
}

void display(node *head) {
    node *temp = head;

    if (temp == NULL) {
        printf("\nThe list is empty\n");
        return;
    }

    printf("\n");
    while (temp != NULL) {
        printf("%d ", temp->data);
        if (temp->next != NULL)
            printf("-> ");
        temp = temp->next;
    }
    printf("\n");
}

node *search(node *head, int key) {
    node *temp = head;

    if (temp == NULL) {
        printf("\nThe linked list is empty\n");
        return NULL;
    }

    while (temp != NULL) {
        if (temp->data == key) {
            printf("\nThe element is present in the list\nThe element is Deleted");
            return temp;
        }
        temp = temp->next;
    }

    printf("\nThe element is not present in the list\n");
    return NULL;
}

node *insert(node *head) {
    int choice;
    head = insert_head(head);
    head = insert_last(head);
    insert_after(head);
    return head;
}

node *insert_head(node *head) {
    int val;
    node *New = get_node();

    printf("\nEnter the element you want to insert: ");
    scanf("%d", &val);
    New->data = val;
    New->next = head;

    return New;
}

node *insert_last(node *head) {
    int val;
    node *New = get_node();
    node *temp = head;

    printf("\nEnter the element you want to insert: ");
    scanf("%d", &val);
    New->data = val;
    New->next = NULL;

    if (head == NULL)
        head = New;
    else {
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = New;
    }

    return head;
}

void insert_after(node *head) {
    int key;
    node *New = get_node();
    node *temp = head;

    printf("\nEnter the element after which you want to insert the node: ");
    scanf("%d", &key);

    while (temp != NULL) {
        if (temp->data == key) {
            printf("\nEnter the element you want to insert: ");
            scanf("%d", &New->data);
            New->next = temp->next;
            temp->next = New;
            return;
        }
        temp = temp->next;
    }

    printf("\nThe specified element is not found in the list\n");
}

int main() {
    int choice;
    node *head = NULL;

    do {
        printf("\nProgram to perform various operations on heap using dynamic memory management\n");
        printf("1. Create\n");
        printf("2. Display\n");
        printf("3. Insert an element in the list\n");
        printf("4. Delete an element from the list\n");
        printf("5. Quit\n");
        printf("Enter your choice (1-5): ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                head = create();
                break;
            case 2:
                display(head);
                break;
            case 3:
                head = insert(head);
                break;
            case 4:
                dele(&head);
                break;
            case 5:
                printf("Exiting the program...\n");
                exit(0);
            default:
                printf("Invalid choice, try again.\n");
        }
    } while (choice != 5);

    return 0;
}
```
# OUTPUT:
<img width="737" alt="1" src="https://github.com/manomadhivanan/Ex-12-IMPLEMENTATION-OF-HEAP-STORAGE-ALLOCATION-STRATEGY/assets/115543366/0e5cdcac-1045-4efb-98a1-0a7c7d5a45e9">
<img width="696" alt="2" src="https://github.com/manomadhivanan/Ex-12-IMPLEMENTATION-OF-HEAP-STORAGE-ALLOCATION-STRATEGY/assets/115543366/d8086e9b-6911-4777-ab87-19b2dda8c50c">
<img width="766" alt="3" src="https://github.com/manomadhivanan/Ex-12-IMPLEMENTATION-OF-HEAP-STORAGE-ALLOCATION-STRATEGY/assets/115543366/5e73ef62-67f0-44c4-bb15-a97549c5b2d8">

# RESULT:
The heap storage allocation strategy is implemented successfully, and the output is 
verified.
