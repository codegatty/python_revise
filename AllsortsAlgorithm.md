## Bubble sort

<ul>
    <li>select first elemnt in outer loop</li>
    <li>compare elemnet and find maximum elemnt inner loop</li>
    <li>trim from back</li>
</ul>


```python
arr = [2, 34, 5, 6, 73, 73, 36, 78]  # Initialize the array
n = len(arr)  # Get the length of the array

# Outer loop to go through the entire array
for i in range(0, n):
    # Inner loop to compare adjacent elements
    # The range decreases by i since the last i elements will already be sorted
    for j in range(0, n - i - 1):
        # Compare adjacent elements
        if arr[j] > arr[j + 1]:
            # Swap if the current element is greater than the next
            temp = arr[j]
            arr[j] = arr[j + 1]
            arr[j + 1] = temp

# Print the sorted array
print(arr)

```

    [2, 5, 6, 34, 36, 73, 73, 78]
    

## selection sort
<ul>
    <li>select minimum in outer loop</li>
    <li>compare elemnet and find minimum inner loop</li>
    <li>trim from front</li>
</ul>


```python
arr = [2, 34, 5, 6, 73, 73, 36, 78]  # Initialize the array
n = len(arr)  # Get the length of the array

# Outer loop to go through the entire array
for i in range(0, n):
    min = i  # Assume the current element is the minimum
    
    # Inner loop to find the minimum element in the unsorted portion of the array
    for j in range(i, n):
        if arr[min] > arr[j]:  # If a smaller element is found
            min = j  # Update the index of the minimum element
    
    # Swap the found minimum element with the first element of the unsorted portion
    temp = arr[min]
    arr[min] = arr[i]
    arr[i] = temp

# Print the sorted array
print(arr)

```

    [2, 5, 6, 34, 36, 73, 73, 78]
    

## Insertion Sort
<ul>
    <li>outer loop moves the bound of sorted array</li>
    <li>Innter loop compares the element and add to the element to sorted  part</li>
</ul>


```python
arr = [9, 9, 4, 3, 1, 2, 0, 8, 4, 2]  # Initialize the array
n = len(arr)  # Get the length of the array

# Outer loop to iterate through the array from the second element
for i in range(1, n):
    temp = arr[i]  # Store the current element in a temporary variable
    j = i  # Set `j` to the current index
    
    # Inner loop to find the correct position for the element in the sorted portion of the array
    while j > 0 and arr[j - 1] > temp:
        arr[j] = arr[j - 1]  # Shift the larger element to the right
        j -= 1  # Move one step to the left
    
    # Place the current element at its correct position
    arr[j] = temp

# Print the sorted array
print(arr)

```

    [0, 1, 2, 2, 3, 4, 4, 8, 9, 9]
    

## Merge sort
<ul>
    <li>divide by middle element</li>
    <li>use extra array to merge element with old array</li>
</ul>


```python
def mergeSort(arr, low, high):
    if low < high:
        mid = (low + high) // 2
        mergeSort(arr, low, mid)
        mergeSort(arr, mid + 1, high)
        mergeIt(arr, low, mid, high)

def mergeIt(arr, low, mid, high):
    temp = []
    i = low
    j = mid + 1
    
    # Merging the two halves
    while i <= mid and j <= high:
        if arr[i] <= arr[j]:
            temp.append(arr[i])
            i += 1
        else:
            temp.append(arr[j])
            j += 1
    
    # Copy remaining elements of the first half (if any)
    while i <= mid:
        temp.append(arr[i])
        i += 1
    
    # Copy remaining elements of the second half (if any)
    while j <= high:
        temp.append(arr[j])
        j += 1
    
    # Copy sorted elements back into the original array
    for k in range(low, high + 1):
        arr[k] = temp[k - low]

# Test case
arr = [1, 23, 4, 3, 2, 6, 9, 1, 1, 24, 567, 9, 2]
mergeSort(arr, 0, len(arr) - 1)
print(arr)
```

    [1, 1, 1, 2, 2, 3, 4, 6, 9, 9, 23, 24, 567]
    

## Quick sort
<ul>
<li>split not by middle element<li>
<li>split by the proper postion of pivot element</li>
</ul>


```python
def partition(arr, low, high):
    pivot = arr[low]
    i = low
    j = high

    # Partition the array
    while i < j:
        # Move 'i' to the right while elements are less than or equal to the pivot
        while arr[i] <= pivot and i < high:
            i += 1
        
        # Move 'j' to the left while elements are greater than the pivot
        while arr[j] > pivot and j > low:
            j -= 1

        # Swap elements if needed
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

    # Place pivot in its correct position
    arr[low], arr[j] = arr[j], arr[low]
    return j

def quicksort(arr, low, high):
    if low < high:
        # Partition the array and get the pivot index
        p_index = partition(arr, low, high)

        # Recursively sort elements before and after the partition
        quicksort(arr, low, p_index - 1)
        quicksort(arr, p_index + 1, high)

def quick_sort(arr):
    quicksort(arr, 0, len(arr) - 1)
    return arr

# Test the quicksort implementation
arr = [4, 6, 2, 5, 7, 9, 1, 3]
print("Before Using quick sort:")
print(arr)

sorted_arr = quick_sort(arr)
print("After Using quick sort:")
print(sorted_arr)

        
```
