slip sy
Assignment 1
Set A
a) Implement a Binary search tree (BST) library (btree h) with operations -
create, scarch, insert, inorder, preorder and postorder. Write a menu driven
program that performs the above operations.
Header File:
#include<stdio.h>
#include<stdlib.h>
struct bst
{
int data;
struct bst *lchild, *rchild;
} node;
int cnt=0,leafcnt=0,nleafcnt=0;
struct bst *create()
{
struct bst *temp=(struct bst*)malloc(sizeof(struct bst));
temp->lchild=NULL;
temp->rchild=NULL;
return temp;
}
void insert (struct bst *r, struct bst *new1)
{
if (new1->data < r->data)
{
if(r->lchild==NULL)
r->lchild=new1;
else
insert(r->lchild,new1);
}
if(new1->data > r->data)
{
if(r->rchild==NULL)
r->rchild=new1;
else
insert(r->rchild,new1);
}
}
struct bst *search (struct bst *r, int key)
Assignment 1: Binary search tree and traversals
{
struct bst *temp;
temp=r;
while(temp!=NULL)
{
if(temp ->data==key)
return temp;
if(key < temp->data)
temp=temp->lchild;
else
temp=temp->rchild;
}
return NULL;
}
void inorder(struct bst *temp)
{
if(temp!=NULL)
{
inorder(temp->lchild);
printf("%d\t", temp->data);
inorder(temp->rchild);
}
}
void postorder(struct bst *temp)
{
if(temp!=NULL)
{
postorder(temp->lchild);
postorder(temp->rchild);
printf("%d\t",temp->data);
}
}
void preorder(struct bst *temp)
{
if(temp!=NULL)
{
preorder(temp->lchild);
preorder(temp->rchild);
printf("%d\t",temp->data);
}
}
void inorder_n(struct bst *r)
{
struct bst *stack[100];
int top=-1;
if(r!=NULL)
{
top++;
stack[top]=r;
r=r->lchild;
while(top>=0)
{
while(r!=NULL)
{
top++;
stack[top]=r;
r=r->lchild;
}
r=stack[top];
top--;
printf("%d\t",r->data);
r=r->rchild;
}
}
}
Menu driven program:
#include<stdio.h>
#include<stdlib.h>
#include"btree.h"
int main()
{
int ch,n,i,value;
struct bst *newnode, *root, *temp;
root=NULL;
while(1)
{
printf("\n---Binary search treee---\n");
printf("1.create\n");
printf("2.Insert\n");
printf("3.search\n");
printf("4.inorder traversal (recursive)\n");
printf("5.postorder traversal (recursive)\n");
printf("6.preorder traversal (recursive)\n");
printf("7.inorder traversal (non recursive)\n");
printf("8.exit \n");
printf("enter your choice:");
scanf("%d",&ch);
switch(ch)
{
case 1: printf("\n how many node to create:");
scanf("%d",&n);
for(i=0;i<n;i++)
{
newnode=create();
printf("\nenter the node data:");
scanf("%d",&newnode->data);
if(root==NULL)
root=newnode;
else
insert(root,newnode);
}
break;
case 2: printf("\nenter the node value to searched:");
scanf("%d",&value);
temp=search(root,value);
if(temp==NULL)
printf("\nnode not found \n");
else
printf("\nnode found\n");
break;
case 3: printf("\n inorder traversal=");
inorder(root);
break;
case 4: printf("\n postorder traversal=");
postorder(root);
break;
case 5: printf("\n preorder traversal=");
preorder(root);
break;
case 6: printf("\n inorder traversal=");
inorder_n(root);
break;
case 7: exit(0);
default: printf("\n invalid choice \n");
}
}
}
Output:
---Binary search treee---
1.create
2.search
3.inorder traversal (recursive)
4.postorder traversal (recursive)
5.preorder traversal (recursive)
6.inorder traversal (non recursive)
7.exit
enter your choice:1
how many node to create:3
enter the node data:1
enter the node data:23
enter the node data:25
---Binary search treee---
1.create
2.search
3.inorder traversal (recursive)
4.postorder traversal (recursive)
5.preorder traversal (recursive)
6.inorder traversal (non recursive)
7.exit
enter your choice:3
inorder traversal=1 23 25
---Binary search treee---
1.create
2.search
3.inorder traversal (recursive)
4.postorder traversal (recursive)
5.preorder traversal (recursive)
6.inorder traversal (non recursive)
7.exit
enter your choice:7
b) Write a program which uses binary search tree library and counts the total
nodes and total leaf nodes in the tree.
int count(T) returns the total number of nodes from BST int countLeaf(T)-
returns the total number of leaf nodes from BST
Program:
#include<stdio.h>
#include<stdlib.h>
typedef struct Node
{
int data;
struct Node*left;
struct Node*right;
}Node;
Node* createNode(int data)
{
Node* newNode=(Node*)malloc(sizeof(Node));
newNode->data=data;
newNode->left=NULL;
newNode->right=NULL;
return newNode;
}
Node * insert(Node* root,int data)
{
if(root==NULL)
{
root = createNode(data);
}
else
if(data<=root->data)
{
root->left=insert(root->left,data);
}
else
{
root->right=insert(root->right,data);
}
return root;
}
int count (Node*root)
{
if(root==NULL)
{
return 0;
}
else
return 1+count(root->left)+count(root->right);
}
int main()
{
Node *root=NULL;
root=insert(root,8);
root=insert(root,3);
root=insert(root,10);
root=insert(root,1);
root=insert(root,6);
root=insert(root,14);
root=insert(root,4);
root=insert(root,7);
root=insert(root,13);
int totalcount=count(root);
int leafcount=count(root);
printf("total number of nodes in the binary search
tree:%d\n",totalcount);
printf("total number of nodes in the binary search
tree:%d\n",leafcount);
return 0;
}
Output:
total number of nodes in the binary search tree:9
total number of nodes in the binary search tree:9
Set B
a) Write a C program which uses Binary search tree library and implements following
function with recursion:
T copy(T) - create another BST which is exact copy of BST which is passed as parameter. int
compare(T1, T2) - compares two binary search trees and returns 1 if they are equal and 0
otherwise.
Program:
#include <stdio.h>
#include <stdlib.h>
typedef struct node {
int data;
struct node* left;
struct node* right;
} node;
// Function to create a new node
node* newNode(int data) {
node* new = (node*)malloc(sizeof(node));
new->data = data;
new->left = NULL;
new->right = NULL;
return new;
}
// Function to insert a node in the BST
node* insert(node* root, int data) {
if (root == NULL) {
return newNode(data);
}
if (data < root->data) {
root->left = insert(root->left, data);
} else if (data > root->data) {
root->right = insert(root->right, data);
}
return root;
}
// Function to copy a BST
node* copy(node* root) {
if (root == NULL) {
return NULL;
}
node* new = newNode(root->data);
new->left = copy(root->left);
new->right = copy(root->right);
return new;
}
// Function to compare two BSTs
int compare(node* root1, node* root2) {
if (root1 == NULL && root2 == NULL) {
return 1;
}
if (root1 != NULL && root2 != NULL) {
return (root1->data == root2->data &&
compare(root1->left, root2->left) &&
compare(root1->right, root2->right));
}
return 0;
}
// Driver code
int main() {
node* root1 = NULL;
node* root2 = NULL;
root1 = insert(root1, 50);
insert(root1, 30);
insert(root1, 20);
insert(root1, 40);
insert(root1, 70);
insert(root1, 60);
insert(root1, 80);
root2 = copy(root1);
if (compare(root1, root2) == 1) {
printf("BSTs are equal\n");
} else {
printf("BSTs are not equal\n");
}
return 0;
}
Output: BSTs are equal
Set C
a) Write a C program which uses Binary search tree library and implements
following two functions
int sumodd(T) - returnssum of all odd numbers from BST intsumeven(T) -
returnssum of all even numbers from BST mirror(T) -converts given tree into its
mirror image.
Program:
#include <stdio.h>
#include <stdlib.h>
// Binary search tree node structure
struct node {
int data;
struct node *left, *right;
};
// Create a new node
struct node* newNode(int data) {
struct node* node = (struct node*)malloc(sizeof(struct node));
node->data = data;
node->left = node->right = NULL;
return node;
}
// Insert a node in BST
struct node* insert(struct node* node, int data) {
if (node == NULL) {
return newNode(data);
}
if (data < node->data) {
node->left = insert(node->left, data);
}
else if (data > node->data) {
node->right = insert(node->right, data);
}
return node;
}
// In-order traversal of BST
void inorder(struct node* root) {
if (root != NULL) {
inorder(root->left);
printf("%d ", root->data);
inorder(root->right);
}
}
// Sum of all odd numbers in BST
int sumodd(struct node* root) {
int sum = 0;
if (root != NULL) {
sum += sumodd(root->left);
if (root->data % 2 == 1) {
sum += root->data;
}
sum += sumodd(root->right);
}
return sum;
}
// Sum of all even numbers in BST
int sumeven(struct node* root) {
int sum = 0;
if (root != NULL) {
sum += sumeven(root->left);
if (root->data % 2 == 0) {
sum += root->data;
}
sum += sumeven(root->right);
}
return sum;
}
// Convert given tree into its mirror image
void mirror(struct node* root) {
if (root == NULL) {
return;
}
mirror(root->left);
mirror(root->right);
// Swap left and right sub-trees
struct node* temp = root->left;
root->left = root->right;
root->right = temp;
}
// Driver program
int main() {
struct node* root = NULL;
root = insert(root, 6);
insert(root, 3);
insert(root, 9);
insert(root, 1);
insert(root, 5);
insert(root, 7);
insert(root, 11);
printf("In-order traversal of BST: ");
inorder(root);
printf("\n");
printf("Sum of all odd numbers in BST: %d\n", sumodd(root));
printf("Sum of all even numbers in BST: %d\n", sumeven(root));
mirror(root);
printf("In-order traversal of BST after mirror image conversion:
");
inorder(root);
printf("\n");
return 0;
}
Output:
In-order traversal of BST: 1 3 5 6 7 9 11
Sum of all odd numbers in BST: 36
Sum of all even numbers in BST: 6
In-order traversal of BST after mirror image conversion: 11 9 7 6 5 3 1
b) Write a function to delete an element from BST.
Function:
1. void deletion(Node*& root, int item)
2. {
3. Node* parent = NULL;
4. Node* cur = root;
5.
6. search(cur, item, parent);
7. if (cur == NULL)
8. return;
9.
10. if (cur->left == NULL && cur->right == NULL)
11. {
12. if (cur != root)
13. {
14. if (parent->left == cur)
15. parent->left = NULL;
16. else
17. parent->right = NULL;
18. }
19. else
20. root = NULL;
21.
22. free(cur);
23. }
24. else if (cur->left && cur->right)
25. {
26. Node* succ = findMinimum(cur- >right);
27.
28. int val = succ->data;
29.
30. deletion(root, succ->data);
31.
32. cur->data = val;
33. }
34.
35. else
36. {
37. Node* child = (cur->left)? Cur- >left: cur->right;
38.
39. if (cur != root)
40. {
41. if (cur == parent->left)
42. parent->left = child;
43. else
44. parent->right = child;
45. }
46.
47. else
48. root = child;
49. free(cur);
50. }
51. }
52.
53. Node* findMinimum(Node* cur)
54. {
55. while(cur->left != NULL) {
56. cur = cur->left;
57. }
58. return cur;
59. }
c) What modifications are required in search function to count the number of
comparisons required?
Program :
int binarySearch(int arr[], int n, int x, int *count)
{
 int low = 0, high = n - 1;
 while (low <= high)
 {
 int mid = (low + high) / 2;
 (*count)++; // increment comparison counter
 if (arr[mid] == x)
 return mid;
 if (arr[mid] < x)
 low = mid + 1;
 else
 high = mid - 1;
 }
 return -1;
}
This in this modified function, we have added a new parameter count, which is pointer to an
integer that will keep track of the number of comparisons made. inside the while loop, we
increment the count variable each time a comparison is made. this modificatin will allow us
to keep track of the number of comparisons made during the search.


