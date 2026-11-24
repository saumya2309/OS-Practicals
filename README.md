# OS-Practicals
12. best fit , worst fit
```


blocks = [100, 500, 200, 300, 600]
processes = [212, 417, 112, 426]

def allocate(method):
    memory = blocks.copy()
    print("\n", method)

    for p in processes:
        allocated = False

        if method == "First Fit":
            indexes = range(len(memory))
        elif method == "Best Fit":
            indexes = sorted(range(len(memory)), key=lambda i: memory[i])
        else:
            indexes = sorted(range(len(memory)), key=lambda i: memory[i], reverse=True)

        for i in indexes:
            if memory[i] >= p:
                print(p, "KB allocated in block", memory[i], "KB")
                memory[i] -= p
                allocated = True
                break

        if not allocated:
            print(p, "KB not allocated")

allocate("First Fit")
allocate("Best Fit")
allocate("Worst Fit")

```

11. sum of N numbers
```

import threading

def calculate_sum():
    global total

    total = sum(numbers)

n = int(input("Enter number of elements: "))

numbers = []

for i in range(n):
    num = int(input("Enter number: "))
    numbers.append(num)

total = 0

# Create thread
t = threading.Thread(target=calculate_sum)

# Start thread
t.start()

# Wait for thread to finish
t.join()

print("Sum of numbers:", total)
print("Thread execution completed")


```
10. non-preemptive scheduling
```

n = int(input("Enter number of processes: "))

bt = []
priority = []

for i in range(n):
    b = int(input("Enter burst time: "))
    p = int(input("Enter priority: "))

    bt.append(b)
    priority.append(p)

# Sort according to priority
processes = sorted(range(n), key=lambda i: priority[i])

wt = [0] * n
tat = [0] * n

# Calculate waiting time
for i in range(1, n):
    current = processes[i]
    previous = processes[i-1]

    wt[current] = wt[previous] + bt[previous]

# Calculate turnaround time
for i in range(n):
    tat[i] = wt[i] + bt[i]

print("\nProcess\tBT\tPriority\tWT\tTAT")

for p in processes:
    print("P", p+1, "\t", bt[p], "\t",
          priority[p], "\t\t", wt[p], "\t", tat[p])

print("Average Waiting Time:", sum(wt)/n)
print("Average Turnaround Time:", sum(tat)/n)

```
9. SJF

```

n = int(input("Enter number of processes: "))

bt = []

for i in range(n):
    b = int(input("Enter burst time: "))
    bt.append(b)

# Sort processes according to burst time
processes = sorted(range(n), key=lambda i: bt[i])

wt = [0] * n
tat = [0] * n

# Calculate waiting time
for i in range(1, n):
    p = processes[i]
    prev = processes[i-1]
    wt[p] = wt[prev] + bt[prev]

# Calculate turnaround time
for i in range(n):
    tat[i] = wt[i] + bt[i]

print("\nProcess\tBT\tWT\tTAT")

for p in processes:
    print("P", p+1, "\t", bt[p], "\t", wt[p], "\t", tat[p])

print("Average Waiting Time:", sum(wt)/n)
print("Average Turnaround Time:", sum(tat)/n)
```

8. FCFS
```

n = int(input("Enter number of processes: "))

bt = []
wt = [0] * n
tat = [0] * n

for i in range(n):
    b = int(input("Enter burst time: "))
    bt.append(b)

# Calculate waiting time
for i in range(1, n):
    wt[i] = wt[i-1] + bt[i-1]

# Calculate turnaround time
for i in range(n):
    tat[i] = wt[i] + bt[i]

print("\nProcess\tBT\tWT\tTAT")

for i in range(n):
    print("P", i+1, "\t", bt[i], "\t", wt[i], "\t", tat[i])

print("Average Waiting Time:", sum(wt)/n)
print("Average Turnaround Time:", sum(tat)/n)

```
7. copy files using system call

```

import os

source = input("Enter source file name: ")
destination = input("Enter destination file name: ")

# Open source file
fd1 = os.open(source, os.O_RDONLY)

# Create destination file
fd2 = os.open(destination, os.O_WRONLY | os.O_CREAT | os.O_TRUNC, 0o644)

# Copy file contents
while True:
    data = os.read(fd1, 1024)

    if not data:
        break

    os.write(fd2, data)

# Close files
os.close(fd1)
os.close(fd2)

print("File copied successfully!")
```

6. configures memory
```

print("Memory Information")

memory = {}

# Read memory information
with open("/proc/meminfo", "r") as file:
    for line in file:
        key, value = line.split(":")
        memory[key] = int(value.strip().split()[0])

total = memory["MemTotal"]
free = memory["MemFree"]
available = memory["MemAvailable"]
used = total - available

print("Total Memory:", total, "KB")
print("Free Memory:", free, "KB")
print("Available Memory:", available, "KB")
print("Used Memory:", used, "KB")
```

5. Linux kernel info

```

import platform

print("Linux Kernel Information")

# Kernel information
print("Kernel Name:", platform.system())
print("Kernel Version:", platform.release())
print("Kernel Details:", platform.version())

# CPU information
print("CPU Architecture:", platform.machine())
print("Processor:", platform.processor())

# Read detailed CPU information
with open("/proc/cpuinfo", "r") as file:
    print("\nCPU Information:")
    print(file.read())
```

4. Write programs using fork() and/or exec() commands where parent and child execute different tasks.
i. Same program, same code
```

import os

pid = os.fork()

print("Hello from process")
print("Process ID:", os.getpid())
print("Parent Process ID:", os.getppid())
```
ii. Same program, different code
```

import os

pid = os.fork()

if pid == 0:
    print("I am Child Process")
    print("Child Process ID:", os.getpid())

else:
    print("I am Parent Process")
    print("Parent Process ID:", os.getpid())
    print("Child Process ID:", pid)
```

iii.Parent waits for child to finish its task
```

import os

pid = os.fork()

if pid == 0:
    print("Child Process Started")
    print("Child Process ID:", os.getpid())

    print("Child Process Working...")
    print("Child Process Finished")

else:
    print("Parent Process Started")

    os.wait()

    print("Child Process Completed")
    print("Parent Process Finished")
```
3. To execute Linux commands related to process control, communication and protection management.
```

echo $$
ps
sleep 5
ps
```
to demonstrate kill
```

sleep 100 &
ps
kill $!
```
B. input/output direction

```

echo "Hello this is my operating system practical" > file.txt

wc -w < file.txt
date > output.txt
