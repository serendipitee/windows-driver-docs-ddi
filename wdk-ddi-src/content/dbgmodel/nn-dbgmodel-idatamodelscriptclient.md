---
UID: NN:dbgmodel.IDataModelScriptClient
title: IDataModelScriptClient (dbgmodel.h)
description: Interface a component directly using debugger script must implement as a multi-way communication channel with the script.
ms.date: 07/13/2018
keywords: ["IDataModelScriptClient interface"]
req.header: dbgmodel.h
req.include-header: 
req.target-type: 
req.target-min-winverclnt: 
req.target-min-winversvr: 
req.umdf-ver: 
req.ddi-compliance: 
req.unicode-ansi: 
req.idl: 
req.max-support: 
req.namespace: 
req.assembly: 
req.type-library: 
targetos: Windows
tech.root: debugger
ms.custom: RS5
f1_keywords:
 - IDataModelScriptClient
 - dbgmodel/IDataModelScriptClient
topic_type:
 - apiref
api_type:
 - COM
api_location:
 - dbgmodel.h
api_name:
 - IDataModelScriptClient
---

# IDataModelScriptClient interface


## -description

Interface a component directly using debugger script must implement as a multi-way communication channel with the script.

## -inheritance

IDataModelScriptClient inherits from IUnknown.

## -remarks

A client interface which is used by the script provider in order to communicate information to a user interface. Script providers do not implement this interface. The application hosting the data model which wishes to make use of script providers does. A script provider will call into methods of the script client to report status, errors, etc...

## -see-also

[Debugger Data Model C++ Overview](/windows-hardware/drivers/debugger/data-model-cpp-overview)
