---
UID: NC:dispmprt.DXGKDDI_CONTROL_ETW_LOGGING
title: DXGKDDI_CONTROL_ETW_LOGGING (dispmprt.h)
description: The DxgkDdiControlEtwLogging function enables or disables Event Tracing for Windows (ETW) event logging.
old-location: display\dxgkddicontroletwlogging.htm
tech.root: display
ms.date: 05/10/2018
keywords: ["DXGKDDI_CONTROL_ETW_LOGGING callback function"]
ms.keywords: DXGKDDI_CONTROL_ETW_LOGGING, DXGKDDI_CONTROL_ETW_LOGGING callback, DmFunctions_87548564-6b7b-431b-b68c-202af84deefc.xml, DxgkDdiControlEtwLogging, DxgkDdiControlEtwLogging callback function [Display Devices], display.dxgkddicontroletwlogging, dispmprt/DxgkDdiControlEtwLogging
req.header: dispmprt.h
req.include-header: Dispmprt.h
req.target-type: Desktop
req.target-min-winverclnt: Windows Vista
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
req.irql: PASSIVE_LEVEL
targetos: Windows
req.typenames: 
f1_keywords:
 - DXGKDDI_CONTROL_ETW_LOGGING
 - dispmprt/DXGKDDI_CONTROL_ETW_LOGGING
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - UserDefined
api_location:
 - dispmprt.h
api_name:
 - DXGKDDI_CONTROL_ETW_LOGGING
---

# DXGKDDI_CONTROL_ETW_LOGGING callback function


## -description

The <i>DxgkDdiControlEtwLogging </i>function enables or disables Event Tracing for Windows (ETW) event logging.

## -parameters

### -param Enable [in]


A Boolean value that indicates whether <i>DxgkDdiControlEtwLogging </i>enables or disables ETW event logging. <b>TRUE</b> indicates that it enables and <b>FALSE</b> indicates that it disables.

### -param Flags [in]


A valid bitwise OR of values. Currently, no flags are defined.

### -param Level [in]


A value that indicates the level of event logging.

