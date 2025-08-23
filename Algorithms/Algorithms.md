---
tags:
  - old_docs
---

# Binary Search Trees

Refs: [geeksforgeeks](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) 

* Symbol table implementation   
* Node based binary tree data structure  
* Properties   
  * Left node must be of lesser value than parent node  
  * Right node must be of greater value than parent node  
  * Left and right tree must be binary search trees themselves  
  * Must be duplicate nodes  
* Searching a key in BST

| struct node\* search(struct node\* root, int key){    //Covers the cases where the key is root or the root is NULL    if (root \== NULL || root-\>key \== key){      return root;   }   if  (root-\>key \< key){      return  search(root-\>right, key);   }   return search(root-\>left, key);}   |
| :---- |

* Insertion of a key  
  * Always inserting at a leaf 

| /\* A utility function to insert a new node with given key in BST \*/struct node\* insert(struct node\* node, int key){    /\* If the tree is empty, return a new node \*/    if (node \== NULL) return newNode(key);      /\* Otherwise, recur down the tree \*/    if (key \< node-\>key)        node-\>left  \= insert(node-\>left, key);    else if (key \> node-\>key)        node-\>right \= insert(node-\>right, key);	      /\* return the (unchanged) node pointer \*/    return node;} |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

	

* Time complexity:  
  * Worst case balanced tree: O(h) where h is the height of the tree  
  * Worst case skewed tree: O(n)   
* Inorder traversal of BST \-\> always sorted output   
* Constructing a BST only with preorder, postorder, level order traversal  
* Deleting Node   
  * Three cases  
    * Node has no children  
    * Node has 1 child   
    * Node has 2 children 

| struct node\* deleteNode(struct node\* root, int key){    // base case    if (root \== NULL) return root;      // If the key to be deleted is smaller than the root's key,    // then it lies in left subtree    if (key \< root-\>key)        root-\>left \= deleteNode(root-\>left, key);      // If the key to be deleted is greater than the root's key,    // then it lies in right subtree    else if (key \> root-\>key)        root-\>right \= deleteNode(root-\>right, key);      // if key is same as root's key, then This is the node    // to be deleted    else    {        // node with only one child or no child        if (root-\>left \== NULL)        {            struct node \*temp \= root-\>right;            free(root);            return temp;        }        else if (root-\>right \== NULL)        {            struct node \*temp \= root-\>left;            free(root);            return temp;        }          // node with two children: Get the inorder successor (smallest        // in the right subtree)        struct node\* temp \= minValueNode(root-\>right);          // Copy the inorder successor's content to this node        root-\>key \= temp-\>key;          // Delete the inorder successor        root-\>right \= deleteNode(root-\>right, temp-\>key);    }    return root;} |
| :---- |

 

* Advantages of BST over Hash Table   
  * Inorder traversal gives us all the keys in sorted order   
  * Order statistics, finding lower and greater elements, range queries are easy for BSTs   
  * Easier to implement (\*)   
  * Self-balancing BSTs are guaranteed to work in O(Log(n))   
    * Hashing is O(1) is the average time   
* K-th smallest element in BST   
  * Method 1: In order traversal   
    * Time Complexity: O(n)  
  * Aguument tree data structure  
    * Maintain rank of each node   
    * Keep track of eleents in a subtree of any node   
    * Can maintain number of element of left subtree every node  
    * Time Complexity: O(h)

| start:if K \= root.leftElement \+ 1   root node is the K th node.   goto stopelse if K \> root.leftElements   K \= K \- (root.leftElements \+ 1)   root \= root.right   goto startelse   root \= root.left   goto startstop: |
| :---- |

* Construct BST from given preorder traversal  
  * Preorder traversal (root, left, right )  
  * Method 1  
    * Time COmplexity O(n^2)  
    * Steps:  
      * First element is always root   
      * Find index of ifrst element greater than root   
        * Let the index be i   
      * Values between root and i will be part of left subreww  
      * Values between i+1 and n-1 will be part of right subreee  
      * Divide given pre\[\] at index i and recur for left and right subtrees   
  * Method 2 (\*)  
    * Tiem Complexity O(n)  
      * Trick is to set a range  for every node   
    * Steps  
      * Initialized the range   
      * First node will be in range, create the root nod   
      * Costructing the left subtree  
        * Set range as int\_min … root-\>data  
      * Constructing the right subtree  
        * Set range as root-\>data … int\_max  
  * Method 3   
    * Time Complexity: O(n)  
    * Steps  
      * Create an empty stack   
      * Make the first value as root and push to stack   
      * Keep on popping while the stack is not empty and the next value is greater than stack’s top value   
        * Make this value as the right child of the last popped node   
        * Push the new node to the stack   
      * If the next value is less than the stack’s top value, make this value as the left child of the stacl’s top node   
        * Push the node to the stack   
      * Repeat 2nd and 3rd steps until there are no items in the remaining pre\[\]  
* Binary Tree to Binary Search Tree Conversion   
  * Converstion must keep the original structure of the binary tree  
  * Steps:  
    * Create a temp array arr\[\[ that stores inorder traversal of the tree  
      * O(n)  
    * Sort the temp array   
    * Again do inorder traversal of tree and copy array elements to tree nodes one by one   
      * O(n)  
      * 