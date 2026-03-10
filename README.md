class Solution:
    # Function to check whether a Binary Tree is BST or not.
    def isBST(self, root):
        # We use a helper function to carry the min and max constraints
        return self.validate(root, float('-inf'), float('inf'))

    def validate(self, node, min_val, max_val):
        # An empty tree is a valid BST
        if not node:
            return True
            
        # Check if current node violates the range constraints
        # Note: We use <= and >= because duplicates are not allowed
        if node.data <= min_val or node.data >= max_val:
            return False
            
        # Recursively check subtrees with updated constraints
        # Left child: max boundary becomes current node's data
        # Right child: min boundary becomes current node's data
        return (self.validate(node.left, min_val, node.data) and 
                self.validate(node.right, node.data, max_val))


