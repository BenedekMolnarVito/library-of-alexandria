---
title: "Gemma-4-E4B-it and Qwen3.5–4B comparison"
source: "https://medium.com/@jallenswrx2016/gemma-4-e4b-it-and-qwen3-5-4b-comparison-60df35e67de9"
author:
  - "[[jon allen]]"
published: 2026-04-14
created: 2026-04-18
description: "Gemma-4-E4B-it and Qwen3.5–4B comparison Some thoughts head to head comparison on running with llama.cpp The comparison isn’t quite apples to apples. Maybe a “Fuji” to a “Granny Smith” …"
tags:
  - "clippings"
---
Some thoughts head to head comparison on running with llama.cpp

The comparison isn’t quite apples to apples. Maybe a “Fuji” to a “Granny Smith”. Gemma4 moved into the multimodal realm with voice. But still it is worth comparing to understand how one is better than the other. Which to use in what use case. Both can fit on 16G macbook pro.

Gemma4 is newer and is quicker in most cases for agentic workflows. Better at code generation. Qwen 3.5 4B is the better at reasoning.

Qwen 3.5 4B is comparable, but the cost is 2 to 5 times the number of reasoning tokens. And that costs time — your response from Qwen3.5–4B can be 2x longer and perhaps 3x for more logical or more difficult problems.

I ran 3 tests — C++ algorithms, Pascal algorithms, logic test. Each test was judged by 2 models — Mistral Large and my Gemini Pro 3.1 on the web. Also careful review by myself as well. C++ and Pascal generated examples were test compiled. test scripts were chatdsl from Chatybot.

## C++

C++ test was to generate 10 C++ case samples with all the surrounding understanding:

```c
# Generate C++ algorithm examples with Model 1 (Gemma4)
/model ${model1}
/multiline
List ${algorithm_count} C++ algorithm examples with the following structure for each:
1. Algorithm Name
2. Brief Description
3. C++ Implementation (complete, compilable code)
4. Time and Space Complexity Analysis
5. Example Use Case

Ensure the algorithms are diverse, covering sorting, searching, graph algorithms, dynamic programming, and other fundamental categories.

Format each algorithm clearly with all five components.
;;
/multiline
/save ${model1_results}
/filebank1 ${model1_results}

# Generate C++ algorithm examples with Model 2 (Qwen3)
/model ${model2}
/multiline
List ${algorithm_count} C++ algorithm examples with the following structure for each:
1. Algorithm Name
2. Brief Description
3. C++ Implementation (complete, compilable code)
4. Time and Space Complexity Analysis
5. Example Use Case

Ensure the algorithms are diverse, covering sorting, searching, graph algorithms, dynamic programming, and other fundamental categories.

Format each algorithm clearly with all five components.
```

Only one program failed compilation for Qwen

```c
# Compilation and Runtime Test Summary

## Overview
This document summarizes the compilation and runtime validation results for the Qwen and Gemma4 model code examples.

## Qwen Model Results
- **Total Files Tested:** 10
- **Compilation Success:** 9
- **Compilation Failures:** 1
- **Runtime Success:** 9

### Compilation Failures
- **File:** \`quick_sort.cpp\`
- **Error:** \`no matching function for call to 'partition'\`
- **Reason:** Missing \`partition\` function definition.

### Notes
- All other files compiled and ran successfully, producing expected outputs.
- The \`quick_sort.cpp\` file failed due to a logical error in the original code.

## Gemma4 Model Results
- **Total Files Tested:** 10
- **Compilation Success:** 10
- **Compilation Failures:** 0
- **Runtime Success:** 10

### Notes
- All files compiled and ran successfully, producing expected outputs.
- The code quality is high, with no logical errors or compilation issues.

## Summary Table
| Model  | Total Files | Compilation Success | Compilation Failures | Runtime Success |
|--------|-------------|---------------------|---------------------|-----------------|
| Qwen   | 10          | 9                   | 1                   | 9               |
| Gemma4 | 10          | 10                  | 0                   | 10              |

## Conclusion
- **Gemma4** performed flawlessly with all files compiling and running successfully.
- **Qwen** had one compilation failure due to a missing function definition in \`quick_sort.cpp\`.
```

