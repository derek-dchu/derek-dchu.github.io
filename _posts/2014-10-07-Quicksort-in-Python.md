---
layout:	post
title:	"Quicksort in Python"
date:	2014-10-07 21:36
categories:	Python
---

When exploring a programming language, it is always a good idea to get familiar with syntax by implementing general data structures and algorithms. Quicksort is one of the best options. It is a practical and widely used sorting algorithm because of its excellent average complexity of [O(n log n)][bigO-notation]. However, we also note that in the worst case, it has O(n^2) complexity, though this behavior is rare.

Quicksort only has two basic operations which are swapping items and partitioning a section of the array. We will first implement these two operations and then put them into our final quicksort function.

Swapping
----
swap function swaps two items within a given array by providing their indexes.

{% highlight python %}

def swap(arr, index1, index2):
	arr[index1], arr[index2] = arr[index2], arr[index1]

{% endhighlight %}

Partitioning
----
The goal for paritioning is to divide an array into two sections separated by pivot item, and all items within left section are smaller than pivot item, while the right section contain all the items that are larger than pivot item. Here are basic steps to partition an array:

1. Pick up a pivot item in the array, then swap it with the first item.
2. Create two pointers (left and right) at the second and last items in the array respectively.
3. While the left pointer has the value that is less than pivot value, move it to the right by adding 1. If the left pointer has the value that is not less than pivot value or reach the last item, then stop and move to next step.
4. While the right pointer has the value that is larger than or equal to pivot value, move it to the left by subtracting 1. If the right pointer has the value that is not larger than pivot value or reach the first item, then stop and move to next step.
5. If the left pointer is less than to the right pointer, then swap two items which are pointing by them.
6. Move left pointer to right by adding 1, and move right pointer to left by subtracting 1.
7. If the left pointer is not equal to or larger then right pointer, then go to step 1. Otherwise, swap the first item with item pointing by right pointer, and finish partition.

{% highlight python %}

def partition(arr, first, last):
	# step 1
	pivot = first + int((first - last) / 2)
	swap(arr, first, pivot)

	# step 2
	left = first + 1
	right = last

	while True:
		# step 3
		while arr[left] < arr[first]:
			if left == last:
				break
			left += 1

		# step 4
		while arr[right] >= arr[first]:
			if right == first:
				break
			right -= 1

		# step 7
		if left >= right:
			break

		# step 5
		swap(arr, left, right)

		# step 6
		left += 1
		right -= 1

	# step 7
	swap(arr, first, right)
	return right

{% endhighlight %}

Quicksort
----
Quicksort is based on the [Divide and Conquer][divide-and-conquer] algorithm design paradigm. Following the Divide and Conquer paradigm, we first partition the whole array, then divide it into a left section and a right section of the pivot item. After that, we recursively partition all sections which produce sub-sections of sections until all those sub-sections contain only no more than one item. Now each item within the array have all  smaller items on their left and larger items on their right, in other words, the array is in ascending order.

{% highlight python %}

def quick_sort(arr, first=None, last=None):
	if arr is None:
		return arr

	if first is None:
		first = 0

	if last is None:
		last = len(arr)-1

	if first < last:
		pivot = partition(arr, first, last)
		quick_sort(arr, first, pivot-1)
		quick_sort(arr, pivot+1, last)

	return arr

{% endhighlight %}

### What do you think?
What if we want to return the array in descending order?

[bigO-notation]:	http://en.wikipedia.org/wiki/Big_O_notation
[divide-and-conquer]:	http://en.wikipedia.org/wiki/Divide_and_conquer_algorithms