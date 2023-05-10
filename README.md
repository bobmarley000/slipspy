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


