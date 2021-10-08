[TOC]

# 1 Morris遍历

## 1.1 Morris遍历目的

在二叉树的遍历中，有递归方式遍历和非递归遍历两种。不管哪种方式，时间复杂度为O(N)，空间复杂度为O(h),h为树的高度。Morris遍历可以在时间复杂度O(N),空间复杂度O(1)实现二叉树的遍历


### 算法流程

从一个树的头结点cur开始：

1、cur的左树为null，cur = cur.right

2、cur有左树，找到左树的最右的节点mostRight

- mostRight的右孩子指向null，让mostRigth.right = cur;cur = cur.left
- mostRight的右孩子指向当前节点cur，让mostRigth.right = null;cur = cur.rigth
- cur为null的时候，整个流程结束

cur经过的各个节点，称为Morris序，例如如下的树结构：

```
graph TD
1-->2
1-->3
2-->4
2-->5
3-->6
3-->7
```

cur经过的路径也就是Morris序为：1，2，4，2，5，1，3，6，3，7

可以发现，只要当前节点有左孩子，当前节点会来到两次。当左树最右节点的右孩子指向null，可以判定第一次来到cur节点，下一次来到cur就是发现左树的最右节点指向的是自己，说明第二次来到cur节点

在Morris遍历的过程中，第一次到达cur就打印（只会来cur一次的节点也打印）就是树的先序遍历，第二次到达（只会来到cur一次的节点也打印）打印为中序。第二次来到cur节点的时候逆序打印cur左树的右边界，最后逆序打印整颗树的右边界，逆序打印右边界不可以使用额外的结构，因为我们要求空间复杂度为O(1)，可以使用翻转链表

翻转链表：例如a->b->c->d->null。可以让a-null,b->a,c->b,d->c即可。打印完之后把链表再翻转过来

### 时间复杂度估计

cur来到节点的时间复杂度为O(N),每个cur遍历左树最右边界的代价最多为O(2N),所以整个遍历过程为O(N)，整个遍历过程只用到到有限的几个变量，其他使用的都是树本身的指针关系。



