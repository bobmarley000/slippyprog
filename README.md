# slippyprog
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
// Function to compare two binary search trees node datawise
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
 


1
Set A
A.Write a C program that accepts the vertices and edges of 
a graph. Create adjacency list and display the adjacency list:
#include <stdio.h>
#include <stdlib.h>
struct Node {
int vertex;
struct Node* next;
};
struct Graph {
int numVertices;
struct Node** adjLists;
};
struct Node* createNode(int v) {
struct Node* newNode = (struct Node*) 
malloc(sizeof(struct Node));
newNode->vertex = v;
newNode->next = NULL;
return newNode;
}
struct Graph* createGraph(int vertices) {
struct Graph* graph = (struct Graph*) 
malloc(sizeof(struct Graph));
graph->numVertices = vertices;
graph->adjLists = (struct Node**) malloc(vertices * 
sizeof(struct Node*));
int i;
for (i = 0; i < vertices; i++)
graph->adjLists[i] = NULL;
return graph;
}
void addEdge(struct Graph* graph, int src, int dest) {
Assignment 4: Graph as adjacency list
2
struct Node* newNode = createNode(dest);
newNode->next = graph->adjLists[src];
graph->adjLists[src] = newNode;
newNode = createNode(src);
newNode->next = graph->adjLists[dest];
graph->adjLists[dest] = newNode;
}
void displayGraph(struct Graph* graph) {
int i;
for (i = 0; i < graph->numVertices; i++) {
struct Node* temp = graph->adjLists[i];
printf("\nAdjacency list of vertex %d:\n", i);
while (temp) {
printf("%d -> ", temp->vertex);
temp = temp->next;
}
printf("NULL\n");
}
}
int main() {
int vertices, edges, i, src, dest;
printf("Enter the number of vertices: ");
scanf("%d", &vertices);
struct Graph* graph = createGraph(vertices);
printf("\nEnter the number of edges: ");
scanf("%d", &edges);
for (i = 0; i < edges; i++) {
printf("\nEnter edge %d (source, destination): ", 
i + 1);
scanf("%d%d", &src, &dest);
addEdge(graph, src, dest);
}
displayGraph(graph);
3
return 0;
}
Output:-
Enter the number of vertices: 4
Enter the number of edges: 4
Enter edge 1 (source, destination): 1 2
Enter edge 2 (source, destination): 2 3
Enter edge 3 (source, destination): 3 4
Enter edge 4 (source, destination): 5 6
Adjacency list of vertex 0: NULL
Adjacency list of vertex 1:
2 -> NULL
Adjacency list of vertex 2:
3 -> 13449240 -> NULL
Adjacency list of vertex 3:
4 -> 2 -> NULL
B. Write a C program that accepts the vertices and edges of a 
graph. Create adjacency list. Implement functions to print indegree, 
outdegree and total degree of all vertex of graph.
#include <stdio.h>
#include <stdlib.h>
struct Node {
int vertex;
struct Node* next;
};
struct Graph {
int numVertices;
struct Node** adjLists;
int* inDegree;
int* outDegree;
};
4
struct Node* createNode(int v) {
struct Node* newNode = (struct Node*) 
malloc(sizeof(struct Node));
newNode->vertex = v;
newNode->next = NULL;
return newNode;
}
struct Graph* createGraph(int vertices) {
struct Graph* graph = (struct Graph*) 
malloc(sizeof(struct Graph));
graph->numVertices = vertices;
graph->adjLists = (struct Node**) malloc(vertices * 
sizeof(struct Node*));
graph->inDegree = (int*) malloc(vertices * 
sizeof(int));
graph->outDegree = (int*) malloc(vertices * 
sizeof(int));
int i;
for (i = 0; i < vertices; i++) {
graph->adjLists[i] = NULL;
graph->inDegree[i] = 0;
graph->outDegree[i] = 0;
}
return graph;
}
void addEdge(struct Graph* graph, int src, int dest) {
struct Node* newNode = createNode(dest);
newNode->next = graph->adjLists[src];
graph->adjLists[src] = newNode;
graph->outDegree[src]++;
graph->inDegree[dest]++;
newNode = createNode(src);
newNode->next = graph->adjLists[dest];
graph->adjLists[dest] = newNode;
5
graph->outDegree[dest]++;
graph->inDegree[src]++;
}
void printDegrees(struct Graph* graph) {
int i;
for (i = 0; i < graph->numVertices; i++) {
printf("Vertex %d: in-degree = %d, out-degree = 
%d, total degree = %d\n", i, graph->inDegree[i], graph-
>outDegree[i], graph->inDegree[i] + graph->outDegree[i]);
}
}
int main() {
int vertices, edges, i, src, dest;
printf("Enter the number of vertices: ");
scanf("%d", &vertices);
struct Graph* graph = createGraph(vertices);
printf("\nEnter the number of edges: ");
scanf("%d", &edges);
for (i = 0; i < edges; i++) {
printf("\nEnter edge %d (source, destination): ", 
i + 1);
scanf("%d%d", &src, &dest);
addEdge(graph, src, dest);
}
printDegrees(graph);
return 0;
}
Output: Enter the number of vertices: 5
Enter the number of edges: 4
6
Enter edge 1 (source, destination): 1 3
Enter edge 2 (source, destination): 2 3 
Enter edge 3 (source, destination): 3 5
Enter edge 4 (source, destination): 6
7
Vertex 0: in-degree = 0, out-degree = 0, total degree = 0
Vertex 1: in-degree = 1, out-degree = 1, total degree = 2
Vertex 2: in-degree = 1, out-degree = 1, total degree = 2
Vertex 3: in-degree = 3, out-degree = 3, total degree = 6
Vertex 4: in-degree = 0, out-degree = 0, total degree = 0
Set B
A.Write a C program that accepts the vertices and edges of a graph and 
store it as an adjacency list. Implement function to traverse the graph 
using Breadth First Search (BFS) traversal.
#include <stdio.h>
#include <stdlib.h>
struct Node {
int vertex;
struct Node* next;
};
struct Graph {
int numVertices;
struct Node** adjLists;
int* visited;
};
struct Node* createNode(int v) {
struct Node* newNode = (struct Node*) malloc(sizeof(struct
Node));
newNode->vertex = v;
newNode->next = NULL;
7
return newNode;
}
struct Graph* createGraph(int vertices) {
struct Graph* graph = (struct Graph*) malloc(sizeof(struct
Graph));
graph->numVertices = vertices;
graph->adjLists = (struct Node**) malloc(vertices * 
sizeof(struct Node*));
graph->visited = (int*) malloc(vertices * sizeof(int));
int i;
for (i = 0; i < vertices; i++) {
graph->adjLists[i] = NULL;
graph->visited[i] = 0;
}
return graph;
}
void addEdge(struct Graph* graph, int src, int dest) {
struct Node* newNode = createNode(dest);
newNode->next = graph->adjLists[src];
graph->adjLists[src] = newNode;
newNode = createNode(src);
newNode->next = graph->adjLists[dest];
graph->adjLists[dest] = newNode;
}
void BFS(struct Graph* graph, int startVertex) {
int queue[graph->numVertices];
int front = 0, rear = 0;
graph->visited[startVertex] = 1;
queue[rear] = startVertex;
rear++;
printf("BFS traversal starting from vertex %d: ", 
startVertex);
while (front < rear) {
int currentVertex = queue[front];
printf("%d ", currentVertex);
8
front++;
struct Node* temp = graph->adjLists[currentVertex];
while (temp) {
int adjVertex = temp->vertex;
if (graph->visited[adjVertex] == 0) {
graph->visited[adjVertex] = 1;
queue[rear] = adjVertex;
rear++;
}
temp = temp->next;
}
}
}
int main() {
int vertices, edges, i, src, dest, startVertex;
printf("Enter the number of vertices: ");
scanf("%d", &vertices);
struct Graph* graph = createGraph(vertices);
printf("\nEnter the number of edges: ");
scanf("%d", &edges);
for (i = 0; i < edges; i++) {
printf("\nEnter edge %d (source, destination): ", i + 
1);
scanf("%d%d", &src, &dest);
addEdge(graph, src, dest);
}
printf("\nEnter the starting vertex for BFS: ");
scanf("%d", &startVertex);
BFS(graph, startVertex);
return 0;
}
9
Output:- Enter the number of vertices: 5
Enter the number of edges: 6
Enter edge 1 (source, destination): 1 2
Enter edge 2 (source, destination): 2 3
Enter edge 3 (source, destination): 3 4
Enter edge 4 (source, destination): 4 5
Enter edge 5 (source, destination): 5 6
Enter edge 6 (source, destination): 3 7
Enter the starting vertex for BFS: 2
BFS traversal starting from vertex 2: 2 3 1 4
B. Write a C program that accepts the vertices and edges of a 
graph and store it as an adjacency list. Implement function to 
traverse the graph using Depth First Search (BFS) traversal.
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 100
typedef struct node {
int vertex;
struct node* next;
10
} node;
node* graph[MAX_VERTICES] = { NULL };
int visited[MAX_VERTICES] = { 0 };
void addEdge(int u, int v) {
node* newNode = (node*)malloc(sizeof(node));
newNode->vertex = v;
newNode->next = graph[u];
graph[u] = newNode;
}
void dfs(int vertex) {
visited[vertex] = 1;
printf("%d ", vertex);
node* ptr = graph[vertex];
while (ptr != NULL) {
int adjVertex = ptr->vertex;
if (!visited[adjVertex]) {
dfs(adjVertex);
}
ptr = ptr->next;
}
}
int main() {
int numVertices, numEdges;
printf("Enter the number of vertices: ");
scanf("%d", &numVertices);
printf("Enter the number of edges: ");
scanf("%d", &numEdges);
printf("Enter the edges (u, v):\n");
for (int i = 0; i < numEdges; i++) {
int u, v;
scanf("%d %d", &u, &v);
addEdge(u, v);
}
printf("Depth First Traversal: ");
for (int i = 0; i < numVertices; i++) {
11
if (!visited[i]) {
dfs(i);
}
}
return 0;
}
Output:
Enter the number of vertices: 4
Enter the number of edges: 3
Enter the edges (u, v):
1 2
2 4
4 6
Depth First Traversal: 0 1 2 4 6 3
Set c
B.Which data structure is used to implement Depth First Search?
Ans: Depth First Search (DFS) is typically implemented using a stack data structure. By 
using a stack, DFS is able to explore all reachable nodes in a graph, visiting nodes in 
depth-first order.
B. Where the new node is appended in Breadth-first search of OPEN 
list?
Ans: In Breadth-first search (BFS), the new node is typically appended at the end of 
the OPEN list.
C. What is complete graph?
12
Ans: . A complete graph is a type of graph in which every pair of distinct 
vertices is connected by an edge. In other words, in a complete graph, every 
vertex is directly connected to every other vertex.


