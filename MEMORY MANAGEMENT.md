### MEMORY MANAGEMENT:

```c
1. Write a C program to demonstrate dynamic memory allocation using malloc()?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int *arr;
        int n=5,i;
        arr=(int*)malloc(n*sizeof(int));//dynamically allocate memory using malloc()
        if(arr==NULL)
        {
                printf("memory alloction failed!\n");
                return 1;
        }
        printf("enter %d integer :\n",n);
        for(i=0;i<n;i++)
        {
                printf("element %d:",i+1);
                scanf("%d",&arr[i]);
        }
        printf("you entered:\n");
        for(i=0;i<n;i++)
        {
                printf("%d",arr[i]);
        }
                        printf("\n");
        free(arr);//free the allocate memory
        return 0;
}
/**********************************************************************************************************************************************************/
2. Implement a C program to allocate memory for an array dynamically using calloc().
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int *arr;
        int n,i;
        printf("enter the number of elements:");
        scanf("%d",&n);
        arr=(int *)calloc(n,sizeof(int));
        if(arr==NULL)
        {
                printf("memory allocation failed!\n");
                return 1;
        }
        printf("\n");
        printf("enter %d integers:\n",n);
        for(i=0;i<n;i++)
        {
                printf("element %d:",i+1);
                scanf("%d",&arr[i]);
        }
        printf("you entered:\n");
        for(i=0;i<n;i++)
        {
        printf("%d",arr[i]);
        }
        free(arr);
        return 0;
}
/***************************************************************************************************************************/
//3. Write a C program to resize dynamically allocated memory using realloc?
#include<stdio.h>
#include<stdlib.h>
int main()
{
        int *arr;
        int i,n,newsize;
        printf("enter the number of elements:");
        scanf("%d",&n);
        arr=(int*)malloc(n*sizeof(int));
        if(arr==NULL)
        {
                printf("memory allocation failed!\n");
                return 1;
        }
        printf("enter %d integers:\n");
        for(i=0;i<n;i++)
        {
                printf("element %d:",i+1);
                scanf("%d",&arr[i]);
        }
        printf("enter the new size of the array:");
        scanf("%d",&newsize);
        int *temp=(int*)realloc(arr,newsize*sizeof(int));
        if(temp==NULL)
        {
                printf("memory reallocation failed!\n");
                free(arr);
                return 1;
        }
        arr=temp;
        if(newsize>n)
        {
                for(i=n;i<newsize;i++)
                {
                        arr[i]=0;
                }
/*************************************************************************************************************************/
4. Develop a program in C to allocate memory for a linked list node dynamically?
#include <stdio.h>
#include <stdlib.h>
// Define the structure of a linked list node
struct Node {
    int data;
    struct Node* next;
};

int main() {
    // Dynamically allocate memory for a node
    struct Node* head = (struct Node*)malloc(sizeof(struct Node));

    // Check if memory was successfully allocated
    if (head == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    // Assign values to the node
    head->data = 10;
    head->next = NULL;

    // Print the values
    printf("Data = %d\n", head->data);

    // Free the allocated memory
    free(head);

    return 0;
}
                               }
        }
        printf("array after resizing:\n");
        for(i=0;i<newsize;i++)
        {
                printf("%d",arr[i]);
        }
        printf("\n");
        free(arr);
        return 0;
}

/************************************************************************************************************************/
5. Implement a C program to simulate memory allocation using the first-fit algorithm.
#include <stdio.h>

#define MAX_BLOCKS 10
#define MAX_PROCESSES 10

void firstFit(int blockSize[], int m, int processSize[], int n) {
    int allocation[MAX_PROCESSES];

    // Initialize all allocations to -1 (not allocated)
    for (int i = 0; i < n; i++)
        allocation[i] = -1;

    // Pick each process and find the first block that fits
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (blockSize[j] >= processSize[i]) {
                // Allocate block j to process i
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                break;
            }
        }
    }

    // Display the allocation result
    printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < n; i++) {
        printf("  %d\t\t%d\t\t", i + 1, processSize[i]);
        if (allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);
        else
            printf("Not Allocated\n");
    }
}

int main() {
    // Example input
    int blockSize[MAX_BLOCKS] = {100, 500, 200, 300, 600};
    int processSize[MAX_PROCESSES] = {212, 417, 112, 426};
    int m = 5; // Number of memory blocks
    int n = 4; // Number of processes

    firstFit(blockSize, m, processSize, n);

    return 0;
}
/*******************************************************************************************************************************************/
6. Write a C program to simulate memory allocation using the best-fit algorithm.
#include <stdio.h>

#define MAX_BLOCKS 10
#define MAX_PROCESSES 10

void bestfit(int blocksize[], int m, int processsize[], int n) {
    int allocation[MAX_PROCESSES];

    // Initialize all allocations to -1
    for (int i = 0; i < n; i++) {
        allocation[i] = -1;
    }

    // Best-Fit algorithm
    for (int i = 0; i < n; i++) {
        int bestindex = -1;
        for (int j = 0; j < m; j++) {
            if (blocksize[j] >= processsize[i]) {
                if (bestindex == -1 || blocksize[j] < blocksize[bestindex]) {
                    bestindex = j;
                }
            }
        }

        if (bestindex != -1) {
            allocation[i] = bestindex;
            blocksize[bestindex] -= processsize[i];
        }
    }

    // Print allocation result
    printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < n; i++) {
        printf("%d\t\t%d\t\t", i + 1, processsize[i]);

        if (allocation[i] != -1)
            printf("%d\n", allocation[i] + 1);
        else
            printf("Not Allocated\n");
    }
}

int main() {
    int blocksize[MAX_BLOCKS] = {100, 500, 200, 300, 600};
    int processsize[MAX_PROCESSES] = {212, 417, 112, 426};
    int m = 5;
    int n = 4;

    bestfit(blocksize, m, processsize, n);

    return 0;
}
/***************************************************************************************************************************/
7. Implement a C program to simulate memory allocation using the next-fit algorithm
#include <stdio.h>

#define MAX_BLOCKS 10
#define MAX_PROCESSES 10

void nextFit(int blockSize[], int m, int processSize[], int n) {
    int allocation[MAX_PROCESSES];
    int lastAllocatedIndex = 0;
  for (int i = 0; i < n; i++) {
        allocation[i] = -1;
    }
    for (int i = 0; i < n; i++) {
        int j = lastAllocatedIndex;
        int count = 0;

        while (count < m) {
            if (blockSize[j] >= processSize[i]) {
                // Allocate block j to process i
                allocation[i] = j;
                blockSize[j] -= processSize[i];
                lastAllocatedIndex = j;
                break;
            }

            j = (j + 1) % m;
            count++;
        }
    }
 printf("\nProcess No.\tProcess Size\tBlock No.\n");
    for (int i = 0; i < n; i++) {
        printf("%d\t\t%d\t\t", i + 1, processSize[i]);
        if (allocation[i] != -1)
            printf("%d\n", allocation[i] + 1); // Display block number as 1-based
        else
            printf("Not Allocated\n");
    }
}

int main() {
    int blockSize[MAX_BLOCKS] = {100, 500, 200, 300, 600};
    int processSize[MAX_PROCESSES] = {212, 417, 112, 426};
    int m = 5; // Number of memory blocks
    int n = 4; // Number of processes

    nextFit(blockSize, m, processSize, n);

    return 0;
}
/**********************************************************************************************************************************/
8. Write a C program to implement a simple memory allocator using the buddy system.
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>

#define MAX 1024  // Total memory size
#define MIN_BLOCK_SIZE 16  // Smallest allocatable block (must be power of 2)

int memory[MAX];  // Simulated memory

typedef struct Block {
    int size;
    int start;
    int is_free;
    struct Block* next;
} Block;

Block* free_list = NULL;

// Helper function to create a new block
Block* create_block(int start, int size) {
    Block* b = (Block*)malloc(sizeof(Block));
    b->start = start;
    b->size = size;
    b->is_free = 1;
    b->next = NULL;
    return b;
}

// Initialize memory with one big free block
void initialize_memory() {
    free_list = create_block(0, MAX);
}

// Round up to next power of two ≥ n
int next_power_of_two(int n) {
    int p = MIN_BLOCK_SIZE;
    while (p < n) p <<= 1;
    return p;
}

// Split a block until it matches required size
Block* split_block(Block* b, int required_size) {
    while (b->size > required_size) {
        int half_size = b->size / 2;
        Block* buddy = create_block(b->start + half_size, half_size);
        buddy->next = b->next;
        b->next = buddy;
        b->size = half_size;
    }
    return b;
}

// Allocate memory using buddy system
int allocate(int size) {
    int required_size = next_power_of_two(size);
    Block* prev = NULL;
    Block* curr = free_list;

    while (curr != NULL) {
        if (curr->is_free && curr->size >= required_size) {
            curr = split_block(curr, required_size);
            curr->is_free = 0;
            printf("Allocated %d bytes at address %d\n", required_size, curr->start);
            return curr->start;
        }
        prev = curr;
        curr = curr->next;
    }

    printf("Allocation failed: Not enough memory.\n");
    return -1;
}

// Merge buddies (simplified version: merge only consecutive free blocks of same size)
void merge_blocks() {
    Block* curr = free_list;
    while (curr && curr->next) {
        if (curr->is_free && curr->next->is_free && curr->size == curr->next->size &&
            curr->start + curr->size == curr->next->start) {
            curr->size *= 2;
            Block* temp = curr->next;
            curr->next = curr->next->next;
            free(temp);
        } else {
            curr = curr->next;
        }
    }
}

// Free memory
void free_block(int address) {
    Block* curr = free_list;
    while (curr) {
        if (curr->start == address) {
            curr->is_free = 1;
            printf("Freed memory at address %d\n", address);
            merge_blocks();  // Try merging after free
            return;
        }
        curr = curr->next;
    }
    printf("Invalid free request at address %d\n", address);
}

// Display memory blocks
void display_memory() {
    Block* curr = free_list;
    printf("\nMemory Blocks:\n");
    printf("Start\tSize\tStatus\n");
    while (curr) {
        printf("%d\t%d\t%s\n", curr->start, curr->size, curr->is_free ? "Free" : "Allocated");
        curr = curr->next;
    }
    printf("\n");
}

int main() {
    initialize_memory();

    int a = allocate(100);
    int b = allocate(50);
    int c = allocate(200);

    display_memory();

    free_block(b);
    free_block(a);

    display_memory();

    int d = allocate(120);
    display_memory();

    return 0;
}
/**********************************************************************************************************************/
9. Develop a C program to implement a memory allocator using a custom memory
management algorithm
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#include <string.h>

#define HEAP_SIZE 1024  // Total heap size in bytes
#define ALIGN4(size) (((size) + 3) & ~3)  // Align to 4 bytes

typedef struct Block {
    size_t size;
    int free;
    struct Block* next;
} Block;

#define BLOCK_SIZE sizeof(Block)

static uint8_t heap[HEAP_SIZE];  // Simulated memory
static Block* free_list = NULL;

// Initialize memory with a single large block
void init_memory() {
    free_list = (Block*)heap;
    free_list->size = HEAP_SIZE - BLOCK_SIZE;
    free_list->free = 1;
    free_list->next = NULL;
}

// Split block if too big
void split_block(Block* block, size_t size) {
    Block* new_block = (Block*)((uint8_t*)block + BLOCK_SIZE + size);
    new_block->size = block->size - size - BLOCK_SIZE;
    new_block->free = 1;
    new_block->next = block->next;

    block->size = size;
    block->next = new_block;
}

// Custom malloc function
void* allocate(size_t size) {
    size = ALIGN4(size);

    Block* curr = free_list;
    while (curr) {
        if (curr->free && curr->size >= size) {
            if (curr->size >= size + BLOCK_SIZE + 4) {
                split_block(curr, size);
            }
            curr->free = 0;
            return (void*)((uint8_t*)curr + BLOCK_SIZE);
        }
        curr = curr->next;
    }

    printf("Allocation failed: Not enough memory.\n");
    return NULL;
}

// Custom free function
void free_block(void* ptr) {
    if (!ptr) return;

    Block* block = (Block*)((uint8_t*)ptr - BLOCK_SIZE);
    block->free = 1;

    // Coalesce with next block if it's free
    if (block->next && block->next->free) {
        block->size += BLOCK_SIZE + block->next->size;
        block->next = block->next->next;
    }
}

// Display current memory state
void display_memory() {
    Block* curr = (Block*)heap;
    printf("\nMemory Blocks:\n");
    printf("Address\t\tSize\tStatus\n");
    while ((uint8_t*)curr < heap + HEAP_SIZE) {
        printf("%p\t%zu\t%s\n", (void*)curr, curr->size, curr->free ? "Free" : "Used");
        if (!curr->next) break;
        curr = curr->next;
    }
    printf("\n");
}


int main() {
    init_memory();

    void* p1 = allocate(100);
    void* p2 = allocate(200);
    display_memory();

    free_block(p1);
    display_memory();

    void* p3 = allocate(50);
    display_memory();

    return 0;
}
/********************************************************************************************************************************/
10. Write a C program to demonstrate memory mapping using mmap().
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <unistd.h>
#include <string.h>

#define FILEPATH "mapped_file.txt"
#define SIZE 4096  // 4KB

int main() {
    int fd;
    char *map;

    // 1. Create or open the file
    fd = open(FILEPATH, O_RDWR | O_CREAT, 0666);
    if (fd == -1) {
        perror("Error opening file");
        exit(EXIT_FAILURE);
    }

    // 2. Stretch the file size
    if (lseek(fd, SIZE - 1, SEEK_SET) == -1) {
        perror("Error calling lseek()");
        close(fd);
        exit(EXIT_FAILURE);
    }

    // Write a dummy byte to set the size
    if (write(fd, "", 1) != 1) {
        perror("Error writing to file");
        close(fd);
        exit(EXIT_FAILURE);
    }

    // 3. Memory map the file
    map = mmap(NULL, SIZE, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (map == MAP_FAILED) {
        perror("Error mmapping the file");
        close(fd);
        exit(EXIT_FAILURE);
    }

    // 4. Write to the mapped memory
    const char *message = "Hello from mmap!";
    memcpy(map, message, strlen(message));

    printf("Message written to memory-mapped file: %s\n", message);

    // 5. Read from the mapped memory
    printf("Reading from mapped memory: %s\n", map);

    // 6. Unmap and close
    if (munmap(map, SIZE) == -1) {
        perror("Error unmapping the file");
    }

    close(fd);
    return 0;
}
/*****************************************************************************************************************/
11. Implement a C program to read from and write to a memory-mapped file.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <unistd.h>
#define FILE_PATH "mapped_file.txt"
#define FILE_SIZE 1024  // 1 KB

int main() {
    int fd;
    char *map;
    fd = open(FILE_PATH, O_RDWR | O_CREAT, 0666);
    if (fd == -1) {
        perror("Error opening file");
        return 1;
    }
    if (ftruncate(fd, FILE_SIZE) == -1) {
        perror("Error setting file size");
        close(fd);
        return 1;
    }
    map = mmap(0, FILE_SIZE, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (map == MAP_FAILED) {
        perror("Error mapping file");
        close(fd);
        return 1;
    }
    const char *text = "Hello, this is a memory-mapped file!\n";
    memcpy(map, text, strlen(text));
    printf("Read from file: %s", map);
    if (msync(map, FILE_SIZE, MS_SYNC) == -1) {
        perror("Could not sync the file to disk");
    }

    if (munmap(map, FILE_SIZE) == -1) {
        perror("Error un-mmapping the file");
    }

    close(fd);
    return 0;
}
/**********************************************************************************************************************/
12. Develop a C program to demonstrate shared memory usage using shmget() and shmat().
 Explanation:
    shmget() creates or accesses a shared memory segment.
    shmat() attaches it to the process address space.
    shmdt() detaches the shared memory.
    shmctl(..., IPC_RMID, ...) marks the segment for deletion.
    The child waits for 1 second (sleep(1)) to ensure the parent writes first.
#include <stdio.h>
#include <stdlib.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <unistd.h>
#include <string.h>

#define SHM_SIZE 1024  // Shared memory size in bytes
#define SHM_KEY 0x1234 // Unique shared memory key

int main() {
    int shmid;
    char *shm_ptr;
shmid = shmget(SHM_KEY, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid == -1) {
        perror("shmget failed");
        exit(1);
    }
pid_t pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    }

    else if (pid == 0) {
        sleep(1); // Ensure parent writes first
        shm_ptr = (char *) shmat(shmid, NULL, 0);
        if (shm_ptr == (char *)(-1)) {
            perror("shmat failed in child");
            exit(1);
        }
      printf("Child read from shared memory: %s\n", shm_ptr);
      shmdt(shm_ptr);
    }

    else {
        shm_ptr = (char *) shmat(shmid, NULL, 0);
        if (shm_ptr == (char *)(-1)) {
            perror("shmat failed in parent");
            exit(1);
        }
        const char *message = "Hello from parent via shared memory!";
        strncpy(shm_ptr, message, SHM_SIZE);
        wait(NULL);
        shmdt(shm_ptr);
        shmctl(shmid, IPC_RMID, NULL);
    }
    return 0;
}
/*****************************************************************************************************************************/
13. Write a C program to create a shared memory segment and synchronize access using
semaphores
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/sem.h>
#include <sys/wait.h>

#define SHM_KEY 0x1234
#define SEM_KEY 0x5678
#define SHM_SIZE 1024

// Semaphore union needed for semctl
union semun {
    int val;
    struct semid_ds *buf;
    unsigned short *array;
};

// Semaphore wait (P operation)
void sem_wait(int semid) {
    struct sembuf sb = {0, -1, 0};  // Decrease semaphore by 1
    semop(semid, &sb, 1);
}

// Semaphore signal (V operation)
void sem_signal(int semid) {
    struct sembuf sb = {0, 1, 0};   // Increase semaphore by 1
    semop(semid, &sb, 1);
}

int main() {
    int shmid, semid;
    char *shm_ptr;

    // Step 1: Create shared memory
    shmid = shmget(SHM_KEY, SHM_SIZE, IPC_CREAT | 0666);
    if (shmid == -1) {
        perror("shmget failed");
        exit(1);
    }

    // Step 2: Create semaphore
    semid = semget(SEM_KEY, 1, IPC_CREAT | 0666);
    if (semid == -1) {
        perror("semget failed");
        exit(1);
    }

    // Step 3: Initialize semaphore to 1
    union semun sem_union;
    sem_union.val = 1;
    semctl(semid, 0, SETVAL, sem_union);

    // Step 4: Fork process
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    }

    else if (pid == 0) {
        // Child process: read from shared memory
        sleep(1);  // Wait to ensure parent writes first

        shm_ptr = (char *)shmat(shmid, NULL, 0);
        if (shm_ptr == (char *)(-1)) {
            perror("shmat failed in child");
            exit(1);
        }

        sem_wait(semid);
        printf("Child reads from shared memory: %s\n", shm_ptr);
        sem_signal(semid);

        shmdt(shm_ptr);
    }

    else {
        // Parent process: write to shared memory
        shm_ptr = (char *)shmat(shmid, NULL, 0);
        if (shm_ptr == (char *)(-1)) {
            perror("shmat failed in parent");
            exit(1);
        }
        sem_wait(semid);
        const char *msg = "Hello from parent with semaphore!";
        strncpy(shm_ptr, msg, SHM_SIZE);
        sem_signal(semid);
        wait(NULL); // Wait for child
        // Cleanup
        shmdt(shm_ptr);
        shmctl(shmid, IPC_RMID, NULL);
        semctl(semid, 0, IPC_RMID);
    }

    return 0;
}
/***********************************************************************************************************************************/
14.Implement a C program to simulate page replacement algorithms like FIFO, LRU, and
optimal.
#include <stdio.h>
#include <stdlib.h>

#define MAX_FRAMES 10
#define MAX_PAGES 100

int isPageInFrame(int frames[], int frame_count, int page) {
    for (int i = 0; i < frame_count; i++) {
        if (frames[i] == page)
            return 1;
    }
    return 0;
}

// FIFO algorithm
int fifo(int pages[], int n, int frame_count) {
    int frames[MAX_FRAMES];
    int front = 0, page_faults = 0;

    for (int i = 0; i < frame_count; i++)
        frames[i] = -1;

    for (int i = 0; i < n; i++) {
        if (!isPageInFrame(frames, frame_count, pages[i])) {
            frames[front] = pages[i];
            front = (front + 1) % frame_count;
            page_faults++;
        }
    }
    return page_faults;
}

// LRU algorithm
int lru(int pages[], int n, int frame_count) {
    int frames[MAX_FRAMES], time[MAX_FRAMES];
    int page_faults = 0, t = 0;

    for (int i = 0; i < frame_count; i++) {
        frames[i] = -1;
        time[i] = 0;
    }

    for (int i = 0; i < n; i++) {
        int found = 0;
        for (int j = 0; j < frame_count; j++) {
            if (frames[j] == pages[i]) {
                time[j] = t++;
                found = 1;
                break;
            }
        }
        if (!found) {
            int lru_index = 0;
            for (int j = 1; j < frame_count; j++) {
                if (time[j] < time[lru_index])
                    lru_index = j;
            }
            frames[lru_index] = pages[i];
            time[lru_index] = t++;
            page_faults++;
        }
    }
    return page_faults;
}

// Optimal algorithm
int optimal(int pages[], int n, int frame_count) {
    int frames[MAX_FRAMES];
    int page_faults = 0;

    for (int i = 0; i < frame_count; i++)
        frames[i] = -1;

    for (int i = 0; i < n; i++) {
        if (!isPageInFrame(frames, frame_count, pages[i])) {
            int replace_index = -1, farthest = i + 1;

            for (int j = 0; j < frame_count; j++) {
                int k;
                for (k = i + 1; k < n; k++) {
                    if (frames[j] == pages[k])
                        break;
                }

                if (k == n) {
                    replace_index = j;
                    break;
                }

                if (k > farthest) {
                    farthest = k;
                    replace_index = j;
                }

                if (replace_index == -1)
                    replace_index = 0;
            }

            frames[replace_index] = pages[i];
            page_faults++;
        }
    }
    return page_faults;
}

int main() {
    int pages[MAX_PAGES], n, frame_count;

    printf("Enter number of pages: ");
    scanf("%d", &n);

    printf("Enter page reference string: ");
    for (int i = 0; i < n; i++)
        scanf("%d", &pages[i]);

    printf("Enter number of frames: ");
    scanf("%d", &frame_count);

    printf("\nPage Faults:\n");
    printf("FIFO: %d\n", fifo(pages, n, frame_count));
    printf("LRU : %d\n", lru(pages, n, frame_count));
    printf("Optimal: %d\n", optimal(pages, n, frame_count));

    return 0;
}
/**********************************************************************************************************************************/

```

