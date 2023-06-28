
### N-way caching (Set Associative Mapping)

Every row in the memory have a particular set in the cache, in which it can be cache.
For example row 0 is mapping to set 0 and can be in the rows range [0, 2] in the cache.
![[Pasted image 20230625164449.png]]


### False Sharing

![[False Sharing]]


Fiber -> Thread only in User Mode
cpu -> Thread

### FastLock
Spinlock for very small CS

### Obj_handles
 * The handles are used to insure that objects that may have users pointing
 * at them will not be freed. The algorithm used is as follows:
 * - For each type of object we want to protect, we allocate a handle factory
 * - When an object is allocated, the allocator of the objects calls
 *   allocateHandle() to allocate an entry in the factory. Each entry has a
 *   version assigned to it. This version is stored in the handle along with a
 *   pointer to the object and the index of the entry.
 * - In order to access an object, users call acquire() providing the handle.
 *   the acquire() function checks whether the entry refereed to by the handle
 *   is still valid (the version number is still the same and the entry was not
 *   deleted). If the entry is valid it increments the reference count of the
 *   entry and returns success, otherwise it returns staleHandle.
 * - When the user is done with accessing the object, he calls release() which
 *   decrements the entry's refcount.
 * - Before freeing the object, the handle needs to be freed by calling
 *   freeHandle(). If the refcount of the entry is 0, the handle is freed.
 *   Otherwise, freeHandle() marks the entry as delete pending and returns
 *   notReady. An entry that is marked delete pending cannot be acquired, and
 *   when the last user that acquired the handle releases it, a callback
 *   provided by the creator of the handle factory is called.

