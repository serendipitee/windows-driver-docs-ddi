---
UID: NI:mountmgr.IOCTL_MOUNTMGR_CREATE_POINT
title: IOCTL_MOUNTMGR_CREATE_POINT (mountmgr.h)
description: Learn about the IOCTL_MOUNTMGR_CREATE_POINT IOCTL.
tech.root: storage
ms.date: 06/04/2024
keywords: ["IOCTL_MOUNTMGR_CREATE_POINT IOCTL"]
ms.keywords: IOCTL_MOUNTMGR_CREATE_POINT, IOCTL_MOUNTMGR_CREATE_POINT control, IOCTL_MOUNTMGR_CREATE_POINT control code [Storage Devices], k307_c1159db5-2699-4bac-9fe9-67ceda477ddb.xml, mountmgr/IOCTL_MOUNTMGR_CREATE_POINT, storage.ioctl_mountmgr_create_point
req.header: mountmgr.h
req.include-header: Mountmgr.h
req.target-type: Windows
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: 
req.dll: 
req.irql: 
targetos: Windows
req.typenames: 
f1_keywords:
 - IOCTL_MOUNTMGR_CREATE_POINT
 - mountmgr/IOCTL_MOUNTMGR_CREATE_POINT
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - HeaderDef
api_location:
 - Mountmgr.h
api_name:
 - IOCTL_MOUNTMGR_CREATE_POINT
---

## -description

The mount manager clients can use this IOCTL to request that the mount manager create a persistent symbolic link name for the indicated volume.

## -ioctlparameters

### -ioctl-major-code

[IRP_MJ_DEVICE_CONTROL](/windows-hardware/drivers/kernel/irp-mj-device-control)

### -input-buffer

The mount point manager places a [**MOUNTMGR_CREATE_POINT_INPUT**](ns-mountmgr-_mountmgr_create_point_input.md) structure at the beginning of the buffer at **Irp->AssociatedIrp.SystemBuffer**. The mount manager inserts the newly-assigned persistent symbolic link name at the address pointed to by the **SymbolicLinkNameOffset** member of this structure, and it inserts the nonpersistent device name at the address pointed to by the **DeviceNameOffset** member of this structure.

### -input-buffer-length

**Parameters.DeviceIoControl.InputBufferLength** in the I/O stack location of the IRP indicates the size, in bytes, of the input buffer, which must be greater than or equal to ```sizeof(MOUNTMGR_CREATE_POINT_INPUT)```.

### -output-buffer

None.

### -output-buffer-length

None.

### -in-out-buffer

N/A

### -inout-buffer-length

N/A

### -status-block

If the operation is successful, the **Status** field is set to STATUS_SUCCESS.

If **InputBufferLength** is less than ```sizeof(MOUNTMGR_CREATE_POINT_INPUT)```, the **Status** field is set to STATUS_INVALID_PARAMETER.

## -remarks

The input to this request is the persistent symbolic link name to be created and a name that is already valid for purposes of identifying the volume. The name given for purposes of identifying the volume can be of any type: a unique volume name, a symbolic link name, or a nonpersistent device name. If the new persistent name is not already in use, the call will succeed and the mount manager database will be modified to reflect that the new persistent name belongs to the volume. If the mount manager database already contains the new persistent name but the volume that owns that name is not in the system, this call will overwrite ownership of the given persistent name.

The mount manager allows the creation of a new persistent symbolic link name even if it has not yet been notified of the given volume in the MOUNTDEV_MOUNTED_DEVICE_GUID device interface notification. In such a case, the mount manager simply creates the symbolic link and updates the mount manager database.

The mount manager enforces a policy of at most one persistent drive letter per volume. If an **IOCTL_MOUNTMGR_CREATE_POINT** request is sent with a drive letter, the request will fail if there is already a drive letter assigned to the volume, unless the mount manager has not yet been notified of the volume by means of the MOUNTDEV_MOUNTED_DEVICE_GUID device interface notification. In the latter case, the call succeeds and the mount manager purges the mount manager database of any other drive letters previously assigned to the volume.

If IOCTL_MOUNTMGR_CREATE_POINT specifies a drive letter, the drive letter must be upper case.

Note that a client can discover whether the mount manager has received the MOUNTDEV_MOUNTED_DEVICE_GUID device interface notification for its volume by querying the mount manager with [**IOCTL_MOUNTMGR_QUERY_POINTS**](ni-mountmgr-ioctl_mountmgr_query_points.md).

In this pseudocode sample, a mount manager client uses IOCTL_MOUNTMGR_CREATE_POINT to send the mount manager a device object name and its corresponding symbolic link:

``` C
    // The persistent symbolic link is a drive letter in
    // this case:
    wsprintf(dosBuffer, L"\\DosDevices\\%C:", DriveLetter);
    RtlInitUnicodeString(&dosName, dosBuffer);
    // The nonpersistent volume (device) object name is
    // formed using the volume number as a suffix
    wsprintf(ntBuffer, L"\\Device\\HarddiskVolume%D", 
                       Extension->VolumeNumber);
    RtlInitUnicodeString(&ntName, ntBuffer);
    createPointSize = sizeof(MOUNTMGR_CREATE_POINT_INPUT) +
                      dosName.Length + ntName.Length;
    // Allocate a header with length and offset information
    createPoint = (PMOUNTMGR_CREATE_POINT_INPUT)
                  ExAllocatePool(PagedPool, 
                  createPointSize);
    createPoint->SymbolicLinkNameOffset = 
                  sizeof(MOUNTMGR_CREATE_POINT_INPUT);
    createPoint->SymbolicLinkNameLength = dosName.Length;
    createPoint->DeviceNameOffset = 
        createPoint -> SymbolicLinkNameOffset +
        createPoint -> SymbolicLinkNameLength;
    createPoint->DeviceNameLength = ntName.Length;
    RtlCopyMemory((PCHAR) createPoint + 
                  createPoint -> SymbolicLinkNameOffset,
                  dosName.Buffer, dosName.Length);
    RtlCopyMemory((PCHAR) createPoint + 
                  createPoint->DeviceNameOffset,
                  ntName.Buffer, ntName.Length);
    // Use the name of the mount manager device object
    // defined in mountmgr.h (MOUNTMGR_DEVICE_NAME) to
    // obtain a pointer to the mount manager.
    RtlInitUnicodeString(&name, MOUNTMGR_DEVICE_NAME);
    status = IoGetDeviceObjectPointer(&name,
                              FILE_READ_ATTRIBUTES, 
                              &fileObject, &deviceObject);
    KeInitializeEvent(&event, NotificationEvent, FALSE);
    irp = IoBuildDeviceIoControlRequest(
            IOCTL_MOUNTMGR_CREATE_POINT,
            deviceObject, createPoint, createPointSize, 
            NULL, 0, FALSE, &event, &ioStatus);
    // Send the irp to the mount manager requesting
    // that a new mount point (persistent symbolic link)
    // be created for the indicated volume.
    status = IoCallDriver(deviceObject, irp);
```

For more information, see [Supporting Mount Manager Requests in a Storage Class Driver](/windows-hardware/drivers/storage/supporting-mount-manager-requests-in-a-storage-class-driver).

## -see-also

[**MOUNTMGR_CREATE_POINT_INPUT**](ns-mountmgr-_mountmgr_create_point_input.md)
