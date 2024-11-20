# MettleCI CLI produces error 'Incorrectly typed data found for annotation element'

# Symptom

When using the S2PX plugin you receive

```
Exception in thread "main" java.lang.annotation.AnnotationTypeMismatchException: Incorrectly typed data found for annotation element public abstract java.lang.Class[] com.beust.jcommander.Parameter.validateWith() (Found data of type class java.lang.Class[class com.datamigrators.mettle.svpx.application.FileExists])
	at sun.reflect.annotation.AnnotationTypeMismatchExceptionProxy.generateException(AnnotationTypeMismatchExceptionProxy.java:57)
	at sun.reflect.annotation.AnnotationInvocationHandler.invoke(AnnotationInvocationHandler.java:84)
	at com.sun.proxy.$Proxy2.validateWith(Unknown Source)
```

# Cause

You are using versions of the MettleCI Command Shell and one or more MettleCI CLI plugins which are incompatible with one another.

*   `dm-s2px-convertion-plugin` versions >= 1.0-626 is only compatible with Command Shell version >= 1.1-182
    
*   `dm-s2px-conversion-plugin` versions < 1.0-626 is only compatible with Command Shell version < 1.1-182.
    

If an incompatible combination of versions is used, exceptions will occur when attempting to execute the `s2px` convert command. The exact error depends on whether a `s2px` plugin is newer the command shell or vice versa. The error reported will state that an older version of s2px is being used with a newer version of the command shell.

# Solution

Ensure you’re using a MettleCI Command Shell version compatible with the MettleCI CLI plugins you have installed.