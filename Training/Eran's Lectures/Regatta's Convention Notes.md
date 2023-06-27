
### Includes
1. Include "core_intf.h" in all cpp file
2. Never include "core_intf.h" in header file


### Exceptions
```cpp
CORE__RETURN_RC LsaDeleteEngine::init(PUINT32 pDeleteQueueBucketBoundaries)
{
    CoreRC rc;
    struct Rollback rollback;
    rollback.setAll(false);

    rc = initDeleteQueues();
    CORE__GOTO_IF_NO_SUCCESS(rc, cleanup);
    rollback.m_bDeleteQueuesArrays = true;

    rc = initBoundaries(pDeleteQueueBucketBoundaries);
    CORE__GOTO_IF_NO_SUCCESS(rc, cleanup);
    rollback.m_bBoundaries = true;

    rc = initDeleteEntriesArena();
    CORE__GOTO_IF_NO_SUCCESS(rc, cleanup);
    rollback.m_bDeleteEntriesBuffersArena = true;

    rc = initLsaDeleteWorkers();
    CORE__GOTO_IF_NO_SUCCESS(rc, cleanup);
    rollback.m_bLsaDeleteWorkers = true;

    return rc;
cleanup:
    rollbackResources(rollback);
    return rc;
}
```

