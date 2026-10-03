# SArray-Based Number Manipulator

This project implements and compares several classical sorting algorithms in Java. The program reads an array of integers from a file, allows the user to select a sorting algorithm, sorts the data, prints the resulting array, and reports the number of comparisons performed.

The implemented algorithms are:

* Selection Sort
* Merge Sort
* Heap Sort
* Quick Sort using a first-element pivot
* Quick Sort using a randomized pivot

## Overview

The project consists of a sorting implementation, a driver program for user interaction, and a shell script for compiling and running the program.

The driver reads the input array from a text file and presents the following menu:

```text
selection-sort (s)
merge-sort (m)
heap-sort (h)
quick-sort-fp (q)
quick-sort-rp (r)
Enter the algorithm:
```

The user enters the corresponding letter to select the sorting algorithm.

## Project Structure

```text
.
├── Sort.java
├── SortDriver.java
├── random.txt
└── run.sh
```

### `Sort.java`

Contains the implementations of the sorting algorithms and supporting methods.

Implemented methods include:

* `seS()` — Selection Sort
* `meS()` — Merge Sort
* `heapS()` — Heap Sort
* `quickSL()` / `quickL()` — Quick Sort using the first element as pivot
* `quickSR()` / `quickR()` — Quick Sort using a randomized pivot
* `printF()` — Prints the array in forward order
* `printR()` — Prints the array in reverse order
* `getCount()` — Returns the comparison counter
* `swap()` — Swaps two array elements

### `SortDriver.java`

Provides the main program interface.

It:

1. Reads the input filename from the command line.
2. Opens the input file.
3. Reads the first line of integers.
4. Converts the values into an integer array.
5. Displays the sorting algorithm menu.
6. Reads the user's algorithm selection.
7. Executes the selected sorting algorithm.
8. Prints the sorted array.
9. Prints the recorded comparison count.

### `run.sh`

The shell script compiles the Java source files and runs the sorting driver:

```bash
javac Sort.java
javac SortDriver.java

java SortDriver random.txt
```

## Requirements

You need:

* Java Development Kit (JDK)
* A terminal or command-line environment
* An input text file containing integers

Verify Java is installed with:

```bash
java --version
javac --version
```

## Running the Program

### Using the Shell Script

Make the script executable if necessary:

```bash
chmod +x run.sh
```

Then run:

```bash
./run.sh
```

The script compiles:

```bash
javac Sort.java
javac SortDriver.java
```

and then runs:

```bash
java SortDriver random.txt
```

### Running Manually

You can also compile and run the program directly:

```bash
javac Sort.java
javac SortDriver.java
java SortDriver random.txt
```

The input filename can be changed:

```bash
java SortDriver input.txt
```

## Input Format

The driver reads the **first line** of the input file and separates the values using whitespace.

For example:

```text
8 3 1 7 0 10 2
```

The values are converted from strings to integers and stored in an `int[]`.

```java
String[] stF = reader.readLine().split("\\s+");
```

Each value is then converted using:

```java
arr[i] = Integer.parseInt(stF[i]);
```

## Selecting an Algorithm

After the input is loaded, the program displays:

```text
selection-sort (s)
merge-sort (m)
heap-sort (h)
quick-sort-fp (q)
quick-sort-rp (r)
Enter the algorithm:
```

The corresponding choices are:

| Input | Algorithm                 |
| ----- | ------------------------- |
| `s`   | Selection Sort            |
| `m`   | Merge Sort                |
| `h`   | Heap Sort                 |
| `q`   | Quick Sort — First Pivot  |
| `r`   | Quick Sort — Random Pivot |

For example:

```text
Enter the algorithm:
m
```

selects Merge Sort.

## Selection Sort

Selection Sort is implemented by repeatedly finding the largest element in the remaining portion of the array and moving it toward the beginning.

The main method is:

```java
public void seS(int[] arr)
```

The implementation increments `count` for each comparison:

```java
if (arr[index] < arr[j]) {
    index = j;
}
count++;
```

After sorting, the array is printed using `printR()`.

The program reports:

```text
#Selection-sort comparisons: ...
```

## Merge Sort

Merge Sort is implemented recursively.

The main method is:

```java
public void meS(int[] arr, int left, int right)
```

The array is divided into two sections:

```java
int mid = (left + right) / 2;
```

The two halves are recursively sorted and then combined using:

