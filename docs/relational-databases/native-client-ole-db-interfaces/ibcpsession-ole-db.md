---
title: IBCPSession (OLE DB) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f3ea8d1e52ba5fc4d34f5bee1c728ff7ca3db2d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "73789576"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Die **IBCPSession**-Schnittstelle unterstützt dateibasierte Massenkopiervorgänge für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die **IBCPSession** Schnittstelle wird im OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client auf derselben Ebene wie Session-Objekte verfügbar gemacht. Im OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sind Datenquellenobjekte Factorys für Session-Objekte, und Massenkopiervorgänge werden in der Verbindungseigenschaft SSPROP_ENABLEBULKCOPY angegeben. Außerdem sollte die SSPROP_ENABLEFASTLOAD-Eigenschaft auf true festgelegt werden.  
  
 Ein Aufruf der **IDBCreateSession::CreateSession** -Methode führt dann zur Erstellung eines **BulkCopySession** -Objekts. Alle durch das **IBCPSession** -Objekt verfügbar gemachten dateibasierten Massenkopiermethoden sind mit einer ganz ähnlichen Syntax über die **IBCPSession** -Schnittstelle dieses **IBCPSession** -Objekts aufrufbar.  
  
> [!NOTE]  
>  Der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unterstützt speicherbasierte Massenkopiervorgänge durch die [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) -Schnittstelle.  
  
 Weitere Informationen zur Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-OLE DB Anbieters für Massen Kopiervorgänge finden Sie unter [Durchführen von Massen Kopier Vorgängen](../../relational-databases/native-client/features/performing-bulk-copy-operations.md).  
  
 Ein Beispiel für die Verwendung der **IBCPSession** -Schnittstelle finden Sie unter ' [IBCPSession:: BCPDone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Methode|BESCHREIBUNG|  
|------------|-----------------|  
|[IBCPSession:: bcpcolf MT &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|Erstellt eine Bindung zwischen Programmvariablen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Spalten.|  
|[IBCPSession:: BCPColumns &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|Legt die Anzahl von Feldern fest, die an die Spalten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle gebunden werden sollen.|  
|[IBCPSession:: BCPControl &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|Legt die Optionen für einen Massenkopiervorgang fest.|  
|[IBCPSession:: BCPDone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|Führt einen Commit für die übrigen Zeilen aus, die an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gesendet werden sollen.|  
|[IBCPSession:: BCPExec &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|Führt den Massenkopiervorgang aus.|  
|[IBCPSession:: BCPInit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|Initialisiert die Massenkopierstruktur, führt einige Fehlerprüfungen durch, überprüft die korrekte Angabe der Daten- und Formatdateinamen und öffnet dann diese Dateien.|  
|[IBCPSession:: bcpreadf-&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|Liest für jede Spalte Formatinformationen aus der Formatdatei.|  
|[IBCPSession:: bcpschreitef &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|Schreibt für jede Spalte Formatinformationen in die Formatdatei.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Schnittstellen &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
