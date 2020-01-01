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

Figure (a) and (c) are unbalanced.

## Q2. After executing all the questions in task 1 (Q1 ~ Q3), is the binary search tree balanced or not?

The BST in Task 1 is not balanced. The subtree of node '10' has two right branches and zero left branches. As |left branches - right branches| > 1, the BST is unbalanced.

## Q3. If the binary search tree in Q2 is unbalanced, write a function rebalance () to rebalance the tree after each operation by using the AVL algorithm. As there are many approaches to make it balanced (e.g., RR, LL).

The unbalanced part of the tree is the node '10'. It forms a linear search. To solve the unbalance, we can execute a left rotation and then a right rotation. That is the Left-Right rotation case.

The following is the additional functions for AVL Trees.



    //to calculate the maximum height of the BST
    int BST::height_private(Node * Ptr)         
    {
        if (root == NULL)
        {
            return 0;
        }
        else 
        {
            if (Ptr != NULL)
            {
                int left_height_private = height_private(Ptr -> left);
                int right_height_private = height_private(Ptr -> right);
                return 1 + std::max(left_height_private, right_height_private);
            }
            else
            {
                return 0;
            }
        }
    }

    int BST::height()
    {
        return height_private(root);
    }



    BST::Node * BST:: RR_rotation(Node * Ptr)       //Task 2: RR rotation for AVL
    {
        Node * temp;
        temp = Ptr -> right;
        Ptr -> right = temp -> left;
        temp -> left = Ptr;
        return temp;
    }

    BST::Node * BST:: LL_rotation(Node * Ptr)       //Task 2: LL rotation for AVL
    {
        Node * temp;
        temp = Ptr -> left;
        Ptr -> left = temp -> right;
        temp -> right = Ptr;
        return temp;
    }

    BST::Node * BST:: LR_rotation(Node * Ptr)       //Task 2: LR rotation for AVL
    {
        Node * temp;
        temp = Ptr -> left;
        Ptr -> left = RR_rotation(temp);
        return LL_rotation(Ptr);
    }

    BST::Node * BST:: RL_rotation(Node * Ptr)       //Task 2: RL rotation for AVL
    {
        Node * temp;
        temp = Ptr -> right;
        Ptr -> right = LL_rotation(temp);
        return RR_rotation(Ptr);
    }

    //calculate the difference in height between the branches on the left and right
    int BST::difference_private(Node * Ptr)         
    {
        int left_height = height_private(Ptr -> left);
        int right_height = height_private(Ptr -> right);
        int difference = left_height - right_height;
        return difference;
    }

    //to check the AVL algorithm for the unbalanced BST (Total of 4 cases)
    BST::Node * BST::rebalance(Node * Ptr)     
    {
        int difference = difference_private(Ptr);
        if (difference > 1)        
        {
            if (difference_private(Ptr -> left) > 0)        //LL case
            {
                Ptr = LL_rotation(Ptr);
            }
            else                                            //LR case
            {
                Ptr = LR_rotation(Ptr);
            }
        }
        else if (difference < -1)
        {
            if (difference_private(Ptr -> right) > 0)       //RL case
            {
                Ptr = RL_rotation(Ptr);
            }
            else
            {
                Ptr = RR_rotation(Ptr);                     //RR case
            }
        }
        return Ptr;
    }
