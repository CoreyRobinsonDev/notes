# Attributes
- **attributes** start to matter in cases of extreme performance optimization
- doesn't matter for most use cases
- use `pthread_attr_setstacksize()` to set the thread's stack size
- use `pthread_attr_setschedpolicy()` to change how the threads scheduled
- use `sched_param.sched_priority` to set the priority of a specific thread based on a scheduling policy

```c
#define _GNU_SOURCE
#include <pthread.h>
#include <sched.h>

void set_cpu_affinity() {
    pthread_t thread;
    pthread_attr_t attr;
    cpu_set_t cpus;

    pthread_attr_init(&attr);
    CPU_ZERO(&cpus);
    CPU_SET(0, &cpus);  // Set thread to run on CPU 0

    pthread_attr_setaffinity_np(&attr, sizeof(cpu_set_t), &cpus);
    pthread_create(&thread, &attr, thread_function, NULL);
    pthread_join(thread, NULL);
    pthread_attr_destroy(&attr);
}

void* thread_function(void* arg) {
    // Thread tasks here
    return NULL;

```

## Key Attributes and Configurations
### Detach State
- Determines whether a thread is joinable or detached at creation

### Stack Size
- Set the size of the stack used by a thread

### Scheduling Policy
- Defines the scheduling policy (e.g., FIFO, Round Robin) of the thread

## CPU Affinity
- Setting CPU affinity restricts a thread to run a on specific CPUs
- this optimizes performance by reducing cache misses and improving data locality
- compile with `-D_GNU_SOURCE` flag to get access to the *cpu set* macros
- the compiled code will be need to be ran by root

