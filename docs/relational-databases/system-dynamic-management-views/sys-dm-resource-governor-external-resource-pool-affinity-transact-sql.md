---
title: sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 02ec95d318825c1759067455b62f3dae6a86c184
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053328"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Gilt für:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] und [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Gibt CPU-Affinitäts Informationen über die aktuelle Konfiguration des externen Ressourcenpools zurück.
  
|Spaltenname|Datentyp|BESCHREIBUNG|
|----------------|---------------|-----------------|
|pool_id|**int**|Die ID des externen Ressourcenpools. Lässt keine NULL-Werte zu.|
|processor_group|**smallint**|Die ID der logischen Windows-Prozessorgruppe. Lässt keine NULL-Werte zu.|
|cpu_mask|**BIGINT**|Die binäre Maske, die die diesem Pool zugeordneten CPUs darstellt. Lässt keine NULL-Werte zu.|
  
## <a name="remarks"></a>Bemerkungen

Pools, die mit einer Affinität von `AUTO` erstellt werden, werden in dieser Sicht nicht angezeigt, weil Sie keine Affinität haben. Weitere Informationen finden Sie unter [Erstellen eines externen Ressourcenpools &#40;Transact-SQL-&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) und [Alter externer Ressourcenpool &#40;Transact-SQL-&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) Anweisungen.

## <a name="permissions"></a>Berechtigungen

Erfordert die `VIEW SERVER STATE`-Berechtigung.

## <a name="see-also"></a>Weitere Informationen

[Ressourcenkontrolle für Machine Learning in SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)

[sys. dm_resource_governor_resource_pool_affinity &#40;Transact-SQL-&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Externe Skripts aktiviert – Serverkonfigurationsoption](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[Alter externer Ressourcen Pool &#40;Transact-SQL-&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
