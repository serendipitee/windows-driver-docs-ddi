---
UID: NF:wdfdevice.WdfDeviceCreate
title: WdfDeviceCreate function (wdfdevice.h)
description: The WdfDeviceCreate method creates a framework device object.
old-location: wdf\wdfdevicecreate.htm
tech.root: wdf
ms.date: 03/02/2018
keywords: ["WdfDeviceCreate function"]
ms.keywords: DFDeviceObjectGeneralRef_bd1ae89e-0e52-4c30-8ca4-9eaf6994a2f2.xml, WdfDeviceCreate, WdfDeviceCreate method, kmdf.wdfdevicecreate, wdf.wdfdevicecreate, wdfdevice/WdfDeviceCreate
req.header: wdfdevice.h
req.include-header: Wdf.h
req.target-type: Universal
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.kmdf-ver: 1.0
req.umdf-ver: 2.0
req.ddi-compliance: AccessHardwareKey, AddPdoToStaticChildList, ChangeQueueState, ChildDeviceInitAPI, ChildListConfiguration, ControlDeviceDeleted, ControlDeviceInitAllocate, ControlDeviceInitAPI, CtlDeviceFinishInitDeviceAdd, CtlDeviceFinishInitDrEntry, DeviceCreateFail, DeviceInitAllocate, DeviceInitAPI, DriverCreate, InitFreeDeviceCreate, InitFreeDeviceCreateType2, InitFreeDeviceCreateType4, InitFreeNull, KmdfIrql, KmdfIrql2, PdoDeviceInitAPI, PdoInitFreeDeviceCreate, PdoInitFreeDeviceCreateType2, PdoInitFreeDeviceCreateType4
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
req.lib: Wdf01000.sys (KMDF); WUDFx02000.dll (UMDF)
req.dll: 
req.irql: PASSIVE_LEVEL
targetos: Windows
req.typenames: 
f1_keywords:
 - WdfDeviceCreate
 - wdfdevice/WdfDeviceCreate
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - LibDef
api_location:
 - Wdf01000.sys
 - Wdf01000.sys.dll
 - WUDFx02000.dll
 - WUDFx02000.dll.dll
api_name:
 - WdfDeviceCreate
---

# WdfDeviceCreate function


## -description

[Applies to KMDF and UMDF]

The <b>WdfDeviceCreate</b> method creates a framework device object.

## -parameters

### -param DeviceInit [in, out]

The address of a pointer to a <a href="/windows-hardware/drivers/wdf/wdfdevice_init">WDFDEVICE_INIT</a> structure. If <b>WdfDeviceCreate</b> encounters no errors, it sets the pointer to <b>NULL</b>.

### -param DeviceAttributes [in, optional]

