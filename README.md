// Node class represents each node in the BST
class Node {
    int value;
    Node left, right;

    Node(int item) {
        value = item;
        left = right = null;
    }
}

// BinarySearchTree class represents the entire BST
class BinarySearchTree {
    Node root;

    BinarySearchTree() {
        root = null;
    }

    // Insert method
    void insert(int key) {
        root = insertRec(root, key);
    }

    // Recursive insert method
    Node insertRec(Node root, int key) {
        if (root == null) {
            root = new Node(key);
            return root;
        }
        if (key < root.value) {
            root.left = insertRec(root.left, key);
        } else if (key > root.value) {
            root.right = insertRec(root.right, key);
        }
        return root;
    }

    // Search method
    boolean search(int key) {
        return searchRec(root, key);
    }

    // Recursive search method
    boolean searchRec(Node root, int key) {
        if (root == null) {
            return false;
        }
        if (key == root.value) {
            return true;
        }
        if (key < root.value) {
            return searchRec(root.left, key);
        } else {
            return searchRec(root.right, key);
        }
    }

    // Delete method
    void delete(int key) {
        root = deleteRec(root, key);
    }

    // Recursive delete method
    Node deleteRec(Node root, int key) {
        if (root == null) {
            return root;
        }
        if (key < root.value) {
            root.left = deleteRec(root.left, key);
        } else if (key > root.value) {
            root.right = deleteRec(root.right, key);
        } else {
            // Node with only one child or no child
            if (root.left == null) {
                return root.right;
            } else if (root.right == null) {
                return root.left;
            }
            // Node with two children: Get the inorder successor (smallest in the right subtree)
            root.value = minValue(root.right);
            // Delete the inorder successor
            root.right = deleteRec(root.right, root.value);
        }
        return root;
    }

    // Find the minimum value node in a tree
    int minValue(Node root) {
        int minValue = root.value;
        while (root.left != null) {
            root = root.left;
            minValue = root.value;
        }
        return minValue;
    }

    // InOrder Traversal
    void inOrder() {
        inOrderRec(root);
        System.out.println();
    }

    void inOrderRec(Node root) {
        if (root != null) {
            inOrderRec(root.left);
            System.out.print(root.value + " ");
            inOrderRec(root.right);
        }
    }

    // PreOrder Traversal
    void preOrder() {
        preOrderRec(root);
        System.out.println();
    }

    void preOrderRec(Node root) {
        if (root != null) {
            System.out.print(root.value + " ");
            preOrderRec(root.left);
            preOrderRec(root.right);
        }
    }

    // PostOrder Traversal
    void postOrder() {
        postOrderRec(root);
        System.out.println();
    }

    void postOrderRec(Node root) {
        if (root != null) {
            postOrderRec(root.left);
            postOrderRec(root.right);
            System.out.print(root.value + " ");
        }
    }

    // Main method to test the BST implementation
    public static void main(String[] args) {
        BinarySearchTree bst = new BinarySearchTree();

        // Insert elements
        bst.insert(50);
        bst.insert(30);
        bst.insert(20);
        bst.insert(40);
        bst.insert(70);
        bst.insert(60);
        bst.insert(80);

        // Print traversals
        System.out.print("InOrder Traversal: ");
        bst.inOrder();

        System.out.print("PreOrder Traversal: ");
        bst.preOrder();

        System.out.print("PostOrder Traversal: ");
        bst.postOrder();

        // Search for elements
        System.out.println("Search for 40: " + bst.search(40));
        System.out.println("Search for 90: " + bst.search(90));

        // Delete an element
        bst.delete(20);
        System.out.print("InOrder Traversal after deleting 20: ");
        bst.inOrder();
    }
}
