---
UID: NF:wdfsync.WdfObjectAcquireLock
title: WdfObjectAcquireLock function (wdfsync.h)
description: The WdfObjectAcquireLock method acquires an object's synchronization lock.
old-location: wdf\wdfobjectacquirelock.htm
tech.root: wdf
ms.date: 04/29/2023
keywords: ["PFN_WDFOBJECTACQUIRELOCK callback"]
ms.keywords: wdf.wdfobjectacquirelock, PFN_WDFOBJECTACQUIRELOCK, WdfObjectAcquireLock callback function, WdfObjectAcquireLock, wdfsync/WdfObjectAcquireLock, DFSynchroRef_d6a841c3-cbcb-4072-861a-5666dc2b4b02.xml, kmdf.wdfobjectacquirelock
req.header: wdfsync.h
req.include-header: Wdf.h
req.target-type: Universal
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.kmdf-ver: 1.0
req.umdf-ver: 2.0
req.ddi-compliance: DriverCreate, KmdfIrql, KmdfIrql2
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: 
req.dll: 
req.irql: See Remarks section.
targetos: Windows
req.typenames: "*PWDF_REQUEST_SEND_OPTIONS, WDF_REQUEST_SEND_OPTIONS"
f1_keywords:
 - PFN_WDFOBJECTACQUIRELOCK
 - wdfsync/PFN_WDFOBJECTACQUIRELOCK
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - UserDefined
api_location:
 - wdfsync.h
api_name:
 - PFN_WDFOBJECTACQUIRELOCK
---

# WdfObjectAcquireLock function


## -description

<p class="CCE_Message">[Applies to KMDF and UMDF]</p>

The <b>WdfObjectAcquireLock</b> method acquires an object's synchronization lock.

## -syntax

```cpp
VOID WdfObjectAcquireLock(
  _In_ WDFOBJECT Object
);
```
## -parameters


### -param Object [in]

A handle to a framework device object or a framework queue object.


## -remarks

A bug check occurs if the driver supplies an invalid object handle.

A driver can call the <b>WdfObjectAcquireLock</b> method to acquire the synchronization lock that is associated with a specified framework device object or framework queue object. The method does not return until the lock has been acquired.

When the driver no longer needs the object's synchronization lock, it must call <a href="/previous-versions/ff548765(v=vs.85)">WdfObjectReleaseLock</a>.

If the driver specified <b>WdfExecutionLevelPassive</b> for the <b>ExecutionLevel</b> member of the specified object's <a href="..\wdfobject\ns-wdfobject-_wdf_object_attributes.md">WDF_OBJECT_ATTRIBUTES</a> structure, the driver must call <b>WdfObjectAcquireLock</b> at IRQL <= APC_LEVEL. <b>WdfObjectAcquireLock</b> acquires a <a href="/windows-hardware/drivers/kernel/fast-mutexes-and-guarded-mutexes">fast mutex</a> and returns at the caller's IRQL. (In this case, <b>WdfObjectAcquireLock</b> also calls <a href="..\wdm\nf-wdm-keentercriticalregion.md">KeEnterCriticalRegion</a> before returning so that <a href="/windows-hardware/drivers/kernel/types-of-apcs">normal kernel APCs</a> are disabled.)

If the driver did <i>not</i> specify <b>WdfExecutionLevelPassive</b> for the <b>ExecutionLevel</b> member of the specified object's WDF_OBJECT_ATTRIBUTES structure, the driver must call <b>WdfObjectAcquireLock</b> at IRQL <= DISPATCH_LEVEL. <b>WdfObjectAcquireLock</b> acquires a <a href="/windows-hardware/drivers/kernel/spin-locks">spin lock</a> and returns at IRQL = DISPATCH_LEVEL.

For more information about synchronization locks, see <a href="/windows-hardware/drivers/wdf/synchronization-techniques-for-wdf-drivers">Synchronization Techniques for Framework-Based Drivers</a>.

## -see-also

<a href="..\wdfobject\ns-wdfobject-_wdf_object_attributes.md">WDF_OBJECT_ATTRIBUTES</a>

<a href="..\wdm\nf-wdm-keentercriticalregion.md">KeEnterCriticalRegion</a>

<a href="/previous-versions/ff548765(v=vs.85)">WdfObjectReleaseLock</a>