A pointer to a caller-allocated <a href="/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes">WDF_OBJECT_ATTRIBUTES</a> structure that contains attributes for the new object. (The structure's <b>ParentObject</b> member must be <b>NULL</b>.) This parameter is optional and can be WDF_NO_OBJECT_ATTRIBUTES.

### -param Device [out]

A pointer to a location that receives a handle to the new framework device object.

## -returns

If the **WdfDeviceCreate** method encounters no errors, it returns STATUS_SUCCESS. Additional return values include:

|Return code|Description|
|--- |--- |
|**STATUS_INVALID_PARAMETER**|An invalid *Device* or *DeviceInit* handle is supplied.|
|**STATUS_INVALID_DEVICE_STATE**|The driver has already created a device object for the device.|
|**STATUS_INVALID_SECURITY_DESCR**|The driver called **WdfDeviceInitAssignSDDLString** or **WdfDeviceInitSetDeviceClass** but did not provide a name for the device object.|
|**STATUS_INSUFFICIENT_RESOURCES**|A device object could not be allocated.|
|**STATUS_OBJECT_NAME_COLLISION**|The device name that was specified by a call to **WdfDeviceInitAssignName** already exists. The driver can call **WdfDeviceInitAssignName** again to assign a new name.|

For a list of other return values that **WdfDeviceCreate** can return, see <a href="/windows-hardware/drivers/wdf/framework-object-creation-errors">Framework Object Creation Errors</a>.

The method might return other <a href="/windows-hardware/drivers/kernel/ntstatus-values">NTSTATUS values</a>.

## -remarks

Before calling <b>WdfDeviceCreate</b>, the driver must call framework-supplied functions that initialize the WDFDEVICE_INIT structure. For more information about initializing this structure, see <a href="/windows-hardware/drivers/wdf/wdfdevice_init">WDFDEVICE_INIT</a>. If the driver encounters errors while calling the initialization functions, it must not call <b>WdfDeviceCreate</b>. In this case, the driver might have to call <a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree">WdfDeviceInitFree</a>. For information about when to call <b>WdfDeviceInitFree</b>, see <a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree">WdfDeviceInitFree</a>.

A call to <b>WdfDeviceCreate</b> creates a framework device object that represents either a functional device object (FDO) or a physical device object (PDO). The type of device object that the function creates depends on how the driver obtained the WDFDEVICE_INIT structure: 

<ul>
<li>
If the driver received the WDFDEVICE_INIT structure from an <a href="/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add">EvtDriverDeviceAdd</a> callback, <b>WdfDeviceCreate</b> creates an FDO. 

</li>
<li>
If the driver received the WDFDEVICE_INIT structure from an <a href="/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device">EvtChildListCreateDevice</a> callback, or from a call to <a href="/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate">WdfPdoInitAllocate</a>, <b>WdfDeviceCreate</b> creates a PDO.

</li>
</ul>
After the driver calls <b>WdfDeviceCreate</b>, it can no longer access the WDFDEVICE_INIT structure.

Miniport drivers that use the framework must call <a href="/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate">WdfDeviceMiniportCreate</a> instead of <b>WdfDeviceCreate</b>. 

The parent of each framework device object is the driver's framework driver object. The driver cannot change this parent, and the <b>ParentObject</b> member of the <a href="/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes">WDF_OBJECT_ATTRIBUTES</a> structure must be <b>NULL</b>. The framework deletes each framework device object (except for some <a href="/windows-hardware/drivers/wdf/using-control-device-objects">control device objects</a>) when the Plug and Play (PnP) manager determines that the device has been removed.

If your driver provides <a href="/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup">EvtCleanupCallback</a> or <a href="/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy">EvtDestroyCallback</a> callback functions for the framework device object, note that the framework calls these callback functions at IRQL = PASSIVE_LEVEL.

For more information about creating device objects, see <a href="/windows-hardware/drivers/wdf/creating-a-framework-device-object">Creating a Framework Device Object</a>.


#### Examples

The following code example shows how an <a href="/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add">EvtDriverDeviceAdd</a> callback function might initialize and create a device object.

```cpp
NTSTATUS
MyEvtDeviceAdd(
    IN WDFDRIVER  Driver,
    IN PWDFDEVICE_INIT  DeviceInit
    )
{
    WDF_PNPPOWER_EVENT_CALLBACKS  pnpPowerCallbacks;
    WDF_OBJECT_ATTRIBUTES  attributes;
    NTSTATUS  status;
    WDFDEVICE  device;
 
    //
    // Initialize the WDF_PNPPOWER_EVENT_CALLBACKS structure.
    //
    WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&pnpPowerCallbacks);
    pnpPowerCallbacks.EvtDevicePrepareHardware = MyEvtDevicePrepareHardware;
    pnpPowerCallbacks.EvtDeviceD0Entry = MyEvtDeviceD0Entry;
    pnpPowerCallbacks.EvtDeviceD0Exit  = MyEvtDeviceD0Exit;
    WdfDeviceInitSetPnpPowerEventCallbacks(
                                           DeviceInit,
                                           &pnpPowerCallbacks
                                           );
    //
    // This driver uses buffered I/O.
    //
    WdfDeviceInitSetIoType(
                           DeviceInit,
                           WdfDeviceIoBuffered
                           );
 
    //
    // Specify the device object's context space by
    // using a driver-defined DEVICE_CONTEXT structure.
 //
    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(
                                            &attributes,
                                            DEVICE_CONTEXT
                                            );
 //
    // Create the device object.
    //
    status = WdfDeviceCreate(
                             &DeviceInit,
                             &attributes,
                             &device
                             );
    if (!NT_SUCCESS(status)) {
        return status;
    }
    return STATUS_SUCCESS;
}
```

## -see-also

<a href="/windows-hardware/drivers/wdf/wdfdevice_init">WDFDEVICE_INIT</a>



<a href="/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes">WDF_OBJECT_ATTRIBUTES</a>



<a href="/windows-hardware/drivers/wdf/wdf-object-attributes-init-context-type">WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE</a>



<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdf_pnppower_event_callbacks_init">WDF_PNPPOWER_EVENT_CALLBACKS_INIT</a>



<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree">WdfDeviceInitFree</a>



<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype">WdfDeviceInitSetIoType</a>



<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks">WdfDeviceInitSetPnpPowerEventCallbacks</a>



<a href="/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate">WdfDeviceMiniportCreate</a>
