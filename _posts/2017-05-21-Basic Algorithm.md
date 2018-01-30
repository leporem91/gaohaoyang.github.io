---
layout: post
title:  "Basic Algorithm"
date:   2017-05-21 21:46:00
categories: ProblemSolving
tags: ProblemSolving
---

* content
{:toc}

## 1. Sorting (정렬)

Data를 정렬할 때 사용하는 알고리즘 정리

#### Bubble Sort

설명이 필요 없음.

Time Complexity: O(N^2)

```
for (int i=0; i<N; i++)
 for (int j=i+1; j<N; j++)
  if(arr[i] > arr[j]) SWAP(i,j);
```

#### Merge Sort

분할정복 기법을 이용한 정렬 방법.
최악의 경우에도 NlogN의 시간복잡도를 가지지만, Merge할 때의 N개의 메모리가 더 필요하고,
상수배 연산이 QuickSort에 비해 크다.

Time Complexity: O(NlogN)

Algorithm:
1. 리스트 길이가 0 또는 1이면 정렬되어 있다고 생각한다.
2. 정렬되지 않은 리스트를 반으로 나눈다.
3. 각 부분 리스트를 재귀적으로 MergeSort한다.
4. 각각 정렬되어 있는 List1, List2를 각 앞의수로만 비교하여 List1, List2를 합친다.(정렬한다.)

```
void MergeSort(int l, int r)
{
	if (l >= r) return;
	int m = (l + r) >> 1;

	MergeSort(l, m);
	MergeSort(m + 1, r);

	int p1 = l, p2 = m + 1, p3 = l;
	while (p1 <= m && p2 <= r) tmp[p3++] = (arr[p1] < arr[p2]) ? arr[p1++] : arr[p2++];
	while (p1 <= m) tmp[p3++] = arr[p1++];
	while (p2 <= r) tmp[p3++] = arr[p2++];

	for (int i = l; i <= r; i++) arr[i] = tmp[i];
}
```

#### Quick Sort

최악의 경우 BubbleSort와 같지만 평균적으로 O(NlogN)

Pivot을 중앙에 가까운 값을 어떻게 선택하느냐가 성능을 결정한다. Randomized QuickSort, Median Of 3 등을 이용할 경우 최악의 경우가 확률적으로 거의 등장하지 않는다.
다른 NlogN 정렬 알고리즘에 비하여 별개의 메모리가 필요하지 않으며 상수계수로 인하여 매우 빠르다.

Time Complexity: Worst. O(N^2) , Average. O(NlogN)

Algorithm: 분할정복을 이용한다.
1. 리스트 중 하나의 원소를 피벗으로 정한다.
2. 피벗 앞에는 피벗보다 작은 값을, 피벗 뒤에는 피벗보다 큰 값을 배치시킨 후 리스트를 둘로 나눈다. (분할, 이때 피벗은 정렬된 후의 자리가 된다.)
3. 분할된 두개의 작은 리스트에 대하여 Recursion으로 돌린다.

분할하는 방법도 Lomuto partition, Hoare partition 등이 있는데 Hoare partition으로 정리해본다. [자세한 내용은 WIKI](https://en.wikipedia.org/wiki/Quicksort)

```
void Qsort(int l, int r)
{
	if (l >= r) return;
	int m = (l + r) >> 1;
	SWAP(m, r);

	int ll = l, rr = r - 1;
	while (ll <= rr)
	{
		while (ll <= rr && arr[r] <= arr[rr]) rr--;
		while (ll <= rr && arr[r] >= arr[ll]) ll++;
		if (ll < rr) SWAP(ll, rr);
	}
	SWAP(ll, r);
	Qsort(l, ll - 1);
	Qsort(ll + 1, r);
}
```


#### Counting Sort

모든 경우에 대한 정렬의 시간복잡도는 O(NlogN)이 가장 빠른 것으로 증명되었다.

하지만 특정한 조건 내에서는 더 빠른 시간복잡도를 가질 수 있는데, 대표적으로 Counting Sort가 있다.

Counting Sort은 다음과 같은 조건을 만족할때 성능이 좋다.
1. 데이터가 일정 범위내 있을 것 (그 범위가 작을 것)
2. 데이터가 정수일 것

데이터가 일정 범위 내 (1<= K <= 10000) 데이터가 N개(만개 이상의 큰 수) 들어온다면 비둘기 원리에 의해 N개의 데이터가 중복되는 경우가 생긴다.
즉 K범위 배열에 카운팅하여 각 인덱스의 개수만큼 결과를 뿌리면 된다.

하지만 K가 커지면 메모리 자체가 너무 많이 필요하고, N보다 크면 결국 NlogN보다 느리다.

Time Complexity : O(N+K) K가 작을 경우 O(N)이다.

```
	int cnt[10005];
	scanf("%d", &N);
	for (int i = 0, x; i < N; i++) scanf("%d", &x), cnt[x]++;
	for (int i = 0; i <= 10000; i++)
		while (cnt[i]--) printf("%d\n", i);
```


***

이 외에도 Selection Sort, Insertion Sort, Heap Sort, Radix Sort, Shell's Sort 등 다양한 정렬방법있다. [자세한 내용은 WIKI](https://namu.wiki/w/%EC%A0%95%EB%A0%AC%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)

연습문제(기초)
1. https://www.acmicpc.net/problem/2751
2. https://www.acmicpc.net/problem/10989

연습문제(응용)


