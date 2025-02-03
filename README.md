# 🔷 Advanced Systems Programming: Doubly-Linked Circular List & Transaction Sorting

## 🔶 Overview
This project implements a **doubly-linked circular list** (`MyList`) and a **transaction sorting utility** (`transaction.c`). The doubly-linked circular list serves as a fundamental data structure for handling transactions, which are read from a file or standard input. The project emphasizes **low-level memory management**, **pointer manipulation**, and **efficient sorting algorithms** to ensure correct functionality.

---
## 🔷 Libraries Used:
- **stdio.h** – Standard I/O operations.
- **stdlib.h** – Memory allocation and process control.(malloc, free)
- **string.h** – String manipulation.(strcmp, strcpy)
- **time.h** – Handling UNIX timestamps (ctime, time)
- **ctype.h** – Character handling.
- **unistd.h** – File access control.
- **errno.h** - Error handling

 ---

## 🔷 Data Structure: Doubly-Linked Circular List (`MyList`)

### 🔶 Structure & Characteristics:
The `MyList` is a **circular doubly-linked list** with an **anchor node** that simplifies list operations. Unlike a traditional doubly-linked list, the **anchor node is always present** and is used as a placeholder to manage list boundaries effectively.

### 🔶 Components:
- **Anchor Node (`anchor`)**: 
  - A sentinel node that **does not store user data**.
  - Its `next` pointer points to the **first real element**, and its `prev` pointer points to the **last real element**.
  - This eliminates edge cases when inserting/removing elements.
  
- **List Elements (`MyListElem`)**:
  - Each element stores an **object (`obj`)** representing a transaction.
  - Contains two pointers:
    - `next` → Points to the next element in the list.
    - `prev` → Points to the previous element in the list.
  
- **List Operations**:
  - `MyListInit()` → Initializes an empty list with only the anchor node.
  - `MyListAppend()` → Inserts an element at the end of the list.
  - `MyListPrepend()` → Inserts an element at the beginning of the list.
  - `MyListInsertAfter()` → Inserts an element after a given node.
  - `MyListInsertBefore()` → Inserts an element before a given node.
  - `MyListUnlink()` → Removes a specific element from the list.
  - `MyListUnlinkAll()` → Clears the entire list.
  - `MyListFirst()` → Returns the first element in the list.
  - `MyListLast()` → Returns the last element in the list.
  - `MyListNext()` → Returns the next element in the list.
  - `MyListPrev()` → Returns the previous element in the list.

### 🔶 Benefits of Circular Design:
- **Avoids null pointer checks** at list boundaries.
- **Simplifies iteration** through the list.
- **Efficient insertion/deletion** at both ends without special conditions.

---

## 🔷 Transaction Sorting (`transaction.c`)
This program reads a file containing **financial transactions**, stores them in a `MyList`, and sorts them by date.

### 🔶 Transaction Data Format:
Each transaction is stored as a **line** in the input file and consists of:
[TYPE] [TIMESTAMP] [AMOUNT] [DESCRIPTION]
- `[TYPE]`: `+` for **credit**, `-` for **debit**.
- `[TIMESTAMP]`: Unix timestamp indicating the transaction time.
- `[AMOUNT]`: Decimal value representing the transaction amount.
- `[DESCRIPTION]`: A string describing the transaction.

### 🔶 Parsing and Validation:
- Ensures the **correct number of fields** are present.
- Verifies that the **timestamp is a valid numeric value**.
- Confirms the **amount is non-negative and formatted correctly**.
- **Trims leading/trailing spaces** from the description.

### 🔶 Sorting Algorithm:
- Transactions are stored in a `MyList` and **sorted by timestamp**.
- Uses **Insertion Sort** due to the **small dataset size** (efficient for up to a few thousand elements).
- Maintains **stable sorting** so that transactions with identical timestamps **retain their input order**.

---
## 🔷 Steps Taken to Accomplish the Project

### 🔶 1. Implementing the Doubly-Linked Circular List
- Developed a custom linked list to manage transactions efficiently.
- Implemented O(1) insertion and deletion operations.
- Ensured the list remains circular by updating `next` and `prev` pointers.

### 🔶 2. Parsing and Validating Transaction Data
- Read transaction records from an input file or `stdin`.
- Tokenized each line using **tab-separated fields**.
- Checked the validity of timestamps, amounts, and descriptions:
  - **Timestamps**: Must be **greater than zero** and **less than the current time**.
  - **Amounts**: Must be **formatted correctly** with **two decimal places**.
  - **Descriptions**: Cannot be **empty** after trimming leading spaces.

### 🔶 3. Sorting Transactions by Timestamp
- Implemented **bubble sort** for sorting linked list elements **in-place**.
- Ensured **O(n²) complexity** is reasonable given the constraints.
- Handled **duplicate timestamps** by printing an error and terminating execution.

### 🔶 4. Formatting and Displaying Transactions
- Used **structured formatting** for output:
  - **Date Field**: Converted UNIX timestamps using `ctime()`.
  - **Description Field**: Truncated to **24 characters max**.
  - **Amount Field**: Right-aligned and formatted correctly.
  - **Balance Field**: Updated dynamically while processing transactions.
- Printed the **transaction history** as an **80-character-wide table**.

### 🔶 5. Handling Edge Cases
- **Empty Files**: Checked for empty input and **printed an error**.
- **Malformed Transactions**: Handled incorrect formats gracefully.
- **Extreme Balances**: Ensured balances over **10 million** were marked as `?,???,???.??`.

### 🔶 6. Testing and Debugging
- Used `gdb` to **debug segmentation faults** and **memory allocation errors**.
- Verified correctness using **sample test cases**.
- Ensured **no memory leaks** by freeing allocated structures before exit.

---
  ## 🔷 Rigorous Testing Procedure

To ensure the correctness and robustness of the implementation, the following testing strategies were employed:

### 🔶 1. Unit Testing of Individual Components
- **Doubly-Linked Circular List**: Verified insertion, deletion, and traversal.
- **Sorting Algorithm**: Ensured the transactions are sorted correctly by timestamps.
- **Transaction Parsing**: Checked handling of various formats and erroneous data.

### 🔶 2. Edge Case Handling
- **Empty Input File**: Confirmed that the program properly detects and handles empty files.
- **Malformed Transactions**: Tested various incorrect formats (e.g., missing fields, invalid timestamps, incorrect amounts).
- **Duplicate Timestamps**: Ensured that duplicate timestamps trigger an error message and halt execution.

### 🔶 3. Memory Management Validation
- **Valgrind Analysis**: Used valgrind to detect memory leaks and invalid memory accesses.
- **Pointer Debugging**: Ensured proper freeing of allocated memory to avoid segmentation faults.

### 🔶 4. Stress Testing
- **Large Dataset Processing**: Evaluated performance with a high number of transactions.
- **Extreme Values**: Tested balances exceeding 10 million to check correct formatting (?,???,???.??).
- **High-Frequency Transactions**: Ensured sorting and display work efficiently with closely spaced timestamps.

### 🔶 5. Automated Grading Scripts
- Used a predefined grading script that runs multiple test cases and validates output using `diff`.
- Ensured no unexpected formatting issues arise in the final transaction table.

---
📌 **Note**:
The code for this project cannot be made publicly available due to academic restrictions. However, it can be shared upon request for review or discussion purposes.