1
 
Set A
A.Write a C program for the implementation of Topological sorting.
#include <stdio.h>
int main(){
int i,j,k,n,a[10][10],indeg[10],flag[10],count=0;
printf("Enter the no of vertices:\n");
scanf("%d",&n);
printf("Enter the adjacency matrix:\n");
for(i=0;i<n;i++){
printf("Enter row %d\n",i+1);
for(j=0;j<n;j++)
scanf("%d",&a[i][j]);
}
for(i=0;i<n;i++){
indeg[i]=0;
flag[i]=0;
}
for(i=0;i<n;i++)
for(j=0;j<n;j++)
printf("\nThe topological order is:");
while(count<n){
for(k=0;k<n;k++){
if((indeg[k]==0) && (flag[k]==0)){
printf("%d ",(k+1));
flag [k]=1;
}
for(i=0;i<n;i++){
if(a[i][k]==1)
indeg[k]--;
 Assignment 5: Graph Applications 2
2
}
}
count++;
}
return 0;
}
Output:
Enter the no of vertices:
4
Enter the adjacency matrix:
Enter row 1
0 1 1 0
Enter row 2
0 0 0 1
Enter row 3
0 0 0 1
Enter row 4
0 0 0 0
The topological order is:1 2 3 4
B. Write a C program for the Implementation of Prim's Minimum 
spanning tree algorithm.
#include <stdio.h>
#include <limits.h>
#define V 5
int minKey(int key[], int mstSet[]) {
int min = INT_MAX, min_index;
for (int v = 0; v < V; v++) {
if (mstSet[v] == 0 && key[v] < min) {
min = key[v];
min_index = v;
}
}
return min_index;
3
}
void printMST(int parent[], int graph[V][V]) {
printf("Edge \tWeight\n");
for (int i = 1; i < V; i++) {
printf("%d - %d \t%d \n", parent[i], i, 
graph[i][parent[i]]);
}
}
void primMST(int graph[V][V]) {
int parent[V];
int key[V];
int mstSet[V];
for (int i = 0; i < V; i++) {
key[i] = INT_MAX;
mstSet[i] = 0;
}
key[0] = 0;
parent[0] = -1
for (int count = 0; count < V - 1; count++) {
int u = minKey(key, mstSet);
mstSet[u] = 1;
for (int v = 0; v < V; v++) {
if (graph[u][v] && mstSet[v] == 0 && graph[u][v] < key[v]) {
parent[v] = u;
key[v] = graph[u][v];
}
}
}
printMST(parent, graph);
}
int main() {
int graph[V][V] = {{0, 2, 0, 6, 0},
{2, 0, 3, 8, 5},
{0, 3, 0, 0, 7},
{6, 8, 0, 0, 9},
{0, 5, 7, 9, 0}};
4
primMST(graph);
return 0;
}
Output:
Edge Weight
0 - 1 2 
1 - 2 3 
0 - 3 6 
1 – 4 5
Set B
A.Write a C program for the Implementation of Kruskal's Minimum 
spanning tree algorithm.
#include <stdio.h>
#include <stdlib.h>
#define MAX 100
typedef struct Edge {
int u, v, weight;
} Edge;
int parent[MAX];
Edge edges[MAX];
int numVertices, numEdges;
int find(int vertex) {
if (parent[vertex] == -1) {
return vertex;
}
return find(parent[vertex]);
5
}
void unionSet(int u, int v) {
parent[u] = v;
}
void kruskal() {
int i, j, u, v, min, numEdgesSelected = 0;
for (i = 0; i < numVertices; i++) {
parent[i] = -1;
}
i = 0;
while (numEdgesSelected < numVertices - 1) {
min = MAX;
for (j = 0; j < numEdges; j++) {
if (find(edges[j].u) != find(edges[j].v) && 
edges[j].weight < min) {
min = edges[j].weight;
u = edges[j].u;
v = edges[j].v;
}
}
if (find(u) != find(v)) {
 unionSet(find(u), find(v));
 printf("%d - %d\n", u, v);
 numEdgesSelected++;
}
 i++;
}
}
int main() {
int i;
printf("Enter the number of vertices: ");
scanf("%d", &numVertices);
printf("Enter the number of edges: ");
scanf("%d", &numEdges);
printf("Enter the edges (source, destination, 
weight):\n");
for (i = 0; i < numEdges; i++) {
6
scanf("%d %d %d", &edges[i].u, &edges[i].v, 
&edges[i].weight);
}
kruskal();
return 0;
}
Output:
Enter the number of vertices: 4
Enter the number of edges: 4
Enter the edges (source, destination, weight):
1 2
2 3
4 5
2 5
6 8
6 0
1 - 2
3 - 4
2 – 5
7
Set C
A. A graph may not have an edge from a vertex back to itselfself 
edges or self loops). Given an adjacency matrix representation of 
a graph, how to know if there are self edges?
Ans: To determine if a graph has self edges, we need to check if there are any 
non-zero elements on the main diagonal of the adjacency matrix. The main 
diagonal of an adjacency matrix represents the vertices of a graph that have 
self-edges, i.e., an edge that connects a vertex to itself.



 
Set A
A. Write a C program for the implementation of Dijkstra's shortest path 
algorithm for finding shortest path from a given source vertex using 
adjacency cost matrix.
➔ C program for the implementation of Dijkstra's shortest path algorithm 
using adjacency cost matrix:
#include <stdio.h>
#include <limits.h>
#include <stdbool.h>
#define V 6
int minDistance(int dist[], bool visited[]) {
int min = INT_MAX, min_index;
for (int v = 0; v < V; v++)
if (visited[v] == false && dist[v] <= min)
min = dist[v], min_index = v;
return min_index;
}
void dijkstra(int graph[V][V], int src) {
int dist[V];
bool visited[V];
for (int i = 0; i < V; i++)
dist[i] = INT_MAX, visited[i] = false;
dist[src] = 0;
for (int count = 0; count < V - 1; count++) {
int u = minDistance(dist, visited);
visited[u] = true;
for (int v = 0; v < V; v++)
if (!visited[v] && graph[u][v] && dist[u] != INT_MAX && 
dist[u] + graph[u][v] < dist[v])
dist[v] = dist[u] + graph[u][v];
Assignment 6: Graph Applications 2
}
printf("Vertex Distance from Source\n");
for (int i = 0; i < V; i++)
printf("%d \t\t %d\n", i, dist[i]);
}
int main() {
int graph[V][V] = {{0, 1, 4, 0, 0, 0},
{1, 0, 2, 5, 0, 0},
{4, 2, 0, 1, 3, 0},
{0, 5, 1, 0, 0, 2},
{0, 0, 3, 0, 0, 6},
{0, 0, 0, 2, 6, 0}};
dijkstra(graph, 0);
return 0;
}
Output: 
Vertex Distance from Source
0 0
1 1
2 3
3 4
4 6
5 6
---------------------------------------------------------------------------
SET B
A. Write a C program for the implementation of Floyd Warshall's 
algorithm for finding all pairs shortest path using adjacency cost 
matrix.
#include <stdio.h>
#define INF 99999
#define V 4
void printSolution(int dist[][V]);
void floydWarshall(int graph[][V])
{
 int dist[V][V], i, j, k;
 for (i = 0; i < V; i++)
 for (j = 0; j < V; j++)
 dist[i][j] = graph[i][j];
 for (k = 0; k < V; k++)
 {
 for (i = 0; i < V; i++)
 {
 for (j = 0; j < V; j++)
 {
 if (dist[i][k] + dist[k][j] < dist[i][j])
 dist[i][j] = dist[i][k] + dist[k][j];
 }
 }
 }
 printSolution(dist);
}
void printSolution(int dist[][V])
{
 printf ("The following matrix shows the shortest distances between every 
pair of vertices \n");
 for (int i = 0; i < V; i++)
 {
 for (int j = 0; j < V; j++)
 {
 if (dist[i][j] == INF)
 printf("%7s", "INF");
 else
 printf ("%7d", dist[i][j]);
 }
 printf("\n");
 }
}
int main()
{
 int graph[V][V] = { {0, 5, INF, 10},
 {INF, 0, 3, INF},
 {INF, INF, 0, 1},
 {INF, INF, INF, 0}
 };
 floydWarshall(graph);
 return 0;
}
Output: 
The following matrix shows the shortest distances between every pair of vertices 
 0 5 8 10
 INF 0 3 4
 INF INF 0 1
 INF INF INF 0
SET C
A. A graph can be used to show relationships between people. For example 
following list of vertices represent people and list of edges represent the 
friendships like: People George, Jim, Jean, Frank, Fred, John, Susan) 
Friendship ((George, Jean), (Frank, Fred), (George, John),(Jim, Fred), 
(Jim, Frank))
1. Find all friends of John.
2. Find all friends of Susan .
3. find all freinds of jim.
ANS: We first need to represent the graph in a way that we can easily 
manipulate it. One way to do this is to use an adjacency list, where each vertex 
is associated with a list of its neighbors (i.e., its friends).
Here is the adjacency list representation of the friendship graph:
George: Jean, John
Jim: Fred, Frank
Jean: George
Frank: Fred, Jim
Fred: Frank, Jim
John: George
Susan:
To answer the questions:
1. Find all friends of John:
We can simply look up the neighbors of John in the adjacency list. John has 
only one neighbor, George, so his only friend is George.
Therefore, the answer is: George.
2. Find all friends of Susan:
Susan has no neighbors in the adjacency list, which means that she has no 
friends in the graph.
Therefore, the answer is: none.
3. Find all friends of Jim:
We can look up the neighbors of Jim in the adjacency list. Jim is friends with 
Fred and Frank.
Therefore, the answer is: Fred and Frank.
--------------------------------------------------------------------



