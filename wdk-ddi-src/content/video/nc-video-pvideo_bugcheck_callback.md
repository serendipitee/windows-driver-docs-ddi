---
UID: NC:video.PVIDEO_BUGCHECK_CALLBACK
title: PVIDEO_BUGCHECK_CALLBACK (video.h)
description: The HwVidBugcheckCallback function enables the miniport driver to append data to a dump file when a bug check occurs.
old-location: display\hwvidbugcheckcallback.htm
tech.root: display
ms.date: 05/10/2018
keywords: ["PVIDEO_BUGCHECK_CALLBACK callback function"]
ms.keywords: HwVidBugcheckCallback, HwVidBugcheckCallback callback function [Display Devices], PVIDEO_BUGCHECK_CALLBACK, PVIDEO_BUGCHECK_CALLBACK callback, VideoMiniport_Functions_d3dcce93-d172-4948-8cc5-395dd2a1f9a5.xml, display.hwvidbugcheckcallback, video/HwVidBugcheckCallback
req.header: video.h
req.include-header: Video.h
req.target-type: Desktop
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
req.typenames: 
f1_keywords:
 - PVIDEO_BUGCHECK_CALLBACK
 - video/PVIDEO_BUGCHECK_CALLBACK
topic_type:
 - APIRef
 - kbSyntax
api_type:
 - UserDefined
api_location:
 - video.h
api_name:
 - PVIDEO_BUGCHECK_CALLBACK
---

# PVIDEO_BUGCHECK_CALLBACK callback function


## -description

The <i>HwVidBugcheckCallback</i> function enables the miniport driver to append data to a dump file when a bug check occurs.

## -parameters

### -param HwDeviceExtension [in]


Pointer to the miniport driver's per-adapter storage area. For more information, see <a href="/windows-hardware/drivers/kernel/device-extensions">Device Extensions</a>.

### -param BugcheckCode [in]


Specifies a <a href="/windows-hardware/drivers/debugger/bug-check-code-reference2">bug check code</a>.

### -param Buffer [in]


Pointer to the memory location where the miniport driver can store the data that is to be appended to the dump file.

### -param BufferSize [in]


Specifies the size, in bytes, of the buffer pointed to by the <i>Buffer</i> parameter.

## -remarks

This function is available in Windows XP SP1 and later. 

This function is called when a bug check occurs. The miniport driver can collect data that is to be appended to the dump file and write this data to the buffer. The driver must not write more than <i>BufferSize</i> bytes to the buffer.

A video miniport driver registers the <i>HwVidBugcheckCallback</i> function by calling the <a href="/windows-hardware/drivers/ddi/video/nf-video-videoportregisterbugcheckcallback">VideoPortRegisterBugcheckCallback</a> function. The <b>VideoPortRegisterBugcheckCallback</b> function exposes this video miniport driver-supplied callback to the system.

To facilitate system recovery after a bug check, any registers that are accessed by this function must not impede the ability of the hardware to transfer to fallback mode, regardless of the state of the device. Also, the function <i>must</i> return control to its caller.

Because a system can consist of multiple video miniport drivers, vendors should add an identifying string to the data that this function appends to the dump file. 

The function is called at raised IRQL and must not attempt to access pageable code or data.

## -see-also

<a href="/windows-hardware/drivers/ddi/video/nf-video-videoportregisterbugcheckcallback">VideoPortRegisterBugcheckCallback</a>

