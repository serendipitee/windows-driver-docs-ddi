---
UID: NC:d3d10umddi.PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP
title: PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP (d3d10umddi.h)
description: The DefaultConstantBufferUpdateSubresourceUP function updates a destination subresource region that stores constant buffers from a source system-memory region.
old-location: display\defaultconstantbufferupdatesubresourceup.htm
ms.date: 05/10/2018
keywords: ["PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP callback function"]
ms.keywords: DefaultConstantBufferUpdateSubresourceUP, DefaultConstantBufferUpdateSubresourceUP callback function [Display Devices], PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP, PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP callback, UserModeDisplayDriverDx10_Functions_1868c778-0475-4113-8b24-caf7f9822775.xml, d3d10umddi/DefaultConstantBufferUpdateSubresourceUP, display.defaultconstantbufferupdatesubresourceup
req.header: d3d10umddi.h
req.include-header: D3d10umddi.h
req.target-type: Desktop
req.target-min-winverclnt: Available in Windows Vista and later versions of the Windows operating systems.
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
 - PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP
 - d3d10umddi/PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - UserDefined
api_location:
 - d3d10umddi.h
api_name:
 - PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP
---

# PFND3D10DDI_RESOURCEUPDATESUBRESOURCEUP callback function


## -description

The <i>DefaultConstantBufferUpdateSubresourceUP</i> function updates a destination subresource region that stores constant buffers from a source system-memory region.

## -parameters

### -param unnamedParam1

*hDevice* [in]

A handle to the display device (graphics context).

### -param unnamedParam2

*hDstResource* [in]

A handle to the destination resource to copy to.

### -param unnamedParam3

*DstSubresource* [in]

An index that indicates the destination subresource to copy to.

### -param unnamedParam4

*pDstBox* [in, optional]

A pointer to a <a href="/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_ddi_box">D3D10_DDI_BOX</a> structure that specifies the region of the destination subresource to copy data to. If <b>pDstBox</b> is <b>NULL</b>, the driver should copy to the entire destination subresource.

### -param unnamedParam5

*pSysMemUP* [in]

A pointer to the beginning address of the source data that <i>DefaultConstantBufferUpdateSubresourceUP</i> uses to update the destination subresource.

### -param unnamedParam6

*RowPitch* [in]

The offset, in bytes, to move to the next row of source data.

### -param unnamedParam7

*DepthPitch* [in]

The offset, in bytes, to move to the next depth slice of source data.

## -remarks

The driver can use the <a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb">pfnSetErrorCb</a> callback function to set an error code.






For more information about <i>DefaultConstantBufferUpdateSubresourceUP</i>, see the Remarks section of the <a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceupdatesubresourceup">ResourceUpdateSubresourceUP</a> function.

The driver should not encounter any error, except for D3DDDIERR_DEVICEREMOVED. Therefore, if the driver passes any error, except for D3DDDIERR_DEVICEREMOVED, in a call to the <a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb">pfnSetErrorCb</a> function, the Direct3D runtime will determine that the error is critical. Even if the device was removed, the driver is not required to return D3DDDIERR_DEVICEREMOVED; however, if device removal interfered with the operation of <i>DefaultConstantBufferUpdateSubresourceUP</i> (which typically should not happen), the driver can return D3DDDIERR_DEVICEREMOVED.

## -see-also

<a href="/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs">D3D10DDI_DEVICEFUNCS</a>



<a href="/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_ddi_box">D3D10_DDI_BOX</a>



<a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourceupdatesubresourceup">ResourceUpdateSubresourceUP</a>



<a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb">pfnSetErrorCb</a>