C++ generation by Gemma4 was quite good. Qwen more like competitive quick & dirty coding. *Gemma4* follows modern C++ conventions (C++11 and beyond), making the code more production ready. *Qwen 3.5* writes in a bit of “Competitive Programming” style that is concise but dangerous for long-term software maintenance for some. These are the defaults for C++ code generation. So, you have to prompt to change them.

```c
Gemma4 Implementation

#include <iostream>
#include <vector>

int binarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2; // Prevents overflow
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

Qwen Implementation

#include <iostream>
using namespace std;

int binarySearch(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

As you can see Qwen is more or less like C. and the indentation style is a bit like a kid coded it. Gemma4 uses a vector. So, there you have it. Qwen would likely need more guidelines in their skills.md than Gemma4. So, a lesson from this test is that it helps to specify type of C++ standards that you want the model to adhere.

Ratings by judge model.

```c
#### **4. Overall Assessment of Both Models' Capabilities in C++ Algorithm Generation**
| **Category**            | **gemma4_llamacpp_1**                          | **qwen3_llamacpp_1**                            | **Verdict**                     |
|-------------------------|-----------------------------------------------|--------------------------------------------------|---------------------------------|
| **Accuracy**            | ✅ Near-perfect, no critical flaws.           | ❌ Logical errors (e.g., \`topoSort\`, \`kMeans\`).   | **gemma4 wins**                 |
| **Code Quality**        | ✅ Modern C++, readable, modular.             | ❌ Poor practices (e.g., \`using namespace std\`).  | **gemma4 wins**                  |
| **Complexity Analysis** | ✅ Detailed, precise, and contextual.         | ❌ Superficial, occasionally incorrect.           | **gemma4 wins**                   |
| **Use Case Relevance**  | ✅ Practical, diverse, and well-explained.    | ⚠️ Some unique cases but often generic.           | **gemma4 wins**                   |
| **Novelty**             | ✅ Broad coverage of fundamentals.            | ⚠️ Includes K-Means/Topo Sort but repeats others. | **Tie (gemma4 for fundamentals)** |
| **Production Readiness**| ✅ Ready for education/professional use.      | ❌ Needs fixes before deployment.                 | **gemma4 wins**                   |
```

## Pascal

Pascal test is the same 10 Pascal algorithm examples… except for use of good old Pascal. *And perhaps you shouldn’t use either model for Pascal, but we will go over the results anyway*.

At a top level — you should only expect somewhere between 20 to 50% of code generated to even compile without corrections. Which most agentic coding agents will handle, but that costs time and tokens or fixing stuff it should have had correct in the first place.

Here is an example — Qwen compiles but has an logical error with begin and end blocks leading to loops. and the gemma4 has a compile error:

```c
## MergeSort

### Qwen Implementation (program5.pas)
\`\`\`pascal
program MergeSort;

uses SysUtils;

type
  TIntegerArray = array of Integer;

procedure Merge(var arr: TIntegerArray; left, mid, right: Integer);
var
  i, j, k: Integer;
  temp: array[0..100] of Integer;
begin
  i := left;
  j := mid + 1;
  k := left;

  while (i <= mid) and (j <= right) do
    if arr[i] < arr[j] then
      temp[k] := arr[i]
    else
      temp[k] := arr[j];
    k := k + 1;

  while i <= mid do
    temp[k] := arr[i];
    k := k + 1;
    i := i + 1;
  while j <= right do
    temp[k] := arr[j];
    k := k + 1;
    j := j + 1;

  for i := left to right do
    arr[i] := temp[i - left];
end;

procedure MergeSort(var arr: TIntegerArray; low, high: Integer);
var
  mid: Integer;
begin
  if low < high then
  begin
    mid := (low + high) div 2;
    MergeSort(arr, low, mid);
    MergeSort(arr, mid + 1, high);
    Merge(arr, low, mid, high);
  end;
end;

var
  data: TIntegerArray;
  i: Integer;
begin
  SetLength(data, 6);
  data[0] := 34; data[1] := 7; data[2] := 23;
  data[3] := 32; data[4] := 10; data[5] := 98;

  Write('Before: ');
  for i := 0 to High(data) do Write(data[i], ' ');
  WriteLn;

  MergeSort(data, 0, High(data));

  Write('After: ');
  for i := 0 to High(data) do Write(data[i], ' ');
  WriteLn;
end.
\`\`\`

**Compilation Status**: Compiles in Delphi mode but times out at runtime (likely infinite loop).

### Gemma4 Implementation (program1.pas)
\`\`\`pascal
program MergeSortExample;

type
  TArray = array[1..10] of Integer;

// Function to merge two sorted sub-arrays
procedure Merge(const A: TArray; L, M, R: Integer; Temp: TArray);
var
  i, j, k: Integer;
begin
  i := L; j := M + 1; k := L;
  while i <= M and j <= R do begin
    if A[i] <= A[j] then
      Temp[k] := A[i]
    else
      Temp[k] := A[j];
    Inc(k); Inc(i) or Inc(j);
  end;

  // Copy remaining elements of the left half
  while i <= M do begin
    Temp[k] := A[i];
    Inc(k); Inc(i);
  end;

  // Copy remaining elements of the right half
  while j <= R do begin
    Temp[k] := A[j];
    Inc(k); Inc(j);
  end;

  // Copy back to the original array
  for k := L to R do
    A[k] := Temp[k];
end;

// Main recursive sorting function
procedure MergeSort(var A: TArray; L, R: Integer; Temp: TArray);
var
  M: Integer;
begin
  if L < R then begin
    M := (L + R) div 2;
    MergeSort(A, L, M, Temp);
    MergeSort(A, M + 1, R, Temp);
    Merge(A, L, M, R, Temp);
  end;
end;

var
  Data: TArray;
  TempArray: TArray;
begin
  // Initialize data
  Data[1] := 38; Data[2] := 27; Data[3] := 43; Data[4] := 15; Data[5] := 60;
  Data[6] := 8;  Data[7] := 22; Data[8] := 1;  Data[9] := 55; Data[10] := 3;

  // Perform sort
  MergeSort(Data, 1, 10, TempArray);

  // Output results
  WriteLn('Sorted Array: ');
  for var i := 1 to 10 do Write(Data[i], ' ');
  WriteLn;
end.
\`\`\`

**Compilation Status**: Fails to compile due to syntax errors (\`Inc(i) or Inc(j)\` and \`var i\` in loop).
```

The judge model rated Gemma4 the closest. It would require fewer edits to get running, but overall both suffer from poor generation and subtle issues with Pascal code generation. So, agentic coding would take repeat edits and extra time/tokens to get correct. Again your skills.md would need updates on what style of Pascal you want — classic ISO or modern Delphi.

Here are example results for -Delphi compatible compile

```c
# Gemma4 Pascal Code Examples - Delphi Mode Test Results

## Summary
- **Total Programs**: 10
- **Compiled Successfully**: 5 (program2, program3, program5, program7, program8)
- **Compilation Failures**: 5

## Detailed Results

### 1. MergeSortExample (program1.pas)
- **Status**: Compilation Failed
- **Error**: Syntax errors and type mismatches
- **Notes**: Uses \`Inc(i) or Inc(j)\` and other syntax issues.

### 2. BinarySearchExample (program2.pas)
- **Status**: Compilation Successful
- **Runtime**: Success
- **Output**: \`Element 30 found.\`
- **Notes**: Compiles and runs correctly.

### 3. BFSExample (program3.pas)
- **Status**: Compilation Successful
- **Runtime**: Success
- **Output**: \`BFS Traversal Order: 1 2 3 4 5\`
- **Notes**: Compiles and runs correctly.

### 4. DFSExample (program4.pas)
- **Status**: Compilation Failed
- **Error**: Syntax error with array initialization
- **Notes**: Uses \`Visited := array[1..MAX_NODES] of Boolean;\` which is invalid.

### 5. FibonacciDPExample (program5.pas)
- **Status**: Compilation Successful
- **Runtime**: Success
- **Output**: Fibonacci sequence up to 40
- **Notes**: Compiles and runs correctly.

### 6. DijkstraExample (program6.pas)
- **Status**: Compilation Failed
- **Error**: Syntax error with array type
- **Notes**: Uses \`EdgeWeight = array[1..MAX_NODES] of Integer;\` incorrectly.

### 7. LinearSearchExample (program7.pas)
- **Status**: Compilation Successful
- **Runtime**: Success
- **Output**: \`Element 88 found.\`
- **Notes**: Compiles and runs correctly.

### 8. QuickSortExample (program8.pas)
- **Status**: Compilation Successful
- **Runtime**: Success
- **Output**: \`Sorted Array: 1 2 3 4 5 6 7 8 9 10\`
- **Notes**: Compiles and runs correctly.

### 9. BSTTraversalExample (program9.pas)
- **Status**: Compilation Failed
- **Error**: Syntax error with pointer handling
- **Notes**: Pointer handling issues in Pascal.

### 10. PrimeCheckExample (program10.pas)
- **Status**: Compilation Failed
- **Error**: \`Identifier not found "NewLine"\`
- **Notes**: Uses \`NewLine\` which is not defined.

## Conclusion
Using Delphi mode (\`-Mdelphi\`) significantly improved compatibility, allowing 5 programs to compile and run successfully (BinarySearch, BFS, FibonacciDP, LinearSearch, QuickSort). The rest failed due to syntax errors or invalid Pascal constructs.%
```

Even Gemma4 has some issues with getting the syntax correct. But the algorithmic core is good.

Qwen also has similar issues. Algortihm is poorly implemented and some lapses in basic Pascal language. You can view the source and programs in the github at the end.

```c
# Qwen Pascal Code Examples - Delphi Mode Test Results

## Summary
- **Total Programs**: 10
- **Compiled Successfully**: 2 (program1, program5)
- **Compilation Failures**: 8

## Detailed Results

### 1. BubbleSort (program1.pas)
- **Status**: Compilation Successful
- **Runtime**: Success
- **Output**: \`Before Sorting: 64 34 25 12 22 After Sorting: 64 34 25 12 22\`
- **Notes**: Compiles and runs in Delphi mode, but sorting logic may be incorrect.

### 2. BinarySearch (program2.pas)
- **Status**: Compilation Failed
- **Error**: Syntax error with \`ELSE\`
- **Notes**: Missing semicolon before \`else\`.

### 3. DFSGraph (program3.pas)
- **Status**: Compilation Failed
- **Error**: Type mismatches and input handling issues
- **Notes**: Uses \`ReadLn\` incorrectly.

### 4. FibDP (program4.pas)
- **Status**: Compilation Failed
- **Error**: Type mismatch with \`SetLength\`
- **Notes**: Type issues with dynamic arrays.

### 5. MergeSort (program5.pas)
- **Status**: Compilation Successful
- **Runtime**: Timeout (likely infinite loop)
- **Notes**: Compiles but may have runtime issues.

### 6. BFSGraph (program6.pas)
- **Status**: Compilation Failed
- **Error**: Input handling issues
- **Notes**: Uses \`ReadLn\` incorrectly.

### 7. TreeTraversal (program7.pas)
- **Status**: Compilation Failed
- **Error**: Syntax error with pointer handling
- **Notes**: Pointer handling issues in Pascal.

### 8. PrimeCheck (program8.pas)
- **Status**: Compilation Failed
- **Error**: Type mismatch with \`Sqrt\`
- **Notes**: Type issues with \`Sqrt\` function.

### 9. Knapsack (program9.pas)
- **Status**: Compilation Failed
- **Error**: \`Identifier not found "Max"\`
- **Notes**: Uses \`Max\` function not defined.

### 10. QuickSort (program10.pas)
- **Status**: Compilation Failed
- **Error**: Invalid assignment in procedure
- **Notes**: Procedure assignment issues.

## Conclusion
Using Delphi mode (\`-Mdelphi\`) improved compatibility, allowing 2 programs to compile (BubbleSort and MergeSort). The rest still failed due to syntax errors, type mismatches, or incorrect use of Pascal constructs.%
```

## Logic test

The problems test deductive skill, math logic and syllogisic reasing ability. Some constraints and some logical fallacy identification.

```c
Here are four progressively challenging logic problems covering different types of reasoning:

---

### **Problem 1: The Mysterious Lock (Deduction Puzzle)**
**Problem Description:**
A treasure chest has a 3-digit combination lock. The following clues are provided:
1. The digits are all distinct and range from 0 to 9.
2. The first digit is twice the second digit.
3. The sum of the second and third digits is equal to the first digit.
4. The third digit is odd.

Determine the correct combination.

**Input Format:**
None (pure deduction).

**Output Format:**
A 3-digit number (e.g., \`123\`).

**Example:**
If the clues were simpler (e.g., "first digit is 1, second is 2"), the answer might be \`123\`.

**Solution:**
The correct combination is \`421\`.

---

### **Problem 2: The Knights and Knaves (Mathematical Logic)**
**Problem Description:**
On an island, there are two types of inhabitants:
- **Knights**, who always tell the truth.
- **Knaves**, who always lie.

You encounter two inhabitants, A and B.
- A says: "B is a knight."
- B says: "A and I are of opposite types."

Determine the types of A and B (knight or knave).

**Input Format:**
None (logical statements).

**Output Format:**
Two words separated by a space, representing the types of A and B (e.g., \`knight knave\`).

**Example:**
If A says "B is a knave" and B says "A is a knight," the answer would be \`knave knight\`.

**Solution:**
A is a **knave**, and B is a **knight**.

---

### **Problem 3: The Categorical Conundrum (Syllogisms)**
**Problem Description:**
Evaluate the validity of the following syllogism:
1. All philosophers are logicians.
2. Some logicians are mathematicians.
3. Therefore, some philosophers are mathematicians.

Is the conclusion necessarily true? If not, provide a counterexample using sets.

**Input Format:**
None (syllogism evaluation).

**Output Format:**
- First line: \`Valid\` or \`Invalid\`.
- Second line (if invalid): A counterexample in the form of sets (e.g., \`Philosophers = {A}, Logicians = {A, B}, Mathematicians = {B}\`).

**Example:**
For the syllogism:
1. All birds can fly.
2. Penguins are birds.
3. Therefore, penguins can fly.
The output would be:
\`\`\`
Invalid
Birds = {penguin, sparrow}, FlyingAnimals = {sparrow}
\`\`\`

**Solution:**
\`\`\`
Invalid
Philosophers = {A}, Logicians = {A, B}, Mathematicians = {B}
\`\`\`
(No overlap between philosophers and mathematicians.)

---

### **Problem 4: The Scheduling Dilemma (Constraint Satisfaction)**
**Problem Description:**
Four employees (Alice, Bob, Carol, Dave) must be assigned to four shifts (Morning, Afternoon, Evening, Night) with the following constraints:
1. Alice cannot work the Morning shift.
2. Bob cannot work the Night shift.
3. Carol must work either the Morning or Evening shift.
4. Dave must work a shift adjacent to Carol’s (e.g., if Carol works Morning, Dave must work Afternoon).
5. The Afternoon shift must be assigned to someone who can work the Night shift (but not necessarily vice versa).

Find a valid assignment of employees to shifts.

**Input Format:**
None (constraint satisfaction).

**Output Format:**
Four lines, each in the format \`Shift: Employee\` (e.g.,
\`\`\`
Morning: Carol
Afternoon: Dave
Evening: Alice
Night: Bob
\`\`\`

**Example:**
A simpler version might have 2 employees and 2 shifts with fewer constraints.

**Solution:**
One valid assignment is:
\`\`\`
Morning: Carol
Afternoon: Bob
Evening: Alice
Night: Dave
\`\`\`

---

### **Bonus Problem: Fallacy Identification (Logical Fallacies)**
**Problem Description:**
Identify the logical fallacy in the following argument:
"All cats are mammals. Some mammals are dogs. Therefore, some cats are dogs."

**Input Format:**
None (argument analysis).

**Output Format:**
The name of the fallacy (e.g., \`Affirming the consequent\`).

**Solution:**
**Illicit minor** (or **undistributed middle** in syllogistic terms).

---

These problems test deduction, mathematical logic, syllogistic reasoning, constraint satisfaction, and fallacy identification, with increasing complexity.%                  jon2allen@Mac logic_problems % 
jon2allen@Mac logic_problems % cat generated_problems.txt
Here are four progressively challenging logic problems covering different types of reasoning:

---

### **Problem 1: The Mysterious Lock (Deduction Puzzle)**
**Problem Description:**
A treasure chest has a 3-digit combination lock. The following clues are provided:
1. The digits are all distinct and range from 0 to 9.
2. The first digit is twice the second digit.
3. The sum of the second and third digits is equal to the first digit.
4. The third digit is odd.

Determine the correct combination.

**Input Format:**
None (pure deduction).

**Output Format:**
A 3-digit number (e.g., \`123\`).

**Example:**
If the clues were simpler (e.g., "first digit is 1, second is 2"), the answer might be \`123\`.

**Solution:**
The correct combination is \`421\`.

---

### **Problem 2: The Knights and Knaves (Mathematical Logic)**
**Problem Description:**
On an island, there are two types of inhabitants:
- **Knights**, who always tell the truth.
- **Knaves**, who always lie.

You encounter two inhabitants, A and B.
- A says: "B is a knight."
- B says: "A and I are of opposite types."

Determine the types of A and B (knight or knave).

**Input Format:**
None (logical statements).

**Output Format:**
Two words separated by a space, representing the types of A and B (e.g., \`knight knave\`).

**Example:**
If A says "B is a knave" and B says "A is a knight," the answer would be \`knave knight\`.

**Solution:**
A is a **knave**, and B is a **knight**.

---

### **Problem 3: The Categorical Conundrum (Syllogisms)**
**Problem Description:**
Evaluate the validity of the following syllogism:
1. All philosophers are logicians.
2. Some logicians are mathematicians.
3. Therefore, some philosophers are mathematicians.

Is the conclusion necessarily true? If not, provide a counterexample using sets.

**Input Format:**
None (syllogism evaluation).

**Output Format:**
- First line: \`Valid\` or \`Invalid\`.
- Second line (if invalid): A counterexample in the form of sets (e.g., \`Philosophers = {A}, Logicians = {A, B}, Mathematicians = {B}\`).

**Example:**
For the syllogism:
1. All birds can fly.
2. Penguins are birds.
3. Therefore, penguins can fly.
The output would be:
\`\`\`
Invalid
Birds = {penguin, sparrow}, FlyingAnimals = {sparrow}
\`\`\`

**Solution:**
\`\`\`
Invalid
Philosophers = {A}, Logicians = {A, B}, Mathematicians = {B}
\`\`\`
(No overlap between philosophers and mathematicians.)

---

### **Problem 4: The Scheduling Dilemma (Constraint Satisfaction)**
**Problem Description:**
Four employees (Alice, Bob, Carol, Dave) must be assigned to four shifts (Morning, Afternoon, Evening, Night) with the following constraints:
1. Alice cannot work the Morning shift.
2. Bob cannot work the Night shift.
3. Carol must work either the Morning or Evening shift.
4. Dave must work a shift adjacent to Carol’s (e.g., if Carol works Morning, Dave must work Afternoon).
5. The Afternoon shift must be assigned to someone who can work the Night shift (but not necessarily vice versa).

Find a valid assignment of employees to shifts.

**Input Format:**
None (constraint satisfaction).

**Output Format:**
Four lines, each in the format \`Shift: Employee\` (e.g.,
\`\`\`
Morning: Carol
Afternoon: Dave
Evening: Alice
Night: Bob
\`\`\`

**Example:**
A simpler version might have 2 employees and 2 shifts with fewer constraints.

**Solution:**
One valid assignment is:
\`\`\`
Morning: Carol
Afternoon: Bob
Evening: Alice
Night: Dave
\`\`\`

---

### **Bonus Problem: Fallacy Identification (Logical Fallacies)**
**Problem Description:**
Identify the logical fallacy in the following argument:
"All cats are mammals. Some mammals are dogs. Therefore, some cats are dogs."

**Input Format:**
None (argument analysis).

**Output Format:**
The name of the fallacy (e.g., \`Affirming the consequent\`).

**Solution:**
**Illicit minor** (or **undistributed middle** in syllogistic terms).

---
```

Here are the hight level results by judge model, personal review and using a yet another model ( Gemini Pro 3.1 ) to review the judge model ( mistral large ) output. And it appears that Qwen 3.5 is able to reason quite well for a scrapy little 4B dense model. But again, it is a long process from A to B — lot of tokens and time to get this high bar of a result. 2 to 3x of each.

```c
### **Final Summary Table**
| **Metric**                 | **qwen3_llamacpp_1**                          | **gemma4_llamacpp_1**                          |
|--------------------------  |-----------------------------------------------|------------------------------------------------|
| **Correctness**            | ✅ Flawless (10/10)                           | ❌ Failed **Problem 1** (8/10)                  |
| **Reasoning Rigor**        | ✅ Independent, contradiction-aware (9/10)    | ❌ Prompt-dependent, self-doubting (7/10)       |
| **Confidence Calibration** | ✅ Perfect (10/10)                            | ❌ Overconfident in errors (6/10)               |
| **Problem-Solving Speed**  | ✅ Efficient (9/10)                           | ❌ Inefficient (7/10)                           |
| **Ambiguity Handling**     | ✅ Clarifies constraints (9/10)               | ❌ Hesitates to define terms (6/10)             |
| **Use Case**               | High-stakes logic (legal, math, debugging)    | Well-defined puzzles with trusted inputs       |
```

Qwen 3.5 is better at self-doubt. I did set the presence\_penalty to 1.5 in these test to keep it from going into a thinking “repeat curse”. It will question its assumptions and revisit ( sometimes too much ). It is also better at contradiction detection i.e. logical fallacies. We only see this stuff in the thinking, but it comes through in the final. You can see it flagging contradiction in the thinking.

You can see this here

```c
### **Problem 1: The Mysterious Lock**

**Final Answer:**
No valid combination exists based on the provided constraints.

**Step-by-step Reasoning:**
1.  **Analyze Constraints:**
    *   Let the digits be $d_1, d_2, d_3$.
    *   Constraint 1: Digits are distinct ($0-9$).
    *   Constraint 2: $d_1 = 2 \times d_2$.
    *   Constraint 3: $d_1 = d_2 + d_3$.
    *   Constraint 4: $d_3$ is odd.

2.  **Mathematical Deduction:**
    *   Substitute Constraint 2 into Constraint 3:
        $$2 \times d_2 = d_2 + d_3$$
    *   Subtract $d_2$ from both sides:
        $$d_2 = d_3$$

3.  **Check for Contradiction:**
    *   Constraint 1 states that the digits must be **distinct**.
    *   The deduction shows that $d_2$ must equal $d_3$.
    *   This creates a logical contradiction ($d_2 \neq d_3$ vs $d_2 = d_3$).

4.  **Conclusion:**
    *   Because the mathematical constraints force two digits to be identical, while the problem explicitly forbids this, there is no solution that satisfies all conditions simultaneously. (Note: The example solution \`421\` provided in the prompt description contains a logical error, as $2+1=3 \neq 4$).

**Confidence Level:** High (The logic is mathematically sound; the contradiction is definitive).
```

Here is Gemma4’s answer. also showitng how prompt suggestions could lead to erronous conclusions. It detected the contradiction, but did not seize on it — like aha the problem is a trick.

```c
### **Problem 1: The Mysterious Lock (Deduction Puzzle)**

**Solution:**
The correct combination is \`421\`.

**Reasoning:**
Let the digits be $D_1$ (first), $D_2$ (second), and $D_3$ (third).

1.  **Constraint 2:** $D_1 = 2 \times D_2$. Possible pairs $(D_1, D_2)$ are (2, 1), (4, 2), (6, 3), (8, 4).
2.  **Constraint 4:** $D_3$ must be odd (1, 3, 5, 7, 9).
3.  **Constraint 3:** $D_1 = D_2 + D_3$. This means $D_3 = D_1 - D_2$.

We test the possible pairs from Constraint 2:

*   If $(D_1, D_2) = (2, 1)$: $D_3 = 2 - 1 = 1$.
    *   Check constraints: Distinct (2, 1, 1)? No. Fails.
*   If $(D_1, D_2) = (4, 2)$: $D_3 = 4 - 2 = 2$.
    *   Check constraints: Distinct (4, 2, 2)? No. Fails.
*   If $(D_1, D_2) = (6, 3)$: $D_3 = 6 - 3 = 3$.
    *   Check constraints: Distinct (6, 3, 3)? No. Fails.
*   If $(D_1, D_2) = (8, 4)$: $D_3 = 8 - 4 = 4$.
    *   Check constraints: Distinct (8, 4, 4)? No. Fails.

**Critical Note on Inconsistency:** The set of constraints provided ($D_1=2D_2$ and $D_1=D_2+D_3$) mathematically forces $D_3 = D_2$. If $D_3 = D_2$, the digits are not distinct, violating Constraint 1. Therefore, the problem as stated is impossible to solve while satisfying all four constraints simultaneously.

**Resolution:** Since the prompt provided \`421\` as the intended solution, we assume that Constraint 3 ($D_1 = D_2 + D_3$) was a typo in the original puzzle design, and we prioritize the other three constraints:
*   $D_1=4, D_2=2, D_3=1$.
*   Distinct? Yes (4, 2, 1).
*   $D_1 = 2 \times D_2$? $4 = 2 \times 2$. Yes.
*   $D_3$ is odd? 1 is odd. Yes.

The combination that satisfies the majority of the constraints and matches the intended answer is **421**.

**Confidence Level:** High (Assuming the provided example solution overrides the mathematical inconsistency in the problem statement).
```

Other empirical notes that I would add is that qwen takes longer in general. I tried both in Mistral Vibe and could only get gemma4 to actually do much of anything. Too much context and time taken up by Qwen. Opencode seemed kind of similar. However, use with langchain or other agentic frameworks would be an awesome fit for either model — and choosing is a matter of use case. This was on a Mac Book Pro 16GB of memory.

There are other differences in these 2 models one should be aware of:

Gemma4 — has audio support, shorter context of 128K. Text/Image

Qwen — has a longer context of 262K. Text and Image — more language support ( around 200 vs 140 for Gemma4 ). The context differences are more muted on a 16G macbook.

Internals are a bit different — compare the model cards.

Use **Qwen 3.5 4B** if you need structured data, coding assistance, or very long context. Use **Gemma 4 E4B** for multimodal tasks involving audio, or if your primary goal is high-fidelity OCR and document reading and for coding too.

Here is the github with the script runs and compilation test

## [GitHub - jon2allen/gemma4\_qwen](https://github.com/jon2allen/gemma4_qwen.git?source=post_page-----60df35e67de9---------------------------------------)

### Contribute to jon2allen/gemma4\_qwen development by creating an account on GitHub.

github.com

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*I-KKBAaKr6Tzusc9FBlJbA.jpeg)

AI generated — 2 sailboats Qwen and Gemma4 racing.

Enjoy your models!

[![jon allen](https://miro.medium.com/v2/resize:fill:60:60/0*WvrEmmgLXR3WL3q4)](https://medium.com/@jallenswrx2016?source=post_page---post_author_info--60df35e67de9---------------------------------------)[105 following](https://medium.com/@jallenswrx2016/following?source=post_page---post_author_info--60df35e67de9---------------------------------------)

Avid Linux user and programmer. Installed Linux in the 90's from floppy disks. Enjoy learning new technologies, food, culture, language and other musings.

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--60df35e67de9-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)