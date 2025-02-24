---
UID: NC:d3d12umddi.PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088
tech.root: display
title: PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088
ms.date: 02/28/2023
targetos: Windows
description: Learn more about the PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088 callback function.
prerelease: false
req.assembly: 
req.construct-type: function
req.ddi-compliance: 
req.dll: 
req.header: d3d12umddi.h
req.idl: 
req.include-header: 
req.irql: 
req.kmdf-ver: 
req.lib: 
req.max-support: 
req.namespace: 
req.redist: 
req.target-min-winverclnt: Windows 11 (WDDM 3.0)
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
 - d3d12umddi.h
api_name:
 - PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088
f1_keywords:
 - PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088
 - d3d12umddi/PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088
dev_langs:
 - c++
helpviewer_keywords:
 - PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088
---

## -description

**PFND3D12DDI_CALCPRIVATEHEAPANDRESOURCESIZES_0088** calculates the number of bytes required for a private heap and resource.

## -parameters

### -param unnamedParam1

[in] A handle to the display device (graphics context).

### -param unnamedParam2

[in/optional] Pointer to a [**D3D12DDIARG_CREATEHEAP_0001**](ns-d3d12umddi-d3d12ddiarg_createheap_0001.md) structure that describes the heap.

### -param unnamedParam3

[in/optional] Pointer to a [**D3D12DDIARG_CREATERESOURCE_0088**](ns-d3d12umddi-d3d12ddiarg_createresource_0088.md) structure that describes the resource.

### -param unnamedParam4

[in] The protected resource session to use for the heap/resource being created. Zero indicates unprotected resources. See the [Protected Resources Specification](https://microsoft.github.io/DirectX-Specs/d3d/ProtectedResources.html) for more information.

## -returns

Returns a [**D3D12DDI_HEAP_AND_RESOURCE_SIZES**](ns-d3d12umddi-d3d12ddi_heap_and_resource_sizes.md) structure that specifies the sizes of the heap and resource, in bytes.

## -see-also

[**D3D12DDIARG_CREATERESOURCE_0088**](ns-d3d12umddi-d3d12ddiarg_createresource_0088.md)

[**PFND3D12DDI_CREATEHEAPANDRESOURCE_0088**](nc-d3d12umddi-pfnd3d12ddi_createheapandresource_0088.md)
