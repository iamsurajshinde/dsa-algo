# 📑 Index

## Sorting Algorithms
- [Bubble Sort](#1️⃣-bubble-sort)
- [Selection Sort](#2️⃣-selection-sort)
- [Insertion Sort](#3️⃣-insertion-sort)
- [Merge Sort](#4️⃣-merge-sort)
- [Quick Sort](#5️⃣-quick-sort)
- [Heap Sort](#6️⃣-heap-sort)

## Searching Algorithms
- [Linear Search](#1️⃣-linear-search)
- [Binary Search](#2️⃣-binary-search)
- [Ternary Search](#3️⃣-ternary-search)
- [Jump Search](#4️⃣-jump-search)
- [Exponential Search](#5️⃣-exponential-search)


# 🔢 Sorting Algorithms

### 1️⃣ Bubble Sort
✅ `Concept`: Compare adjacent elements and swap them if they are out of order. Repeat until no swaps are needed.

✅ `Use Case`: Good for small or almost sorted datasets.

👉 `Complexity`: Best: O(n) Average/Worst: O(n²)

```java
public static void bubbleSort(int[] arr) {
    int n = arr.length;
    boolean swapped;
    for (int i = 0; i < n-1; i++) {
        swapped = false;
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                int temp = arr[j]; arr[j] = arr[j+1]; arr[j+1] = temp;
                swapped = true;
            }
        }
        if (!swapped) break; // Optimization: Stop early if sorted
    }
}
```

### 2️⃣ Selection Sort
✅ `Concept`: Find the smallest element and put it in the correct position iteratively.

✅ `Use Case`: When memory writes are expensive.

👉 `Complexity`: Always: O(n²)

```java
public static void selectionSort(int[] arr) {
    for (int i = 0; i < arr.length-1; i++) {
        int minIdx = i;
        for (int j = i+1; j < arr.length; j++) {
            if (arr[j] < arr[minIdx]) minIdx = j;
        }
        int temp = arr[minIdx]; arr[minIdx] = arr[i]; arr[i] = temp;
    }
}
```

### 3️⃣ Insertion Sort
✅ `Concept`: Insert elements into the sorted part of the array one by one.

✅ `Use Case`: Efficient for small or partially sorted arrays.

👉 `Complexity`: Best: O(n) Worst: O(n²)

```java
public static void insertionSort(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}
```

### 4️⃣ Merge Sort
✅ `Concept`: Divide the array into halves, sort recursively, and merge.

✅ `Use Case`: Good for large datasets and stable sorting.

👉 `Complexity`: Always: O(n log n)

```java
public static void mergeSort(int[] arr, int l, int r) {
    if (l >= r) return;
    int mid = (l+r)/2;
    mergeSort(arr, l, mid);
    mergeSort(arr, mid+1, r);
    merge(arr, l, mid, r);
}
```

### 5️⃣ Quick Sort
✅ `Concept`: Choose a pivot, partition the array, and sort recursively.

✅ `Use Case`: In-memory sorting, average O(n log n).

👉 `Complexity`: Best/Average: O(n log n) Worst: O(n²)

```java
public static void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int p = partition(arr, low, high);
        quickSort(arr, low, p-1);
        quickSort(arr, p+1, high);
    }
}
```

### 6️⃣ Heap Sort
✅ `Concept`: Build a max heap and repeatedly extract the largest element.

✅ `Use Case`: Requires no extra memory (in-place).

👉 `Complexity`: Always: O(n log n)

```java
public static void heapSort(int[] arr) {
    int n = arr.length;
    for (int i = n/2-1; i>=0; i--) heapify(arr,n,i);
    for (int i=n-1; i>0; i--){
        int temp = arr[0]; arr[0] = arr[i]; arr[i] = temp;
        heapify(arr,i,0);
    }
}
```
<hr>

# 🔍 Searching Algorithms

### 1️⃣ Linear Search
✅ `Concept`: Scan each element sequentially.

✅ `Use Case`: Works on unsorted data.

👉 `Complexity`: Always: O(n)

```java
public static int linearSearch(int[] arr, int target){
    for(int i=0;i<arr.length;i++) if(arr[i]==target) return i;
    return -1;
}
```

### 2️⃣ Binary Search
✅ `Concept`: Divide the sorted array into halves and search recursively or iteratively.

✅ `Use Case`: Fast search on sorted data.

👉 `Complexity`: Always: O(log n)

```java
public static int binarySearch(int[] arr, int target){
    int l=0,r=arr.length-1;
    while(l<=r){
        int mid = l+(r-l)/2;
        if(arr[mid]==target) return mid;
        if(arr[mid]<target) l=mid+1;
        else r=mid-1;
    }
    return -1;
}
```

### 3️⃣ Ternary Search
✅ `Concept`: Similar to binary search but splits into 3 parts.

✅ `Use Case`: Works well for unimodal functions.

👉 `Complexity`: Always: O(log₃ n)

```java
public static int ternarySearch(int[] arr, int l, int r, int x){
    if(r>=l){
        int mid1=l+(r-l)/3;
        int mid2=r-(r-l)/3;
        if(arr[mid1]==x) return mid1;
        if(arr[mid2]==x) return mid2;
        if(x<arr[mid1]) return ternarySearch(arr,l,mid1-1,x);
        else if(x>arr[mid2]) return ternarySearch(arr,mid2+1,r,x);
        else return ternarySearch(arr,mid1+1,mid2-1,x);
    }
    return -1;
}
```

### 4️⃣ Jump Search
✅ `Concept`: Jump fixed steps (√n) and then linear search in the block.

✅ `Use Case`: Sorted data with fewer comparisons.

👉 `Complexity`: Always: O(√n)

```java
public static int jumpSearch(int[] arr, int target){
    int n=arr.length, step=(int)Math.floor(Math.sqrt(n)), prev=0;
    while(arr[Math.min(step,n)-1]<target){
        prev=step; step+=Math.floor(Math.sqrt(n));
        if(prev>=n) return -1;
    }
    while(arr[prev]<target){
        prev++;
        if(prev==Math.min(step,n)) return -1;
    }
    return arr[prev]==target ? prev : -1;
}
```

### 5️⃣ Exponential Search
✅ `Concept`:Exponentially find a range, then do binary search.

✅ `Use Case`: Unknown size sorted arrays or infinite streams.

👉 `Complexity`: Always: O(log n)

```java
public static int exponentialSearch(int[] arr, int target){
    if(arr[0]==target) return 0;
    int i=1;
    while(i<arr.length && arr[i]<=target) i*=2;
    return binarySearchRange(arr, i/2, Math.min(i,arr.length-1), target);
}
