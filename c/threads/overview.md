# Threads and Processes
## Processes
- a **process** is a single cube of execution in the scope of an operating system
- a **process** has independent memory space
- **processes** communicate through inter-process communication mechanisms like pipes, files, and sockets
- **processes** are created using system calls like `fork()` or `exec()`


## Threads
- a **thread** is a lightweight process that has access to the memmory of another process
- **threads** have a shared memory space with their parent process
- **threads** require synchronization mechanisms such as mutexes and semaphores to prevent race conditions

### Using Threads
- use `pthread_create()` to create a **thread**
```c
#include <stdio.h>
#include <pthread.h>

#define THREAD_COUNT 10

void* thread_target(void* arg) {
	printf("I am a thread\n");

	return NULL;
}

int main(int argc, char** argv) {
	pthread_t threads[THREAD_COUNT];

	int i = 0;
	for (i = 0; i < THREAD_COUNT; i++) {
		if (pthread_create(&threads[i], NULL, thread_target, NULL)) {
			return -1;
		}
	}

	return 0;
}
```
- use `pthread_exit()` to terminate the thread
- use `pthread_detach()` to detach a thread from the parent process
    - when a detached thread terminates, its resources are automatically released back to the system without the need for another thread to join
    - is non-blocking
- use `pthread_join()` to join with the terminated thread
    - when a thread joins it writes it's return value to `retval`
    - will block until the thread has finished executing
```c
#include <stdio.h>
#include <pthread.h>

#define THREAD_COUNT 10

void* thread_target(void* arg) {
	printf("I am a thread\n");

	return NULL;
}

int main(int argc, char** argv) {
	pthread_t threads[THREAD_COUNT];

	int i = 0;
	for (i = 0; i < THREAD_COUNT; i++) {
		if (pthread_create(&threads[i], NULL, thread_target, NULL)) {
			return -1;
		}
	}

    for (i = 0; i < THREAD_COUNT; i++) {
        if (pthread_join(threads[i], NULL)) {
            return -1;
        }
    }

	return 0;
}
```
### Passing Arguments to Threads
```c
#include <stdio.h>
#include <pthread.h>

#define THREAD_COUNT 10

typedef struct {
    int arg1;
    short arg2;
} thread_arg_t;

void* thread_target(void* vargs) {
    thread_arg_t* args = (thread_arg_t*)vargs;    
	printf("I am a thread %d\n", args->arg1);

	return NULL;
}

int main(int argc, char** argv) {
	pthread_t threads[THREAD_COUNT];

	int i = 0;
	for (i = 0; i < THREAD_COUNT; i++) {
        thread_arg_t myarg;
        myarg.arg1 = i;

		if (pthread_create(&threads[i], NULL, thread_target, &myarg)) {
			return -1;
		}
	}

    for (i = 0; i < THREAD_COUNT; i++) {
        if (pthread_join(threads[i], NULL)) {
            return -1;
        }
    }

	return 0;
}
```
