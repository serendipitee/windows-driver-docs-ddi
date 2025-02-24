---
UID: NS:d3d12umddi.D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095
tech.root: display
title: D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095
ms.date: 05/14/2024
targetos: Windows
description: Learn more about the D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095 structure.
prerelease: false
req.construct-type: structure
req.ddi-compliance: 
req.dll: 
req.header: d3d12umddi.h
req.include-header: 
req.kmdf-ver: 
req.lib: 
req.max-support: 
req.redist: 
req.target-min-winverclnt: Windows 11, version 24H2 (WDDM 3.2)
req.target-min-winversvr: 
req.target-type: 
req.typenames: D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095
typedef_isUnnamed: false
req.umdf-ver: 
req.unicode-ansi: 
topic_type:
 - apiref
api_type:
 - HeaderDef
api_location:
 - d3d12umddi.h
api_name:
 - D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095
f1_keywords:
 - D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095
 - d3d12umddi/D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095
dev_langs:
 - c++
helpviewer_keywords:
 - D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095
---

## -description

The **D3D12DDI_VIDEO_ENCODER_AV1_SEGMENT_DATA_0095** structure contains segmentation data for a segment within an AV1 frame.

## -struct-fields

### -field EnabledFeatures

A bit mask combination of [**D3D12DDI_VIDEO_ENCODER_AV1_SEGMENTATION_MODE_0095_FLAGS**](ne-d3d12umddi-d3d12ddi_video_encoder_av1_segmentation_mode_0095_flags.md) values that indicates the segmentation modes that are enabled for the segment.

### -field FeatureValue[8]

For the enabled features in the **EnabledFeatures** bit mask, the array **FeatureValue** is indexed by [**D3D12DDI_VIDEO_ENCODER_AV1_SEGMENTATION_MODE_0095**](ne-d3d12umddi-d3d12ddi_video_encoder_av1_segmentation_mode_0095.md) - 1 for its associated feature value.

## -remarks

See [D3D12 AV1 video encoding](/windows-hardware/drivers/display/video-encoding-d3d12-av1) for more information.

## -see-also

[**D3D12DDI_VIDEO_ENCODER_AV1_SEGMENTATION_CONFIG_0095**](ns-d3d12umddi-d3d12ddi_video_encoder_av1_segmentation_config_0095.md)