```Java
public class Code01_MorrisTraversal {

	public static class Node {
		public int value;
		Node left;
		Node right;

		public Node(int data) {
			this.value = data;
		}
	}

        // morris遍历
	public static void morris(Node head) {
		if (head == null) {
			return;
		}
		Node cur = head;
		Node mostRight = null;
		while (cur != null) {
			// cur有没有左树
			mostRight = cur.left;
			if (mostRight != null) { // 有左树的情况下
				// 找到cur左树上，真实的最右
				while (mostRight.right != null && mostRight.right != cur) {
					mostRight = mostRight.right;
				}
				// 从while中出来，mostRight一定是cur左树上的最右节点
				// mostRight如果等于null，说明第一次来到自己
				if (mostRight.right == null) {
					mostRight.right = cur;
					cur = cur.left;
					continue;
                                // 否则第二次来到自己，意味着mostRight.right = cur
				} else { // mostRight.right != null -> mostRight.right == cur
					mostRight.right = null;
				}
			}
			cur = cur.right;
		}
	}

        // Morris中序遍历
	public static void morrisIn(Node head) {
		if (head == null) {
			return;
		}
		Node cur = head;
		Node mostRight = null;
		while (cur != null) {
			mostRight = cur.left;
			if (mostRight != null) {
				while (mostRight.right != null && mostRight.right != cur) {
					mostRight = mostRight.right;
				}
				if (mostRight.right == null) {
					mostRight.right = cur;
					cur = cur.left;
					continue;
				} else {
					mostRight.right = null;
				}
			}
			System.out.print(cur.value + " ");
			cur = cur.right;
		}
		System.out.println();
	}

        // Morris先序遍历
	public static void morrisPre(Node head) {
		if (head == null) {
			return;
		}
		// cur
		Node cur1 = head;
		// mostRight
		Node cur2 = null;
		while (cur1 != null) {
			cur2 = cur1.left;
			if (cur2 != null) {
				while (cur2.right != null && cur2.right != cur1) {
					cur2 = cur2.right;
				}
				if (cur2.right == null) {
					cur2.right = cur1;
					System.out.print(cur1.value + " ");
					cur1 = cur1.left;
					continue;
				} else {
					cur2.right = null;
				}
			} else {
				System.out.print(cur1.value + " ");
			}
			cur1 = cur1.right;
		}
		System.out.println();
	}


        // Morris后序遍历
	public static void morrisPos(Node head) {
		if (head == null) {
			return;
		}
		Node cur = head;
		Node mostRight = null;
		while (cur != null) {
			mostRight = cur.left;
			if (mostRight != null) {
				while (mostRight.right != null && mostRight.right != cur) {
					mostRight = mostRight.right;
				}
				if (mostRight.right == null) {
					mostRight.right = cur;
					cur = cur.left;
					continue;
					// 回到自己两次，且第二次回到自己的时候是打印时机
				} else {
					mostRight.right = null;
					// 翻转右边界链表，打印
					printEdge(cur.left);
				}
			}
			cur = cur.right;
		}
		// while结束的时候，整颗树的右边界同样的翻转打印一次
		printEdge(head);
		System.out.println();
	}

	public static void printEdge(Node head) {
		Node tail = reverseEdge(head);
		Node cur = tail;
		while (cur != null) {
			System.out.print(cur.value + " ");
			cur = cur.right;
		}
		reverseEdge(tail);
	}

	public static Node reverseEdge(Node from) {
		Node pre = null;
		Node next = null;
		while (from != null) {
			next = from.right;
			from.right = pre;
			pre = from;
			from = next;
		}
		return pre;
	}

	// for test -- print tree
	public static void printTree(Node head) {
		System.out.println("Binary Tree:");
		printInOrder(head, 0, "H", 17);
		System.out.println();
	}

	public static void printInOrder(Node head, int height, String to, int len) {
		if (head == null) {
			return;
		}
		printInOrder(head.right, height + 1, "v", len);
		String val = to + head.value + to;
		int lenM = val.length();
		int lenL = (len - lenM) / 2;
		int lenR = len - lenM - lenL;
		val = getSpace(lenL) + val + getSpace(lenR);
		System.out.println(getSpace(height * len) + val);
		printInOrder(head.left, height + 1, "^", len);
	}

	public static String getSpace(int num) {
		String space = " ";
		StringBuffer buf = new StringBuffer("");
		for (int i = 0; i < num; i++) {
			buf.append(space);
		}
		return buf.toString();
	}



        // 在Morris遍历的基础上，判断一颗树是不是一颗搜索二叉树
        // 搜索二叉树是左比自己小，右比自己大
        // 一颗树中序遍历，值一直在递增，就是搜索二叉树
	public static boolean isBST(Node head) {
		if (head == null) {
			return true;
		}
		Node cur = head;
		Node mostRight = null;
		Integer pre = null;
		boolean ans = true;
		while (cur != null) {
			mostRight = cur.left;
			if (mostRight != null) {
				while (mostRight.right != null && mostRight.right != cur) {
					mostRight = mostRight.right;
				}
				if (mostRight.right == null) {
					mostRight.right = cur;
					cur = cur.left;
					continue;
				} else {
					mostRight.right = null;
				}
			}
			if (pre != null && pre >= cur.value) {
				ans = false;
			}
			pre = cur.value;
			cur = cur.right;
		}
		return ans;
	}

	public static void main(String[] args) {
		Node head = new Node(4);
		head.left = new Node(2);
		head.right = new Node(6);
		head.left.left = new Node(1);
		head.left.right = new Node(3);
		head.right.left = new Node(5);
		head.right.right = new Node(7);
		printTree(head);
		morrisIn(head);
		morrisPre(head);
		morrisPos(head);
		printTree(head);

	}

}
```


