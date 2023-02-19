# Lecture 11 answers

Option 1) Recursive Solution
```java
import java.util.ArrayDeque;
import java.util.Queue;
 
// A class to store a binary tree node
class Node
{
    int data;
    Node left, right;
 
    Node(int data) {
        this.data = data;
    }
}
 
class Main
{
    // Function to find the total number of nodes in the binary tree
    private static int size(Node root)
    {
        if (root == null) {
            return 0;
        }
        return 1 + size(root.left) + size(root.right);
    }
 
    // Function to check if a given binary tree is a complete binary tree
    // and each node has a higher value than its parent
    private static boolean isHeap(Node root, int i, int n)
    {
        // base case
        if (root == null) {
            return true;
        }
 
        // not complete binary tree: out of valid index range
        if (i >= n) {
            return false;
        }
 
        // current node has a higher value than its left or right child
        if ((root.left != null && root.left.data <= root.data) ||
                    (root.right != null && root.right.data <= root.data)) {
            return false;
        }
 
        // check for left and right subtree
        return isHeap(root.left, 2*i + 1, n) &&
            isHeap(root.right, 2*i + 2, n);
    }
 
    // Function to check if a given binary tree is a min-heap or not
    public static boolean isHeap(Node root)
    {
        int i = 0;
        return isHeap(root, i, size(root));
    }
 
    public static void main(String[] args)
    {
        /* Construct the following tree
                   2
                 /   \
                /     \
               3       4
              / \     / \
             /   \   /   \
            5     6 8    10
        */
 
        Node root = new Node(2);
        root.left = new Node(3);
        root.right = new Node(4);
        root.left.left = new Node(5);
        root.left.right = new Node(6);
        root.right.left = new Node(8);
        root.right.right = new Node(10);
 
        if (isHeap(root)) {
            System.out.print("The given binary tree is a min-heap");
        }
        else {
            System.out.print("The given binary tree is not a min-heap");
        }
    }
}
```



Option 2) Iterative Solution
```java
import java.util.ArrayDeque;
import java.util.Queue;
 
// A class to store a binary tree node
class Node
{
    int data;
    Node left, right;
 
    Node(int data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}
 
class Main
{
    // Function to check if a given binary tree is a min-heap or not
    public static boolean isHeap(Node root)
    {
        // base case
        if (root == null) {
            return true;
        }
 
        // create an empty queue and enqueue the root node
        Queue<Node> queue = new ArrayDeque<>();
        queue.add(root);
 
        // take a boolean flag, which becomes true when an empty left or right
        // child is seen for a node
        boolean isNullSeen = false;
 
        // loop till queue is empty
        while (!queue.isEmpty())
        {
            // process front node in the queue
            Node curr = queue.poll();
 
            // left child is non-empty
            if (curr.left != null)
            {
                // if either heap property is violated
                if (isNullSeen || curr.left.data <= curr.data) {
                    return false;
                }
 
                // enqueue left child
                queue.add(curr.left);
            }
            // left child is empty
            else {
                isNullSeen = true;
            }
 
            // right child is non-empty
            if (curr.right != null)
            {
                // if either heap property is violated
                if (isNullSeen || curr.right.data <= curr.data) {
                    return false;
                }
 
                // enqueue left child
                queue.add(curr.right);
            }
            // right child is empty
            else {
                isNullSeen = true;
            }
        }
 
        // we reach here only when the given binary tree is a min-heap
        return true;
    }
 
    public static void main(String[] args)
    {
        /* Construct the following tree
                   2
                 /   \
                /     \
               3       4
              / \     / \
             /   \   /   \
            5     6 8    10
        */
 
        Node root = new Node(2);
        root.left = new Node(3);
        root.right = new Node(4);
        root.left.left = new Node(5);
        root.left.right = new Node(6);
        root.right.left = new Node(8);
        root.right.right = new Node(10);
 
        if (isHeap(root)) {
            System.out.print("The given binary tree is a min-heap");
        }
        else {
            System.out.print("The given binary tree is not a min-heap");
        }
    }
}
```
