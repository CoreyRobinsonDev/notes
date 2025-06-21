# Thread Local Storage
- use `__thread` to signal that a variable is unique to each thread
```c
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>
#include <stdio.h>

__thread int x_thd; // 0

void wait_for_event() {
    x_thd++; // 1
    printf("%d\n", x_thd);
    return;
}

int main(int argc, char** argv) {
    pthread_t threads[10];

    for (int i = 0; i < 10; i++) {
        pthread_create(&threads[i], NULL, wait_for_event, NULLL);
    }

    for (int i = 0; i < 10; i++) {
        pthread_join(&threads[i], NULL);
    }

    return 0;
}
```
