---
UID: NC:d3d12umddi.PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022
title: PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022 (d3d12umddi.h)
description: The PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022 callback function checks resource allocation information.
old-location: display\pfnd3d12ddi_checkresourceallocationinfo_0022.htm
ms.date: 05/10/2018
keywords: ["PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022 callback function"]
ms.keywords: PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022, PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022 callback, d3d12umddi/pfnCheckResourceAllocationInfo, display.pfnd3d12ddi_checkresourceallocationinfo_0022, pfnCheckResourceAllocationInfo, pfnCheckResourceAllocationInfo callback function [Display Devices]
req.header: d3d12umddi.h
req.include-header: D3d12umddi.h
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
tech.root: display
req.typenames: 
f1_keywords:
 - PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022
 - d3d12umddi/PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - UserDefined
api_location:
 - D3d12umddi.h
api_name:
 - PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022
---

# PFND3D12DDI_CHECKRESOURCEALLOCATIONINFO_0022 callback function


## -description

The <i>pfnCheckResourceAllocationInfo</i> callback function supports checking resource allocation information.

## -parameters

### -param unnamedParam1

*hDevice*

A handle to the display device (graphics context).

### -param unnamedParam2

*CreateResource* [in]

A pointer to a create resource.

### -param unnamedParam3

*ResourceOptimizationFlags*

Resource optimization flags.

### -param AlignmentRestriction

An alignment restriction value.

### -param VisibleNodeMask

A visible node mask.

### -param unnamedParam6

*pInfo* [out]

Information for resource allocation.

## -remarks

This callback function is part of a two step process of resource creation. This function determines the sizes and alignments of the resource data, additional data header, and additional data is determined, along with the texture layout. When the resource description is passed into this function, the layout of the resource description may be set to _UNDEFINED. This allows the driver to choose any texture layout. When the layout of the resource description is <b>STANDARD_SWIZZLE</b> or <b>ROW_MAJOR</b>, the driver must return out the corresponding value as its choice.

This callback function is accessed by using the <a href="/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddi_device_funcs_core_0010">D3D12DDI_DEVICE_FUNCS_CORE_0010</a> structure.

