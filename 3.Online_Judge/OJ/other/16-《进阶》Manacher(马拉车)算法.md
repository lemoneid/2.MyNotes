[TOC]
# 1 Manacher算法

## 1.1 简介

回文串概念：一个字符串是轴对称的，轴的左侧和右侧是逆序的关系，例如"abcba","abccba"

Manacher算法解决在一个字符串中最长回文子串的大小，例如"abc12321ef"最长回文子串为"12321"大小为5


回文串的用途，例如我们可以把DNA当成一个字符串，有一些基因片段是回文属性的，在生理学上有实际意义


## 1.2 字符串最长回文子串暴力解

遍历str，以i为回文对称的回文串有多长，在i位置左右扩展。所以字符串"abc123df"

i为0的时候，回文串为"a"，长度为1;

i为1的时候，回文串为"b"，左边和右边不相等，长度为1;

i为1的时候，回文串为"b"，长度为1;

。。。。。。


此种方式，无法找到以一个虚轴的最长回文串

所以我们可以通过填充字符，来解决，例如"31211214"我们前后和字符间填充'#'得到"#3#1#2#1#1#2#1#4#",利用该串进行上述步骤来寻找。

i为0的时候，回文串为"#"，长度为1;

i为1的时候，回文串为"#3#"，长度为3;

...

i为8的时候，回文串为"#1#2#1#1#2#1#"，长度为13;

可以找到所有基数或者偶数的所有回文串，但是回文串的长度和原始回文串长度的关系为：当前回文串长度除以2，得到原始串中各个位置的回文串长度


复杂度最差情况是，所有字符长度为n,且所有字符都相等。经过我们的填充，字符串规模扩展到2n+1。每次寻找，都会寻找到左边界或者右边界，该方法的事件复杂度为O(N*N)


Manacher算法解决该类问题，O(N)复杂度！

## 1.3 Manacher解决最长回文串O(N)

概念1：回文半径和回文直径，回文直径指的是，在我们填充串中，每个位置找到的回文串的整体长度，回文半径指的是在填充串中回文串从i位置到左右边界的一侧的长度


概念2：回文半径数组，对于填充串每个i位置，求出来的回文串的长度，都记录下来。pArr[]长度和填充串长度相同

概念3：回文最右右边界R和中心C，R和C初始为-1。例如扩展串为"#1#2#2#1#3#"。O(N)

- i为0的时候，R为0，C为0
- i为1的时候，R为2，C为1
- i为2的时候，R为不变，只要R不变，C就不变


Manacher算法的核心概念就是，回文半径数组pArr[],回文最右边界R，中心C

在遍历填充数组时，会出现i在R外，和i在R内两种情况。


当i在R外时，没有任何优化，继续遍历去寻找。当i在R内涉及到Manacher算法的优化。i在R内的时候，i肯定大于C,我们可以根据R和C求出左边界L,也可以根据i和C求出以C堆成的i'。

- 情况1：i'的回文区域在彻底在L和R的内部。i不需要再求回文串，i的回文串的大小等于pArr[]中i'位置的长度。原因是i和i'关于C对称，整体在R和L范围内，R和L也是关于C对称，传递得到。O(1)


- 情况2：i'的回文区域的左边界在L的左侧。i的回文半径就是i位置到R位置的长度。原因是，L以i'为堆成的L'，R以i为堆成的R'一定在L到R的范围内。且L'到L和R'到R互为回文。所以i区域的回文区域的回文半径至少为i到R的距离。由于以C为对称，得到区域为L到R,L不等于R，此处画图根据传递得到i的回文半径就是i位置到R位置的长度。O(1)


- 情况3：i'的回文区域的左边界和L相等。i'的右区域一定不会再R的右侧。根据情况2，R以i堆成的R'。R和R'确定是回文，需要验证R下一个位置和R'前一个位置是否回文，这里也可以省掉R'到R之间的验证。O(N)


经过以上的情况，整体O(N)复杂度


Code:

