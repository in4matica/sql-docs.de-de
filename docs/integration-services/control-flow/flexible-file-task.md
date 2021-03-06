---
title: Flexibler Dateitask | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4ed8ba34e8e50d6414d68cae4aa386848f88b6d5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "72807413"
---
# <a name="flexible-file-task"></a>Flexibler Dateitask

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Der flexible Dateitask ermöglicht Benutzern das Ausführen von Dateivorgängen für verschiedene unterstützte Speicherdienste.
Zurzeit unterstützte Speicherdienste:

- Lokales Dateisystem
- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

Der flexible Dateitask ist eine Komponente des [SQL Server Integration Services Feature Pack (SSIS) für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Ziehen Sie den flexiblen Dateitask aus der SSIS-Toolbox auf die Designercanvas, um diesen einem Paket hinzuzufügen. Doppelklicken Sie anschließend auf den Task, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie auf **Bearbeiten**, um das Dialogfeld **Flexibler Dateitask-Editor** zu öffnen.

Mit der **Operation**-Eigenschaft wird der auszuführende Dateivorgang angegeben.
Zurzeit werden folgende Vorgänge unterstützt:
- **Kopiervorgang**
- **Löschvorgang**

Die folgenden Eigenschaften sind für den **Kopiervorgang** verfügbar.

- **SourceConnectionType:** Gibt den Typ des Quellverbindungs-Managers an.
- **SourceConnection:** Gibt den Quellverbindungs-Manager an.
- **SourceFolderPath:** Gibt den Pfad des Quellordners an.
- **SourceFileName:** Gibt den Namen der Quelldatei an. Wenn diese Angabe leer gelassen wird, wird der Quellordner kopiert.
- **SearchRecursively:** Gibt an, ob Unterordner rekursiv kopiert werden sollen.
- **DestinationConnectionType:** Gibt den Typ des Zielverbindungs-Managers an.
- **DestinationConnection:** Gibt den Zielverbindungs-Manager an.
- **DestinationFolderPath:** Gibt den Pfad des Zielordners an.
- **DestinationFileName:** Gibt den Namen der Zieldatei an.

Die folgenden Eigenschaften sind für den **Löschvorgang** verfügbar.
- **ConnectionType:** Gibt den Typ des Verbindungs-Managers an.
- **Connection:** Gibt den Verbindungs-Manager an.
- **FolderPath:** Gibt den Ordnerpfad an.
- **FileName:** Gibt den Dateinamen an. Wenn diese Angabe leer gelassen wird, wird der Ordner gelöscht. Für Azure Blob Storage wird das Löschen des Ordners nicht unterstützt.

***Hinweise zur Konfiguration der Dienstprinzipalberechtigung***

Damit die **Testverbindung** funktioniert (Blob Storage oder Data Lake Storage Gen2), müssen Sie dem Dienstprinzipal mindestens die Rolle **Storage-Blobdatenleser** zuweisen.
Dies erfolgt mit der [RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal).

Blob-Speicher-, Lese- und Schreibberechtigungen werden durch das Zuweisen der jeweiligen **Storage Blob Data Reader**- (Storage-Blobdatenleser) und **Storage Blob Data Contributor**-Rollen (Mitwirkender an Storage-Blobdaten) gewährt.

Für Data Lake Storage Gen2 wird die Berechtigung durch die RBAC und [ACLs](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer) bestimmt.
Beachten Sie, dass ACLs wie [hier](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal) beschrieben mithilfe der Objekt-ID (OID) des Dienstprinzipals für die App-Registrierung konfiguriert werden.
Dies unterscheidet sich von der Anwendungs-ID (Client-ID), die mit der RBAC-Konfiguration verwendet wird.
Wenn ein Sicherheitsprinzipal durch eine integrierte Rolle oder eine benutzerdefinierte Rolle RBAC-Datenberechtigungen erhält, werden diese Berechtigungen vor der Autorisierung einer Anforderung zunächst ausgewertet.
Wenn der Anforderungsvorgang von den RBAC-Zuweisungen des Sicherheitsprinzipals autorisiert wurde, wird die Autorisierung sofort aufgelöst, und es werden keine weiteren ACL-Prüfungen durchgeführt.
Wenn der Sicherheitsprinzipal über keine RBAC-Zuweisung verfügt oder der Vorgang der Anforderung nicht mit der zugewiesenen Berechtigung übereinstimmt, werden alternativ ACL-Prüfungen durchgeführt, um zu bestimmen, ob der Sicherheitsprinzipal für die Durchführung des angeforderten Vorgangs autorisiert ist.

- Für die Leseberechtigung müssen Sie mindestens die Berechtigung **Execute** (Ausführen) ab dem Quelldateisystem sowie die Berechtigung **Read** (Lesen) für die zu kopierenden Dateien gewähren. Gewähren Sie alternativ mindestens die Rolle **Storage-Blobdatenleser** mit der RBAC.
- Für die Schreibberechtigung müssen Sie mindestens die Berechtigung **Execute** (Ausführen) ab dem Senkedateisystem sowie die Berechtigung **Write** (Schreiben) für den Senkeordner gewähren. Gewähren Sie alternativ mindestens die Rolle **Storage Blob Data Contributor** (Mitwirkender an Storage-Blobdaten) mit der RBAC.

Weitere Informationen finden Sie in [diesem Artikel](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control).
