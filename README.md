# Task 1

* To perform a BST, a class "BST" is created with Nodes and functions included.
* Traversal through the left side and right side is done by using recursion of functions.
* For insert(), the 'id' is compared with each layer of BST through traversal. Go left if the id is smaller than the current checking id. Vice versa. Then, the node is place in the correct place.
* For search(), the 'id' is compared with each layer of BST through traversal. Go left if the id is smaller than the current checking id. Vice versa. Then, the corresponding age is shown if the id is found.
* For remove(), there are three cases.
    1. The node has no children.
        * Remove directly.
    2. The node has one child.
        * Connect the child to the parent. Then, remove the node.
    3. The node has two children.
        * Search for the smallest number on the right side of the node. Replace the node with the smallest number on the right side. Remove the node and the original node of the smallest number.
* A function Print() is also made to print out the BST with ascending order to check the correctness of the BST.


# Task 2

## Q1. Point out all the unbalanced trees.
### For all three figures in Q1, the node '4' and '5' are mistakenly swapped in the figure.
