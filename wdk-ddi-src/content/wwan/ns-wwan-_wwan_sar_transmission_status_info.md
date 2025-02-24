---
UID: NS:wwan._WWAN_SAR_TRANSMISSION_STATUS_INFO
title: _WWAN_SAR_TRANSMISSION_STATUS_INFO (wwan.h)
description: The WWAN_SAR_TRANSMISSION_STATUS_INFO structure describes a mobile broadband (MBB) modem's Specific Absorption Rate (SAR) transmission status.
tech.root: netvista
ms.date: 08/20/2018
keywords: ["WWAN_SAR_TRANSMISSION_STATUS_INFO structure"]
ms.keywords: _WWAN_SAR_TRANSMISSION_STATUS_INFO, WWAN_SAR_TRANSMISSION_STATUS_INFO, *PWWAN_SAR_TRANSMISSION_STATUS_INFO,
req.header: wwan.h
req.include-header: 
req.target-type: 
req.target-min-winverclnt: Windows 10, version 1703
req.target-min-winversvr: 
req.kmdf-ver: 
req.umdf-ver: 
req.lib: 
req.dll: 
req.ddi-compliance: 
req.unicode-ansi: 
req.max-support: 
req.typenames: WWAN_SAR_TRANSMISSION_STATUS_INFO, *PWWAN_SAR_TRANSMISSION_STATUS_INFO
targetos: Windows
ms.custom: RS5
f1_keywords:
 - _WWAN_SAR_TRANSMISSION_STATUS_INFO
 - wwan/_WWAN_SAR_TRANSMISSION_STATUS_INFO
 - PWWAN_SAR_TRANSMISSION_STATUS_INFO
 - wwan/PWWAN_SAR_TRANSMISSION_STATUS_INFO
 - WWAN_SAR_TRANSMISSION_STATUS_INFO
 - wwan/WWAN_SAR_TRANSMISSION_STATUS_INFO
topic_type:
 - apiref
api_type:
 - HeaderDef
api_location:
 - wwan.h
api_name:
 - _WWAN_SAR_TRANSMISSION_STATUS_INFO
 - PWWAN_SAR_TRANSMISSION_STATUS_INFO
 - WWAN_SAR_TRANSMISSION_STATUS_INFO
---

# _WWAN_SAR_TRANSMISSION_STATUS_INFO structure


## -description

The **WWAN_SAR_TRANSMISSION_STATUS_INFO** structure describes a mobile broadband (MBB) modem's Specific Absorption Rate (SAR) transmission status.

## -struct-fields

### -field ChannelNotification

A [**WWAN_SAR_TRANSMISSION_STATUS_NOTIFICATION_STATE**](ne-wwan-_wwan_sar_transmission_status_notification_state.md) value that specifies whether SAR transmission status notifications are enabled or disabled for the modem.

### -field TransmissionStatus

A [**WWAN_SAR_TRANSMISSION_STATUS**](ne-wwan-_wwan_sar_transmission_status.md) value that describes whether the modem has transmit (Tx) traffic during the hysteresis timer.

### -field HysteresisTimer

A Hysteresis indicator that is used by the modem to determine when to send a [NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](/windows-hardware/drivers/network/ndis-status-wwan-sar-transmission-status) notification to the host. This value is the timer the modem sees as a continuous no-transmit activity before it sends an OFF indicator to host. This timer should be set in seconds, ranging from 1 second to 5 seconds.

## -remarks

This structure is used in the [**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](../ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info.md) structure.

## -see-also

[MB SAR Platform Support](/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_TRANSMISSION_STATUS](/windows-hardware/drivers/network/oid-wwan-sar-transmission-status)

[NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](/windows-hardware/drivers/network/ndis-status-wwan-sar-transmission-status)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](../ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info.md)

[**WWAN_SAR_TRANSMISSION_STATUS_NOTIFICATION_STATE**](ne-wwan-_wwan_sar_transmission_status_notification_state.md)

[**WWAN_SAR_TRANSMISSION_STATUS**](ne-wwan-_wwan_sar_transmission_status.md)

