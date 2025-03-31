# SortingNotes

He (Tianle Ma (i think?)) teaches CSI 2300

[[Selection Sort]] locates the smallest element, puts it in the first index (swap with first index), find the smallest not including the first and put it in the second index, smallest not including first two, put it in the third index, etc until it is all sorted
```java
public static void selectionSort(int[] arr) {
	for (int i = 0; i < arr.length-1; i++) {
		// locate the index of the smallest element in the unsorted half
		int smallestIndex = i;
		for (int j = i+1; j < arr.length; j++) {
			if (arr[j] < arr[smallestIndex]) {
				smallestIndex = j;
			}
		}
		// if the smallest isn't already in the right spot, swap it with i
		if (smallestIndex != i) {
			int temp = arr[i];
			arr[i] = arr[smallestIndex];
			arr[smallestIndex] = temp;
		}
	}
}

// recursive implementation
// input: 
//       arr - array to be sorted
//       n - index to start sort at (arr from n to end will be sorted)
public static void recursiveSelectionSort(int[] arr, int n) {
	// if at last element, it is already sorted
	if (n == arr.length-1) {
		return;
	}
	// otherwise find the min from [n, arr.length-1] and put it at index n
	int minIndex = n;
	for (int i = n+1; i < arr.length; i++) {
		if (arr[i] < arr[minIndex]) {
			minIndex = i;
		}
	}
	if (minIndex != n) {
		int temp = arr[n];
		arr[n] = arr[minIndex];
		arr[minIndex] = temp;
	}
	recursiveSelectionSort(arr, n+1);
}
```

[[Insertion Sort]] splits the array into two sides, starting with just the first element (which is not necessarily the smallest element). Each iteration it grabs the next element, inserting it in the correct spot relative to the rest of the elements in the sorted side.
- Note: the array isn't guaranteed to be completely sorted until the sorting is done
```java
public static void insertionSort(int[] arr) {
	for (int i = 1; i < arr.length; i++) {
		int key = arr[i];
		int j = i - 1;
		while (j >= 0 && arr[j] > key) {
			arr[j + 1] = arr[j--];
		}
		arr[j + 1] = key;
	}
}
```

[[Bubble Sort]] moves the largest element to the right of the array, then does the same with the subarray to the left of it.
```java
// optimized version of Bubble Sort from GeeksForGeeks.org
static void bubbleSort(int arr[]) {
	n = arr.length;
	for (int i = 0; i < n - 1; i++) {
		boolean swapped = false;
		for (int j = 0; j < n - i - 1; j++) {
			if (arr[j] > arr[j + 1]) {
				
				// Swap arr[j] and arr[j+1]
				int temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
				swapped = true;
			}
		}
		// If no two elements were swapped by inner loop, then break
		if (swapped == false)
			break;
	}
}
```

[[Merge Sort]] splits the array into subarrays, compares the subarrays to create sorted arrays.
- "Divide and Conquer" Algorithm
```java
public static void mergeSort(int[] arr, int left, int right) {  
	if (left < right) {  
		int mid = (left + right) / 2;  
		mergeSort(arr, left, mid);  
		mergeSort(arr, mid + 1, right);  
		merge(arr, left, mid, right);  
	}  
}  
  
public static void merge(int[] arr, int left, int mid, int right) {  
	int n1 = mid - left + 1;  
	int n2 = right - mid;  
	  
	int[] leftArray = new int[n1];  
	int[] rightArray = new int[n2];  
	  
	for (int i = 0; i < n1; i++) {  
		leftArray[i] = arr[left + i];  
	}  
	for (int j = 0; j < n2; j++) {  
		rightArray[j] = arr[mid + 1 + j];  
	}  
	int i = 0, j = 0, k = left;  
	while (i < n1 && j < n2) {  
		if (leftArray[i] <= rightArray[j]) {  
			arr[k++] = leftArray[i++];  
		} else {
			arr[k++] = rightArray[j++];  
		}
	}
	while (i < n1) {  
		arr[k++] = leftArray[i++];  
	}
	while (j < n2) {  
		arr[k++] = rightArray[j++];  
	}
}
```
