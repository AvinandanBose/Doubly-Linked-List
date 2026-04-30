

# 📘 Doubly Linked List

🔗 Repository: [https://github.com/AvinandanBose/Doubly-Linked-List](https://github.com/AvinandanBose/Doubly-Linked-List)

---

## 📌 Overview

This repository provides a **comprehensive theoretical and practical understanding** of the **Doubly Linked List (DLL)** data structure. It bridges the gap between abstract concepts and real memory-level implementation using C/C++.

A **Doubly Linked List** is a linear data structure where each node contains:

* Data
* A pointer to the **next node**
* A pointer to the **previous node**

👉 This allows **bidirectional traversal**, unlike singly linked lists .

---

## 🧠 Key Concepts Covered

* Structure of Doubly Linked List
* Node creation and initialization
* Use of `typedef` and `struct`
* Global pointer (`head`) handling
* `nullptr` vs `NULL` (C++11 concept)
* Step-by-step algorithmic explanation
* Memory allocation and representation
* Theoretical vs real-world behavior

---

## 🏗️ Structure of Node

```c
typedef struct DLL
{
    int data;
    struct DLL *next;
    struct DLL *prev;
} Node;
```

Each node consists of:

* `data` → stores value
* `next` → pointer to next node
* `prev` → pointer to previous node

---


# Doubly Linked List in C++

Welcome to the Doubly Linked List repository! This project contains a detailed implementation and theoretical analysis of a Doubly Linked List (DLL) in C++. 

## 📖 Introduction
A doubly linked list is a linked list in which a node contains a pointer to the previous as well as the next node in the sequence. Because of this bidirectional capability, it is also called a two-way linked list. 

Each node consists of three parts:
*   **Data**: The integer value stored in the node.
*   **Next Pointer**: A pointer to the next node in the sequence (points to `NULL`/`nullptr` if it is the final node).
*   **Previous Pointer**: A pointer to the previous node in the sequence (points to `NULL`/`nullptr` if it is the first node).

### Advantages
*   Given a node in the list, we can navigate in both directions.
*   Unlike a singly linked list, we can delete a node even if we don't have the previous node's address, since each node has a left pointer pointing backward.

### Disadvantages
*   Each node requires an extra pointer, which takes up more memory space.
*   The insertion or deletion of a node takes a bit longer due to the extra pointer operations required.

## ⚙️ Operations Implemented

This repository breaks down the fundamental operations of a Doubly Linked List. The code leverages C++11's `nullptr` instead of the traditional `NULL` macro to enhance type safety, prevent accidental integer assignments, and improve code clarity.

### 1. Creation of Empty List
*   **Description**: Initializes a global `head` pointer of type `Node*` to track the start of the list. If no variables are passed, the standard guarantees it is zero-initialized to a null pointer (`nullptr`).
*   **Time Complexity**: O(1) (Constant time).
*   **Space Complexity**: O(1) (Auxiliary space is constant as no new nodes are dynamically created).

### 2. Insert At Beginning
*   **Description**: Allocates memory for a new node. If the list is empty, it points both `prev` and `next` to `nullptr` and assigns `head` to this new node. If the list is not empty, it wires the new node to point to the current head, updates the current head's `prev` pointer to the new node, and shifts the `head` pointer to the new node.
*   **Time Complexity**: O(1).
*   **Space Complexity**: O(1) (Only a single new node is allocated in auxiliary space).

### 3. Insert At End
*   **Description**: Creates a new node and sets its `next` pointer to `nullptr`. If the list is empty, it simply becomes the new head. Otherwise, a temporary pointer traverses the list to the final node, and the new node is attached to the end by updating the final node's `next` and the new node's `prev` pointers.
*   **Time Complexity**: 
    *   Best Case (Empty List): O(1).
    *   Worst Case / Average Case: O(n) (Requires traversing the entire list).
*   **Space Complexity**: O(1).

### 4. Insert At Position
*   **Description**: Inserts a node at a specific numerical index. It handles edge cases like invalid positions (pos < 1) and insertion at the very beginning. For other positions, it traverses `pos - 2` times to find the node right before the target spot, creates the new node, and re-wires the four surrounding pointers to securely splice it into the list.
*   **Time Complexity**: 
    *   Best Case (Position 1 or 2): O(1).
    *   Worst Case (Insert at End / Position n+1): O(n).
    *   Average Case: Θ(n).
*   **Space Complexity**: O(1).

### 5. Insert After Element
*   **Description**: Traverses the list searching for the first node containing a target `element` value. If found, it allocates a new node, inserts it immediately after the target node, and re-wires the pointers. If not found, it prints an error message and safely exits.
*   **Time Complexity**: 
    *   Best Case (Element is at the head): Ω(1).
    *   Worst Case (Element is at the end or missing): O(n).
    *   Average Case: Θ(n).
*   **Space Complexity**: O(1).

### 6. Delete From Beginning
*   **Description**: Checks if the list is empty. If not, it saves the current head in a temporary pointer, advances the `head` pointer to the next node, sets the new head's `prev` pointer to `nullptr`, frees the old head from memory, and sets the temporary pointer to `nullptr` to avoid dangling pointers.
*   **Time Complexity**: O(1) across all cases.
*   **Space Complexity**: O(1).

### 7. Delete From End
*   **Description**: Checks for an empty list or a list with only a single node. For lists with multiple nodes, it traverses until the `next` pointer of the temporary node is `nullptr` (the last node). It then detaches the last node by setting the second-to-last node's `next` pointer to `nullptr`, frees the last node's memory, and avoids dangling pointers by assigning `nullptr` to the temporary pointer.
*   **Time Complexity**: 
    *   Best Case (Empty list or single node): Ω(1).
    *   Worst Case / Average Case (Multiple nodes): O(n).
*   **Space Complexity**: O(1).

## 🧠 Memory Management best practices
Throughout the implementations, strict memory management is observed:
*   `malloc()` is used dynamically to reserve memory (typically 20 bytes per node: 4 for integer data, 8 for the `next` pointer, and 8 for the `prev` pointer on 64-bit systems).
*   Allocation success is immediately verified. If memory allocation fails, the programs catch the `nullptr` and throw an allocation error.
*   `free(temp)` is rigorously utilized during deletion operations to prevent memory leaks.
*   Freed pointers are re-assigned to `nullptr` to ensure no **dangling pointers** crash the application.

## ⚙️ Creation of Empty List

```c
Node *head;

void createEmptyList()
{
    head = nullptr;
}
```

📌 Explanation:

* `head` is a **global pointer**
* Initially points to **nullptr**
* Represents an **empty list** 

---

## ⏱️ Time Complexity Analysis

### 🔹 Creation of Empty List

| Operation      | Complexity |
| -------------- | ---------- |
| Declaration    | O(1)       |
| Initialization | O(1)       |
| Function Call  | O(1)       |

👉 Total Time Complexity:

```text
O(1) + O(1) + O(1) + ... = O(1)
```

✔️ **Final:**
➡️ Creation of empty doubly linked list = **O(1)** 

---

## 📦 Space Complexity Analysis

### 🔹 Components:

1. **Node Structure**

   * data → 4 bytes
   * next → 8 bytes
   * prev → 8 bytes

   👉 Constant space per node → **O(1)**

2. **Head Pointer**

   * Stores address of first node
     👉 **O(1)**

3. **Function Call**

   * Constant auxiliary space
     👉 **O(1)**

---

### ✔️ Final Space Complexity:

👉 **O(1) per node**
👉 **O(n) overall for n nodes**

---



## 🧬 Memory Representation (Very Important)

### 🔹 Theoretical Size

```text
data  = 4 bytes
next  = 8 bytes
prev  = 8 bytes
-----------------
Total = 20 bytes
```

---

### 🔹 Real-World Allocation (64-bit System)

Due to **memory alignment and padding**:

* Compiler aligns data to **8-byte boundary**
* Adds **4 bytes padding** after `data`

---

### ✔️ Actual Layout

```text
Offset   Field
-----------------------
0        data (4B)
4        padding (4B)
8        next (8B)
16       prev (8B)
```

👉 **Total = 24 bytes**

---

### 🔹 Visual Representation

```text
Address → 0x800

+---------+---------+---------+---------+
| data    | padding | next    | prev    |
| 4B      | 4B      | 8B      | 8B      |
+---------+---------+---------+---------+

Total = 24 Bytes
```

---

## 🔄 Traversal Capability

| Type               | Direction |
| ------------------ | --------- |
| Singly Linked List | One-way   |
| Doubly Linked List | Two-way   |

👉 Advantage:

* Forward traversal ✔
* Backward traversal ✔

---

## ⚖️ Advantages

* Bidirectional traversal
* Easier deletion (no need for previous node pointer externally) 
* Flexible navigation

---

## ❌ Disadvantages

* Extra memory required (additional `prev` pointer) 
* More pointer manipulation
* Slightly slower operations due to extra updates

---

## 🔍 Key Insight

> Doubly Linked List is not just a data structure—it is a combination of **pointer logic + memory management + alignment behavior**.

---

## 🚀 Learning Outcome

After exploring this repository, you will understand:

* How linked lists work internally
* How memory is actually allocated
* Why padding occurs
* Difference between theoretical and real-world implementation
* How complexity is derived step-by-step

---
## 📜 License

This project is licensed under the **MIT License**.

---

## 👨‍💻 Author

**Avinandan Bose**
- GitHub: [@AvinandanBose](https://github.com/AvinandanBose)

---

## ⭐ Support

If you found this helpful:

* ⭐ Star the repository
* 🍴 Fork it
* 📢 Share with others

---
<br>
<br>
<br>
<h3><a href="https://github.com/AvinandanBose/CPLUSPLUS_DataStructure/blob/main/DoublyLinkedList.cpp">𝑨. 𝑫𝒐𝒖𝒃𝒍𝒚 𝑳𝒊𝒏𝒌𝒆𝒅 𝑳𝒊𝒔𝒕 𝒘𝒊𝒕𝒉 𝑺𝒕𝒓𝒖𝒄𝒕 </a>  𝒊𝒏 <a href="https://github.com/AvinandanBose/CPLUSPLUS_DataStructure/">𝑪++ 𝑫𝒂𝒕𝒂 𝑺𝒕𝒓𝒖𝒄𝒕𝒖𝒓𝒆 𝑹𝒆𝒑𝒐</a></h3>

<h3><a href="https://github.com/AvinandanBose/CPLUSPLUS_DataStructure/blob/main/DoublyLinkedListwithClass.cpp">𝑩. 𝑫𝒐𝒖𝒃𝒍𝒚 𝑳𝒊𝒏𝒌𝒆𝒅 𝑳𝒊𝒔𝒕 𝒘𝒊𝒕𝒉 𝑪𝒍𝒂𝒔𝒔 </a> 𝒊𝒏 <a href="https://github.com/AvinandanBose/CPLUSPLUS_DataStructure/">𝑪++ 𝑫𝒂𝒕𝒂 𝑺𝒕𝒓𝒖𝒄𝒕𝒖𝒓𝒆 𝑹𝒆𝒑𝒐</a></h3>


