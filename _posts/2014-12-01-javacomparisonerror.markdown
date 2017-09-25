---
layout: post
title: "java比较器报错：Comparison method violates its general contract"
subtitle: ""
date: 2014-11-12
author: 苏爱马
category: Java
tags: 笔记 Java
finished: true
---

转载自：[fanzitao的专栏](http://blog.csdn.net/fanzitao/article/details/8040201)
Brother Zeng遇到的错误：
java.lang.IllegalArgumentException: Comparison method violates its general contract!
网上查到一个解释：
Description: The sorting algorithm used by java.util.Arrays.sort and (indirectly) by java.util.Collections.sort has been replaced. The new sort implementation may throw an IllegalArgumentException if it detects a Comparable that violates the Comparable contract. The previous implementation silently ignored such a situation. If the previous behavior is desired, you can use the new system property, java.util.Arrays.useLegacyMergeSort, to restore previous mergesort behavior.
也就是说jdk 7的sort函数的实现变了，造成了这个问题，具体原因未知。
改一下系统设置，还是选择使用老版本的排序方法，在代码前面加上这么一句话：System.setProperty("java.util.Arrays.useLegacyMergeSort", "true");
import java.util.Collections;
import java.util.Comparator;
import java.util.List;


public class CodeForBrotherZeng {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
			Stu stu1=new Stu("foyd",22.1);
			Stu stu2=new Stu("teddy",19.1);
			Stu stu3=new Stu("dean",26.1);
			Stu stu4=new Stu("lucas",19.1);
			Stu stu5=new Stu("tina",26.1);

			List<Stu> list = new ArrayList<Stu>();
			list.add(stu1);
			list.add(stu2);
			list.add(stu3);
			list.add(stu4);
			list.add(stu5);

			Comparator<Stu> comparator = new Comparator<Stu>() {
				public int compare(Stu p1, Stu p2) {//return必须是int，而str.age是double,所以不能直接return (p1.age-p2.age)
					if((p1.age-p2.age)<0)
						return -1;
					else if((p1.age-p2.age)>0)
						return 1;
					else return 0;
				}
			};
			//jdk 7sort有可能报错，
			//加上这句话:System.setProperty("java.util.Arrays.useLegacyMergeSort", "true");
			//表示，使用以前版本的sort来排序
			Collections.sort(list,comparator);

			for(int i=0;i<list.size();i++)
			{
				System.out.println(list.get(i).age+"  "+list.get(i).name);
			}

	}

}


