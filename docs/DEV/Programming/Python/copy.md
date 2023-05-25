# Python 复制拷贝的六种方法辨析

```py
# 'A and B have the same id' => 'A is in sync with B' / 'A And B Are attached to the same thing'
A = [0, [1, 2]]
B = A
print(id(A) == id(B))  # True
A[0] = -1
print(A, B)  # same
A[1].append(3)
print(A, B)  # same
```

```py
import copy
# 'A and B have different ids' => 'A and B are separate' / 'A and B are attached to two different things'
# But sometimes when you change A, chances are that B also changes
# That's because the two different things that A and B are attaced to
# have something in common, such as ids of elements
A = [0, [1, 2]]
B = A[:]  # slice of a list
# B = list(A)  # instantiation of class list
# B = A.copy()  # copy() method of class list
# B = copy.copy(A)  # copy() method in module copy
print(id(A) == id(B))  # False
A[0] = -1
print(A, B)  # different
A[0] = 0  # restore A
print(id(A[1]) == id(B[1]))  # True
A[1].append(3)
print(A, B)  # same
```

```py
import copy
# This's real deepcopy
A = [0, [1, 2]]
B = copy.deepcopy(A)
print(id(A) == id(B))  # False
A[0] = -1
print(A, B)  # different
A[0] = 0  # restore A
print(id(A[1]) == id(B[1]))  # False
A[1].append(3)
print(A, B)  # different
```