```Java
public class Code01_Manacher {

	public static int manacher(String s) {
		if (s == null || s.length() == 0) {
			return 0;
		}
		// "12132" -> "#1#2#1#3#2#"
		char[] str = manacherString(s);
		// 回文半径的大小
		int[] pArr = new int[str.length];
		int C = -1;
		// 算法流程中，R代表最右的扩成功的位置。coding：最右的扩成功位置的，再下一个位置，即失败的位置
		int R = -1;
		int max = Integer.MIN_VALUE;
		for (int i = 0; i < str.length; i++) {
			// R是第一个违规的位置，i>= R就表示i在R外
			// i位置扩出来的答案，i位置扩的区域，至少是多大。
                        // 2 * C - i 就是i的对称点。
                        // 得到各种情况下无需验的区域
			pArr[i] = R > i ? Math.min(pArr[2 * C - i], R - i) : 1;
      
                        // 右侧不越界，且左侧不越界，检查需不需要扩
			while (i + pArr[i] < str.length && i - pArr[i] > -1) {
				if (str[i + pArr[i]] == str[i - pArr[i]])
					pArr[i]++;
				else {
					break;
				}
			}
                        //i的右边界有没有刷新之前的最右边界。R刷新C要跟着刷新
			if (i + pArr[i] > R) {
				R = i + pArr[i];
				C = i;
			}
			max = Math.max(max, pArr[i]);
		}
		return max - 1;
	}

	public static char[] manacherString(String str) {
		char[] charArr = str.toCharArray();
		char[] res = new char[str.length() * 2 + 1];
		int index = 0;
		for (int i = 0; i != res.length; i++) {
			res[i] = (i & 1) == 0 ? '#' : charArr[index++];
		}
		return res;
	}

	// for test
	public static int right(String s) {
		if (s == null || s.length() == 0) {
			return 0;
		}
		char[] str = manacherString(s);
		int max = 0;
		for (int i = 0; i < str.length; i++) {
			int L = i - 1;
			int R = i + 1;
			while (L >= 0 && R < str.length && str[L] == str[R]) {
				L--;
				R++;
			}
			max = Math.max(max, R - L - 1);
		}
		return max / 2;
	}

	// for test
	public static String getRandomString(int possibilities, int size) {
		char[] ans = new char[(int) (Math.random() * size) + 1];
		for (int i = 0; i < ans.length; i++) {
			ans[i] = (char) ((int) (Math.random() * possibilities) + 'a');
		}
		return String.valueOf(ans);
	}

	public static void main(String[] args) {
		int possibilities = 5;
		int strSize = 20;
		int testTimes = 5000000;
		System.out.println("test begin");
		for (int i = 0; i < testTimes; i++) {
			String str = getRandomString(possibilities, strSize);
			if (manacher(str) != right(str)) {
				System.out.println("Oops!");
			}
		}
		System.out.println("test finish");
	}

}
```

## 1.4 例题

给定一个字符串str，只可在str后添加字符，把该串变成回文字符串最少需要多少个字符？

> 解题思路：转化为必须包含最后一个字符的最长回文串多长？例如，"abc12321"，以最后一个1的最长回文串为"12321"，那么最少需要添加"cba"3个字符


```Java
public class Code02_AddShortestEnd {

	public static String shortestEnd(String s) {
		if (s == null || s.length() == 0) {
			return null;
		}
		char[] str = manacherString(s);
		int[] pArr = new int[str.length];
		int C = -1;
		int R = -1;
		int maxContainsEnd = -1;
		for (int i = 0; i != str.length; i++) {
			pArr[i] = R > i ? Math.min(pArr[2 * C - i], R - i) : 1;
			while (i + pArr[i] < str.length && i - pArr[i] > -1) {
				if (str[i + pArr[i]] == str[i - pArr[i]])
					pArr[i]++;
				else {
					break;
				}
			}
			if (i + pArr[i] > R) {
				R = i + pArr[i];
				C = i;
			}
			if (R == str.length) {
				maxContainsEnd = pArr[i];
				break;
			}
		}
		char[] res = new char[s.length() - maxContainsEnd + 1];
		for (int i = 0; i < res.length; i++) {
			res[res.length - 1 - i] = str[i * 2 + 1];
		}
		return String.valueOf(res);
	}

	public static char[] manacherString(String str) {
		char[] charArr = str.toCharArray();
		char[] res = new char[str.length() * 2 + 1];
		int index = 0;
		for (int i = 0; i != res.length; i++) {
			res[i] = (i & 1) == 0 ? '#' : charArr[index++];
		}
		return res;
	}

	public static void main(String[] args) {
		String str1 = "abcd123321";
		System.out.println(shortestEnd(str1));
	}

}
```












