# Starting, Stopping the Monitoring MettleCI Workbench Service

*   [Unix](#unix)
    *   [Starting](#starting)
    *   [Stopping](#stopping)
    *   [Checking Status](#checking-status)
*   [Windows](#windows)
    *   [Starting](#starting)
    *   [Stopping](#stopping)
    *   [Checking Status](#checking-status)

In all instances a **Restart** of the MettleCI Workbench involves simply following the steps for **Stop** followed by **Start**.

# Unix

## Starting

Start the MettleCI Workbench service using the following command

```
$> sudo service dm-mettleci-workbench start
$> # or for AIX...
$> mciworkbench.rc start
```

## Stopping

Stop the MettleCI Workbench service using the following command

```
$> sudo service dm-mettleci-workbench stop
$> # or for AIX...
$> mciworkbench.rc start
```

## Checking Status

Verify your Workbench service is running:

```
$> sudo service dm-mettleci-workbench status
$> # or for AIX...
$> mciworkbench.rc status
```

# Windows

![](./attachments/Screen%20Shot%202019-11-20%20at%204.11.01%20pm.png)

## Starting

1.  Open the **Services** application.
    
2.  Double-click the **MettleCI Workbench** service.
    
3.  Click the **Start** button.
    
4.  Click the **Apply** button.
    
5.  Click the **OK** button.
    

## Stopping

1.  Open the **Services** application.
    
2.  Double-click the **MettleCI Workbench** service.
    
3.  Click the **Stop** button.
    
4.  Click the **Apply** button.
    
5.  Click the **OK** button.
    

## Checking Status

1.  Open the Services application.
    
2.  Verify that the **MettleCI Workbench** service has the Status **Running**.
    
3.  Verify that the **MettleCI Workbench** service has Startup Type **Automatic**.