```java
merge(array, left, mid, right);
```

The `merge()` method creates temporary left and right arrays and compares their elements while reconstructing the sorted portion.

Comparisons are counted inside the merge operation:

```java
count++;
```

The program reports:

```text
#Merge-sort comparisons: ...
```

## Heap Sort

Heap Sort is implemented using a **max heap**.

The main sorting method is:

```java
public void heapS(int[] arr)
```

The heap is constructed using:

```java
heapB(arr, len, i);
```

The `heapB()` method determines the largest value among a node and its children and moves that value toward the root.

The child indices are calculated as:

```java
int l = 2 * i + 1;
int r = l + 1;
```

The program counts comparisons performed while building and maintaining the heap.

The final result is reported as:

```text
#Heap-sort comparisons: ...
```

## Quick Sort — First Pivot

The first Quick Sort implementation uses the first element of the current partition as the pivot.

The driver calls:

```java
s.quickSL(arr, 0, len - 1);
```

which invokes:

```java
quickL(array, left, right);
```

The pivot is the element at:

```java
arr[left]
```

The algorithm partitions the array around the pivot and recursively processes the two resulting portions.

The comparison count is reported as:

```text
#Quick-sort-fp comparisons: ...
```

## Quick Sort — Random Pivot

The second Quick Sort implementation is intended to use a randomly selected pivot.

The driver calls:

```java
s.quickSR(arr, 0, len - 1);
```

The method uses Java's `Random` class:

```java
Random rand = new Random();
```

to generate a pivot-related value.

The recursive implementation is handled by:

```java
quickR(array, left, right, d);
```

The program reports:

```text
#Quick-sort-rp comparisons: ...
```

## Comparison Counting

The `Sort` class maintains a comparison counter:

```java
private long count = 0;
```

The counter is incremented at comparison points within the sorting implementations.

The current count can be retrieved using:

```java
public long getCount()
```

This allows the program to compare the number of recorded comparisons made by the different sorting algorithms.

## Array Output

Two output methods are provided.

### Forward Order

```java
printF()
```

prints the array from the first element to the last.

### Reverse Order

```java
printR()
```

prints the array from the last element to the first.

Selection Sort uses `printR()`, while the other algorithms use `printF()` through the driver.

## Experiment 2

`SortDriver.java` also contains a commented-out version of `main()` for an additional experiment.

This experiment:

1. Asks the user for an array size.
2. Creates a list containing values from `0` through `n - 1`.
3. Randomly shuffles the values using `Collections.shuffle()`.
4. Copies the shuffled values into an integer array.
5. Allows the user to select one of the sorting algorithms.
6. Reports the comparison count.

The relevant section begins with:

```java
/*
 * The main function for experiment 2
 */
```

The experiment can be enabled by removing the surrounding block comment and replacing the active `main()` implementation.

## Example

Suppose `random.txt` contains:

```text
8 3 1 7 0 10 2
```

Run:

```bash
./run.sh
```

Then select:

```text
m
```

The program sorts the array and prints the sorted result followed by the Merge Sort comparison count.

The exact comparison count depends on the implementation's comparison-counting locations.

## Algorithm Summary

| Algorithm      | Method                   | Main Technique                |
| -------------- | ------------------------ | ----------------------------- |
| Selection Sort | `seS()`                  | Repeatedly selects an element |
| Merge Sort     | `meS()`                  | Divide and merge              |
| Heap Sort      | `heapS()`                | Max heap                      |
| Quick Sort     | `quickSL()` / `quickL()` | First element as pivot        |
| Quick Sort     | `quickSR()` / `quickR()` | Randomized pivot              |

## Key Concepts Demonstrated

This project demonstrates several important algorithms and data-structure concepts:

* Array manipulation
* Recursion
* Divide-and-conquer algorithms
* Partitioning
* Binary heaps
* Randomization
* File input
* Command-line arguments
* Java classes and objects
* Comparison counting
* Algorithm performance analysis

## Quick Start

```bash
# Compile
javac Sort.java
javac SortDriver.java

# Run with the provided input file
java SortDriver random.txt
```

Or use the provided script:

```bash
./run.sh
```

Then choose one of:

```text
s  Selection Sort
m  Merge Sort
h  Heap Sort
q  Quick Sort (First Pivot)
r  Quick Sort (Random Pivot)
```

The program will sort the input and display the resulting array and recorded comparison count.