Assignment 2
Set A
a) Write a C program which uses Binary search tree library and displays nodes
at each level. count of node at each level and total levels in the tree.
Header File:
#include <stdio.h>
#include <stdlib.h>
typedef struct Node
{
int data;
struct Node *left;
struct Node *right;
} Node;
Node *createNode(int data)
{
Node *node = (Node *)malloc(sizeof(Node));
node->data = data;
node->left = NULL;
node->right = NULL;
return node;
}
Node *insert(Node *node, int data)
{
if (node == NULL)
{
return createNode(data);
Assignment 2: Binary Tree applications
}
if (data < node->data)
{
node->left = insert(node->left, data);
}
else if (data > node->data)
{
node->right = insert(node->right, data);
}
return node;
}
void printLevel(Node *root, int level, int *count)
{
if (root == NULL)
{
return;
}
if (level == 1)
{
printf("%d ", root->data);
(*count)++;
}
else if (level > 1)
{
printLevel(root->left, level - 1, count);
printLevel(root->right, level - 1, count);
}
}
void printLevels(Node *root)
{
int i, count;
int height = 0;
int level_counts[100] = {0};
for (i = 1; i <= height + 1; i++)
{
count = 0;
printLevel(root, i, &count);
level_counts[i] = count;
if (count > 0)
{
height = i;
printf("\n");
}
}
printf("Total levels: %d\n", height);
printf("Node count per level: ");
for (i = 1; i <= height; i++)
{
printf("%d ", level_counts[i]);
}
}
Program:
#include <stdio.h>
#include <stdlib.h>
#include "btree2.h"
int main()
{
Node *root = NULL;
root = insert(root, 50);
insert(root, 30);
insert(root, 20);
insert(root, 40);
insert(root, 70);
insert(root, 60);
insert(root, 80);
printLevels(root);
return 0;
}
Output:
50
30 70
20 40 60 80
Total levels: 3
Node count per level: 1 2 4
Set B
a) Write a program to sort n randomly generated elements using Heapsort
method.
Program:
#include <stdio.h>
#include <stdlib.h>
void heapify(int arr[], int n, int i) {
int largest = i; // Initialize largest as root
int l = 2*i + 1; // left = 2*i + 1
int r = 2*i + 2; // right = 2*i + 2
// If left child is larger than root
if (l < n && arr[l] > arr[largest])
largest = l;
// If right child is larger than largest so far
if (r < n && arr[r] > arr[largest])
largest = r;
// If largest is not root
if (largest != i) {
int temp = arr[i];
arr[i] = arr[largest];
arr[largest] = temp;
// Recursively heapify the affected sub-tree
heapify(arr, n, largest);
}
}
void heapsort(int arr[], int n) {
// Build heap (rearrange array)
for (int i = n / 2 - 1; i >= 0; i--)
heapify(arr, n, i);
// One by one extract an element from heap
for (int i = n - 1; i >= 0; i--) {
// Move current root to end
int temp = arr[0];
arr[0] = arr[i];
arr[i] = temp;
// call max heapify on the reduced heap
heapify(arr, i, 0);
}
}
int main() {
int n;
printf("Enter the number of elements: ");
scanf("%d", &n);
int arr[n];
printf("Enter %d elements: ", n);
for (int i = 0; i < n; i++)
scanf("%d", &arr[i]);
heapsort(arr, n);
printf("Sorted array: ");
for (int i = 0; i < n; i++)
printf("%d ", arr[i]);
printf("\n");
return 0;
}
Output:
Enter the number of elements: 9
Enter 9 elements: 15
23
26
29
34
68
12
11
10
Sorted array: 10 11 12 15 23 26 29 34 68
Set C
a) Which data structure will be required to display nodes of BST depth wise?
Program:
#include <stdio.h>
#include <stdlib.h>
struct Node {
int data;
struct Node* left;
struct Node* right;
};
// function to create a new node in BST
struct Node* newNode(int data)
{
struct Node* node = (struct Node*)malloc(sizeof(struct
Node));
node->data = data;
node->left = NULL;
node->right = NULL;
return node;
}
// function to display nodes of BST depth-wise
void displayNodesDepthWise(struct Node* root)
{
// check if the BST is empty
if (root == NULL) {
return;
}
// create a queue and enqueue the root node
struct Node** queue = (struct
Node**)malloc(sizeof(struct Node*));
int front = 0, rear = 0;
queue[rear] = root;
rear++;
// loop through all the nodes in the queue
while (front < rear) {
// dequeue the next node from the front of the queue
struct Node* node = queue[front];
front++;
// print the value of the dequeued node
printf("%d ", node->data);
// enqueue the left and right child of the dequeued
node (if they exist)
if (node->left != NULL) {
queue = (struct Node**)realloc(queue, (rear + 1)
* sizeof(struct Node*));
queue[rear] = node->left;
rear++;
}
if (node->right != NULL) {
queue = (struct Node**)realloc(queue, (rear + 1)
* sizeof(struct Node*));
queue[rear] = node->right;
rear++;
}
}
// free the queue memory
free(queue);
}
// driver code to test the implementation
int main()
{
// create a sample BST
struct Node* root = newNode(50);
root->left = newNode(30);
root->right = newNode(70);
root->left->left = newNode(20);
root->left->right = newNode(40);
root->right->left = newNode(60);
root->right->right = newNode(80);
// display nodes of the BST depth-wise
printf("Nodes of BST displayed depth-wise: ");
displayNodesDepthWise(root);
return 0;
}
Output:
Nodes of BST displayed depth-wise: 50 30 70 20 40 60 80
b) Write a C program to displays nodes of BST depth wise.
Program:
#include<stdio.h>
#include<stdlib.h>
// Definition of a BST node
struct node
{
int data;
struct node* left;
struct node* right;
};
// Function to create a new BST node
struct node* new_node(int data)
{
struct node* temp = (struct node*)malloc(sizeof(struct
node));
temp->data = data;
temp->left = NULL;
temp->right = NULL;
return temp;
}
// Function to insert a new node in the BST
struct node* insert(struct node* root, int data)
{
if(root == NULL)
return new_node(data);
if(data < root->data)
root->left = insert(root->left, data);
else if(data > root->data)
root->right = insert(root->right, data);
return root;
}
// Function to display the nodes of a BST depth-wise
void display_nodes_depth_wise(struct node* root, int level)
{
if(root == NULL)
return;
if(level == 1)
printf("%d ", root->data);
else if(level > 1)
{
display_nodes_depth_wise(root->left, level-1);
display_nodes_depth_wise(root->right, level-1);
}
}
// Function to get the height of a BST
int get_height(struct node* root)
{
if(root == NULL)
return 0;
int left_height = get_height(root->left);
int right_height = get_height(root->right);
return (left_height > right_height ? left_height :
right_height) + 1;
}
// Main function
int main()
{
struct node* root = NULL;
root = insert(root, 50);
insert(root, 30);
insert(root, 20);
insert(root, 40);
insert(root, 70);
insert(root, 60);
insert(root, 80);
int height = get_height(root);
for(int level=1; level<=height; level++)
{
printf("Level %d: ", level);
display_nodes_depth_wise(root, level);
printf("\n");
}
return 0;
}
Output:
Level 1: 50
Level 2: 30 70
Level 3: 20 40 60 80
c) Write a C program to compare two binary search trees (node data wise
comparison).
Program:
#include <stdio.h>
#include <stdlib.h>
// Structure of a node in the binary search tree
struct node {
int data;
struct node* left;
struct node* right;
};
// Function to create a new node with the given data
struct node* newNode(int data) {
struct node* node = (struct node*)malloc(sizeof(struct
node));
node->data = data;
node->left = NULL;
node->right = NULL;
return node;
}
// Function to insert a new node with the given data in the
binary search tree
struct node* insert(struct node* node, int data) {
if (node == NULL)
return newNode(data);
if (data < node->data)
node->left = insert(node->left, data);
else if (data > node->data)
node->right = insert(node->right, data);
return node;
}
// Function to compare two binary search trees node datawise
int compareTrees(struct node* root1, struct node* root2) {
// If both trees are empty, return true
if (root1 == NULL && root2 == NULL)
return 1;
// If one tree is empty and the other is not, return
false
if (root1 == NULL || root2 == NULL)
return 0;
// Compare the data of the current nodes
if (root1->data != root2->data)
return 0;
// Recursively compare the left and right subtrees
return compareTrees(root1->left, root2->left) &&
compareTrees(root1->right, root2->right);
}
// Driver program to test the above functions
int main() {
// Create the first binary search tree
struct node* root1 = NULL;
root1 = insert(root1, 50);
insert(root1, 30);
insert(root1, 20);
insert(root1, 40);
insert(root1, 70);
insert(root1, 60);
insert(root1, 80);
// Create the second binary search tree
struct node* root2 = NULL;
root2 = insert(root2, 50);
insert(root2, 30);
insert(root2, 20);
insert(root2, 90);
insert(root2, 70);
insert(root2, 60);
insert(root2, 80);
// Compare the two binary search trees
if (compareTrees(root1, root2))
printf("The two binary search trees are
identical.\n");
else
printf("The two binary search trees are not
identical.\n");
return 0;
}
Output:
The two binary search trees are not identical.
d) How to implement mirror) and copy() functions without recursion?
ANS:
To implement mirror and copy functions in C language without recursion, you can use
iterative approaches. Here are examples of how you can implement these functions:
(1)Mirror Function:
void mirror(TreeNode* root) {
 if (root == NULL) {
 return;
 }

 Queue q;
 queue_init(&q);
 queue_enqueue(&q, root);

 while (!queue_is_empty(&q)) {
 TreeNode* node = queue_dequeue(&q);

 TreeNode* temp = node->left;
 node->left = node->right;
 node->right = temp;

 if (node->left != NULL) {
 queue_enqueue(&q, node->left);
 }

 if (node->right != NULL) {
 queue_enqueue(&q, node->right);
 }
 }

 queue_destroy(&q);
}
In this implementation, we use a queue to perform a level-order traversal of the
binary tree. At each node, we swap its left and right child pointers. Then, we enqueue
the left and right child pointers (if they exist) onto the queue. We continue this
process until the queue is empty.
(2)Copy Function:
TreeNode* copy(TreeNode* root) {
 if (root == NULL) {
 return NULL;
 }

 Queue q;
 queue_init(&q);
 queue_enqueue(&q, root);

 TreeNode* new_root = create_node(root->data);
 Queue new_q;
 queue_init(&new_q);
 queue_enqueue(&new_q, new_root);

 while (!queue_is_empty(&q)) {
 TreeNode* node = queue_dequeue(&q);
 TreeNode* new_node = queue_dequeue(&new_q);

 if (node->left != NULL) {
 TreeNode* new_left = create_node(node->left->data);
 new_node->left = new_left;
 queue_enqueue(&q, node->left);
 queue_enqueue(&new_q, new_left);
 }

 if (node->right != NULL) {
 TreeNode* new_right = create_node(node->right->data);
 new_node->right = new_right;
 queue_enqueue(&q, node->right);
 queue_enqueue(&new_q, new_right);
 }
 }

 queue_destroy(&q);
 queue_destroy(&new_q);

 return new_root;
}
In this implementation, we also use a queue to perform a level-order traversal of the
binary tree. At each node, we create a new node with the same data and enqueue it
onto a separate queue. We then enqueue the left and right child pointers (if they
exist) onto the original queue and their corresponding new nodes onto the separate
queue. We continue this process until the original queue is empty. Finally, we return
the root of the new binary tree. Note that the create_node function creates a new
node with the given data and NULL left and right child pointers.
e) How to convert singly linked list to binary search tree?
Program:
#include <stdio.h>
#include <stdlib.h>
struct ListNode
{
int val;
struct ListNode *next;
};
struct TreeNode
{
int val;
struct TreeNode *left;
struct TreeNode *right;
};
struct TreeNode *sortedArrayToBST(int *nums, int start, int
end)
{
if (start > end)
{
return NULL;Set A
a) Write a C program which uses Binary search tree library and displays nodes
at each level. count of node at each level and total levels in the tree.
Header File:
#include <stdio.h>
#include <stdlib.h>
typedef struct Node
{
int data;
struct Node *left;
struct Node *right;
} Node;
Node *createNode(int data)
{
Node *node = (Node *)malloc(sizeof(Node));
node->data = data;
node->left = NULL;
node->right = NULL;
return node;
}
Node *insert(Node *node, int data)
{
if (node == NULL)
{
return createNode(data);
Assignment 2: Binary Tree applications
}
if (data < node->data)
{
node->left = insert(node->left, data);
}
else if (data > node->data)
{
node->right = insert(node->right, data);
}
return node;
}
void printLevel(Node *root, int level, int *count)
{
if (root == NULL)
{
return;
}
if (level == 1)
{
printf("%d ", root->data);
(*count)++;
}
else if (level > 1)
{
printLevel(root->left, level - 1, count);
printLevel(root->right, level - 1, count);
}
}
void printLevels(Node *root)
{
int i, count;
int height = 0;
int level_counts[100] = {0};
for (i = 1; i <= height + 1; i++)
{
count = 0;
printLevel(root, i, &count);
level_counts[i] = count;
if (count > 0)
{
height = i;
printf("\n");
}
}
printf("Total levels: %d\n", height);
printf("Node count per level: ");
for (i = 1; i <= height; i++)
{
printf("%d ", level_counts[i]);
}
}
Program:
#include <stdio.h>
#include <stdlib.h>
#include "btree2.h"
int main()
{
Node *root = NULL;
root = insert(root, 50);
insert(root, 30);
insert(root, 20);
insert(root, 40);
insert(root, 70);
insert(root, 60);
insert(root, 80);
printLevels(root);
return 0;
}
Output:
50
30 70
20 40 60 80
Total levels: 3
Node count per level: 1 2 4
Set B
a) Write a program to sort n randomly generated elements using Heapsort
method.
Program:
#include <stdio.h>
#include <stdlib.h>
void heapify(int arr[], int n, int i) {
int largest = i; // Initialize largest as root
int l = 2*i + 1; // left = 2*i + 1
int r = 2*i + 2; // right = 2*i + 2
// If left child is larger than root
if (l < n && arr[l] > arr[largest])
largest = l;
// If right child is larger than largest so far
if (r < n && arr[r] > arr[largest])
largest = r;
// If largest is not root
if (largest != i) {
int temp = arr[i];
arr[i] = arr[largest];
arr[largest] = temp;
// Recursively heapify the affected sub-tree
heapify(arr, n, largest);
}
}
void heapsort(int arr[], int n) {
// Build heap (rearrange array)
for (int i = n / 2 - 1; i >= 0; i--)
heapify(arr, n, i);
// One by one extract an element from heap
for (int i = n - 1; i >= 0; i--) {
// Move current root to end
int temp = arr[0];
arr[0] = arr[i];
arr[i] = temp;
// call max heapify on the reduced heap
heapify(arr, i, 0);
}
}
int main() {
int n;
printf("Enter the number of elements: ");
scanf("%d", &n);
int arr[n];
printf("Enter %d elements: ", n);
for (int i = 0; i < n; i++)
scanf("%d", &arr[i]);
heapsort(arr, n);
printf("Sorted array: ");
for (int i = 0; i < n; i++)
printf("%d ", arr[i]);
printf("\n");
return 0;
}
Output:
Enter the number of elements: 9
Enter 9 elements: 15
23
26
29
34
68
12
11
10
Sorted array: 10 11 12 15 23 26 29 34 68
Set C
a) Which data structure will be required to display nodes of BST depth wise?
Program:
#include <stdio.h>
#include <stdlib.h>
struct Node {
int data;
struct Node* left;
struct Node* right;
};
// function to create a new node in BST
struct Node* newNode(int data)
{
struct Node* node = (struct Node*)malloc(sizeof(struct
Node));
node->data = data;
node->left = NULL;
node->right = NULL;
return node;
}
// function to display nodes of BST depth-wise
void displayNodesDepthWise(struct Node* root)
{
// check if the BST is empty
if (root == NULL) {
return;
}
// create a queue and enqueue the root node
struct Node** queue = (struct
Node**)malloc(sizeof(struct Node*));
int front = 0, rear = 0;
queue[rear] = root;
rear++;
// loop through all the nodes in the queue
while (front < rear) {
// dequeue the next node from the front of the queue
struct Node* node = queue[front];
front++;
// print the value of the dequeued node
printf("%d ", node->data);
// enqueue the left and right child of the dequeued
node (if they exist)
if (node->left != NULL) {
queue = (struct Node**)realloc(queue, (rear + 1)
* sizeof(struct Node*));
queue[rear] = node->left;
rear++;
}
if (node->right != NULL) {
queue = (struct Node**)realloc(queue, (rear + 1)
* sizeof(struct Node*));
queue[rear] = node->right;
rear++;
}
}
// free the queue memory
free(queue);
}
// driver code to test the implementation
int main()
{
// create a sample BST
struct Node* root = newNode(50);
root->left = newNode(30);
root->right = newNode(70);
root->left->left = newNode(20);
root->left->right = newNode(40);
root->right->left = newNode(60);
root->right->right = newNode(80);
// display nodes of the BST depth-wise
printf("Nodes of BST displayed depth-wise: ");
displayNodesDepthWise(root);
return 0;
}
Output:
Nodes of BST displayed depth-wise: 50 30 70 20 40 60 80
b) Write a C program to displays nodes of BST depth wise.
Program:
#include<stdio.h>
#include<stdlib.h>
// Definition of a BST node
struct node
{
int data;
struct node* left;
struct node* right;
};
// Function to create a new BST node
struct node* new_node(int data)
{
struct node* temp = (struct node*)malloc(sizeof(struct
node));
temp->data = data;
temp->left = NULL;
temp->right = NULL;
return temp;
}
// Function to insert a new node in the BST
struct node* insert(struct node* root, int data)
{
if(root == NULL)
return new_node(data);
if(data < root->data)
root->left = insert(root->left, data);
else if(data > root->data)
root->right = insert(root->right, data);
return root;
}
// Function to display the nodes of a BST depth-wise
void display_nodes_depth_wise(struct node* root, int level)
{
if(root == NULL)
return;
if(level == 1)
printf("%d ", root->data);
else if(level > 1)
{
display_nodes_depth_wise(root->left, level-1);
display_nodes_depth_wise(root->right, level-1);
}
}
// Function to get the height of a BST
int get_height(struct node* root)
{
if(root == NULL)
return 0;
int left_height = get_height(root->left);
int right_height = get_height(root->right);
return (left_height > right_height ? left_height :
right_height) + 1;
}
// Main function
int main()
{
struct node* root = NULL;
root = insert(root, 50);
insert(root, 30);
insert(root, 20);
insert(root, 40);
insert(root, 70);
insert(root, 60);
insert(root, 80);
int height = get_height(root);
for(int level=1; level<=height; level++)
{
printf("Level %d: ", level);
display_nodes_depth_wise(root, level);
printf("\n");
}
return 0;
}
Output:
Level 1: 50
Level 2: 30 70
Level 3: 20 40 60 80
c) Write a C program to compare two binary search trees (node data wise
comparison).
Program:
#include <stdio.h>
#include <stdlib.h>
// Structure of a node in the binary search tree
struct node {
int data;
struct node* left;
struct node* right;
};
// Function to create a new node with the given data
struct node* newNode(int data) {
struct node* node = (struct node*)malloc(sizeof(struct
node));
node->data = data;
node->left = NULL;
node->right = NULL;
return node;
}
// Function to insert a new node with the given data in the
binary search tree
struct node* insert(struct node* node, int data) {
if (node == NULL)
return newNode(data);
if (data < node->data)
node->left = insert(node->left, data);
else if (data > node->data)
node->right = insert(node->right, data);
return node;
}
// Function to compare two binary search trees node datawise
int compareTrees(struct node* root1, struct node* root2) {
// If both trees are empty, return true
if (root1 == NULL && root2 == NULL)
return 1;
// If one tree is empty and the other is not, return
false
if (root1 == NULL || root2 == NULL)
return 0;
// Compare the data of the current nodes
if (root1->data != root2->data)
return 0;
// Recursively compare the left and right subtrees
return compareTrees(root1->left, root2->left) &&
compareTrees(root1->right, root2->right);
}
// Driver program to test the above functions
int main() {
// Create the first binary search tree
struct node* root1 = NULL;
root1 = insert(root1, 50);
insert(root1, 30);
insert(root1, 20);
insert(root1, 40);
insert(root1, 70);
insert(root1, 60);
insert(root1, 80);
// Create the second binary search tree
struct node* root2 = NULL;
root2 = insert(root2, 50);
insert(root2, 30);
insert(root2, 20);
insert(root2, 90);
insert(root2, 70);
insert(root2, 60);
insert(root2, 80);
// Compare the two binary search trees
if (compareTrees(root1, root2))
printf("The two binary search trees are
identical.\n");
else
printf("The two binary search trees are not
identical.\n");
return 0;
}
Output:
The two binary search trees are not identical.
d) How to implement mirror) and copy() functions without recursion?
ANS:
To implement mirror and copy functions in C language without recursion, you can use
iterative approaches. Here are examples of how you can implement these functions:
(1)Mirror Function:
void mirror(TreeNode* root) {
 if (root == NULL) {
 return;
 }

 Queue q;
 queue_init(&q);
 queue_enqueue(&q, root);

 while (!queue_is_empty(&q)) {
 TreeNode* node = queue_dequeue(&q);

 TreeNode* temp = node->left;
 node->left = node->right;
 node->right = temp;

 if (node->left != NULL) {
 queue_enqueue(&q, node->left);
 }

 if (node->right != NULL) {
 queue_enqueue(&q, node->right);
 }
 }

 queue_destroy(&q);
}
In this implementation, we use a queue to perform a level-order traversal of the
binary tree. At each node, we swap its left and right child pointers. Then, we enqueue
the left and right child pointers (if they exist) onto the queue. We continue this
process until the queue is empty.
(2)Copy Function:
TreeNode* copy(TreeNode* root) {
 if (root == NULL) {
 return NULL;
 }

 Queue q;
 queue_init(&q);
 queue_enqueue(&q, root);

 TreeNode* new_root = create_node(root->data);
 Queue new_q;
 queue_init(&new_q);
 queue_enqueue(&new_q, new_root);

 while (!queue_is_empty(&q)) {
 TreeNode* node = queue_dequeue(&q);
 TreeNode* new_node = queue_dequeue(&new_q);

 if (node->left != NULL) {
 TreeNode* new_left = create_node(node->left->data);
 new_node->left = new_left;
 queue_enqueue(&q, node->left);
 queue_enqueue(&new_q, new_left);
 }

 if (node->right != NULL) {
 TreeNode* new_right = create_node(node->right->data);
 new_node->right = new_right;
 queue_enqueue(&q, node->right);
 queue_enqueue(&new_q, new_right);
 }
 }

 queue_destroy(&q);
 queue_destroy(&new_q);

 return new_root;
}
In this implementation, we also use a queue to perform a level-order traversal of the
binary tree. At each node, we create a new node with the same data and enqueue it
onto a separate queue. We then enqueue the left and right child pointers (if they
exist) onto the original queue and their corresponding new nodes onto the separate
queue. We continue this process until the original queue is empty. Finally, we return
the root of the new binary tree. Note that the create_node function creates a new
node with the given data and NULL left and right child pointers.
e) How to convert singly linked list to binary search tree?
Program:
#include <stdio.h>
#include <stdlib.h>
struct ListNode
{
int val;
struct ListNode *next;
};
struct TreeNode
{
int val;
struct TreeNode *left;
struct TreeNode *right;
};
struct TreeNode *sortedArrayToBST(int *nums, int start, int
end)
{
if (start > end)
{
return NULL;
}
int mid = (start + end) / 2;
struct TreeNode *root = (struct TreeNode
*)malloc(sizeof(struct TreeNode));
root->val = nums[mid];
root->left = sortedArrayToBST(nums, start, mid - 1);
root->right = sortedArrayToBST(nums, mid + 1, end);
return root;
}
}
int mid = (start + end) / 2;
struct TreeNode *root = (struct TreeNode
*)malloc(sizeof(struct TreeNode));
root->val = nums[mid];
root->left = sortedArrayToBST(nums, start, mid - 1);
root->right = sortedArrayToBST(nums, mid + 1, end);
return root;
}


