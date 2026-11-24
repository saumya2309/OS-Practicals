# OS-Practicals

```

blocks = [100, 500, 200, 300, 600]

processes = [212, 417, 112, 426]

def first_fit():
    memory = blocks.copy()

    print("\nFirst Fit:")

    for p in processes:
        for i in range(len(memory)):
            if memory[i] >= p:
                print(p, "KB allocated to block", i+1)
                memory[i] -= p
                break
        else:
            print(p, "KB not allocated")


def best_fit():
    memory = blocks.copy()

    print("\nBest Fit:")

    for p in processes:
        best = -1

        for i in range(len(memory)):
            if memory[i] >= p:
                if best == -1 or memory[i] < memory[best]:
                    best = i

        if best != -1:
            print(p, "KB allocated to block", best+1)
            memory[best] -= p
        else:
            print(p, "KB not allocated")


def worst_fit():
    memory = blocks.copy()

    print("\nWorst Fit:")

    for p in processes:
        worst = -1

        for i in range(len(memory)):
            if memory[i] >= p:
                if worst == -1 or memory[i] > memory[worst]:
                    worst = i

        if worst != -1:
            print(p, "KB allocated to block", worst+1)
            memory[worst] -= p
        else:
            print(p, "KB not allocated")


first_fit()
best_fit()
worst_fit()
```
