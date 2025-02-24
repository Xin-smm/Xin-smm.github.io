---
layout: post
title: "Basic Stuff about Binary Search Tree"
date: 2025-02-23
categories: blog update
---

#### An Simple Introduction

Everything, whatever what it is, has a definition. So for BST, we also need to define it first.

In short, Binary Search Tree, which is abreviated as BST, is basically a Special type of binary tree, which is a type of non-linear data structure that is commonly used in a lot of places.

The feature of a BST is really simple. i.e. , the left child of a node is always less than the node, and the right child of it is always greater. 



#### Declaration

```c++
struct tree_node
{
    int value;
    tree_node *left;
    tree_node *right;
    int count,size;
    tree_node(int x):
    	value(x),left(nullptr),right(nullptr),count(1),size(1){}
}
```



#### How to Insert

```c++
tree_node *insert(tree_node *root,int x)//insert variable x into BST
{
    //if root does not exist, return a new node contains the value of x
    if (root==nullptr) return new tree_node(x);
    
    //else, compare the value of x and root->value, if it is less than value, insert it to the left child of the node
    if (x<root->value) root->left=insert(root->left,x);
    //vice versa
    else if (x>root->value) root->right=insert(root->right,x);
    //if x is equal to root->value, then increase the value of count
    else root->count++;
    //update the size of the current root
    root->size=root->cnt+(root->left?root->left->size:0)+(root->right?root->right->size:0);
    return root;
}
```

#### How to Remove

```c++
node* remove(node* root,int x)
{
    // the procedure is very similar to Insertion, but there's still something different
    if (root==nullptr)
        return root;
    if (x<root->value)
        root->left=remove(root->left,x);
    else if (x>root->value)
        root->right=remove(root->right,x);
    else if (root->cnt>1)
        root->cnt--;
    else if (root->left==nullptr)
    {
        node* temp=root->right;
        delete root;
        return temp;
    }
    else if (root->right==nullptr)
    {
        node* temp=root->left;
        delete root;
        return temp;
    }
    else
    {
        node* successor=findmin(root->right);
        root->value=successor->value;
        root->cnt=successor->cnt;
        successor->cnt=1;
        root->right=remove(root->right,successor->value);
    }
    root->size=root->cnt+(root->left?root->left->size:0)+(root->right?root->right->cnt:0);
    return root;
}
```