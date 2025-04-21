### What is garbage collection?

useless, occupying valuable space in memory, memory management

The problem with this is that manually freeing objects could be an extremely hard and error-prone process. Failure in terminating obsolete objects often resulted in memory leaks. Terminating non-obsolete objects, on the other hand, could result in runtime errors and inconsistent behavior. In short: a real pain in the neck.

Garbage collection is an automated process that is able to figure out which objects are no longer needed and get rid of them, freeing space in memory.

In the common language runtime (CLR), the garbage collector (GC) serves as an automatic memory manager. The garbage collector manages the allocation and release of memory for an application. Therefore, developers working with managed code don't have to write code to perform memory management tasks.

### **Types of garbage collection**

Reference counting vs Tracing

C# garbage collection belongs to the tracing variety. It’s often called a generational approach since it employs the concept of generations to figure out which objects are eligible for collection.

Memory is divided into spaces called generations. The collector starts claiming objects in the youngest generation.