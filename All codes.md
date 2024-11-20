```c
// 🚀 Arrays and sorting

#include <stdio.h>
#include <stdlib.h>

int linearSearch(int *array, int size, int target) {
  for (int i = 0; i < size; i++) {
    if (array[i] == target) return 1;
  }

  return 0;
}

int binarySearch(int *array, int low, int high, int target) {
  if (low > high) return 0;

  int mid = (low + high) / 2;

  if (array[mid] == target) {
    return 1;
  } else if (array[mid] < target) {
    return binarySearch(array, mid + 1, high, target);
  } else {
    return binarySearch(array, low, mid - 1, target);
  }
}

void bubbleSort(int *array, int size) {
  for (int i = 0; i < size - 1; i++) {
    for (int j = 0; j < size - i - 1; j++) {
      if (array[j] > array[j + 1]) {
        int temp = array[j];
        array[j] = array[j + 1];
        array[j + 1] = temp;
      }
    }
  }
}

void insertionSort(int *array, int size) {
  for (int i = 1; i < size; i++) {
    int key = array[i];
    int j = i - 1;
    while (j >= 0 && array[j] > key) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = key;
  }
}

void selectionSort(int *array, int size) {
  for (int i = 0; i < size - 1; i++) {
    int minIndex = i;
    for (int j = i + 1; j < size; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j;
      }
    }
    int temp = array[minIndex];
    array[minIndex] = array[i];
    array[i] = temp;
  }
}

void merge(int *array, int low, int mid, int high) {
  int n1 = mid - low + 1;
  int n2 = high - mid;

  int left[n1], right[n2];
  for (int i = 0; i < n1; i++) left[i] = array[low + i];
  for (int i = 0; i < n2; i++) right[i] = array[mid + 1 + i];

  int i = 0, j = 0, k = low;
  while (i < n1 && j < n2) {
    if (left[i] <= right[j]) array[k++] = left[i++];
    else array[k++] = right[j++];
  }

  while (i < n1) array[k++] = left[i++];
  while (j < n2) array[k++] = right[j++];
}

void mergeSort(int *array, int low, int high) {
  if (low < high) {
    int mid = (low + high) / 2;
    mergeSort(array, low, mid);
    mergeSort(array, mid + 1, high);
    merge(array, low, mid, high);
  }
}

int partition(int *array, int low, int high) {
  int pivot = array[high];
  int i = low - 1;

  for (int j = low; j < high; j++) {
    if (array[j] < pivot) {
      i++;
      int temp = array[i];
      array[i] = array[j];
      array[j] = temp;
    }
  }

  int temp = array[i + 1];
  array[i + 1] = array[high];
  array[high] = temp;

  return i + 1;
}

void quickSort(int *array, int low, int high) {
  if (low < high) {
    int pi = partition(array, low, high);
    quickSort(array, low, pi - 1);
    quickSort(array, pi + 1, high);
  }
}

void printArray(int *array, int size) {
  for (int i = 0; i < size; i++) {
    printf("%d ", array[i]);
  }
  printf("\n");
}

int main() {
  int array[] = {64, 34, 25, 12, 22, 11, 90};
  int size = sizeof(array) / sizeof(array[0]);

  quickSort(array, 0, size - 1);

  printf("Sorted array: ");
  printArray(array, size);

  return 0;
}

// 🚀 Queue

#include <stdio.h>
#define MAX 100

int queue[MAX];
int front = -1, rear = -1;

int isQueueFull() {
  return rear == MAX - 1;
}

int isQueueEmpty() {
  return front == -1 || front > rear;
}

void enqueue(int value) {
  if (isQueueFull()) {
    printf("Queue Overflow\n");
    return;
  }
  if (front == -1) front = 0;
  queue[++rear] = value;
}

int dequeue() {
  if (isQueueEmpty()) {
    printf("Queue Underflow\n");
    return -1;
  }
  return queue[front++];
}

void displayQueue() {
  if (isQueueEmpty()) {
    printf("Queue is empty\n");
    return;
  }
  for (int i = front; i <= rear; i++) {
    printf("%d ", queue[i]);
  }
  printf("\n");
}

int main() {
  enqueue(30);
  enqueue(40);
  displayQueue();
  dequeue();
  displayQueue();

  return 0;
}

// 🚀 Stack

#include <stdio.h>
#define MAX 100

int stack[MAX];
int top = -1;

int isStackFull() {
  return top == MAX - 1;
}

int isStackEmpty() {
  return top == -1;
}

void push(int value) {
  if (isStackFull()) {
    printf("Stack Overflow\n");
    return;
  }
  stack[++top] = value;
}

int pop() {
  if (isStackEmpty()) {
    printf("Stack Underflow\n");
    return -1;
  }
  return stack[top--];
}

void displayStack() {
  if (isStackEmpty()) {
    printf("Stack is empty\n");
    return;
  }
  for (int i = top; i >= 0; i--) {
    printf("%d ", stack[i]);
  }
  printf("\n");
}

int main() {
  push(10);
  push(20);
  displayStack();
  pop();
  displayStack();

  return 0;
}

// 🚀 Double Ended Queue

#include <stdio.h>
#define MAX 100

int deque[MAX];
int front = -1, rear = -1;

int isDequeFull() {
  return rear == MAX - 1;
}

int isDequeEmpty() {
  return front == -1 || front > rear;
}

void insertFront(int value) {
  if (front == 0) {
    printf("Deque Overflow at Front\n");
    return;
  }
  if (isDequeEmpty()) {
    front = 0;
    rear = 0;
  } else {
    front--;
  }
  deque[front] = value;
}

void insertRear(int value) {
  if (isDequeFull()) {
    printf("Deque Overflow at Rear\n");
    return;
  }
  if (isDequeEmpty()) {
    front = 0;
    rear = 0;
  } else {
    rear++;
  }
  deque[rear] = value;
}

int deleteFront() {
  if (isDequeEmpty()) {
    printf("Deque Underflow at Front\n");
    return -1;
  }
  int value = deque[front++];
  if (front > rear) front = rear = -1;
  return value;
}

int deleteRear() {
  if (isDequeEmpty()) {
    printf("Deque Underflow at Rear\n");
    return -1;
  }
  int value = deque[rear--];
  if (rear < front) front = rear = -1;
  return value;
}

void displayDeque() {
  if (isDequeEmpty()) {
    printf("Deque is empty\n");
    return;
  }
  for (int i = front; i <= rear; i++) {
    printf("%d ", deque[i]);
  }
  printf("\n");
}

int main() {
  insertFront(50);
  insertRear(60);
  displayDeque();
  deleteFront();
  displayDeque();
  deleteRear();
  displayDeque();

  return 0;
}

// 🚀 Circular Queue

#include <stdio.h>
#define MAX 100

int circularQueue[MAX];
int front = -1, rear = -1;

int isCircularQueueFull() {
  return (rear + 1) % MAX == front;
}

int isCircularQueueEmpty() {
  return front == -1;
}

void enqueueCircular(int value) {
  if (isCircularQueueFull()) {
    printf("Circular Queue Overflow\n");
    return;
  }
  if (isCircularQueueEmpty()) {
    front = 0;
    rear = 0;
  } else {
    rear = (rear + 1) % MAX;
  }
  circularQueue[rear] = value;
}

int dequeueCircular() {
  if (isCircularQueueEmpty()) {
    printf("Circular Queue Underflow\n");
    return -1;
  }
  int value = circularQueue[front];
  if (front == rear) {
    front = -1;
    rear = -1;
  } else {
    front = (front + 1) % MAX;
  }
  return value;
}

void displayCircularQueue() {
  if (isCircularQueueEmpty()) {
    printf("Circular Queue is empty\n");
    return;
  }
  int i = front;
  while (1) {
    printf("%d ", circularQueue[i]);
    if (i == rear) break;
    i = (i + 1) % MAX;
  }
  printf("\n");
}

int main() {
  enqueueCircular(70);
  enqueueCircular(80);
  displayCircularQueue();
  dequeueCircular();
  displayCircularQueue();

  return 0;
}

// 🚀 Postfix and Prefix Evaluation

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#define MAX 100

int stack[MAX];
int top = -1;

int isStackFull() {
    return top == MAX - 1;
}

int isStackEmpty() {
    return top == -1;
}

void push(int value) {
    if (isStackFull()) {
        printf("Stack Overflow\n");
        exit(1);
    }
    stack[++top] = value;
}

int pop() {
    if (isStackEmpty()) {
        printf("Stack Underflow\n");
        exit(1);
    }
    return stack[top--];
}

int peek() {
    if (isStackEmpty()) {
        printf("Stack is empty\n");
        exit(1);
    }
    return stack[top];
}

int evaluatePostfix(char *expression) {
    for (int i = 0; expression[i]; i++) {
        if (isdigit(expression[i])) {
            push(expression[i] - '0');
        } else {
            int b = pop();
            int a = pop();
            switch (expression[i]) {
                case '+': push(a + b); break;
                case '-': push(a - b); break;
                case '*': push(a * b); break;
                case '/': push(a / b); break;
            }
        }
    }
    return pop();
}

int evaluatePrefix(char *expression) {
    int length = strlen(expression);
    for (int i = length - 1; i >= 0; i--) {
        if (isdigit(expression[i])) {
            push(expression[i] - '0');
        } else {
            int a = pop();
            int b = pop();
            switch (expression[i]) {
                case '+': push(a + b); break;
                case '-': push(a - b); break;
                case '*': push(a * b); break;
                case '/': push(a / b); break;
            }
        }
    }
    return pop();
}

int main() {
    char postfix[] = "231*+9-";
    printf("Postfix Evaluation of %s = %d\n", postfix, evaluatePostfix(postfix));
    char prefix[] = "-+2319";
    printf("Prefix Evaluation of %s = %d\n", prefix, evaluatePrefix(prefix));
    return 0;
}

// 🚀 All postfix, prefix and infix conversions

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#define MAX 100

char stack[MAX][MAX];
int top = -1;

int isStackFull() {
    return top == MAX - 1;
}

int isStackEmpty() {
    return top == -1;
}

void push(char *value) {
    if (isStackFull()) {
        printf("Stack Overflow\n");
        exit(1);
    }
    strcpy(stack[++top], value);
}

char *pop() {
    if (isStackEmpty()) {
        printf("Stack Underflow\n");
        exit(1);
    }
    return stack[top--];
}

char *peek() {
    if (isStackEmpty()) {
        printf("Stack is empty\n");
        exit(1);
    }
    return stack[top];
}

int precedence(char operator) {
    if (operator == '+' || operator == '-') return 1;
    if (operator == '*' || operator == '/') return 2;
    return 0;
}

void infixToPostfix(char *infix, char *postfix) {
    char stack[MAX];
    int top = -1, k = 0;

    for (int i = 0; infix[i]; i++) {
        if (isalnum(infix[i])) {
            postfix[k++] = infix[i];
        } else if (infix[i] == '(') {
            stack[++top] = infix[i];
        } else if (infix[i] == ')') {
            while (top != -1 && stack[top] != '(')
                postfix[k++] = stack[top--];
            top--; // Pop '('
        } else {
            while (top != -1 && precedence(stack[top]) >= precedence(infix[i]))
                postfix[k++] = stack[top--];
            stack[++top] = infix[i];
        }
    }
    while (top != -1) {
        postfix[k++] = stack[top--];
    }
    postfix[k] = '\0';
}

void reverseString(char *str) {
    int n = strlen(str);
    for (int i = 0; i < n / 2; i++) {
        char temp = str[i];
        str[i] = str[n - i - 1];
        str[n - i - 1] = temp;
    }
}

void infixToPrefix(char *infix, char *prefix) {
    char reversedInfix[MAX], postfix[MAX];
    strcpy(reversedInfix, infix);

    reverseString(reversedInfix);

    for (int i = 0; reversedInfix[i]; i++) {
        if (reversedInfix[i] == '(') reversedInfix[i] = ')';
        else if (reversedInfix[i] == ')') reversedInfix[i] = '(';
    }

    infixToPostfix(reversedInfix, postfix);
    reverseString(postfix);

    strcpy(prefix, postfix);
}

void postfixToPrefix(char *postfix, char *prefix) {
    char stack[MAX][MAX];
    int top = -1;

    for (int i = 0; postfix[i]; i++) {
        if (isalnum(postfix[i])) {
            char operand[2] = {postfix[i], '\0'};
            strcpy(stack[++top], operand);
        } else {
            char op1[MAX], op2[MAX];
            strcpy(op2, stack[top--]);
            strcpy(op1, stack[top--]);

            char temp[MAX];
            sprintf(temp, "%c%s%s", postfix[i], op1, op2);

            strcpy(stack[++top], temp);
        }
    }
    strcpy(prefix, stack[top]);
}

void prefixToPostfix(char *prefix, char *postfix) {
    int length = strlen(prefix);

    for (int i = length - 1; i >= 0; i--) {
        if (isalnum(prefix[i])) {
            char operand[2] = {prefix[i], '\0'};
            push(operand);
        } else {
            char op1[MAX], op2[MAX];
            strcpy(op1, pop());
            strcpy(op2, pop());

            char temp[MAX];
            sprintf(temp, "%s%s%c", op1, op2, prefix[i]);

            push(temp);
        }
    }
    strcpy(postfix, pop());
}

void prefixToInfix(char *prefix, char *infix) {
    int length = strlen(prefix);

    for (int i = length - 1; i >= 0; i--) {
        if (isalnum(prefix[i])) {
            char operand[2] = {prefix[i], '\0'};
            push(operand);
        } else {
            char op1[MAX], op2[MAX];
            strcpy(op1, pop());
            strcpy(op2, pop());

            char temp[MAX];
            sprintf(temp, "(%s%c%s)", op1, prefix[i], op2);

            push(temp);
        }
    }
    strcpy(infix, pop());
}

void postfixToInfix(char *postfix, char *infix) {
    for (int i = 0; postfix[i]; i++) {
        if (isalnum(postfix[i])) {
            char operand[2] = {postfix[i], '\0'};
            push(operand);
        } else {
            char op1[MAX], op2[MAX];
            strcpy(op2, pop());
            strcpy(op1, pop());

            char temp[MAX];
            sprintf(temp, "(%s%c%s)", op1, postfix[i], op2);

            push(temp);
        }
    }
    strcpy(infix, pop());
}

int main() {
    char prefix[] = "-+ABC";
    char postfixFromPrefix[MAX], infixFromPrefix[MAX], infixFromPostfix[MAX];
    char postfix[] = "AB+C-";

    prefixToPostfix(prefix, postfixFromPrefix);
    prefixToInfix(prefix, infixFromPrefix);
    postfixToInfix(postfix, infixFromPostfix);

    printf("Prefix: %s\n", prefix);
    printf("Postfix from Prefix: %s\n", postfixFromPrefix);
    printf("Infix from Prefix: %s\n", infixFromPrefix);

    printf("\nPostfix: %s\n", postfix);
    printf("Infix from Postfix: %s\n", infixFromPostfix);

    return 0;
}

// 🚀 Tower of Hanoi

#include <stdio.h>

void moveDisk(int n, char source, char destination) {
    printf("Move disk %d from %c to %c\n", n, source, destination);
}

void towerOfHanoi(int n, char source, char destination, char auxiliary) {
    if (n == 1) {
        moveDisk(1, source, destination); // Base case: move a single disk
        return;
    }
    
    towerOfHanoi(n - 1, source, auxiliary, destination);
    
    moveDisk(n, source, destination);
    
    towerOfHanoi(n - 1, auxiliary, destination, source);
}

int main() {
    int n;
    printf("Enter the number of disks: ");
    scanf("%d", &n);
    
    towerOfHanoi(n, 'A', 'C', 'B');
    
    return 0;
}

// 🚀 Linked List

#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
  int data;
  struct Node *next;
} Node;

Node *createNode(int data) {
  Node *newNode = (Node *) malloc(sizeof(Node));
  newNode->data = data;
  newNode->next = NULL;
  return newNode;
}

void insertAtFirst(Node **head, int data) {
  Node *newNode = createNode(data);
  newNode->next = *head;
  *head = newNode;
}

void insertAtLast(Node **head, int data) {
  Node *newNode = createNode(data);

  if (*head == NULL) {
    *head = newNode;
    return;
  }

  Node *temp = *head;
  while (temp->next != NULL) {
    temp = temp->next;
  }

  temp->next = newNode;
}

void insertAtPosition(Node **head, int data, int position) {
  Node *newNode = createNode(data);

  if (position == 0) {
    insertAtFirst(head, data);
    return;
  }

  Node *temp = *head;
  for (int i = 0; temp->next != NULL && i < position - 1; i++) {
    temp = temp->next;
  }

  if (temp == NULL) {
    printf("Index out of bounds.");
    free(newNode);
    return;
  }

  newNode->next = temp->next;
  temp->next = newNode;
}

void deleteFromFirst(Node **head) {
  if (head == NULL) {
    printf("List is empty!");
    return;
  }

  Node *temp = *head;
  *head = temp->next;
  free(temp);
}

void deleteFromLast(Node **head) {
  if (head == NULL) {
    printf("List is empty!");
    return;
  }

  Node *temp = *head;
  if (temp->next == NULL) {
    free(temp);
    *head = NULL;
    return;
  }

  while (temp->next->next != NULL) {
    temp = temp->next;
  }

  free(temp->next);
  temp->next = NULL;
}

void deleteFromPosition(Node **head, int position) {
  if (head == NULL) {
    printf("List is empty!");
    return;
  }

  if (position == 0) {
    deleteFromFirst(head);
    return;
  }

  Node *temp = *head;

  for (int i = 0; temp->next != NULL && i < position - 1; i++) {
    temp = temp->next;
  }

  if (temp == NULL || temp->next == NULL) {
    printf("Index out of bounds.");
    return;
  }

  Node *next = temp->next->next;
  free(temp->next);
  temp->next = next;
}

void print(Node *head) {
  Node *temp = head;
  while (temp != NULL) {
    printf("%d -> ", temp->data);
    temp = temp->next;
  }

  printf("NULL \n");
}

int main() {
  Node *head = NULL;

  insertAtFirst(&head, 10);
  printf("Linked list after inserting the node:10 at the beginning \n");
  print(head);

  printf("Linked list after inserting the node:20 at the end \n");
  insertAtLast(&head, 20);
  print(head);

  printf("Linked list after inserting the node:5 at the end \n");
  insertAtLast(&head, 5);
  print(head);

  printf("Linked list after inserting the node:30 at the end \n");
  insertAtLast(&head, 30);
  print(head);

  printf("Linked list after inserting the node:15 at position 2 \n");
  insertAtPosition(&head, 15, 2);
  print(head);

  printf("Linked list after deleting the first node: \n");
  deleteFromFirst(&head);
  print(head);

  printf("Linked list after deleting the last node: \n");
  deleteFromLast(&head);
  print(head);

  printf("Linked list after deleting the node at position 1: \n");
  deleteFromPosition(&head, 1);
  print(head);

  return 0;
}

// 🚀 Doubly Linked List

#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
  int data;
  struct Node *prev;
  struct Node *next;
} Node;

Node *createNode(int data) {
  Node *newNode = (Node *) malloc(sizeof(Node));
  newNode->data = data;
  newNode->prev = NULL;
  newNode->next = NULL;
  return newNode;
}

void insertAtFirst(Node **head, int data) {
  Node *newNode = createNode(data);

  newNode->next = *head;

  if (*head != NULL) {
    (*head)->prev = newNode;
  }

  *head = newNode;
}

void insertAtEnd(Node **head, int data) {
  Node *newNode = createNode(data);

  if (*head == NULL) {
    *head = newNode;
    return;
  }

  Node *temp = *head;

  while (temp->next != NULL) {
    temp = temp->next;
  }

  temp->next = newNode;
  newNode->prev = temp;
}

void insertAtPosition(Node **head, int data, int position) {
  if (position == 0) {
    insertAtFirst(head, data);
    return;
  }

  Node *newNode = createNode(data);
  Node *temp = *head;

  for (int i = 0; temp->next != NULL && i < position - 1; i++) {
    temp = temp->next;
  }

  if (temp == NULL) {
    printf("Index out of bounds!");
    free(newNode);
    return;
  }

  newNode->next = temp->next;
  newNode->prev = temp;

  if (temp->next != NULL) {
    temp->next->prev = newNode;
  }

  temp->next = newNode;
}

void print(Node **head) {
  if (*head == NULL) {
    printf("List is empty!\n");
    return;
  }

  printf("HEAD <-> ");
  Node *temp = *head;

  while (temp != NULL) {
    printf("%d <-> ", temp->data);
    temp = temp->next;
  }

  printf("NULL\n");
}

Node *deleteFromFirst(Node **head) {
  if (head == NULL) {
    printf("List is empty!\n");
    return NULL;
  }

  Node *temp = *head;
  *head = temp->next;

  if (head != NULL) {
    (*head)->prev = NULL;
  }

  free(temp);
  return *head;
}

Node *deleteFromLast(Node **head) {
  if (head == NULL) {
    printf("List is empty!\n");
    return NULL;
  }

  Node *temp = *head;

  if (temp->next == NULL) {
    *head = NULL;
    free(temp);
    return NULL;
  }

  while (temp->next != NULL) {
    temp = temp->next;
  }

  temp->prev->next = NULL;
  free(temp);
  return *head;
}

Node *deleteFromPosition(Node **head, int position) {
  if (*head == NULL) {
    printf("List is empty!\n");
    return NULL;
  }

  if (position == 0) {
    return deleteFromFirst(head);
  }

  Node *temp = *head;

  for (int i = 0; temp->next != NULL && i < position; i++) {
    temp = temp->next;
  }

  if (temp == NULL) {
    printf("Index out of bounds!");
    return NULL;
  }

  if (temp->next != NULL) {
    temp->next->prev = temp->prev;
  }

  if (temp->prev != NULL) {
    temp->prev->next = temp->next;
  }

  free(temp);
  return *head;
}

int main() {
  Node *head = NULL;
  print(&head);

  insertAtFirst(&head, 10);
  print(&head);

  insertAtEnd(&head, 9);
  print(&head);

  insertAtFirst(&head, 11);
  print(&head);

  insertAtPosition(&head, 10, 2);
  print(&head);

  insertAtPosition(&head, 15, 0);
  print(&head);

  deleteFromFirst(&head);
  print(&head);

  deleteFromLast(&head);
  print(&head);

  deleteFromPosition(&head, 1);
  print(&head);

  return 0;
}

// 🚀 Circular Linked List

#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node* next;
} Node;

Node* createNode(int data) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = data;
    newNode->next = newNode;
    return newNode;
}

Node* insert(Node* tail, int data) {
    Node* newNode = createNode(data);
    if (tail == NULL) {
        return newNode;
    }
    newNode->next = tail->next;
    tail->next = newNode;
    return newNode;
}

Node* delete(Node* tail, int key) {
    if (tail == NULL) {
        printf("List is empty. Nothing to delete.\n");
        return NULL;
    }

    Node* current = tail->next;
    Node* prev = tail;

    do {
        if (current->data == key) {
            if (current == tail && current->next == tail) {
                free(current);
                return NULL;
            }
            if (current == tail->next) {
                tail->next = current->next;
            }
            if (current == tail) {
                tail = prev;
            }
            prev->next = current->next;
            free(current);
            return tail;
        }
        prev = current;
        current = current->next;
    } while (current != tail->next);

    printf("Key not found in the list.\n");
    return tail;
}

void traverse(Node* tail) {
    if (tail == NULL) {
        printf("List is empty.\n");
        return;
    }

    Node* current = tail->next;
    do {
        printf("%d ", current->data);
        current = current->next;
    } while (current != tail->next);
    printf("\n");
}

int main() {
    Node* tail = NULL;

    tail = insert(tail, 1);
    tail = insert(tail, 2);
    tail = insert(tail, 3);
    tail = insert(tail, 4);

    printf("Circular Linked List after insertion: ");
    traverse(tail);

    tail = delete(tail, 2);
    printf("Circular Linked List after deleting 2: ");
    traverse(tail);

    tail = delete(tail, 4);
    printf("Circular Linked List after deleting 4: ");
    traverse(tail);

    return 0;
}

// 🚀 Polynomial Application of Linked List - Addition, Multiplication and Equality Check

#include <stdio.h>
#include <stdlib.h>

typedef struct Term {
  int coefficient;
  int exponent;
} Term;

typedef struct Node {
  Term* term;
  struct Node* next;
} Node;

Term* createTerm(int coefficient, int exponent) {
  Term* temp = (Term*) malloc(sizeof(Term));
  temp->coefficient = coefficient;
  temp->exponent = exponent;

  return temp;
}

Node* createNode(int coefficient, int exponent) {
  Term* term = createTerm(coefficient, exponent);
  Node* newNode = (Node*) malloc(sizeof(Node));

  newNode->term = term;
  newNode->next = NULL;

  return newNode;
}


Node* insertAtEnd(Node* head, int coefficient, int exponent) {
  if (head == NULL) return createNode(coefficient, exponent);

  Node* temp = head;

  while (temp->next != NULL) {
    temp = temp->next;
  }

  temp->next = createNode(coefficient, exponent);
  
  return head;
}

int comparePolynomials(Node* polynomial1, Node* polynomial2) {
  while (polynomial1 != NULL && polynomial2 != NULL) {
    if (polynomial1->term->exponent != polynomial2->term->exponent) {
      return 0;
    }
    if (polynomial1->term->coefficient != polynomial2->term->coefficient) {
      return 0;
    }

    polynomial1 = polynomial1->next;
    polynomial2 = polynomial2->next;
  }

  return polynomial1 == NULL && polynomial2 == NULL;
}

void printPolynomial(Node* head) {
  Node* temp = head;

  while (temp != NULL) {
    printf("%dx^%d", temp->term->coefficient, temp->term->exponent);
    if (temp->next != NULL) {
      printf(" + ");
    }
    temp = temp->next;
  }

  printf("\n");
}

void freePolynomial(Node* head) {
  Node* temp;
  while (head != NULL) {
    temp = head;
    head = head->next;
    free(temp->term);
    free(temp);
  }
}

Node* add(Node* polynomial1, Node* polynomial2) {
  Node* result = NULL;

  Node* p1 = polynomial1;
  Node* p2 = polynomial2;

  while (p1 != NULL && p2 != NULL) {
    if (p1->term->exponent == p2->term->exponent) {
      int sumCoeff = p1->term->coefficient + p2->term->coefficient;
      if (sumCoeff != 0) {
        result = insertAtEnd(result, sumCoeff, p1->term->exponent);
      }
      p1 = p1->next;
      p2 = p2->next;
    } else if (p1->term->exponent > p2->term->exponent) {
      result = insertAtEnd(result, p1->term->coefficient, p1->term->exponent);
      p1 = p1->next;
    } else {
      result = insertAtEnd(result, p2->term->coefficient, p2->term->exponent);
      p2 = p2->next;
    }
  }

  while (p1 != NULL) {
    result = insertAtEnd(result, p1->term->coefficient, p1->term->exponent);
    p1 = p1->next;
  }

  while (p2 != NULL) {
    result = insertAtEnd(result, p2->term->coefficient, p2->term->exponent);
    p2 = p2->next;
  }

  return result;
}

int main() {
  Node* poly1 = NULL;
  Node* poly2 = NULL;

  poly1 = insertAtEnd(poly1, 5, 3);
  poly1 = insertAtEnd(poly1, 3, 2);
  poly1 = insertAtEnd(poly1, 1, 0);

  poly2 = insertAtEnd(poly2, 4, 3);
  poly2 = insertAtEnd(poly2, 2, 1);

  printf("Polynomial 1: ");
  printPolynomial(poly1);

  printf("Polynomial 2: ");
  printPolynomial(poly2);

  Node* result = add(poly1, poly2);

  printf("Resultant Polynomial: ");
  printPolynomial(result);

  printf("Polynomials are: ");
  if (comparePolynomials(poly1, poly2)) {
    printf("EQUAL\n");
  } else {
    printf("NOT EQUAL\n");
  }

  Node* poly3 = NULL;
  Node* poly4 = NULL;

  poly3 = insertAtEnd(poly3, 2, 2);
  poly3 = insertAtEnd(poly3, 1, 1);
  poly3 = insertAtEnd(poly3, 3, 0);

  poly4 = insertAtEnd(poly4, 2, 2);
  poly4 = insertAtEnd(poly4, 1, 1);
  poly4 = insertAtEnd(poly4, 3, 0);

  printf("Polynomials are: ");
  if (comparePolynomials(poly3, poly4)) {
    printf("EQUAL\n");
  } else {
    printf("NOT EQUAL\n");
  }

  freePolynomial(poly1);
  freePolynomial(poly2);
  freePolynomial(result);

  return 0;
}

// 🚀 Binary Trees

#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
  int data;
  struct TreeNode* left;
  struct TreeNode* right;
} TreeNode;

TreeNode* createNode(int data) {
  TreeNode* newNode = (TreeNode *) malloc(sizeof(TreeNode));
  newNode->data = data;
  newNode->left = NULL;
  newNode->right = NULL;

  return newNode;
}

TreeNode* insert(TreeNode* root, int data) {
  if (root == NULL) return createNode(data);
  
  TreeNode* queue[100];
  int front = 0, rear = 0;
  queue[rear++] = root;

  while (front < rear) {
    TreeNode* temp = queue[front++];

    if (temp->left == NULL) {
      temp->left = createNode(data);
      break;
    } else {
      queue[rear++] = temp->left;
    }

    if (temp->right == NULL) {
      temp->right = createNode(data);
      break;
    } else {
      queue[rear++] = temp->right;
    }
  }

  return root;
}

int searchDFS(TreeNode* root, int value) {
  if (root == NULL) return 0;

  if (root->data == value) return 1;

  int leftResult = searchDFS(root->left, value);
  int rightResult = searchDFS(root->right, value);

  return leftResult || rightResult;
}

TreeNode* findMin(TreeNode* root) {
  while (root && root->left) {
    root = root->left;
  }
  return root;
}

TreeNode* deleteNode(TreeNode* root, int key) {
  if (root == NULL) {
    return NULL;
  }

  if (key < root->data) {
    root->left = deleteNode(root->left, key);
  }
  else if (key > root->data) {
    root->right = deleteNode(root->right, key);
  }
  else {
    if (root->left == NULL) {
      TreeNode* temp = root->right;
      free(root);
      return temp;
    }
    else if (root->right == NULL) {
      TreeNode* temp = root->left;
      free(root);
      return temp;
    }

    TreeNode* temp = findMin(root->right);

    root->data = temp->data;

    root->right = deleteNode(root->right, temp->data);
  }
  return root;
}

void inOrder(TreeNode* root) {
  if (root) {
    inOrder(root->left);
    printf("%d ", root->data);
    inOrder(root->right);
  }
}

void preOrder(TreeNode* root) {
  if (root) {
    printf("%d ", root->data);
    preOrder(root->left);
    preOrder(root->right);
  }
}

void postOrder(TreeNode* root) {
  if (root) {
    postOrder(root->left);
    postOrder(root->right);
    printf("%d ", root->data);
  }
}

void BFS(TreeNode* root) {
  if (root == NULL) return;

  TreeNode* queue[100];
  int front = 0, rear = 0;
  queue[rear++] = root;

  while (front < rear) {
    TreeNode* node = queue[front++];
    printf("%d ", node->data);
    if (node->left) {
      queue[rear++] = node->left;
    }
    if (node->right) {
      queue[rear++] = node->right;
    }
  }
}

int main() {
  TreeNode* root = createNode(1);
  TreeNode* n1 = createNode(2);
  TreeNode* n2 = createNode(3);
  TreeNode* n3 = createNode(4);
  TreeNode* n5 = createNode(6);
  TreeNode* n6 = createNode(7);

  root->left = n1;
  root->right = n2;
  n1->left = n3;
  n2->left = n5;
  n2->right = n6;

  root = insert(root, 5);
  
  inOrder(root);

  BFS(root);

  return 0;
}

// 🚀 Binary Search Tree

#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
  int data;
  struct TreeNode* left;
  struct TreeNode* right;
} TreeNode;

TreeNode* createNode(int data) {
  TreeNode* newNode = (TreeNode*) malloc(sizeof(TreeNode));
  
  newNode->data = data;
  newNode->left = NULL;
  newNode->right = NULL;

  return newNode;
}

int search(TreeNode* root, int value) {
  if (root == NULL) return 0;
  if (root->data == value) return 1;
  if (root->data < value) return search(root->right, value);
  if (root->data > value) return search(root->left, value);

  return 0;
}

TreeNode* findMin(TreeNode* node) {
  while (node->left != NULL) node = node->left;
  
  return node;
}

TreeNode* findMax(TreeNode* node) {
  while (node->right != NULL) node = node->right;

  return node;
}

TreeNode* insert(TreeNode* root, int value) {
  if (root == NULL) return createNode(value);

  if (value < root->data) {
    root->left = insert(root->left, value);
  }

  if (value > root->data) {
    root->right = insert(root->right, value);
  }

  return root;
}

TreeNode* delete(TreeNode* root, int value) {
  if (root == NULL) return root;

  if (value < root->data) {
    root->left = delete(root->left, value);
  } else if (value > root->data) {
    root->right = delete(root->right, value);
  } else {
    if (root->left == NULL && root->right == NULL) {
      free(root);
      return NULL;
    }

    if (root->left == NULL) {
      TreeNode* temp = root->right;
      free(root);
      return temp;
    } else if (root->right == NULL) {
      TreeNode* temp = root->left;
      free(root);
      return temp;
    }

    TreeNode* temp = findMin(root->right);
    root->data = temp->data;
    root->right = delete(root->right, temp->data);
  }

  return root;
}

void inOrder(TreeNode* root) {
  if (root) {
    inOrder(root->left);
    printf("%d", root->data);
    inOrder(root->right);
  }
}

void preOrder(TreeNode* root) {
  if (root) {
    printf("%d", root->data);
    preOrder(root->left);
    preOrder(root->right);
  }
}

void postOrder(TreeNode* root) {
  if (root) {
    postOrder(root->left);
    postOrder(root->right);
    printf("%d", root->data);
  }
}

void levelOrderTraversal(TreeNode* root) {
  if (root == NULL) return;

  TreeNode* queue[100];
  int front = 0, rear = 0;
  queue[rear++] = root;
  
  while (front < rear) {
    TreeNode* node = queue[front++];
    printf("%d", node->data);
    if (node->left) {
      queue[rear++] = node->left;
    }
    if (node->right) {
      queue[rear++] = node->right;
    }
  }
}

int main()
{
  TreeNode* root = NULL;
  root = insert(root, 50);
  root = insert(root, 30);
  root = insert(root, 20);
  root = insert(root, 40);
  root = insert(root, 70);
  root = insert(root, 60);
  root = insert(root, 80);

  printf("InOrder traversal before deletion: ");
  inOrder(root);
  printf("\n");

  root = delete(root, 20);
  printf("InOrder traversal after deleting 20: ");
  inOrder(root);
  printf("\n");

  root = delete(root, 30);
  printf("InOrder traversal after deleting 30: ");
  inOrder(root);
  printf("\n");

  root = delete(root, 50);
  printf("InOrder traversal after deleting 50: ");
  inOrder(root);
  printf("\n");

  return 0;
}

// 🚀 General Program : BFS, DFS, Dijkstra's, Prim's (use Prim's for Kruskal's also)
#include <limits.h>
#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define MAX_VERTICES 5
#define INF 0

typedef struct Graph
{
  int numVertices;
  int **adjMatrix;
} Graph;

// 🚀 Creating a graph
struct Graph *createGraph(int V)
{
  Graph *graph = (Graph *)malloc(sizeof(Graph));
  graph->numVertices = V;

  graph->adjMatrix = (int **)malloc(V * sizeof(int *));

  for (int i = 0; i < V; i++)
  {
    graph->adjMatrix[i] = (int *)malloc(V * sizeof(int));
    for (int j = 0; j < V; j++)
    {
      graph->adjMatrix[i][j] = 0;
    }
  }

  return graph;
}

// 🚀 Adding an edge
void addEdge(Graph *graph, int source, int destination)
{
  graph->adjMatrix[source][destination] = 1;
  graph->adjMatrix[destination][source] = 1;
}

// 🚀 Depth-first Search
void DFS(Graph *graph, int vertex, bool visited[])
{
  visited[vertex] = true;
  printf("%d ", vertex);

  for (int i = 0; i < graph->numVertices; i++)
  {
    if (graph->adjMatrix[vertex][i] == 1 && !visited[i])
    {
      DFS(graph, i, visited);
    }
  }
}

// 🚀 Breadth-first search
void BFS(Graph *graph, int startVertex)
{
  bool visited[MAX_VERTICES] = {false};
  int queue[graph->numVertices];
  int front = 0, rear = 0;

  visited[startVertex] = true;
  queue[rear++] = startVertex;

  while (front < rear)
  {
    int currentVertex = queue[front++];
    printf("%d ", currentVertex);

    for (int i = 0; i < graph->numVertices; i++)
    {
      if (graph->adjMatrix[currentVertex][i] == 1 && !visited[i])
      {
        queue[rear++] = i;
        visited[i] = true;
      }
    }
  }
}

// 🚀 Parts of Dijkstra's Algorithm
int findMinDistance(int distance[], int visited[])
{
  int min = INT_MAX, minIndex;

  for (int v = 0; v < MAX_VERTICES; v++)
  {
    if (!visited[v] && distance[v] <= min)
    {
      min = distance[v];
      minIndex = v;
    }
  }

  return minIndex;
}

// 🚀 Dijkstra's Algorithm for weighted graphs
void dijkstra(int graph[MAX_VERTICES][MAX_VERTICES], int source)
{
  int distance[MAX_VERTICES];
  int visited[MAX_VERTICES];

  for (int i = 0; i < MAX_VERTICES; i++)
  {
    distance[i] = INT_MAX;
    visited[i] = false;
  }

  distance[source] = 0;

  for (int i = 0; i < MAX_VERTICES - 1; i++)
  {
    int u = findMinDistance(distance, visited);
    visited[u] = true;

    for (int v = 0; v < MAX_VERTICES; v++)
    {
      if (!visited[v] && graph[u][v] && distance[u] != INT_MAX &&
          distance[u] + graph[u][v] < distance[v])
      {
        distance[v] = distance[u] + graph[u][v];
      }
    }
  }

  printf("Vertex\tDistance From Source\n");
  for (int i = 0; i < MAX_VERTICES; i++)
  {
    printf("%d\t%d\n", i, distance[i]);
  }
}

// 🚀 Part of Prim's Algorithm
int findMinKey(int key[], bool inMST[])
{
  int min = INT_MAX, minIndex;

  for (int v = 0; v < MAX_VERTICES; v++)
  {
    if (!inMST[v] && key[v] < min)
    {
      min = key[v];
      minIndex = v;
    }
  }

  return minIndex;
}

// 🚀 Prim's Algorithm
void primMST(int graph[MAX_VERTICES][MAX_VERTICES])
{
  int parent[MAX_VERTICES];
  int key[MAX_VERTICES];
  bool inMST[MAX_VERTICES];

  for (int i = 0; i < MAX_VERTICES; i++)
  {
    key[i] = INT_MAX;
    inMST[i] = false;
  }

  key[0] = 0;
  parent[0] = -1;

  for (int count = 0; count < MAX_VERTICES - 1; count++)
  {
    int u = findMinKey(key, inMST);
    inMST[u] = true;

    for (int v = 0; v < MAX_VERTICES; v++)
    {
      if (graph[u][v] && !inMST[v] && graph[u][v] < key[v])
      {
        parent[v] = u;
        key[v] = graph[u][v];
      }
    }
  }

  printMST(parent, graph);
}

void printMST(int parent[], int graph[MAX_VERTICES][MAX_VERTICES])
{
  printf("Edge\tWeight\n");
  for (int i = 1; i < MAX_VERTICES; i++)
  {
    printf("%d - %d\t%d\n", parent[i], i, graph[i][parent[i]]);
  }
}

void printAdjMatrix(Graph *graph)
{
  for (int i = 0; i < graph->numVertices; i++)
  {
    for (int j = 0; j < graph->numVertices; j++)
    {
      printf("%d ", graph->adjMatrix[i][j]);
    }

    printf("\n");
  }
}

int main()
{
  struct Graph *graph = createGraph(MAX_VERTICES);
  addEdge(graph, 0, 1);
  addEdge(graph, 0, 4);
  addEdge(graph, 1, 2);
  addEdge(graph, 1, 3);
  addEdge(graph, 1, 4);
  addEdge(graph, 2, 3);
  addEdge(graph, 3, 4);

  bool visited[MAX_VERTICES] = {false};
  int vertex = 0;

  printf("DFS starting from vertex 0:\n");
  DFS(graph, 0, visited);

  printf("\n");

  printf("BFS starting from vertex 0:\n");
  BFS(graph, 0);

  int newGraph[MAX_VERTICES][MAX_VERTICES] = {
      {0, 10, 3, 0, 0},
      {0, 0, 1, 2, 0},
      {0, 4, 0, 8, 2},
      {0, 0, 0, 0, 7},
      {0, 0, 0, 9, 0}};

  int source = 0;
  printf("\nDijkstra's Shortest Path for Directed Graph starting from vertex %d:\n", source);
  dijkstra(newGraph, source);

  int newGraph2[MAX_VERTICES][MAX_VERTICES] = {
      {0, 2, 0, 6, 0},
      {2, 0, 3, 8, 5},
      {0, 3, 0, 0, 7},
      {6, 8, 0, 0, 9},
      {0, 5, 7, 9, 0}};

  printf("Prim's Minimum Spanning Tree:\n");
  primMST(newGraph2);

  return 0;
}

// 🚀 Path printing Dijkstra's Algorithm

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define MAX 100

int dist[MAX], prev[MAX], visited[MAX];
int graph[MAX][MAX];

void addEdge(int u, int v, int w)
{
  graph[u][v] = w;
  graph[v][u] = w;
}

void dijkstra(int source, int n)
{
  for (int i = 0; i < n; i++)
  {
    dist[i] = INT_MAX;
    visited[i] = 0;
    prev[i] = -1;
  }
  dist[source] = 0;

  for (int i = 0; i < n - 1; i++)
  {
    int minDist = INT_MAX, minIndex = -1;
    for (int j = 0; j < n; j++)
    {
      if (!visited[j] && dist[j] < minDist)
      {
        minDist = dist[j];
        minIndex = j;
      }
    }
    visited[minIndex] = 1;

    for (int j = 0; j < n; j++)
    {
      if (graph[minIndex][j] != 0 && !visited[j])
      {
        int weight = graph[minIndex][j];
        if (dist[minIndex] + weight < dist[j])
        {
          dist[j] = dist[minIndex] + weight;
          prev[j] = minIndex;
        }
      }
    }
  }
}

void printPath(int destination)
{
  if (prev[destination] == -1)
  {
    printf("No path found\n");
    return;
  }
  int path[MAX], pathIndex = 0;
  for (int v = destination; v != -1; v = prev[v])
  {
    path[pathIndex++] = v;
  }
  printf("Shortest path: ");
  for (int i = pathIndex - 1; i > 0; i--)
  {
    printf("%d -> ", path[i]);
  }
  printf("%d\n", path[0]);
  printf("Shortest distance: %d\n", dist[destination]);
}

int main()
{
  int n, m, u, v, w, s, d;
  scanf("%d", &n);
  scanf("%d", &m);

  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < n; j++)
    {
      graph[i][j] = 0;
    }
  }

  for (int i = 0; i < m; i++)
  {
    scanf("%d %d %d", &u, &v, &w);
    addEdge(u, v, w);
  }

  scanf("%d", &s);
  scanf("%d", &d);

  dijkstra(s, n);
  printPath(d);

  return 0;
}

// 🚀 Cycle Detection

// Cycle detection

#include <stdio.h>
#include <limits.h>

#define MAX_VERTICES 5
#define INF INT_MAX

int adjMatrix[MAX_VERTICES][MAX_VERTICES];

int findShortestCycle(int v)
{
  int shortestCycle = INF;

  for (int start = 0; start < v; ++start)
  {
    int distance[MAX_VERTICES];
    int queue[MAX_VERTICES], front = 0, back = 0;

    for (int i = 0; i < v; ++i)
    {
      distance[i] = INF;
    }
    distance[start] = 0;
    queue[back++] = start;

    while (front < back)
    {
      int u = queue[front++];
      for (int dest = 0; dest < v; ++dest)
      {
        if (adjMatrix[u][dest] > 0)
        {
          if (distance[dest] == INF)
          {
            distance[dest] = distance[u] + adjMatrix[u][dest];
            queue[back++] = dest;
          }
          else if (distance[u] + adjMatrix[u][dest] < shortestCycle)
          {
            shortestCycle = distance[u] + adjMatrix[u][dest];
          }
        }
      }
    }
  }

  return (shortestCycle == INF) ? -1 : shortestCycle;
}

int main()
{
  int v, e;
  printf("Enter the number of vertices: ");
  scanf("%d", &v);
  printf("Enter the number of edges: ");
  scanf("%d", &e);

  for (int i = 0; i < v; i++)
  {
    for (int j = 0; j < v; j++)
    {
      adjMatrix[i][j] = 0;
    }
  }

  printf("Enter edges in format (source destination weight):\n");
  for (int i = 0; i < e; i++)
  {
    int src, dest, weight;
    scanf("%d %d %d", &src, &dest, &weight);
    adjMatrix[src][dest] = weight;
  }

  int result = findShortestCycle(v);
  if (result == -1)
  {
    printf("No cycle found in the graph.\n");
  }
  else
  {
    printf("Length of the shortest cycle: %d\n", result);
  }

  return 0;
}

// 🚀 Length of longest path

#include <stdio.h>

#define MAX 5

int directions[8][2] = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}, {-1, -1}, {-1, 1}, {1, -1}, {1, 1}};

int isValid(int x, int y, int n, int m)
{
  return x >= 0 && x < n && y >= 0 && y < m;
}

int dfs(char matrix[MAX][MAX], int x, int y, int n, int m, char prevChar)
{
  int maxLength = 1;

  for (int i = 0; i < 8; i++)
  {
    int newX = x + directions[i][0];
    int newY = y + directions[i][1];

    if (isValid(newX, newY, n, m) && matrix[newX][newY] == prevChar + 1)
    {
      int pathLength = 1 + dfs(matrix, newX, newY, n, m, matrix[newX][newY]);
      if (pathLength > maxLength)
      {
        maxLength = pathLength;
      }
    }
  }

  return maxLength;
}

int findLongestPath(char matrix[MAX][MAX], int n, int m, char startChar)
{
  int longestPath = 0;

  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < m; j++)
    {
      if (matrix[i][j] == startChar)
      {
        int currentPathLength = dfs(matrix, i, j, n, m, startChar);
        if (currentPathLength > longestPath)
        {
          longestPath = currentPathLength;
        }
      }
    }
  }

  return longestPath;
}

int main()
{
  int n, m;
  printf("Enter the number of rows: ");
  scanf("%d", &n);
  printf("Enter the number of columns: ");
  scanf("%d", &m);

  char matrix[MAX][MAX];
  printf("Enter the matrix of characters:\n");
  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < m; j++)
    {
      scanf(" %c", &matrix[i][j]);
    }
  }

  char startChar;
  printf("Enter the starting character: ");
  scanf(" %c", &startChar);

  int longestPath = findLongestPath(matrix, n, m, startChar);
  printf("The length of the longest path with consecutive characters starting from character %c is %d\n", startChar, longestPath);

  return 0;
}

// 🚀 Level of a node

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define MAX_NODES 100

int bfs(int V, int adj_matrix[MAX_NODES][MAX_NODES], int X)
{
  int visited[MAX_NODES] = {0};
  int level[MAX_NODES] = {-1};
  int queue[MAX_NODES], front = 0, rear = 0;

  visited[0] = 1;
  level[0] = 0;
  queue[rear++] = 0;

  while (front < rear)
  {
    int node = queue[front++];

    for (int i = 0; i < V; i++)
    {
      if (adj_matrix[node][i] == 1 && !visited[i])
      {
        visited[i] = 1;
        level[i] = level[node] + 1;
        queue[rear++] = i;

        if (i == X)
        {
          return level[i];
        }
      }
    }
  }

  return -1;
}

int main()
{
  int V, E;
  scanf("%d %d", &V, &E);

  int adj_matrix[MAX_NODES][MAX_NODES] = {0};

  for (int i = 0; i < E; i++)
  {
    int u, v;
    scanf("%d %d", &u, &v);
    adj_matrix[u][v] = 1;
    adj_matrix[v][u] = 1;
  }

  int X;
  scanf("%d", &X);

  int result = bfs(V, adj_matrix, X);

  printf("%d\n", result);

  return 0;
}

// 🚀 Shortest path using BFS

#include <stdio.h>
#include <stdlib.h>

#define MAX_VERTICES 7

typedef struct Queue
{
  int items[MAX_VERTICES];
  int front, rear;
} Queue;

Queue *createQueue()
{
  Queue *q = (Queue *)malloc(sizeof(Queue));
  q->front = -1;
  q->rear = -1;
  return q;
}

int isEmpty(Queue *q)
{
  return q->rear == -1;
}

void enqueue(Queue *q, int value)
{
  if (q->rear == MAX_VERTICES - 1)
    return;
  if (q->front == -1)
    q->front = 0;
  q->rear++;
  q->items[q->rear] = value;
}

int dequeue(Queue *q)
{
  int item;
  if (isEmpty(q))
  {
    return -1;
  }
  else
  {
    item = q->items[q->front];
    q->front++;
    if (q->front > q->rear)
    {
      q->front = q->rear = -1;
    }
  }
  return item;
}

void findShortestPath(int n, int adjMatrix[MAX_VERTICES][MAX_VERTICES], int source, int goal)
{
  if (source < 0 || source >= n || goal < 0 || goal >= n)
  {
    printf("Not found\n");
    return;
  }

  int visited[MAX_VERTICES] = {0};
  int parent[MAX_VERTICES];
  for (int i = 0; i < n; i++)
  {
    parent[i] = -1;
  }

  Queue *q = createQueue();
  visited[source] = 1;
  enqueue(q, source);

  int found = 0;

  while (!isEmpty(q) && !found)
  {
    int current = dequeue(q);

    for (int i = 0; i < n; i++)
    {
      if (adjMatrix[current][i] == 1 && !visited[i])
      {
        visited[i] = 1;
        parent[i] = current;
        enqueue(q, i);

        if (i == goal)
        {
          found = 1;
          break;
        }
      }
    }
  }

  if (!found)
  {
    printf("Not found\n");
    return;
  }

  int path[MAX_VERTICES];
  int pathLength = 0;
  for (int v = goal; v != -1; v = parent[v])
  {
    path[pathLength++] = v;
  }

  printf("%d\n", pathLength - 1);
  for (int i = pathLength - 1; i >= 0; i--)
  {
    printf("%d ", path[i]);
  }
  printf("\n");

  free(q);
}

int main()
{
  int n;
  printf("Enter the number of vertices: ");
  scanf("%d", &n);

  int adjMatrix[MAX_VERTICES][MAX_VERTICES];

  printf("Enter the adjacency matrix:\n");
  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < n; j++)
    {
      scanf("%d", &adjMatrix[i][j]);
    }
  }

  int source, goal;
  printf("Enter the source and goal vertices: ");
  scanf("%d %d", &source, &goal);

  findShortestPath(n, adjMatrix, source, goal);

  return 0;
}

// 🚀 Kruskal's with minimum cost and all the paths

#include <stdio.h>
#include <stdlib.h>

#define MAX_ROADS 45

typedef struct
{
  int u, v, cost;
} Edge;

Edge edges[MAX_ROADS];
int parent[10];

int find(int i)
{
  if (parent[i] == i)
    return i;
  return parent[i] = find(parent[i]);
}

void unionSets(int u, int v)
{
  int rootU = find(u);
  int rootV = find(v);
  if (rootU != rootV)
  {
    parent[rootV] = rootU;
  }
}

int compareEdges(const void *a, const void *b)
{
  return ((Edge *)a)->cost - ((Edge *)b)->cost;
}

void kruskalMST(int N, int R)
{
  int totalCost = 0;
  int edgesInMST = 0;

  for (int i = 0; i < N; i++)
  {
    parent[i] = i;
  }

  qsort(edges, R, sizeof(Edge), compareEdges);

  printf("Minimum Spanning Tree:\n");

  for (int i = 0; i < R && edgesInMST < N - 1; i++)
  {
    Edge currentEdge = edges[i];
    int u = currentEdge.u;
    int v = currentEdge.v;
    int cost = currentEdge.cost;

    if (find(u) != find(v))
    {
      unionSets(u, v);
      printf("Building %d - Building %d: %d\n", u, v, cost);
      totalCost += cost;
      edgesInMST++;
    }
  }

  printf("Total Cost for Installation: %d\n", totalCost);
}

int main()
{
  int N, R;

  printf("Enter the number of buildings: ");
  scanf("%d", &N);

  printf("Enter the number of roads: ");
  scanf("%d", &R);

  printf("Enter the roads with their costs:\n");
  for (int i = 0; i < R; i++)
  {
    scanf("%d %d %d", &edges[i].u, &edges[i].v, &edges[i].cost);
  }

  kruskalMST(N, R);

  return 0;
}

// 🚀 Prims with minimum cost and all the paths

#include <stdio.h>
#include <limits.h>
#include <stdbool.h>

#define MAX_CITIES 8

int findMinKey(int key[], bool mstSet[], int n)
{
  int min = INT_MAX, minIndex;

  for (int v = 0; v < n; v++)
  {
    if (!mstSet[v] && key[v] < min)
    {
      min = key[v];
      minIndex = v;
    }
  }
  return minIndex;
}

void primMST(int costMatrix[MAX_CITIES][MAX_CITIES], int n)
{
  int parent[MAX_CITIES];
  int key[MAX_CITIES];
  bool mstSet[MAX_CITIES];

  for (int i = 0; i < n; i++)
  {
    key[i] = INT_MAX;
    mstSet[i] = false;
  }

  key[0] = 0;
  parent[0] = -1;

  for (int count = 0; count < n - 1; count++)
  {
    int u = findMinKey(key, mstSet, n);
    mstSet[u] = true; // Add the city to the MST set

    for (int v = 0; v < n; v++)
    {
      if (costMatrix[u][v] && !mstSet[v] && costMatrix[u][v] < key[v])
      {
        parent[v] = u;
        key[v] = costMatrix[u][v];
      }
    }
  }

  int totalCost = 0;
  printf("Minimum Spanning Tree:\n");

  for (int i = 1; i < n; i++)
  {
    printf("Edge %d:(%d %d) cost:%d\n", i, parent[i] + 1, i + 1, costMatrix[i][parent[i]]);
    totalCost += costMatrix[i][parent[i]];
  }

  printf("Minimum cost = %d\n", totalCost);
}

int main()
{
  int n;
  int costMatrix[MAX_CITIES][MAX_CITIES];

  printf("Enter the number of cities: ");
  scanf("%d", &n);

  printf("Enter the cost matrix:\n");
  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < n; j++)
    {
      scanf("%d", &costMatrix[i][j]);
    }
  }

  primMST(costMatrix, n);

  return 0;
}

// 🚀 Bipartite Graph

#include <stdio.h>
#include <stdbool.h>

#define MAX 6
#define UNCOLORED -1
#define RED 0
#define BLUE 1

bool isBipartite(int G[MAX][MAX], int n, int src)
{
  int color[MAX];
  for (int i = 0; i < n; i++)
  {
    color[i] = UNCOLORED;
  }

  color[src] = RED;
  int queue[MAX];
  int front = 0, rear = 0;
  queue[rear++] = src;

  while (front != rear)
  {
    int u = queue[front++];

    for (int v = 0; v < n; v++)
    {
      if (G[u][v] == 1 && u == v)
      {
        return false;
      }

      if (G[u][v] == 1 && color[v] == UNCOLORED)
      {
        color[v] = (color[u] == RED) ? BLUE : RED;
        queue[rear++] = v;
      }
      else if (G[u][v] == 1 && color[v] == color[u])
      {
        return false;
      }
    }
  }

  return true;
}

int main()
{
  int n;
  printf("Enter the number of computers (nodes): ");
  scanf("%d", &n);

  int G[MAX][MAX];
  printf("Enter the adjacency matrix:\n");
  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < n; j++)
    {
      scanf("%d", &G[i][j]);
    }
  }

  int src;
  printf("Enter the source computer (starting node): ");
  scanf("%d", &src);

  if (isBipartite(G, n, src))
  {
    printf("Yes, the given graph is Bipartite\n");
  }
  else
  {
    printf("No, the given graph is not Bipartite\n");
  }

  return 0;
}



// Hash Map

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 10

// Node structure for chaining
typedef struct Node {
    char key[50];
    int value;
    struct Node* next;
} Node;

// Hash table structure
Node* hashTable[TABLE_SIZE];

// Hash function
int hashFunction(char* key) {
    int hash = 0;
    while (*key) {
        hash += *key;
        key++;
    }
    return hash % TABLE_SIZE;
}

// Insert key-value pair
void insert(char* key, int value) {
    int index = hashFunction(key);
    Node* newNode = (Node*)malloc(sizeof(Node));
    strcpy(newNode->key, key);
    newNode->value = value;
    newNode->next = hashTable[index];
    hashTable[index] = newNode;
}

// Search for a key
int search(char* key) {
    int index = hashFunction(key);
    Node* temp = hashTable[index];
    while (temp) {
        if (strcmp(temp->key, key) == 0) {
            return temp->value;
        }
        temp = temp->next;
    }
    return -1; // Key not found
}

// Display the hashmap
void display() {
    for (int i = 0; i < TABLE_SIZE; i++) {
        printf("Bucket %d: ", i);
        Node* temp = hashTable[i];
        while (temp) {
            printf("(%s, %d) -> ", temp->key, temp->value);
            temp = temp->next;
        }
        printf("NULL\n");
    }
}

int main() {
    // Initialize hash table
    for (int i = 0; i < TABLE_SIZE; i++) {
        hashTable[i] = NULL;
    }

    insert("Alice", 20);
    insert("Bob", 25);
    insert("Charlie", 30);
    insert("Alice", 22); // Handles collision (same key)

    printf("Searching for Bob: %d\n", search("Bob"));
    printf("Searching for Alice: %d\n", search("Alice"));
    printf("Searching for Eve: %d\n", search("Eve"));

    display();

    return 0;
}

```
