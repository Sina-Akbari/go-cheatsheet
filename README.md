# Go Data Structures Cheatsheet (For LeetCode Interviews)

## Slices (Dynamic Arrays)

- Create: `s := []int{}`
- Append: `s = append(s, val)`
- Remove at index i: `s = append(s[:i], s[i+1:]...)`
- Copy: `copy(dst, src)`
- Length: `len(s)`, Capacity: `cap(s)`

---

## Maps (Hash Tables)

```go
m := make(map[int]int)
m[key] = val
val, ok := m[key]
delete(m, key)

for k, v := range m {
    // iterate
}
```

---

## Stack (using slice)

```go
type Stack []int

func (s *Stack) Push(v int) {
    *s = append(*s, v)
}

func (s *Stack) Pop() int {
    n := len(*s)
    val := (*s)[n-1]
    *s = (*s)[:n-1]
    return val
}
```

---

## Queue (using slice)

```go
type Queue []int

func (q *Queue) Enqueue(v int) {
    *q = append(*q, v)
}

func (q *Queue) Dequeue() int {
    val := (*q)[0]
    *q = (*q)[1:]
    return val
}
```

---

## Queue (efficient - container/list)

```go
import "container/list"

q := list.New()
q.PushBack(val) // enqueue

e := q.Front()
val := e.Value
q.Remove(e) // dequeue
```

---

## Set (using map)

```go
set := make(map[int]struct{})
set[val] = struct{}{}
_, exists := set[val]
delete(set, val)
```

---

## Heap / Priority Queue

```go
import "container/heap"

type IntHeap []int

func (h IntHeap) Len() int            { return len(h) }
func (h IntHeap) Less(i, j int) bool  { return h[i] < h[j] } // min-heap
func (h IntHeap) Swap(i, j int)       { h[i], h[j] = h[j], h[i] }

func (h *IntHeap) Push(x interface{}) {
    *h = append(*h, x.(int))
}

func (h *IntHeap) Pop() interface{} {
    old := *h
    n := len(old)
    val := old[n-1]
    *h = old[0 : n-1]
    return val
}
```

Usage:

```go
h := &IntHeap{}
heap.Init(h)
heap.Push(h, 3)
heap.Push(h, 1)
x := heap.Pop(h).(int) // returns 1 for min-heap
```

---

## Notes

- Go slices are reference types.
- `append` creates a new slice if capacity is exceeded.
- Use `heap` and `list` from standard lib for efficient PQs and linked lists.