Set A
a) Write a program to implement various types of hash functions which are used to place the 
data in a hash table.
a. Division Method
b. Mid Square Method
c. Digit Folding Method
Accept n values from the user and display appropriate message in case of collision for each 
of the above functions.
Program:-
#include <stdio.h>
#include <stdlib.h>
#define SIZE 10
// Structure for linked list node
typedef struct node
{
int key;
int value;
struct node *next;
} Node;
// Structure for hash table
typedef struct
{
Node *head;
} HashTable;
// Function to create a new node
Node *create_node(int key, int value)
{
Node *new_node = (Node *)malloc(sizeof(Node));
new_node->key = key;
new_node->value = value;
new_node->next = NULL;
return new_node;
}
// Hash function - Division Method
int hash_division(int key)
{
return key % SIZE;
}
Assignment 7: Hash Table-I
// Hash function - Mid Square Method
int hash_mid_square(int key)
{
int square = key * key;
int mid = (int)(square / 10) % 10;
return mid;
}
// Hash function - Digit Folding Method
int hash_digit_folding(int key)
{
int sum = 0;
while (key)
{
sum += key % 10;
key /= 10;
}
return sum % SIZE;
}
// Function to insert a key-value pair in the hash table
void insert(int key, int value, HashTable *table, int 
(*hash_func)(int))
{
int index = hash_func(key);
Node *new_node = create_node(key, value);
if (table[index].head)
{
printf("Collision occurred at index %d for key %d\n", index, 
key);
new_node->next = table[index].head;
}
table[index].head = new_node;
}
// Function to display the contents of the hash table
void display(HashTable *table)
{
for (int i = 0; i < SIZE; i++)
{
printf("Index %d: ", i);
if (table[i].head)
{
Node *temp = table[i].head;
while (temp)
{
printf("(%d,%d) ", temp->key, temp->value);
temp = temp->next;
}
}
printf("\n");
}
}
// Main function
int main()
{
HashTable table[SIZE];
for (int i = 0; i < SIZE; i++)
{
table[i].head = NULL;
}
int n, key, value, choice;
printf("Enter the number of values to insert: ");
scanf("%d", &n);
printf("Choose a hash function:\n1. Division Method\n2. Mid Square 
Method\n3. Digit Folding Method\n");
scanf("%d", &choice);
int (*hash_func)(int);
switch (choice)
{
case 1:
hash_func = hash_division;
break;
case 2:
hash_func = hash_mid_square;
break;
case 3:
hash_func = hash_digit_folding;
break;
default:
printf("Invalid choice\n");
exit(0);
}
for (int i = 0; i < n; i++)
{
printf("Enter key and value: ");
scanf("%d %d", &key, &value);
insert(key, value, table, hash_func);
}
display(table);
return 0;
}
Output:-
Enter the number of values to insert: 6 
Choose a hash function:
1. Division Method
2. Mid Square Method
3. Digit Folding Method
3
Enter key and value: 1 2
Enter key and value: 2 6
Enter key and value: 23 45
Enter key and value: 13 36
Enter key and value: 15 34
Enter key and value: 12 20
Index 0:
Index 1: (1,2)
Index 2: (2,6)
Index 3: (12,20)
Index 4: (13,36)
Index 5: (23,45)
Index 6: (15,34)
Index 7:
Index 8:
Index 9:
Set B
a) Write a menu driven program to implement hash table using array (insert, search, 
delete, display). Use any of the above-mentioned hash functions. In case of collision 
apply linear probing.
Program:-
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define SIZE 10
// Structure for hash table
typedef struct
{
int key;
char value[20];
} Node;
// Function to insert a key-value pair in the hash table
void insert(Node table[], int key, char value[])
{
int index = key % SIZE;
int i = 0;
while (table[index].key != -1)
{
index = (index + 1) % SIZE;
i++;
if (i == SIZE)
{
printf("Hash table is full\n");
return;
}
}
table[index].key = key;
strcpy(table[index].value, value);
}
// Function to search for a key-value pair in the hash table
void search(Node table[], int key)
{
int index = key % SIZE;
int i = 0;
while (table[index].key != key)
{
index = (index + 1) % SIZE;
i++;
if (table[index].key == -1 || i == SIZE)
{
printf("Key not found\n");
return;
}
}
printf("Value: %s\n", table[index].value);
}
// Function to delete a key-value pair from the hash table
void delete(Node table[], int key)
{
int index = key % SIZE;
int i = 0;
while (table[index].key != key)
{
index = (index + 1) % SIZE;
i++;
if (table[index].key == -1 || i == SIZE)
{
printf("Key not found\n");
return;
}
}
table[index].key = -1;
strcpy(table[index].value, "");
}
// Function to display the contents of the hash table
void display(Node table[])
{
printf("Index\tKey\tValue\n");
for (int i = 0; i < SIZE; i++)
{
printf("%d\t%d\t%s\n", i, table[i].key, table[i].value);
}
}
// Main function
int main()
{
Node table[SIZE];
for (int i = 0; i < SIZE; i++)
{
table[i].key = -1;
strcpy(table[i].value, "");
}
int choice, key;
char value[20];
do
{
printf("\nHash Table Operations\n");
printf("1. Insert\n");
printf("2. Search\n");
printf("3. Delete\n");
printf("4. Display\n");
printf("5. Exit\n");
printf("Enter your choice: ");
scanf("%d", &choice);
switch (choice)
{
case 1:
printf("Enter key and value: ");
scanf("%d %s", &key, value);
insert(table, key, value);
break;
case 2:
printf("Enter key to search: ");
scanf("%d", &key);
search(table, key);
break;
case 3:
printf("Enter key to delete: ");
scanf("%d", &key);
delete (table, key);
break;
case 4:
display(table);
break;
case 5:
exit(0);
default:
printf("Invalid choice\n");
}
} while (choice != 5);
return 0;
}
Output:-
Hash Table Operations
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your choice: 1
Enter key and value: 23 32
Hash Table Operations
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your choice: 4
Index Key Value
0 -1
1 -1
2 -1
3 23 32
4 -1
5 -1
6 -1
7 -1
8 -1
9 -1
Hash Table Operations
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your choice: 5
b) Write a menu driven program to implement hash table using array (insert, search, delete, 
display). Use any of the above-mentioned hash functions. In case of collision apply quadratic 
probing.
Program:-
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define SIZE 10
// Structure for hash table
typedef struct
{
int key;
char value[20];
} Node;
// Function to insert a key-value pair in the hash table
void insert(Node table[], int key, char value[])
{
int index = key % SIZE;
int i = 0;
while (table[index].key != -1)
{
index = (index + i * i) % SIZE;
i++;
if (i == SIZE)
{
printf("Hash table is full\n");
return;
}
}
table[index].key = key;
strcpy(table[index].value, value);
}
// Function to search for a key-value pair in the hash table
void search(Node table[], int key)
{
int index = key % SIZE;
int i = 0;
while (table[index].key != key)
{
index = (index + i * i) % SIZE;
i++;
if (table[index].key == -1 || i == SIZE)
{
printf("Key not found\n");
return;
}
}
printf("Value: %s\n", table[index].value);
}
// Function to delete a key-value pair from the hash table
void delete(Node table[], int key)
{
int index = key % SIZE;
int i = 0;
while (table[index].key != key)
{
index = (index + i * i) % SIZE;
i++;
if (table[index].key == -1 || i == SIZE)
{
printf("Key not found\n");
return;
}
}
table[index].key = -1;
strcpy(table[index].value, "");
}
// Function to display the contents of the hash table
void display(Node table[])
{
printf("Index\tKey\tValue\n");
for (int i = 0; i < SIZE; i++)
{
printf("%d\t%d\t%s\n", i, table[i].key, table[i].value);
}
}
// Main function
int main()
{
Node table[SIZE];
for (int i = 0; i < SIZE; i++)
{
table[i].key = -1;
strcpy(table[i].value, "");
}
int choice, key;
char value[20];
do
{
printf("\nHash Table Operations\n");
printf("1. Insert\n");
printf("2. Search\n");
printf("3. Delete\n");
printf("4. Display\n");
printf("5. Exit\n");
printf("Enter your choice: ");
scanf("%d", &choice);
switch (choice)
{
case 1:
printf("Enter key and value: ");
scanf("%d %s", &key, value);
insert(table, key, value);
break;
case 2:
printf("Enter key to search: ");
scanf("%d", &key);
search(table, key);
break;
case 3:
printf("Enter key to delete: ");
scanf("%d", &key);
delete (table, key);
break;
case 4:
display(table);
break;
case 5:
exit(0);
default:
printf("Invalid choice\n");
}
} while (choice != 5);
return 0;
}
Output:-
Hash Table Operations
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your choice: 1
Enter key and value: 12 14
Hash Table Operations
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your choice: 1
Enter key and value: 36
41
Hash Table Operations
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your choice: 2
Enter key to search: 36
Value: 41
Hash Table Operations
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter your choice: 5
Set C
a)Calculate the time complexity of hash table with Linear Probing.
b) The keys 12, 18, 13, 2, 3, 23, 5 and 15 are inserted into an initially empty 
hash table of length 10 using open addressing with hash function h(k) = k mod 
10 and linear probing. What is the resultant hash table?
(a) (d) 
Which data structure is appropriate for simple chaining ? Why?
ANS:
Hash table: [None, None, 12, 13, 2, 3, 23, 5, 18, 15]
Means (C) is the resultant hash table.
And 
For simple chaining, the appropriate data structure is a linked list. In a 
linked list, each element contains a pointer to the next element in the list. 
When implementing simple chaining, each index in the hash table corresponds to 
a linked list.
0
1
2 2
3 23
4
5 15
6
7
8 18
9
(b)
0
1
2 12
3 13
4
5 5
6
7
8 18
9
(c)
0
1
2 12
3 13
4 2
5 3
6 23
7 5
8 18
9 15
0
1
2 12,2
3 13,3,23
4
5 5,15
6
7
8
9




