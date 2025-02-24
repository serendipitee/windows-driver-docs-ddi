---
UID: NC:fwpsk.FWPS_CALLOUT_NOTIFY_FN3
tech.root: netvista
title: FWPS_CALLOUT_NOTIFY_FN3
ms.date: 06/27/2024
targetos: Windows
description: Version 3 of the function invoked during classification when a callout filter matches.
prerelease: false
req.assembly: 
req.construct-type: function
req.ddi-compliance: 
req.dll: 
req.header: fwpsk.h
req.idl: 
req.include-header: 
req.irql: <= DISPATCH_LEVEL
req.kmdf-ver: 
req.lib: 
req.max-support: 
req.namespace: 
req.redist: 
req.target-min-winverclnt: Available starting with Windows Vista.
req.target-min-winversvr: 
req.target-type: 
req.type-library: 
req.umdf-ver: 
req.unicode-ansi: 
topic_type:
 - apiref
api_type:
 - LibDef
api_location:
 - fwpsk.h
api_name:
 - FWPS_CALLOUT_NOTIFY_FN3
f1_keywords:
 - FWPS_CALLOUT_NOTIFY_FN3
 - fwpsk/FWPS_CALLOUT_NOTIFY_FN3
dev_langs:
 - c++
helpviewer_keywords:
 - FWPS_CALLOUT_NOTIFY_FN3
---

## -description

Version 3 of the function invoked during classification when a callout filter matches. The difference being that this callback returns an [FWPS_FILTER3](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_filter3) structure.

## -parameters

### -param notifyType

A value that indicates the type of notification that the filter engine is sending to the callout. Valid values for this parameter are:

- **FWPS_CALLOUT_NOTIFY_ADD_FILTER**: A filter is being added to the filter engine that specifies the callout for the filter's action.
- **FWPS_CALLOUT_NOTIFY_DELETE_FILTER**: A filter is being deleted from the filter engine that specifies the callout for the filter's action.
- **FWPS_CALLOUT_NOTIFY_TYPE_MAX**: A maximum value for testing purposes.

### -param filterKey

A pointer to the management identifier for the filter, as specified by the application or driver that is adding or deleting the filter. Must be **NULL** if the *notifyType* parameter is set to **FWPS_CALLOUT_NOTIFY_DELETE_FILTER**. For more information, see [Remarks](#remarks).

### -param filter

A pointer to an [FWPS_FILTER3](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_filter3) structure. This structure describes the filter that is being added to or deleted from the filter engine.

A callout's **notifyFn3** callout function can set the context member of this structure to point to a callout driver-supplied context structure when the filter is added to the filter engine. This context structure is opaque to the filter engine, and can be used by the callout driver's **classifyFn3** callout function to preserve any driver-specific data or state information between calls by the filter engine to the callout driver's **classifyFn3** callout function.

A callout's **notifyFn3** callout function can clean up any context associated with the filter when the filter is deleted from the filter engine.

## -returns

A callout's **notifyFn3** function returns one of the following **NTSTATUS** codes.

| Return code | Description |
|--|--|
| STATUS_SUCCESS | The callout driver accepts the notification from the filter engine. |
| Other status codes | An error occurred. If the *notifyType* parameter is **FWPS_CALLOUT_NOTIFY_ADD_FILTER**, the filter will not be added to the filter engine. If the *notifyType* parameter is **FWPS_CALLOUT_NOTIFY_DELETE_FILTER**, the filter will still be deleted from the filter engine. |

## -remarks

A callout driver registers a callout's callout functions with the filter engine by calling the **FwpsCalloutRegister2** function.

The filter engine calls a callout's **notifyFn3** callout function to notify the callout driver about events that are associated with the callout. If the callout driver's **notifyFn3** callout function does not recognize the type of notification that is passed in the *notifyType* parameter, it ignores the notification and return **STATUS_SUCCESS**.

If a callout driver registers a callout with the filter engine after filters that specify the callout for the filter's action have already been added to the filter engine, the filter engine does not call the callout driver's **notifyFn3** callout function to notify the callout about any of the existing filters. The filter engine calls the callout driver's **notifyFn3** callout function to notify the callout when new filters that specify the callout for the filter's action are added to the filter engine. In this situation, a callout's **notifyFn3** callout function might not get called for every filter in the filter engine that specifies the callout for the filter's action. If a callout driver registers a callout after the filter engine is started and the callout needs to know about every filter in the filter engine that specifies the callout for the filter's action, the callout driver must call the appropriate management functions to enumerate all the filters in the filter engine and sort through the resulting list of filters to find those that specify the callout for the filter's action. For more information about calling these functions, see [Calling other Windows Filtering Platform functions](/windows-hardware/drivers/network/calling-other-windows-filtering-platform-functions).

When a filter that specifies a callout for the filter's action is deleted from the filter engine, the filter engine calls the callout driver's **notifyFn3** callout function and passes FWP_CALLOUT_NOTIFY_DELETE_FILTER in the *notifyType* parameter and **NULL** in the filterKey parameter. For more information, see [Processing notify callouts](/windows-hardware/drivers/network/processing-notify-callouts).

## -see-also

- [FWPS_FILTER3](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_filter3)
- [Calling other Windows Filtering Platform functions](/windows-hardware/drivers/network/calling-other-windows-filtering-platform-functions)
- [Processing notify callouts](/windows-hardware/drivers/network/processing-notify-callouts)
