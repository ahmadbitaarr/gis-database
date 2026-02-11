🗺 GIS Database – KD-Tree + BST Multi-Index System

⚠️ The full source code is private due to course policy.
Access is available upon request for recruiters and interviewers.
⚡ Fully handwritten with 90%+ mutation-tested validation.

One-Line Summary

A fully handwritten Geographic Information System (GIS) database in Java that combines a 2D KD-Tree for spatial indexing and a Binary Search Tree for name-based indexing, with synchronized multi-index mutations and extensive structural testing.

Highlights

Custom 2D KD-Tree with correct deletion via subtree minimum replacement

Name-indexed BST supporting duplicate keys and object-specific removal

Strict synchronization between spatial and name indices

Circular range search with pruning using splitting plane logic

Distance-squared comparisons (no floating-point error)

90%+ mutation testing coverage with ~2000 lines of structured tests

Tech Stack

Language: Java

Data Structures: Custom KD-Tree + Custom BST

Testing: Extensive unit testing with mutation coverage

No external data structure libraries

Getting Started
Compile
javac *.java

Run
java GISDB

Example Usage
insert("Blacksburg", 120, 450);
insert("Roanoke", 300, 800);

info(120, 450);
search(200, 500, 250);
delete("Blacksburg");
print();


All operations maintain consistency between both indexing structures.

Problem & Motivation

Each city contains:

name (String)

x coordinate (int)

y coordinate (int)

To support efficient queries, the system maintains two independent indices:

KD-Tree → Spatial queries

BST → Alphabetical name queries

The challenge is not just implementing each structure individually, but ensuring they remain fully synchronized across insertions and deletions.

The goal of this project was to design a multi-index system from scratch, preserving structural correctness and algorithmic efficiency.

Architecture
1️⃣ KD-Tree (2D Spatial Index)

Used for:

Insertion by (x, y)

Deletion by coordinates

Exact coordinate lookup

Circular range search

Key Properties:

Alternating discriminator (x → y → x → …)

Duplicate coordinates rejected

Correct KD-Tree deletion using subtree minimum replacement

Range search pruning using splitting plane logic

Distance-squared comparisons to avoid floating-point error

Node visit tracking for performance insight

2️⃣ Binary Search Tree (Name Index)

Used for:

Listing cities alphabetically

Retrieving all cities with a given name

Deleting all cities with a given name

Key Properties:

Generic BST implementation

Duplicate names supported (inserted consistently into left subtree)

Object-specific removal

Preorder retrieval for batch deletions

Depth-indented debug printing

3️⃣ GIS Database Layer

GISDB integrates both trees and ensures:

Coordinate bounds validation

Insertion into KD-Tree first (enforces coordinate uniqueness)

Consistent propagation of deletions across both indices

Structural integrity after every mutation

Supported Operations
Operation	Description
insert(name, x, y)	Insert a city (unique coordinates required)
delete(x, y)	Delete city at coordinates
delete(name)	Delete all cities with given name
info(x, y)	Retrieve city name at coordinates
info(name)	Retrieve all coordinates for a name
search(x, y, radius)	Circular range search
debug()	Depth-indented KD-Tree traversal
print()	Alphabetical BST traversal
Algorithmic Complexity

Let n = number of cities.

KD-Tree

Average insert/search/delete: O(log n)

Worst-case: O(n)

Range search: sublinear in practice due to pruning

BST

Average insert/search/delete: O(log n)

Worst-case: O(n)

Range queries benefit significantly from spatial pruning.

Testing

The project includes ~2000 lines of structured testing with 90%+ mutation coverage.

Tests validate:

Edge cases

Duplicate handling

Deletion invariants

Subtree restructuring correctness

Range search pruning logic

Node visit tracking

Empty structure behavior

Boundary validation

Testing verifies both functional correctness and structural integrity after mutations.

Design Decisions

City.compareTo() compares by name only

City.equals() requires name + coordinates

Duplicate names allowed

Duplicate coordinates disallowed

Strict synchronization across both indices

No floating-point arithmetic for distance comparisons

Challenges & Lessons Learned

Implementing correct KD-Tree deletion (subtree minimum replacement is non-trivial)

Maintaining multi-index consistency during cascading deletions

Designing pruning logic that avoids unnecessary subtree traversal

Writing tests that validate structural invariants, not just outputs

This project significantly deepened my understanding of spatial indexing, tree invariants, and multi-structure synchronization.

Future Improvements

Self-balancing BST variant

KD-Tree rebalancing strategy

Persistent storage layer

Performance benchmarking on large datasets

Visualization of tree structures
