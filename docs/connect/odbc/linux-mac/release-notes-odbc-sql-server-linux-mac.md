---
title: Versionshinweise zur ODBC für Linux und macOS | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/30/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-jizho2
ms.technology: connectivity
ms.topic: conceptual
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 39e010f87b9cf0785ba025cfb8a9cf96825ae9d9
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896762"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-to-sql-server-on-linux-and-macos"></a>Versionshinweise zu Microsoft ODBC Driver for SQL Server für Linux und macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

In diesem Artikel werden die Neuerungen der Releases der Versionen des [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für Linux und macOS aufgeführt und beschrieben.

<!--
Going forward, please use the new 2-column markdown table for each new H2 version section.
And we are keeping the H2 titles much shorter, partly by removing redundant or obvious info.
We want to track the Month YYYY each new version H2 section is added, at the end of the H2 title.
This is the new standard format for Release Notes article content.

OLD     FILE NAME:    linux-mac/release-notes.md
NOW NEW FILE NAME:    linux-mac/release-notes-odbc-sql-server-linux-mac.md

Thank you.
GeneMi.  2019/04/03.
-->

## <a name="1752-march-2020"></a>17.5.2, März 2020

| Neues Feature | Details |
| :------------ | :------ |
| Unterstützung für die Authentifizierung mit einer verwalteten Identität bei Azure Key Vault | Siehe [Verwenden von Always Encrypted mit dem ODBC-Treiber](../using-always-encrypted-with-the-odbc-driver.md). |
| Unterstützung für zusätzliche Azure Key Vault-Endpunkte | Siehe [Verwenden von Always Encrypted mit dem ODBC-Treiber](../using-always-encrypted-with-the-odbc-driver.md). |
| Fehlerbehebungen. | Siehe [Fehlerbehebungen](../bug-fixes.md) |
| &nbsp; | &nbsp; |

## <a name="175-january-2020"></a>Version 17.5, Januar 2020

| Neues Feature | Details |
| :------------ | :------ |
| SQL_COPT_SS_SPID-Verbindungsattribut zum Abrufen der SPID ohne Roundtrip zum Server | Siehe [Schlüsselwörter und Attribute von DSN- und Verbindungszeichenfolgen](../dsn-connection-string-attribute.md). |
| Unterstützung für das Angeben der EULA-Annahme über `debconf` in Debian und Ubuntu. | Siehe [Installieren des Treibers](./installing-the-microsoft-odbc-driver-for-sql-server.md). |
| Neue Verteilungen werden unterstützt | &bull; &nbsp; &nbsp; Alpine Linux (3.10, 3.11)<br/>&bull; &nbsp; &nbsp; Oracle Linux 8<br/>&bull; &nbsp; &nbsp; Ubuntu 19.10<br/>&bull; &nsbp; &nbsp; macOS 10.15 |
| Fehlerbehebungen. | Siehe [Fehlerbehebungen](../bug-fixes.md) |
| &nbsp; | &nbsp; |

## <a name="1742-october-2019"></a>17.4.2, Oktober 2019

| Neues Feature | Details |
| :------------ | :------ |
| Unterstützung für zusätzliche Azure Key Vault-Endpunkte | Siehe [Verwenden von Always Encrypted mit dem ODBC-Treiber](../using-always-encrypted-with-the-odbc-driver.md). |
| Unterstützung für das Festlegen der Datenklassifizierungsversion | Siehe [Data Classification (Datenklassifizierung)](../data-classification.md#bkmk-version) |
| Fehlerbehebungen. | Siehe [Fehlerbehebungen](../bug-fixes.md) |
| &nbsp; | &nbsp; |

**Bekanntes Problem:**

Bei Verwendung von Always Encrypted mit Secure Enclaves und Azure Key Vault können ungewöhnliche Schlüsselpfadlängen zu Fehlern bei der CMK-Signaturverifizierung führen. Wenn dieses Problem auftritt, sollten Sie die Länge des Schlüsselpfads um ein Zeichen verringern oder erhöhen, indem Sie den AKV-Schlüssel umbenennen.

## <a name="174-august-2019"></a>17.4, August 2019

| Neues Feature | Details |
| :------------ | :------ |
| Always Encrypted mit Secure Enclaves. | Siehe [Verwenden von Always Encrypted mit dem ODBC-Treiber](../using-always-encrypted-with-the-odbc-driver.md). |
| Dynamisches Laden von OpenSSL | Siehe [Programmierrichtlinien](programming-guidelines.md#bkmk-openssl). |
| Konfigurierbare TCP-Keep-Alive-Einstellungen. | Siehe [Herstellen einer Verbindung mit SQL Server](connection-string-keywords-and-data-source-names-dsns.md). |
| Fehlerbehebungen. | Siehe [Fehlerbehebungen](../bug-fixes.md) |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>Februar 2019: Version 17.3

| Neues Element | Details |
| :------- | :------ |
| Neue Verteilungen werden unterstützt | &bull; &nbsp; &nbsp; SuSE 15<br/>&bull; &nbsp; &nbsp; Ubuntu 18.10<br/>&bull; &nbsp; &nbsp; macOS 10.14 |
| Authentifizierungsmodus für (systemweite und benutzerseitig zugewiesene) verwaltete Azure Active Directory-Dienstidentitäten | Siehe [Using Azure Active Directory with the ODBC Driver (Verwenden von Azure Active Directory mit dem ODBC-Treiber)](../using-azure-active-directory.md) |
| Übermitteln von Eingabeparametern für Always Encrypted-Spalten | Weitere Informationen finden Sie unter [Limitations of the ODBC driver when using Always Encrypted (Einschränkungen des ODBC-Treibers bei Verwendung von Always Encrypted)](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted) |
| Verteilte XA-Transaktionen | Siehe [Using XA Transactions (Verwenden von XA-Transaktionen)](../use-xa-with-dtc.md)<br/><br/>XA ist ein Akronym für _eXtended Architecture_. Dabei handelt es sich um einen Standard für die Ausführung einer globalen Transaktion, die auf mehrere serverseitige Datenspeichersysteme zugreift. |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>Juli 2018: Version 17.2

| Neues Element | Details |
| :------- | :------ |
| Neue Verteilungen werden unterstützt | &bull; &nbsp; &nbsp; Ubuntu 18.04 |
| Datenklassifizierung für Azure SQL-Datenbank und SQL Server | Siehe [Data Classification (Datenklassifizierung)](../data-classification.md) |
| Unterstützung der UTF-8-Servercodierung | &nbsp; |
| `SQLBrowseConnect` | &nbsp; |
| Dynamische Abhängigkeit von `libcurl` | Ab dieser Version stellt das `libcurl`-Paket keine explizite Abhängigkeit dar.<br/>Das `libcurl`-Paket für OpenSSL oder NSS ist bei der Verwendung der Azure Key Vault- oder Azure Active Directory-Authentifizierung erforderlich.<br/>Wenn im Bezug zu `libcurl` ein Fehler auftritt, überprüfen Sie ob es installiert ist. |
| Resilienz von Verbindungen im Leerlauf mit den Schlüsselwörtern „ConnectRetryCount“ und „ConnectRetryInterval“ in der Verbindungszeichenfolge wurde hinzugefügt | &bull; &nbsp; &nbsp; Verwenden Sie `SQL_COPT_SS_CONNECT_RETRY_COUNT` (schreibgeschützt), um die Anzahl der Versuche zum Wiederherstellen der Verbindung abzurufen.<br/><br/>&bull; &nbsp; &nbsp; Verwenden Sie `SQL_COPT_SS_CONNECT_RETRY_INTERVAL` (schreibgeschützt), um die Länge des Intervalls zum Wiederherstellen der Verbindung abzurufen.<br/><br/>Siehe [Connection Resiliency in the Windows ODBC Driver (Verbindungsresilienz im Windows ODBC-Treiber)](../windows/connection-resiliency-in-the-windows-odbc-driver.md) |
| Fehlerbehebungen. | Siehe [Fehlerbehebungen](../bug-fixes.md) |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>März 2018: Version 17.1

| Neues Element | Details |
| :------- | :------ |
| Unterstützung der Verbindungsattribute `SQL_COPT_SS_CEKCACHETTL` und `SQL_COPT_SS_TRUSTEDCMKPATHS` | &bull; &nbsp; &nbsp; `SQL_COPT_SS_CEKCACHETTL` ermöglicht das Steuern und Leeren der Zeit, für die der lokale Cache von Spaltenverschlüsselungsschlüsseln vorhanden ist.<br/><br/>&bull; &nbsp; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS` ermöglicht der Anwendung das Einschränken von Always Encrypted-Vorgängen, sodass diese nur die festgelegte Liste von Spaltenhauptschlüsseln nutzen.<br/><br/>Siehe [Using Always Encrypted with the ODBC Driver for SQL Server (Verwenden von Always Encrypted mit dem ODBC Driver for SQL Server)](../using-always-encrypted-with-the-odbc-driver.md) |
| Unterstützung für das Laden von `.rll` aus dem Standardspeicherort | Weitere Informationen finden Sie im [Abschnitt „Laden von Ressourcendateien“ der Dokumentation der Installation](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading) |
| Fehlerbehebungen. | Siehe [Fehlerbehebungen](../bug-fixes.md) |
| &nbsp; | &nbsp; |

## <a name="17"></a>17

**Neue unterstützte Verteilungen:** macOS High Sierra und Ubuntu 17.10 

**Leistungsverbesserungen**: Die Leistung bei der Konvertierung von und in UTF-8/16 wurde um das Zehnfache verbessert.

**Neue Features:**

Always Encrypted-Unterstützung für die BCP-API

Das neue Verbindungszeichenfolgenattribut „UseFMTOnly“ bewirkt, dass der Treiber in besonderen Fällen ältere Metadaten verwendet, die temporäre Tabellen erfordern.

Unterstützung für verwaltete Azure SQL-Instanzen (verlängerte private Vorschau) 
> [!NOTE]
> Bei der Verwendung verwalteter Instanzen gibt es einige Unterschiede:
> -   FILESTREAM wird nicht unterstützt 
> -   Der Zugriff auf das lokale Dateisystem wird nicht unterstützt, ist jedoch für Dinge wie Ablaufverfolgungsdateien erforderlich 
> -   Das Erstellen von benutzerdefinierten Typen aus lokalen Pfaden wird nicht unterstützt 
> -   Die integrierte Windows-Authentifizierung wird nicht unterstützt 
> -   DTC wird nicht unterstützt. 
> -   Das Konto „sa“ ist nicht vorhanden (das Standardkonto heißt „cloudSA“)
> -   Fehler beim TDS-Token (0xAA) gibt einen falschen Servernamen zurück
> -   Sonderzeichen werden im Datenbanknamen nicht unterstützt 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] wird nicht unterstützt
> -   Fehlermeldungen werden unabhängig von Ihren Spracheinstellungen immer in englischer Sprache angezeigt (wie bei Azure) 

## <a name="131-for-ssnoversion-on-linux-and-macos-may-2017"></a>Mai 2017: Version 13.1 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unter Linux und macOS

Mit dem ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] wurde Unterstützung für Always Encrypted und Azure Active Directory bei Verwendung mit Microsoft SQL Server 2016 hinzugefügt.

**Neue Verteilungen werden unterstützt:** OS X 10.11 und macOS 10.12 werden im ersten Release des ODBC-Treibers für macOS unterstützt. Ubuntu 16.10 wird jetzt zusammen mit Red Hat 6, 7 und SUSE 12 unterstützt. Jede Plattform verfügt über ein für die Plattform relevantes Paket (RPM oder DEB), um die Installation und Konfiguration zu vereinfachen.  Installationsanweisungen finden Sie unter [Installing the Driver (Installieren des Treibers)](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

**Änderungen bei der Unterstützung des unixODBC-Treiber-Managers 2.3.1**: Der ODBC-Treiber ist nicht mehr von benutzerdefinierten Paketen für den unixODBC-Treiber-Manager (mit Ausnahme von Red Hat 6) abhängig. Stattdessen wird nun der Verteilungspaket-Manager genutzt, um die unixODBC-Abhängigkeit von den Repositorys der Verteilung aufzulösen.

**Unterstützung der BCP-API**: Der ODBC-Treiber für Linux und macOS unterstützt nun die Verwendung der [BCP-API-Funktionen (**bcp_init** usw.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="130-for-ssnoversion-on-linux"></a>Version 13.0 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für Linux

Mit dem Microsoft ODBC Driver 13.0 for SQL Server werden jetzt auch SQL Server 2014 und SQL Server 2016 unterstützt.  

**Neue Verteilungen werden unterstützt:**

Ubuntu wird jetzt zusammen mit Red Hat und SUSE unterstützt. Jede Plattform verfügt über ein für die Plattform relevantes Paket (RPM oder DEB), um die Installation und Konfiguration zu vereinfachen.  Installationsanweisungen finden Sie unter [Installing the Driver (Installieren des Treibers)](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

**Unterstützung des unixODBC-Treiber-Managers 2.3.1**: Zusätzlich zu einem neueren Treiber-Manager gibt es auch ein Paket zum Installieren dieser Abhängigkeit, durch die die Installation und Konfiguration vereinfacht wird.  

**Transparente Netzwerk-IP-Adressauflösung**: Die transparente Netzwerk-IP-Adressauflösung ist eine Neuauflage des vorhandenen Features für das Multisubnetz-Failover, das sich auf die Verbindungssequenz des Treibers auswirkt, wenn die erste aufgelöste IP-Adresse des Hostnamens nicht reagiert und dem Hostnamen mehrere IP-Adressen zugeordnet sind.

**Unterstützung für TLS 1.2**: Microsoft ODBC Driver 13.0 for SQL Server unter Linux unterstützt nun TLS 1.2, wenn eine sichere Kommunikation mit SQL Server verwendet wird.

## <a name="11-for-ssnoversion-on-linux"></a>Version 11 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für Linux

Der ODBC-Treiber unter SUSE Linux (Preview) unterstützt das 64-Bit-SUSE Linux Enterprise 11 Service Pack 2. Weitere Informationen finden Sie unter [Systemanforderungen](../../../connect/odbc/linux-mac/system-requirements.md).  

Der ODBC-Treiber unter Linux unterstützt [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Weitere Informationen finden Sie unter [ODBC Driver on Linux Support for High Availability, Disaster Recovery (Unterstützung des ODBC-Treibers für Linux für Hochverfügbarkeit und Notfallwiederherstellung)](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

Der ODBC-Treiber unter Linux unterstützt Verbindungen mit Microsoft Azure SQL-Datenbanken. Weitere Informationen finden Sie unter [Vorgehensweise: Herstellen einer Verbindung mit einer Azure SQL-Datenbank mithilfe von ODBC](https://msdn.microsoft.com/library/hh974312.aspx).  

Die `-l`-Option (Anmeldungstimeout) wurde zu `bcp` hinzugefügt. Weitere Informationen finden Sie unter [Connecting with **bcp** (Herstellen einer Verbindung mit bcp)](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
