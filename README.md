# SYSC4001 – Assignment 3 – Part 2  

This README implements a simplified concurrent exam-marking system for Teaching Assistants (TAs).  

## Introduction & Key Assignment 3 - Part 2 Features

- **Part 2.a:** A version with **no synchronization**, demonstrating race conditions.  
- **Part 2.b:** A **synchronized** version using Unix System V **semaphores** and **shared memory**.  
- **Part 2.c:** A short PDF report describing deadlock / livelock behavior.

The system simulates several TAs running as separate processes, all marking a shared set of exam files and using a shared rubric stored in shared memory.


## File List

SYSC4001_A3P2
 ├── part2a_101249786_101307407.c
 ├── part2b_101249786_101307407.c
 ├── reportPartC.pdf
 ├── README.md
 ├── rubric.txt
 ├── exam_0001.txt
 ├── exam_0002.txt
 ├── exam_0003.txt
 ├── exam_0004.txt
 ├── exam_0005.txt
 ├── exam_0006.txt
 ├── exam_0007.txt
 ├── exam_0008.txt
 ├── exam_0009.txt
 ├── exam_0010.txt
 ├── exam_0011.txt
 ├── exam_0012.txt
 ├── exam_0013.txt
 ├── exam_0014.txt
 ├── exam_0015.txt
 ├── exam_0016.txt
 ├── exam_0017.txt
 ├── exam_0018.txt
 ├── exam_0019.txt
 ├── exam_9999.txt

## Compilation Instructions

This project uses a standard GCC compiler on Linux.

### **Compile Part 2.a**

```
gcc part2a_300326924.c -o part2a
```

### **Compile Part 2.b**

```
gcc part2b_300326924.c -o part2b
```

Both programs require:

- System V shared memory  
- System V semaphores (for Part 2.b)

Ensure you compile on a Linux system that supports `<sys/sem.h>`.

---

## Running the Programs

Both programs require **one argument**:  
the number of TA processes (must be ≥ 2).

Example with **3 TA processes**:

### **Run Part 2.a (no semaphores)**

```
./part2a 3
```

### **Run Part 2.b (with semaphores)**

```
./part2b 3
```

---

## Required Input Files

Make sure the following files are in the **same directory** as the compiled programs:

- `rubric.txt`  
- `exam_0001.txt` ... `exam_0019.txt`  
- `exam_9999.txt`  

The program automatically loads all 20 exam files plus the terminating file.

---

## Expected Behavior

### Part 2.a:
- TAs may modify the rubric at the same time.
- TAs may mark the same question.
- TAs may load the same exam concurrently.
- This version demonstrates race conditions.

### Part 2.b:
- Semaphores ensure:
  - Only one TA modifies the rubric at a time.
  - Only one TA loads the next exam.
  - Only one TA selects the next question.
- Execution is synchronized and consistent.

---

## Notes

- `exam_9999.txt` is a special exam that causes all TAs to stop.
- Output may interleave differently depending on OS scheduling.
- The program uses shared memory for the rubric, exam content, and current marking progress.

---

## Cleaning Up

After running Part 2.b, System V shared memory and semaphores are automatically removed using:

```
shmctl(..., IPC_RMID)
semctl(..., IPC_RMID)
```

No manual cleanup is required.