Assignment 3
Set A
A . Write a C program that accepts the vertices and edges of a graph and
stores it as an adjacency matrix. Display the adjacency matrix.
Ans: program in C that accepts the number of vertices and edges of a graph,
and stores it as an adjacency matrix. It then displays the adjacency matrix:
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 100
int adjMatrix[MAX_VERTICES][MAX_VERTICES];
int numVertices;
// Initialize the graph with the given number of vertices
void initGraph(int n) {
int i, j;
numVertices = n;
for (i = 0; i < numVertices; i++) {
for (j = 0; j < numVertices; j++) {
adjMatrix[i][j] = 0;
}
}
}
// Add a directed edge from vertex i to vertex j
void addEdge(int i, int j) {
adjMatrix[i][j] = 1;
}
// Displays the adjacency matrix for the graph
void displayAdjMatrix() {
int i, j;
printf("Adjacency matrix:\n");
for (i = 0; i < numVertices; i++) {
for (j = 0; j < numVertices; j++) {
printf("%d ", adjMatrix[i][j]);
}
printf("\n");
}
}
int main() {
int numEdges, i, j, v1, v2;
 Assignment 3: Graph as adjacency list
printf("Enter the number of vertices: ");
scanf("%d", &numVertices);
initGraph(numVertices);
printf("Enter the number of edges: ");
scanf("%d", &numEdges);
printf("Enter the edges as pairs of vertices (e.g. 1 2):\n");
for (i = 0; i < numEdges; i++) {
scanf("%d %d", &v1, &v2);
addEdge(v1, v2);
}
displayAdjMatrix();
return 0;
}
Output :
Enter the number of vertices: 4
Enter the number of edges: 5
Enter the edges as pairs of vertices (e.g. 1 2):
0 1
1 2
2 3
3 0
1 3
Adjacency matrix:
0 1 0 0
0 0 1 1
0 0 0 1
1 0 0 0
------------------------------------------------------------------------------------------
B. Write a C program that accepts the vertices and edges of a graph and
store it as an adjacency matrix. Implement functions to print indegree,
outdegree and total degree of all vertices of graph.
Ans: program that accepts the vertices and edges of a graph and stores it as an
adjacency matrix. It also implements functions to print the indegree, outdegree,
and total degree of all vertices of the graph:
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 100
int adjMatrix[MAX_VERTICES][MAX_VERTICES];
int numVertices;
// Initialize the graph with the given number of vertices
void initGraph(int n) {
int i, j;
numVertices = n;
for (i = 0; i < numVertices; i++) {
for (j = 0; j < numVertices; j++) {
adjMatrix[i][j] = 0;
}
}
}
// Add a directed edge from vertex i to vertex j
void addEdge(int i, int j) {
adjMatrix[i][j] = 1;
}
// Displays the adjacency matrix for the graph
void displayAdjMatrix() {
int i, j;
printf("Adjacency matrix:\n");
for (i = 0; i < numVertices; i++) {
for (j = 0; j < numVertices; j++) {
printf("%d ", adjMatrix[i][j]);
}
printf("\n");
}
}
// Returns the indegree of the given vertex
int indegree(int vertex) {
int i, in = 0;
for (i = 0; i < numVertices; i++) {
if (adjMatrix[i][vertex]) {
in++;
}
}
return in;
}
// Returns the outdegree of the given vertex
int outdegree(int vertex) {
int i, out = 0;
for (i = 0; i < numVertices; i++) {
if (adjMatrix[vertex][i]) {
out++;
}
}
return out;
}
// Returns the total degree of the given vertex
int degree(int vertex) {
return indegree(vertex) + outdegree(vertex);
}
// Displays the indegree, outdegree, and total degree of all
vertices
void displayDegree() {
int i;
printf("Vertex\tIndegree\tOutdegree\tTotal degree\n");
for (i = 0; i < numVertices; i++) {
printf("%d\t%d\t\t%d\t\t%d\n", i, indegree(i), outdegree(i),
degree(i));
}
}
int main() {
int numEdges, i, v1, v2;
printf("Enter the number of vertices: ");
scanf("%d", &numVertices);
initGraph(numVertices);
printf("Enter the number of edges: ");
scanf("%d", &numEdges);
printf("Enter the edges as pairs of vertices (e.g. 1 2):\n");
for (i = 0; i < numEdges; i++) {
scanf("%d %d", &v1, &v2);
addEdge(v1, v2);
}
displayAdjMatrix();
displayDegree();
return 0;
}
Output:
Enter the number of vertices: 2
Enter the number of edges: 3
Enter the edges as pairs of vertices (e.g. 1 2):
3 5
2 3
5 6
Adjacency matrix:
0 0
0 0
Vertex Indegree Outdegree Total degree
0 0 0 0 0 0
1 0 0 0 0 0
Set B
A.Write a C program that accepts the vertices and edges of a
graph and store it as an adjacency matrix. Implement function
to traverse the graph using Breadth First Search (BFS)
traversal.
Ans: C program that accepts the vertices and edges of a graph and stores it
as an adjacency matrix. It also implements a function to traverse the graph
using Breadth First Search (BFS) traversal:
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 100
Int adjMatrix[MAX_VERTICES] [MAX_VERTICES];
int visited[MAX_VERTICES];
int queue[MAX_VERTICES];
int numVertices;
// Initialize the graph with the given number of vertices
void initGraph(int n) {
int i, j;
numVertices = n;
for (i = 0; i < numVertices; i++) {
for (j = 0; j < numVertices; j++) {
adjMatrix[i][j] = 0;
}
}
}
// Add a directed edge from vertex i to vertex j
void addEdge(int i, int j) {
adjMatrix[i][j] = 1;
}
// Breadth First Search (BFS) traversal of the graph
void bfs(int start) {
int i, front = 0, rear = 0;
for (i = 0; i < numVertices; i++) {
visited[i] = 0;
}
visited[start] = 1;
queue[rear++] = start;
printf("BFS traversal: ");
while (front != rear) {
int current = queue[front++];
printf("%d ", current);
for (i = 0; i < numVertices; i++) {
if (adjMatrix[current][i] && !visited[i]) {
visited[i] = 1;
queue[rear++] = i;
}
}
}
printf("\n");
}
int main() {
int numEdges, i, v1, v2, start;
printf("Enter the number of vertices: ");
scanf("%d", &numVertices);
initGraph(numVertices);
printf("Enter the number of edges: ");
scanf("%d", &numEdges);
printf("Enter the edges as pairs of vertices (e.g. 1 2):\n");
for (i = 0; i < numEdges; i++) {
scanf("%d %d", &v1, &v2);
addEdge(v1, v2);
}
printf("Enter the starting vertex for BFS traversal: ");
scanf("%d", &start);
bfs(start);
return 0;
}
Output:
Enter the number of vertices: 5
Enter the number of edges: 6
Enter the edges as pairs of vertices (e.g. 1 2):
0 1
0 2
1 3
2 3
3 4
4 0
BFS traversal: 0 1 2 3 4
B. write a C program that accepts the vertices and edges of a graph and store
it as an adjacency matrix. Implement function to traverse the graph using
Depth First Search (BFS) traversal.
Ans: C program that accepts the vertices and edges of a graph and stores it
as an adjacency
matrix. It also implements a function to traverse the graph using Depth First
Search (DFS) traversal:
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 100
int adjMatrix[MAX_VERTICES][MAX_VERTICES];
int visited[MAX_VERTICES];
int numVertices;
// Initialize the graph with the given number of vertices
void initGraph(int n) {
int i, j;
numVertices = n;
for (i = 0; i < numVertices; i++) {
for (j = 0; j < numVertices; j++) {
adjMatrix[i][j] = 0;
}
}
}
// Add a directed edge from vertex i to vertex j
void addEdge(int i, int j) {
adjMatrix[i][j] = 1;
}
// Depth First Search (DFS) traversal of the graph
void dfs(int start) {
int i;
visited[start] = 1;
printf("%d ", start);
for (i = 0; i < numVertices; i++) {
if (adjMatrix[start][i] && !visited[i]) {
dfs(i);
}
}
}
int main() {
int numEdges, i, v1, v2, start;
printf("Enter the number of vertices: ");
scanf("%d", &numVertices);
initGraph(numVertices);
printf("Enter the number of edges: ");
scanf("%d", &numEdges);
printf("Enter the edges as pairs of vertices (e.g. 1 2):\n");
for (i = 0; i < numEdges; i++) {
scanf("%d %d", &v1, &v2);
addEdge(v1, v2);
}
printf("Enter the starting vertex for DFS traversal: ");
scanf("%d", &start);
printf("DFS traversal: ");
for (i = 0; i < numVertices; i++) {
visited[i] = 0;
}
dfs(start);
printf("\n");
return 0;
}
Output:
Enter the number of vertices: 5
Enter the number of edges: 6
Enter the edges as pairs of vertices (e.g. 1 2):
0 1
0 2
1 3
2 3
3 4
4 0
Enter the starting vertex for DFS traversal: 0
DFS traversal: 0 1 3 4 2
-------------------------------------------------------------
Set C
A. Which data structure is used to implement Breadth First Search?
Ans: Breadth First Search (BFS) is typically implemented using a queue
data structure. The basic idea is to start from a source vertex and visit all
vertices in the graph in breadth-first order, meaning that we visit all the
vertices at distance 1 from the source, then all the vertices at distance 2,
and so on, until all vertices have been visited.
B. Where the new node is appended in Depth first search of OPEN list?
Ans: In Depth First Search (DFS), there is no concept of an OPEN list, as there is
in some other search algorithms like Breadth First Search (BFS) or A* search. DFS
traverses the graph by exploring one path as far as possible before backtracking
and exploring other paths. As the algorithm visits each node, it marks the node
as visited and recursively visits all of its unvisited neighbors
C. What is simple graph?
Ans: A simple graph in C is a graph data structure that consists of a set of
vertices and edges. It is called "simple" because it has no self-loops or multiple
edges
D.Which data structure is used to implement adjacency matrix method?
Ans: The data structure used to implement the adjacency matrix method is a
two-dimensional array.
