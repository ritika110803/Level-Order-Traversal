C Program: Level Order Traversal of Binary Tree

This project demonstrates how to perform *Level Order Traversal (Breadth-First Traversal)* of a Binary Tree in C using a simple array-based queue.

---

Description

This program:

* Defines a binary tree node using struct
* Dynamically creates tree nodes using malloc()
* Implements a simple queue using an array
* Performs *Level Order Traversal* (Breadth-First Search)
* Prints nodes level by level from left to right

Level Order Traversal visits nodes in the order:


Root → Level 1 → Level 2 → Level 3 → ...


---

What is Level Order Traversal?

Level Order Traversal (also called *Breadth-First Search - BFS*) visits:

* First the root node
* Then all nodes at level 1
* Then all nodes at level 2
* And so on

It uses a *Queue* data structure internally.

---

Source Code

c

#include <stdio.h>

#include <stdlib.h>

// Structure of Node

struct Node {
    
    int data;
    struct Node* left;
    struct Node* right;
};

// Create new node

struct Node* createNode(int value) {
    
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Simple queue implementation for tree nodes

struct Node* queue[100];

int front = -1, rear = -1;

void enqueue(struct Node* node) {
    
    if (rear == 99)
        return;
    
    if (front == -1)
        front = 0;
    queue[++rear] = node;
}

struct Node* dequeue() {
    
    if (front == -1 || front > rear)
        return NULL;
    return queue[front++];
}

// Level Order Traversal

void levelOrder(struct Node* root) {
    
    if (root == NULL)
        return;

    enqueue(root);

    while (front <= rear) {
        
        struct Node* temp = dequeue();
        printf("%d ", temp->data);

        if (temp->left != NULL)
            enqueue(temp->left);

        if (temp->right != NULL)
            enqueue(temp->right);
    }
}

// Main function

int main() {
    
    struct Node* root = NULL;

    // Creating sample tree manually
    
    root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    printf("Level Order Traversal: ");
    levelOrder(root);

    return 0;
}


---

How to Compile and Run

Using GCC

1. Save the file as levelorder.c
2. Open terminal or command prompt
3. Compile the program:

bash
gcc levelorder.c -o levelorder


4. Run the program:

bash
./levelorder


(On Windows, use levelorder.exe)

---

Sample Output


Level Order Traversal: 1 2 3 4 5


---

Tree Structure Used in Example

The manually created tree:


        1
       / \
      2   3
     / \
    4   5


Traversal order:


1 → 2 → 3 → 4 → 5


---

Concepts Covered

* Binary Tree
* Breadth-First Search (BFS)
* Queue implementation using array
* Dynamic memory allocation
* Tree traversal algorithms

---

Time and Space Complexity

| Operation     | Complexity |
| ------------- | ---------- |
| Traversal     | O(n)       |
| Space (Queue) | O(n)       |

Where *n* is the number of nodes in the tree.

---

Possible Improvements

* Use dynamic queue instead of fixed-size array
* Add menu-driven tree creation
* Implement other traversals:

  * Inorder
  * Preorder
  * Postorder
* Add height and leaf node count functions

---
