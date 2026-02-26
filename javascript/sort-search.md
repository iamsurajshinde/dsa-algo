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

```javascript
function bubbleSort(arr) {
    const n = arr.length;
    let swapped;

    for (let i = 0; i < n - 1; i++) {
        swapped = false;
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                const temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        if (!swapped) break;
    }
}
```

### 2️⃣ Selection Sort
✅ `Concept`: Find the smallest element and put it in the correct position iteratively.

✅ `Use Case`: When memory writes are expensive.

👉 `Complexity`: Always: O(n²)

```javascript
function selectionSort(arr) {
    for (let i = 0; i < arr.length - 1; i++) {
        let minIdx = i;
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[minIdx]) minIdx = j;
        }
        const temp = arr[minIdx];
        arr[minIdx] = arr[i];
        arr[i] = temp;
    }
}
```

### 3️⃣ Insertion Sort
✅ `Concept`: Insert elements into the sorted part of the array one by one.

✅ `Use Case`: Efficient for small or partially sorted arrays.

👉 `Complexity`: Best: O(n) Worst: O(n²)

```javascript
function insertionSort(arr) {
    for (let i = 1; i < arr.length; i++) {
        const key = arr[i];
        let j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### 4️⃣ Merge Sort
✅ `Concept`: Divide the array into halves, sort recursively, and merge.

✅ `Use Case`: Good for large datasets and stable sorting.

👉 `Complexity`: Always: O(n log n)

```javascript
function mergeSort(arr, l, r) {
    if (l >= r) return;
    const mid = Math.floor((l + r) / 2);
    mergeSort(arr, l, mid);
    mergeSort(arr, mid + 1, r);
    merge(arr, l, mid, r);
}

function merge(arr, l, m, r) {
    const left = arr.slice(l, m + 1);
    const right = arr.slice(m + 1, r + 1);

    let i = 0;
    let j = 0;
    let k = l;

    while (i < left.length && j < right.length) {
        if (left[i] <= right[j]) arr[k++] = left[i++];
        else arr[k++] = right[j++];
    }
    while (i < left.length) arr[k++] = left[i++];
    while (j < right.length) arr[k++] = right[j++];
}
```

### 5️⃣ Quick Sort
✅ `Concept`: Choose a pivot, partition the array, and sort recursively.

✅ `Use Case`: In-memory sorting, average O(n log n).

👉 `Complexity`: Best/Average: O(n log n) Worst: O(n²)

```javascript
function quickSort(arr, low, high) {
    if (low < high) {
        const p = partition(arr, low, high);
        quickSort(arr, low, p - 1);
        quickSort(arr, p + 1, high);
    }
}

function partition(arr, low, high) {
    const pivot = arr[high];
    let i = low - 1;

    for (let j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            const temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }

    const temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;

    return i + 1;
}
```

### 6️⃣ Heap Sort
✅ `Concept`: Build a max heap and repeatedly extract the largest element.

✅ `Use Case`: Requires no extra memory (in-place).

👉 `Complexity`: Always: O(n log n)

```javascript
function heapSort(arr) {
    const n = arr.length;

    for (let i = Math.floor(n / 2) - 1; i >= 0; i--) heapify(arr, n, i);
    for (let i = n - 1; i > 0; i--) {
        const temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        heapify(arr, i, 0);
    }
}

function heapify(arr, n, i) {
    let largest = i;
    const left = 2 * i + 1;
    const right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest]) largest = left;
    if (right < n && arr[right] > arr[largest]) largest = right;

    if (largest !== i) {
        const swap = arr[i];
        arr[i] = arr[largest];
        arr[largest] = swap;
        heapify(arr, n, largest);
    }
}
```

<hr>

# 🔍 Searching Algorithms

### 1️⃣ Linear Search
✅ `Concept`: Scan each element sequentially.

✅ `Use Case`: Works on unsorted data.

👉 `Complexity`: Always: O(n)

```javascript
function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) return i;
    }
    return -1;
}
```

### 2️⃣ Binary Search
✅ `Concept`: Divide the sorted array into halves and search recursively or iteratively.

✅ `Use Case`: Fast search on sorted data.

👉 `Complexity`: Always: O(log n)

```javascript
function binarySearch(arr, target) {
    let l = 0;
    let r = arr.length - 1;

    while (l <= r) {
        const mid = l + Math.floor((r - l) / 2);
        if (arr[mid] === target) return mid;
        if (arr[mid] < target) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}
```

### 3️⃣ Ternary Search
✅ `Concept`: Similar to binary search but splits into 3 parts.

✅ `Use Case`: Works well for unimodal functions.

👉 `Complexity`: Always: O(log₃ n)

```javascript
function ternarySearch(arr, l, r, x) {
    if (r >= l) {
        const mid1 = l + Math.floor((r - l) / 3);
        const mid2 = r - Math.floor((r - l) / 3);

        if (arr[mid1] === x) return mid1;
        if (arr[mid2] === x) return mid2;

        if (x < arr[mid1]) return ternarySearch(arr, l, mid1 - 1, x);
        if (x > arr[mid2]) return ternarySearch(arr, mid2 + 1, r, x);
        return ternarySearch(arr, mid1 + 1, mid2 - 1, x);
    }
    return -1;
}
```

### 4️⃣ Jump Search
✅ `Concept`: Jump fixed steps (√n) and then linear search in the block.

✅ `Use Case`: Sorted data with fewer comparisons.

👉 `Complexity`: Always: O(√n)

```javascript
function jumpSearch(arr, target) {
    const n = arr.length;
    let step = Math.floor(Math.sqrt(n));
    let prev = 0;

    while (arr[Math.min(step, n) - 1] < target) {
        prev = step;
        step += Math.floor(Math.sqrt(n));
        if (prev >= n) return -1;
    }

    while (arr[prev] < target) {
        prev++;
        if (prev === Math.min(step, n)) return -1;
    }

    return arr[prev] === target ? prev : -1;
}
```

### 5️⃣ Exponential Search
✅ `Concept`:Exponentially find a range, then do binary search.

✅ `Use Case`: Unknown size sorted arrays or infinite streams.

👉 `Complexity`: Always: O(log n)

```javascript
function exponentialSearch(arr, target) {
    if (arr[0] === target) return 0;

    let i = 1;
    while (i < arr.length && arr[i] <= target) i *= 2;

    return binarySearchRange(arr, Math.floor(i / 2), Math.min(i, arr.length - 1), target);
}

function binarySearchRange(arr, l, r, target) {
    while (l <= r) {
        const mid = l + Math.floor((r - l) / 2);
        if (arr[mid] === target) return mid;
        if (arr[mid] < target) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}
```
