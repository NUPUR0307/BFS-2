# BFS-2
TC = O(n)
SC = O(n)

//Approach: 
1. We will use queue to store all the tree node
2. We will process the nodes at every level and update the rightmost variable in the level so that in the end we are left with the element which was added in the last and will ve seen 
3. add the rightmost element to the ans list

## Problem 1

Binary Tree Right Side View (https://leetcode.com/problems/binary-tree-right-side-view/)

class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) return ans;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            int len = queue.size();
            TreeNode rightmost = null;

            for (int i = 0; i < len; i++) {
                TreeNode curr = queue.poll();
                rightmost = curr; // the last node in this level will be the rightmost

                if (curr.left != null) queue.offer(curr.left);
                if (curr.right != null) queue.offer(curr.right);
            }

            ans.add(rightmost.val); // add the last node's value at this level
        }

        return ans;
    }
}
## Problem 2
TC = O(n)
SC = O(n)

//Approach: 
1. We will check if we found the x and y nodes but we will check if they are from the same parent if yes then we will return false
2. If x & y not found in the current level then we will add the left and right children of the current node in the queue

Cousins in binary tree (https://leetcode.com/problems/cousins-in-binary-tree/)

class Solution {
    public boolean isCousins(TreeNode root, int x, int y) {
        if (root == null) return false;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        boolean xFound = false;
        boolean yFound = false;

        while (!queue.isEmpty()) {
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();

                // Check if x and y are children of the same parent
                if (curr.left != null && curr.right != null) {
                    if ((curr.left.val == x && curr.right.val == y) || 
                        (curr.left.val == y && curr.right.val == x)) {
                        return false;
                    }
                }

                if (curr.val == x) xFound = true;
                if (curr.val == y) yFound = true;

                if (curr.left != null) queue.offer(curr.left);
                if (curr.right != null) queue.offer(curr.right);
            }

            // If both found at the same level and not siblings
            if (xFound && yFound) return true;
            // If only one is found, they can’t be cousins
            if (xFound || yFound) return false;
        }

        return false;
    }
}