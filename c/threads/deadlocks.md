# Deadlocks
- **deadlocks** occur in concurrent programming when two or more processes or threads are unable to proceed because each is waiting for the other to release a resource

## Solutions
### Limit the Number of Accesses
- scaling the number of threads to be less than the number of resources to ensure there is always an accessible resource avaiable

### Resoure Hierarchy
- invovles assigning a strict order to the resources and requriing that all processes acquire resources in a specific order
- this prevents circular wait conditions

### Non-blocking Techniques
- involve designing the system so that processes do not wait indefinitely for resources
- if a resource cannot be accessed the process releases any resources aquired and try again later
