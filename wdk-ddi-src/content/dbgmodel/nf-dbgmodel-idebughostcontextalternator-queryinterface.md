---
UID: NF:dbgmodel.IDebugHostContextAlternator.QueryInterface
tech.root: debugger
title: IDebugHostContextAlternator::QueryInterface
ms.date: 12/16/2024
targetos: Windows
description: The QueryInterface method queries for a specific interface on the current context.
prerelease: false
req.assembly: 
req.construct-type: function
req.ddi-compliance: 
req.dll: 
req.header: dbgmodel.h
req.idl: 
req.include-header: 
req.irql: 
req.kmdf-ver: 
req.lib: 
req.max-support: 
req.namespace: 
req.redist: 
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.target-type: 
req.type-library: 
req.umdf-ver: 
req.unicode-ansi: 
topic_type:
 - apiref
api_type:
 - COM
api_location:
 - dbgmodel.h
api_name:
 - IDebugHostContextAlternator::QueryInterface
f1_keywords:
 - IDebugHostContextAlternator::QueryInterface
 - dbgmodel/IDebugHostContextAlternator::QueryInterface
dev_langs:
 - c++
helpviewer_keywords:
 - QueryInterface
---

## -description

Retrieves pointers to the supported interfaces on an object. This method calls IUnknown::AddRef on the pointer it returns. 

For more information, see [IUnknown::QueryInterface](/windows/win32/api/Unknwn/nf-unknwn-iunknown-queryinterface(refiid_void)) and [Introduction to COM](/cpp/atl/introduction-to-com).

## -parameters

### -param iid

The interface ID. A pointer to an existing object provided as input.

### -param iface

The returned pointer to the requested COM interface.

## -returns

This method returns HRESULT which indicates success or failure.

## -remarks

Standard COM method.

## -see-also

[IDebugHostContextAlternator interface](nn-dbgmodel-idebughostcontextalternator.md)