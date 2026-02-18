# Resolving Scouter Client JVM Error After macOS Big Sur Update

<br>

<br>

### Problem

: After updating to Big Sur, the following error occurs indicating that a JVM cannot be created

![scouter_client_jvm_error](../kor/images/scouter_client_jvm_error.png)

<br>

<br>

### Cause

- When updating to Big Sur, Java is installed by default
  - The issue appears to be caused by a mismatch between the Java version that Scouter points to and the Java version configured in Big Sur

<br>

<br>

### Solution

: Resolved by specifying the installed JDK path in the scouter.client.app/Contents/Eclipse/scouter.ini file

```bash
-vm
/Library/Java/JavaVirtualMachines/jdk1.8.0_271.jdk/Contents/Home/bin/java
```

<br>

<br>

#### Reference

: <https://github.com/scouter-project/scouter/issues/764>