## 1.2 Morris遍历的应用

在一颗二叉树中，求该二叉树的最小高度。最小高度指的是，所有叶子节点距离头节点的最小值

> 二叉树递归求解，求左树的最小高度加1和右树的最小高度加1，比较

> Morris遍历求解，每到达一个cur的时候，记录高度。每到达一个cur的时候判断cur是否为叶子节点，更新全局最小值。最后看一下最后一个节点的高度和全局最小高度对比，取最小高度

```Java
public class Code05_MinHeight {

	public static class Node {
		public int val;
		public Node left;
		public Node right;

		public Node(int x) {
			val = x;
		}
	}

        // 解法1 运用二叉树的递归
	public static int minHeight1(Node head) {
		if (head == null) {
			return 0;
		}
		return p(head);
	}

	public static int p(Node x) {
		if (x.left == null && x.right == null) {
			return 1;
		}
		// 左右子树起码有一个不为空
		int leftH = Integer.MAX_VALUE;
		if (x.left != null) {
			leftH = p(x.left);
		}
		int rightH = Integer.MAX_VALUE;
		if (x.right != null) {
			rightH = p(x.right);
		}
		return 1 + Math.min(leftH, rightH);
	}

	// 解法2 根据morris遍历改写
	public static int minHeight2(Node head) {
		if (head == null) {
			return 0;
		}
		Node cur = head;
		Node mostRight = null;
		int curLevel = 0;
		int minHeight = Integer.MAX_VALUE;
		while (cur != null) {
			mostRight = cur.left;
			if (mostRight != null) {
				int rightBoardSize = 1;
				while (mostRight.right != null && mostRight.right != cur) {
					rightBoardSize++;
					mostRight = mostRight.right;
				}
				if (mostRight.right == null) { // 第一次到达
					curLevel++;
					mostRight.right = cur;
					cur = cur.left;
					continue;
				} else { // 第二次到达
					if (mostRight.left == null) {
						minHeight = Math.min(minHeight, curLevel);
					}
					curLevel -= rightBoardSize;
					mostRight.right = null;
				}
			} else { // 只有一次到达
				curLevel++;
			}
			cur = cur.right;
		}
		int finalRight = 1;
		cur = head;
		while (cur.right != null) {
			finalRight++;
			cur = cur.right;
		}
		if (cur.left == null && cur.right == null) {
			minHeight = Math.min(minHeight, finalRight);
		}
		return minHeight;
	}

	// for test
	public static Node generateRandomBST(int maxLevel, int maxValue) {
		return generate(1, maxLevel, maxValue);
	}

	// for test
	public static Node generate(int level, int maxLevel, int maxValue) {
		if (level > maxLevel || Math.random() < 0.5) {
			return null;
		}
		Node head = new Node((int) (Math.random() * maxValue));
		head.left = generate(level + 1, maxLevel, maxValue);
		head.right = generate(level + 1, maxLevel, maxValue);
		return head;
	}

	public static void main(String[] args) {
		int treeLevel = 7;
		int nodeMaxValue = 5;
		int testTimes = 100000;
		System.out.println("test begin");
		for (int i = 0; i < testTimes; i++) {
			Node head = generateRandomBST(treeLevel, nodeMaxValue);
			int ans1 = minHeight1(head);
			int ans2 = minHeight2(head);
			if (ans1 != ans2) {
				System.out.println("Oops!");
			}
		}
		System.out.println("test finish!");

	}

}
```

## 1.3 Morris遍历为最优解的情景

> 如果我们算法流程设计成，每来到一个节点，需要左右子树的信息进行整合，那么无法使用Morris遍历。该种情况的空间复杂度也一定不是O(1)的

> 如果算法流程是，当前节点使用完左树或者右树的信息后，无需整合，那么可以使用Morris遍历

> Morris遍历属于比较复杂的问题
