# Mutexs
- a **mutex** is a mutual exclusion object
- if a resource is locked, other threads requesting access to that resource will sleep until it's unlocked
- use `pthread_mutex_lock()` to lock a resource
- use `pthread_mutex_unlock()` to unlock a resource
```c
int counter = 0;
pthread_mutex_t counter_lock = PTHREAD_MUTEX_INITIALIZER;

void* thread_target(void* vargs) {
    pthread_mutex_lock(&counter_lock);
    for (int i = 0; i < 1000000; i++) {
        counter += 1;
    }
    pthread_mutex_unlock(&counter_lock);

    return NULL;
}
```

# Semaphores
- **semaphores** are a signaling mechanism
```c
#include <semaphore.h>
#include <pthread.h>
#include <stdio.h>

sem_t semaphore;
char message[100];  // Shared resource

// Publisher thread function
void* publisher(void* arg) {
    sprintf(message, "Data published");
    sem_post(&semaphore);  // Signal subscriber
    return NULL;
}

// Subscriber thread function
void* subscriber(void* arg) {
    sem_wait(&semaphore);  // Wait for the signal
    printf("Received message: %s\n", message);
    return NULL;
}

int main() {
    pthread_t pub, sub;
    sem_init(&semaphore, 0, 0);
    pthread_create(&pub, NULL, publisher, NULL);
    pthread_create(&sub, NULL, subscriber, NULL);
    pthread_join(pub, NULL);
    pthread_join(sub, NULL);
    sem_destroy(&semaphore);
    return 0;
}
```

# Spin Locks
- a **spin lock** is like a mutux
- if a resource is locked, other threads requesting access to that resource will wait in an infinity loop until it's unlocked
- its more performant to use a mutex if a thread has to wait for longer than a few milliseconds
