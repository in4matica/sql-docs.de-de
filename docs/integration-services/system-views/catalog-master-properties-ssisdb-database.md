---
title: catalog.master_properties (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3ce06430094825bf3268836657661930fea058e4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296623"
---
# <a name="catalogmaster_properties-ssisdb-database"></a>catalog.master_properties (SSISDB-Datenbank)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Zeigt die Eigenschaften des ausgewählten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Masters an.

|Spaltenname|Datentyp|BESCHREIBUNG|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Der Name der Scale Out-Mastereigenschaft.|  
|property_value|**nvarchar(max)**|Der Wert der Scale Out-Mastereigenschaft.|

## <a name="remarks"></a>Bemerkungen
In dieser Sicht wird für jede Scale Out-Mastereigenschaft eine Zeile angezeigt. In dieser Sicht werden folgende Eigenschaften angezeigt:

|Eigenschaftenname|BESCHREIBUNG|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|Die SQL Server-Instanz, die die Protokolldatenbank enthält.|
|**LAST_ONLINE_TIME**|Zeitpunkt, zu dem der Scale Out-Master zuletzt online war.|
|**MACHINE_IP**|Die IP-Adresse des Computers.|
|**MACHINE_NAME**|Der Name des Computers.|
|**MASTER_ADDRESS**|Der Endpunkt des Scale Out-Masters.|
|**MASTER_SERVICE_PORT**|Der Port im Endpunkt des Scale Out-Masters.|
|**SSLCERT_THUMBPRINT**|Der Fingerabdruck des Scale Out-Masterzertifikats.|

## <a name="permissions"></a>Berechtigungen
Alle Mitglieder der öffentlichen Datenbankrolle besitzen die Leseberechtigung für diese Sicht. 
