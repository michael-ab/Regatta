### Serial Connection Diagram Flow
![[Serial Connection Diagram Flow | 600]]

### JDBC DOC
[https://docs.oracle.com/javase/8/docs/api/java/sql/package-summary.html](https://docs.oracle.com/javase/8/docs/api/java/sql/package-summary.html)


JDBC <-> JNI <-> Code C <-> Client (Regatta API)

StatementRequest (class) -> request for execute

Statement = set of queries

#### F2F 2 Yana

ExecuteBatch for JDBC we are not saving the result set.
But we need to save some infos before we free the result set (num rows, etc.).

RegConnection m_state is not the state for the serial connection. it's a internal java state to help to reduce JNI call.

Need to cast Java type to C++ type (jstring, jobject, etc.). We need JNI cast function for it when we return to C++.
```cpp
JNIEXPORT jlong JNICALL
Java_dev_regatta_jdbc_RegJNI_createConnection(JNIEnv *pEnv,
                                              jclass jRegJNICls,
                                              jobject jExceptionHelper,
                                              jstring jUsername,
                                              jstring jPassword,
                                              jstring jUrl)
{
    CORE__UNUSED_VAR(jRegJNICls);
    ClientRC rc;
    SerialConn::Error error;
    PRegattaClient pClient = getClient();

  
    drivers::jdbc::PConnection pConnection =
        core::mem::mallocObject<drivers::jdbc::Connection>();
    if (pConnection == nullptr) {
        pEnv->CallVoidMethod(jExceptionHelper,
                             drivers::jdbc::gEnvironment.m_noResourcesErr);
        return 0;
    }
    PConstCharA pNativeUser = pEnv->GetStringUTFChars(jUsername, nullptr);
    PConstCharA pNativePassword = pEnv->GetStringUTFChars(jPassword, nullptr);
    PConstCharA pNativeUrl = pEnv->GetStringUTFChars(jUrl, nullptr);
    if (pNativeUser == nullptr || pNativePassword == nullptr ||
        pNativeUrl == nullptr) {
        pEnv->CallVoidMethod(jExceptionHelper,
                             drivers::jdbc::gEnvironment.m_noResourcesErr);
        goto cleanup;
    }
   return reinterpret_cast<jlong>(pConnection);
```

**Convention**: JAVA object start with "j"

The return from c++ (reg_init.cc) need to be cast with reinteprete_cast to java type.

CheckIfClosed() throw exception if connection is closed.

![[JAVA/Untitled Diagram.svg]]
We have holdability only for JDBC, not for the native client.


