### Examples
```c++
PSerialConn pSerialConn;
RegattaClient::createSerialConn(..., &pSerialConn);
...
...
pSerialConn->executeBatch(....);
pSerialConn->commit();
...
...
RegattaClient::closeSerialConn(pSerialConn);
RegattaClient:freeSerialConn(pSerialConn);
```

### ExecuteBatch function for Serial Conn
![[ExecuteBatch]]