Set A
a) Implement hash table using singly linked lists. Write a menu driven program to 
perform operations on the hash table (insert, search, delete, display). Select 
appropriate hashing function. In case of collision, use separate chaining.
Program:-
#include <stdio.h>
#include <stdlib.h>
#define MAX_SIZE 10
// node structure for linked list
typedef struct node
{
int key;
struct node *next;
} node;
// hash table structure
typedef struct hashTable
{
node *heads[MAX_SIZE]; // array of pointers to heads of linked lists
} hashTable;
// hash function - simple mod operation
int hash(int key)
{
return key % MAX_SIZE;
}
// create new node for linked list
node *createNode(int key)
{
node *newNode = (node *)malloc(sizeof(node));
newNode->key = key;
newNode->next = NULL;
return newNode;
}
// insert a key-value pair into the hash table
void insert(hashTable *ht, int key)
{
int index = hash(key);
node *newNode = createNode(key);
if (ht->heads[index] == NULL)
{
ht->heads[index] = newNode;
}
Assignment 8: Hash Table-II
else
{
node *current = ht->heads[index];
while (current->next != NULL)
{
current = current->next;
}
current->next = newNode;
}
printf("Inserted key %d at index %d\n", key, index);
}
// search for a key in the hash table
void search(hashTable *ht, int key)
{
int index = hash(key);
node *current = ht->heads[index];
while (current != NULL)
{
if (current->key == key)
{
printf("Key %d found at index %d\n", key, index);
return;
}
current = current->next;
}
printf("Key %d not found\n", key);
}
// delete a key from the hash table
void delete(hashTable *ht, int key)
{
int index = hash(key);
node *current = ht->heads[index];
node *prev = NULL;
while (current != NULL)
{
if (current->key == key)
{
if (prev == NULL)
{
ht->heads[index] = current->next;
}
else
{
prev->next = current->next;
}
free(current);
printf("Deleted key %d from index %d\n", key, index);
return;
}
prev = current;
current = current->next;
}
printf("Key %d not found\n", key);
}
// display the contents of the hash table
void display(hashTable *ht)
{
for (int i = 0; i < MAX_SIZE; i++)
{
printf("Index %d: ", i);
node *current = ht->heads[i];
while (current != NULL)
{
printf("%d ", current->key);
current = current->next;
}
printf("\n");
}
}
int main()
{
hashTable ht;
for (int i = 0; i < MAX_SIZE; i++)
{
ht.heads[i] = NULL;
}
int choice, key;
while (1)
{
printf("\n1. Insert\n2. Search\n3. Delete\n4. Display\n5. Exit\nEnter 
choice: ");
scanf("%d", &choice);
switch (choice)
{
case 1:
printf("Enter key to insert: ");
scanf("%d", &key);
insert(&ht, key);
break;
case 2:
printf("Enter key to search: ");
scanf("%d", &key);
search(&ht, key);
break;
case 3:
printf("Enter key to delete: ");
scanf("%d", &key);
delete (&ht, key);
break;
case 4:
display(&ht);
break;
case 5:
exit(0);
default:
printf("Invalid choice\n");
}
}
return 0;
}
Output:-
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter choice: 1
Enter key to insert: 12
Inserted key 12 at index 2
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter choice: 2
Enter key to search: 12
Key 12 found at index 2
Set B
a) Implement hash table using doubly linked lists Write a menu driven program to 
perform operations on the hash table (insert, search delete, display). Select 
appropriate hashing function In case of collision, use separate chaining.
Program:-
#include <stdio.h>
#include <stdlib.h>
#define MAX_HASH 10
typedef struct node
{
int key;
struct node *prev;
struct node *next;
} Node;
typedef struct hashTable
{
Node *heads[MAX_HASH];
} HashTable;
int hash(int key)
{
return key % MAX_HASH;
}
void insert(HashTable *ht, int key)
{
int index = hash(key);
Node *newNode = (Node *)malloc(sizeof(Node));
newNode->key = key;
newNode->prev = NULL;
newNode->next = NULL;
if (ht->heads[index] == NULL)
{
ht->heads[index] = newNode;
}
else
{
Node *current = ht->heads[index];
while (current->next != NULL)
{
current = current->next;
}
current->next = newNode;
newNode->prev = current;
}
printf("Inserted key %d at index %d\n", key, index);
}
void search(HashTable *ht, int key)
{
int index = hash(key);
Node *current = ht->heads[index];
while (current != NULL && current->key != key)
{
current = current->next;
}
if (current == NULL)
{
printf("Key %d not found in hash table\n", key);
}
else
{
printf("Key %d found at index %d\n", key, index);
}
}
void delete(HashTable *ht, int key)
{
int index = hash(key);
Node *current = ht->heads[index];
while (current != NULL && current->key != key)
{
current = current->next;
}
if (current == NULL)
{
printf("Key %d not found in hash table\n", key);
return;
}
if (current->prev != NULL)
{
current->prev->next = current->next;
}
else
{
ht->heads[index] = current->next;
}
if (current->next != NULL)
{
current->next->prev = current->prev;
}
free(current);
printf("Deleted key %d from index %d\n", key, index);
}
void display(HashTable *ht)
{
for (int i = 0; i < MAX_HASH; i++)
{
printf("Index %d:", i);
Node *current = ht->heads[i];
while (current != NULL)
{
printf(" %d", current->key);
current = current->next;
}
printf("\n");
}
}
int main()
{
HashTable ht = {0};
int choice, key;
while (1)
{
printf("\n1. Insert\n2. Search\n3. Delete\n4. Display\n5. Exit\nEnter 
choice: ");
scanf("%d", &choice);
switch (choice)
{
case 1:
printf("Enter key to insert: ");
scanf("%d", &key);
insert(&ht, key);
break;
case 2:
printf("Enter key to search: ");
scanf("%d", &key);
search(&ht, key);
break;
case 3:
printf("Enter key to delete: ");
scanf("%d", &key);
delete (&ht, key);
break;
case 4:
display(&ht);
break;
case 5:
exit(0);
default:
printf("Invalid choice\n");
}
}
return 0;
}
Output:-
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter choice: 1
Enter key to insert: 15
Inserted key 15 at index 5
 1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter choice: 4
Index 0:
Index 1:
Index 2:
Index 3:
Index 4:
Index 5: 15
Index 6:
Index 7:
Index 8:
Index 9:
1. Insert
2. Search
3. Delete
4. Display
5. Exit
Enter choice: 5
Set C
a) What the pseudo code to find all the pairs of two integers in an unsorted array 
that sum up to a given S using hash tables.
Example: if the array is [3, 5, 2, 4, 8, 11] and the sum is 7, program should 
return [[11, -4], [2, 5]] since11 +4=7 and 2+5=7.
ANS:
1. Create an empty hash table
2. For each element x in the array:
a. Calculate the complement y = S - x
b. If y is present in the hash table:
i. Add [x, y] to the result list
c. Add x to the hash table
3. Return the result list
