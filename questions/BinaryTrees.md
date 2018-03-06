# Binary trees

A binary tree is a tree whose every node either branches to two binary
trees or is a leaf, i.e. contains a value. Here is an example of a
binary tree

```
     3
   /   \
  1     5
 / \   / \
0   2 4   6
```


* (**A**) Design a DTD for representing binary trees and nothing but
  binary trees. The branching nodes should not carry any information,
  whereas every leaf should carry a value that can be any string
  (`#PCDATA`).

* (**B**) Show an XML element representing the above example tree, and
  which is valid according to your DTD.

* (**C**) Write an XPath query that returns all leaf elements of a
  binary tree. For the above example, it should return 0,1,2,3,4,5,6 (without
  any XML tags).
