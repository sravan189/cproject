# cproject
first project
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
};

struct node* head = NULL;

// Create initial list
void createList() {
    struct node* newnode, *temp;
    int choice = 1;

    while (choice) {
        newnode = (struct node*)malloc(sizeof(struct node));
        if (newnode == NULL) {
            printf("Memory allocation failed\n");
            return;
        }

        printf("Enter data: ");
        scanf("%d", &newnode->data);
        newnode->next = NULL;

        if (head == NULL) {
            head = temp = newnode;
        } else {
            temp->next = newnode;
            temp = newnode;
        }

        printf("Do you want to continue adding nodes? (1 = Yes / 0 = No): ");
        scanf("%d", &choice);
    }
}

// Insert at beginning
void insertAtBeginning() {
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    if (newnode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    printf("Enter data: ");
    scanf("%d", &newnode->data);
    newnode->next = head;
    head = newnode;
}

// Insert at end
void insertAtEnd() {
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    if (newnode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    printf("Enter data: ");
    scanf("%d", &newnode->data);
    newnode->next = NULL;

    if (head == NULL) {
        head = newnode;
    } else {
        struct node* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newnode;
    }
}

// Insert at specific position
void insertAtPosition() {
    int pos, i = 0;
    printf("Enter position to insert after (starting from 0): ");
    scanf("%d", &pos);

    struct node* temp = head;
    while (temp != NULL && i < pos) {
        temp = temp->next;
        i++;
    }

    if (temp == NULL) {
        printf("Invalid position\n");
        return;
    }

    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    if (newnode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }

    printf("Enter data: ");
    scanf("%d", &newnode->data);
    newnode->next = temp->next;
    temp->next = newnode;
}

// Delete from beginning
void deleteFromBeginning() {
    struct node* temp;
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }
    temp = head;
    head = head->next;
    free(temp);
    printf("Node deleted from beginning.\n");
}

// Delete from end
void deleteFromEnd()
 {
    struct node *temp, *prevnode;

    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }

    temp = head;

    if (temp->next == NULL) {
        head = NULL;
        free(temp);
        printf("Last node deleted.\n");
        return;
    }

    while (temp->next != NULL) {
        prevnode = temp;
        temp = temp->next;
    }

    prevnode->next = NULL;
    free(temp);
    printf("Node deleted from end.\n");
}

// Delete from a specific position
void deleteFromPosition() {
    struct node *temp, *nextnode;
    int pos, i = 1;

    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }

    printf("Enter position to delete (starting from 1): ");
    scanf("%d", &pos);

    temp = head;

    if (pos == 1) {
        head = head->next;
        free(temp);
        printf("Node deleted from position 1.\n");
        return;
    }

    while (i < pos - 1 && temp != NULL) {
        temp = temp->next;
        i++;
    }

    if (temp == NULL || temp->next == NULL) {
        printf("Invalid position.\n");
        return;
    }

    nextnode = temp->next;
    temp->next = nextnode->next;
    free(nextnode);
    printf("Node deleted from position %d.\n", pos);
}

// Display linked list
void display() {
    struct node* temp = head;
    if (temp == NULL) {
        printf("List is empty.\n");
        return;
    }

    printf("Linked List: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

// Main menu
int main() {
    int choice;

    do {
        printf("\n--- Singly Linked List Menu ---\n");
        printf("1. Create List\n2. Insert at Beginning\n3. Insert at End\n4. Insert at Position\n");
        printf("5. Delete from Beginning\n6. Delete from End\n7. Delete from Position\n");
        printf("8. Display List\n9. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: createList(); break;
            case 2: insertAtBeginning(); break;
            case 3: insertAtEnd(); break;
            case 4: insertAtPosition(); break;
            case 5: deleteFromBeginning(); break;
            case 6: deleteFromEnd(); break;
            case 7: deleteFromPosition(); break;
            case 8: display(); break;
            case 9: printf("Exiting...\n"); break;
            default: printf("Invalid choice. Try again.\n");
        }
    } while (choice != 9);

    return 0;
}
