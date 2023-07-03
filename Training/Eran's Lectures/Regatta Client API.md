

## Overview

The file implements a standard interface for all drivers and connectors, including JDBC and ODBC, making it easier to integrate new drivers and connectors. The Regatta API is a client library designed for interacting with Regatta databases only and cannot connect to other databases.

## Asynchronous API

The Regatta API is an Asynchronous API, allowing the concurrent submission of multiple transactions to the database. The request object is used for client interactions throughout the lifetime of an operation with the database, providing functionalities such as waiting for the request, aborting it, and retrieving completion status and data. However, only a single inflight statement per transaction is permitted.

## Connection

The Regatta API incorporates connection caching, eliminating the need for user-level caching mechanisms like connection pools.

## Result Cursors

Result cursors in the database allow applications to retrieve and process the rows of a result set one by one, rather than all at once, which can be more efficient in terms of memory usage and network bandwidth. The Regatta API only supports client-side cursors and forward cursors. All rows are pushed to the client machine, and consumed rows are discarded.


> [!NOTE] ChatGPT What is a result cursor?
>   
A result cursor, in the context of databases, is a pointer or iterator-like object that allows you to traverse the results of a database query. It provides a way to retrieve and access individual rows or records returned by the query.

## Signal Handling

When executing Regatta threads, the program alters the default operating system signal handling to that of Regatta, which includes signals like SIGSEGV, SIGINT, SIGTERM, SIGFPE, SIGBUS, SIGILL, and SIGQUIT. Users have the option to choose whether to retain their thread's default signal handling or allow Regatta to switch to its signal handling within the client options.

## Tracer

The tracer in Regatta records sequences of events or steps during database execution, providing log messages with information such as timestamp, source location, log level, and contextual data. Traces help developers and system administrators gain insights into program execution, identify potential issues, and analyze performance bottlenecks.

## Usage

To utilize the Regatta API, the initialization process must be invoked first. Then, a client instance can be acquired to interact with the library. The API supports functions for establishing a connection, creating transactions, executing statements, monitoring connection and transaction progress, committing or rolling back transactions, and closing connections.

## Initialization

The init function sets up the library and should be called before any other function to ensure proper functioning.

## Destroy

The destroy function for the client object must be called once all connections and associated objects are properly closed to avoid errors and unexpected behavior.

## Getting a Client

The RegattaClient can be accessed through the getClient() function, acting as an intermediary between the application and the database.

## Basic Usage Example

```cpp
regatta_api::init(nullptr, nullptr); 
regatta_api::PRegattaClient pClient = regatta_api::getClient();  
.. Work ..
regatta_api::destroy();
```

## Working with Requests

An asynchronous request object represents a pending request that can be executed in a non-blocking manner. Examples of waiting for a request, polling for a request, and using callbacks are provided.

# Working with Requests

An asynchronous request object represents a pending request. The request is executed in a non-blocking manner, allowing the program to continue executing other tasks while the request is being processed.

## Wait Example:
```cpp
regatta_api::RequestOptions pOptions;
regatta_api::PConnectionRequest pFirstRequest;

regatta_api::ClientRC status = pClient->createConnection(
    &pOptions, "url", "user", "pass", nullptr, &pFirstRequest);

if (status != regatta_api::ClientRC::kPending) {
    // failed to start
}
pFirstRequest->wait(0);
if (pFirstRequest->getStatus() !=
    regatta_api::Request::Status::kCompleted) {
    // request failed
}
regatta_api::PConnection pConn;
pFirstRequest->getConnection(&pConn);
```

## Polling Example:
```cpp
regatta_api::PConnection pConn;
regatta_api::PConnectionRequest pRequest;
regatta_api::ClientRC status = pClient->createConnection(pOptions, "url",
                                         "user", "pass", nullptr, &pRequest);
if (status != regatta_api::ClientRC::kPending) {
    // failed to start
}
while (pRequest->getStatus() == regatta_api::Request::Status::kPending){
  other_logic();
}
if (pRequest->getStatus() == regatta_api::Request::Status::kDone)
     pRequest->getConnection(&pConn);
```

## Callback example:

```cpp
static void connectionReqCallback(regatta_api::PRequest pRequest)
{
    if (pRequest->getStatus() != regatta_api::Request::Status::kCompleted) {
        // handle failed
    }
    void* context;
    pRequest->getContext(&context);
    alertNewConnection(context);
}

void connect(void* context)
{
    regatta_api::PRegattaClient pClient = regatta_api::getClient();
    regatta_api::RequestOptions pOptions;
    pOptions.m_callback = connectionReqCallback;
    pOptions.m_pUserCtx = context;

    regatta_api::PConnection pConn;
    regatta_api::PConnectionRequest pReq;
    regatta_api::ClientRC status = pClient->createConnection(
        &pOptions, "url", "user", "pass", nullptr, &pReq);

    if (status != regatta_api::ClientRC::kPending) {
        // failed to start
    }
}
```

## Execute example:
```cpp
regatta_api::PStatementRequest pReq;
const char* sqlCommands[2] = {
    "INSERT INTO users (name, email) VALUES ('John Doe', "
    "'johndoe@example.com');",
    "INSERT INTO users (name, email) VALUES ('Jane Smith', "
    "'janesmith@example.com');"};
status = pClient->executeBatchStatement(&pOptions,
                                       pTxn,
                                       sqlCommands,
                                       2,
                                       regatta_api::CommitAfterBatch::kFalse,
                                       &pReq);
if (status != regatta_api::ClientRC::kPending) {
    // failed to start
}
pReq->wait(0);
if (pReq->getStatus() != regatta_api::Request::Status::kCompleted) {
    // error handling
} else {
    // all statements executed successfully
    regatta_api::HasMore not_done;
    pReq->hasMoreResultSets(&not_done);
    for (int i = 0; not_done == regatta_api::HasMore::kTrue; i++) {
        uint64_t rows;
        pReq->getAffectedRows(&rows);
        std::cout << " insert number " << i << " affected: " << rows
                  << " rows" << std::endl;
        pReq->hasMoreResultSets(&not_done);
    }
}
```

### F2F Eran

2 connections types:
1. Asynchrony
2. Synchrony (serial connection)

We can choose different permission per:
1. connection
2. Transaction
3. Batch

In this context:
```
connection == session
```

In the end of a transaction we can **commit** or **rollback**

