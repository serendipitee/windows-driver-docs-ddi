---
UID: NS:d3dkmdt._DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
title: _DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS (d3dkmdt.h)
description: The DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS structure contains parameters that are used to retrieve information from a protected output object in a call to the DxgkDdiOPMGetCOPPCompatibleInformation function.
old-location: display\dxgkmdt_opm_copp_compatible_get_info_parameters.htm
tech.root: display
ms.date: 05/10/2018
keywords: ["DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS structure"]
ms.keywords: "*PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS, DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS, DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS structure [Display Devices], DmStructs_2e356de0-a1ca-4f75-a3f2-c72be3bdf87f.xml, PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS, PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS structure pointer [Display Devices], _DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS, d3dkmdt/DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS, d3dkmdt/PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS, display.dxgkmdt_opm_copp_compatible_get_info_parameters"
req.header: d3dkmdt.h
req.include-header: 
req.target-type: Windows
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
req.irql: 
targetos: Windows
req.typenames: DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS, *PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
f1_keywords:
 - _DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
 - d3dkmdt/_DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
 - PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
 - d3dkmdt/PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
 - DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
 - d3dkmdt/DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - HeaderDef
api_location:
 - d3dkmdt.h
api_name:
 - _DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
 - PDXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
 - DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS
---

# _DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS structure


## -description

The DXGKMDT_OPM_COPP_COMPATIBLE_GET_INFO_PARAMETERS structure contains parameters that are used to retrieve information from a protected output object in a call to the <a href="/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information">DxgkDdiOPMGetCOPPCompatibleInformation</a> function.

## -struct-fields

### -field rnRandomNumber

A <a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_random_number">DXGKMDT_OPM_RANDOM_NUMBER</a> structure that contains a protected output object's 128-bit cryptographically secure random number. This random number is generated by an application and supplied to the display miniport driver in <b>rnRandomNumber</b> in a call to the driver's <a href="/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information">DxgkDdiOPMGetCOPPCompatibleInformation</a> function.

### -field guidInformation

The GUID that is used to retrieve the information. <b>guidInformation</b> can be set to one of the following GUIDs:

<ul>
<li>
DXGKMDT_OPM_GET_CONNECTED_HDCP_DEVICE_INFORMATION

</li>
<li>
DXGKMDT_OPM_GET_CONNECTOR_TYPE

</li>
<li>
DXGKMDT_OPM_GET_SUPPORTED_PROTECTION_TYPES

</li>
<li>
DXGKMDT_OPM_GET_VIRTUAL_PROTECTION_LEVEL

</li>
<li>
DXGKMDT_OPM_GET_ACTUAL_PROTECTION_LEVEL

</li>
<li>
DXGKMDT_OPM_GET_ACTUAL_OUTPUT_FORMAT

</li>
<li>
DXGKMDT_OPM_GET_ADAPTER_BUS_TYPE

</li>
<li>
DXGKMDT_OPM_GET_ACP_AND_CGMSA_SIGNALING

</li>
</ul>

### -field ulSequenceNumber

A sequence number. For the <a href="/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information">DxgkDdiOPMGetCOPPCompatibleInformation</a> function to process an information request, the value in <b>ulSequenceNumber</b> must match the current 4-byte sequence number that the display miniport driver stores. If a match is not detected, <i>DxgkDdiOPMGetCOPPCompatibleInformation</i> returns an error code. If a match is detected, <i>DxgkDdiOPMGetCOPPCompatibleInformation</i> increments the stored sequence number before returning. The initial 4-byte sequence number was part of the 256-byte array that the <i>EncryptedParameters</i> parameter of the <a href="/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers">DxgkDdiOPMSetSigningKeyAndSequenceNumbers</a> function pointed to.

### -field cbParametersSize

The size, in bytes, of the valid data that the <b>abParameters</b> member points to.

### -field abParameters

A 4056-byte array that contains the data that accompanies the information request that is identified by the <b>guidInformation</b> member. 

No data is required for the DXGKMDT_OPM_GET_CONNECTOR_TYPE, DXGKMDT_OPM_GET_SUPPORTED_PROTECTION_TYPES, DXGKMDT_OPM_GET_ACTUAL_OUTPUT_FORMAT, DXGKMDT_OPM_GET_CONNECTED_HDCP_DEVICE_INFORMATION, DXGKMDT_OPM_GET_ADAPTER_BUS_TYPE, and DXGKMDT_OPM_GET_ACP_AND_CGMSA_SIGNALING requests.

The DXGKMDT_OPM_GET_ACTUAL_PROTECTION_LEVEL and DXGKMDT_OPM_GET_VIRTUAL_PROTECTION_LEVEL requests require data that identifies the protection type that the protection level is requested for. Therefore, these requests require that the first 4 bytes in the <b>abParameters</b> array contain the protection type.

## -see-also

<a href="/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_random_number">DXGKMDT_OPM_RANDOM_NUMBER</a>



<a href="/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information">DxgkDdiOPMGetCOPPCompatibleInformation</a>

