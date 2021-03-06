---
title: Verwenden der transparenten Netzwerk-IP-Adressauflösung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2020
ms.locfileid: "68008484"
---
# <a name="using-transparent-network-ip-resolution"></a>Verwenden der transparenten Netzwerk-IP-Adressauflösung
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

Die transparente Netzwerk-IP-Adressauflösung ist eine im Microsoft ODBC-Treiber 13.1 für SQL Server verfügbare Neuauflage des vorhandenen Features für das Multisubnetz-Failover und wirkt sich auf die Verbindungssequenz des Treibers aus, wenn die erste aufgelöste IP-Adresse des Hostnamens nicht reagiert und dem Hostnamen mehrere IP-Adressen zugeordnet sind. Sie interagiert mit dem Multisubnetz-Failover, um die folgenden drei Verbindungssequenzen bereitzustellen:

* 0: Erst wird eine IP-Adresse ausprobiert, dann alle IP-Adressen gleichzeitig.
* 1: Die IP-Adressen werden alle gleichzeitig ausprobiert.
* 2: Die IP-Adressen werden alle nacheinander ausprobiert.

|TransparentNetworkIPResolution|MultiSubnetFailover|Verhalten|
|:-:|:-:|:-:|
|(Standard)|(Standard)|0|
|(Standard)|Aktiviert|1|
|(Standard)|Disabled|0|
|Aktiviert|(Standard)|0|
|Aktiviert|Aktiviert|1|
|Aktiviert|Disabled|0|
|Disabled|(Standard)|2|
|Disabled|Aktiviert|1|
|Disabled|Disabled|2|

Auf Ebene der Verbindungszeichenfolge wird diese Einstellung über `TransparentNetworkIPResolution` als Verbindungszeichenfolge und DSN-Schlüsselwort gesteuert. Die Standardeinstellung ist aktiviert.

Schlüsselwort|Werte|Standard
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

Mithilfe des Vorverbindungsattributs `SQL_COPT_SS_TNIR` können Anwendungen diese Einstellung programmgesteuert steuern:

Verbindungsattribut|   Größe/Typ|  Standard| value| Beschreibung
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` oder `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Dieses Attribut aktiviert oder deaktiviert die transparente Netzwerk-IP-Adressauflösung.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>Weitere Informationen zu MultiSubnetFailover finden Sie unter [Der ODBC-Treiber unter Linux und macOS für Hochverfügbarkeit und Notfallwiederherstellung](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).
--------------------------------------------------
## <a name="see-also"></a>Weitere Informationen  
* [Microsoft ODBC Driver for SQL Server unter Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server-Multisubnetzclustering (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
