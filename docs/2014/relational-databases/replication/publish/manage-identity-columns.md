---
title: Verwalten von Identitätsspalten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbfad718850df4c66572999735fbee58fb530424
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/08/2020
ms.locfileid: "73882293"
---
# <a name="manage-identity-columns"></a>Verwalten von Identitätsspalten
  In diesem Thema wird beschrieben, wie Identitätsspalten in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]verwaltet werden. Wenn Einfügungen von Abonnenten zurück auf den Verleger repliziert werden, müssen Identitätsspalten verwaltet werden, um zu verhindern, dass der gleiche Identitätswert sowohl dem Abonnenten als auch dem Verleger zugewiesen wird. Die Replikation kann Identitätsbereiche automatisch verwalten, oder Sie können sich dafür entscheiden, Identitätsbereiche manuell zu verwalten.  Informationen über die von der Replikation zur Verfügung gestellten Verwaltungsoptionen für Identitätsbereiche finden Sie unter [Replizieren von Identitätsspalten](replicate-identity-columns.md).  
  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wird eine Tabelle in mehr als einer Veröffentlichung veröffentlicht, müssen Sie für diese Veröffentlichungen die gleichen Verwaltungsoptionen für Identitätsbereiche angeben. Weitere Informationen finden Sie unter „Veröffentlichen von Tabellen in mehreren Veröffentlichungen“ in [Veröffentlichen von Daten und Datenbankobjekten](publish-data-and-database-objects.md).  
  
-   Weitere Informationen zu einer automatisch inkrementierten Zahl, die in mehreren Tabellen verwendet oder aus Anwendungen aufgerufen werden kann, ohne dass auf eine Tabelle verwiesen wird, finden Sie unter [Sequenznummern](../../sequence-numbers/sequence-numbers.md).  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Geben Sie im Assistenten für neue Veröffentlichung im Dialogfeld **Artikeleigenschaften – **Artikel>** auf der Registerkarte \<Properties** eine Verwaltungsoption für Identitätsspalten an. Weitere Informationen zum Zugreifen auf diesen Assistenten finden Sie unter [Erstellen einer Veröffentlichung](create-a-publication.md). Führen Sie im Assistenten für neue Veröffentlichung folgende Aktionen aus:  
  
-   Wenn Sie auf der Seite **Veröffentlichungstyp** die Option **Mergeveröffentlichung** oder **Transaktionsveröffentlichung mit aktualisierbaren Abonnements** auswählen, wählen Sie die automatische oder manuelle Identitätsbereichsverwaltung aus (automatisch, die Standardeinstellung, wird empfohlen). Nach dem Veröffentlichen der Tabelle kann die Eigenschaft nicht geändert werden. Es können jedoch andere, verbundene Eigenschaften geändert werden.  
  
-   Wenn Sie andere Veröffentlichungstypen auswählen, legen Sie die manuelle Identitätsbereichsverwaltung fest.  
  
 Ändern Sie die Identitätsbereiche und Schwellenwerte im Dialogfeld **Artikeleigenschaften - **Artikel>** auf der Registerkarte \<Eigenschaften**. Dieses Dialogfeld ist über das Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** verfügbar. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-an-identity-column-management-option"></a>So geben Sie eine Verwaltungsoption für Identitätsspalten an  
  
1.  Wenn auf dem Verleger eine Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird, die älter als [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ist, wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Veröffentlichungstyp** die Option **Mergeveröffentlichung** oder **Transaktionsveröffentlichung mit aktualisierbaren Abonnements**aus.  
  
2.  Wählen Sie auf der Seite **Artikel** eine Tabelle mit einer Identitätsspalte aus.  
  
3.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Artikels festlegen**.  
  
4.  Legen Sie im Dialogfeld **Artikeleigenschaften - **Artikel>** auf der Registerkarte \<Eigenschaften** im Abschnitt **Identitätsbereichsverwaltung** die Eigenschaft **Identitätsbereiche automatisch verwalten** auf **Automatisch** oder **Manuell** (bei Verlegern, auf denen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird) oder auf **TRUE** oder **FALSE** (bei Verlegern, auf denen eine Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird, die älter als [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ist) fest.  
  
5.  Wenn Sie in Schritt 4 **Automatisch** oder **Wahr** ausgewählt haben, geben Sie Werte für die Optionen der folgenden Tabelle ein. Weitere Informationen zum Verwenden dieser Einstellungen finden Sie im Abschnitt „Zuweisen von Identitätsbereichen“ unter [Replizieren von Identitätsspalten](replicate-identity-columns.md).  
  
    |Option|value|BESCHREIBUNG|  
    |------------|-----------|-----------------|  
    |**Größe des Verleger Bereichs**|Ganze Zahl für die Bereichsgröße (z. B. 20000).|Weitere Informationen finden Sie im Abschnitt „Zuweisen von Identitätsbereichen“ von [Replizieren von Identitätsspalten](replicate-identity-columns.md).|  
    |**Größe des Abonnenten Bereichs**|Ganze Zahl für die Bereichsgröße (z. B. 10000).|Weitere Informationen finden Sie im Abschnitt „Zuweisen von Identitätsbereichen“ von [Replizieren von Identitätsspalten](replicate-identity-columns.md).|  
    |**Bereichs Schwellenwert in Prozent**|Ganze Zahl für Schwellenwert in Prozent (z. B. 90 entspricht 90 %)|Der Prozentsatz der Identitätswerte, die in einem Knoten insgesamt verwendet werden, bevor ein neuer Identitätsbereich zugewiesen wird.<br /><br /> Hinweis: Der Wert muss angeben werden, er wird jedoch nur von Abonnenten verwendet, die Abonnements mit verzögertem Update über eine Warteschlange verwenden, und von Abonnenten für Mergeveröffentlichungen, auf denen [!INCLUDE[ssEW](../../../includes/ssew-md.md)] oder frühere Versionen von anderen SQL Server-Editionen ausgeführt werden. Weitere Informationen finden Sie im Abschnitt „Zuweisen von Identitätsbereichen“ in [Replizieren von Identitätsspalten](replicate-identity-columns.md).|  
    |**Startwert des nächsten Bereichs**|Wert für ganze Zahl. Schreibgeschützt.|Der Wert, bei dem der nächste Bereich beginnt. Wenn der aktuelle Bereich z. B. 5001-6000 lautet, liegt dieser Wert bei 6001.|  
    |**Maximaler Identitäts Wert**|Wert für ganze Zahl. Schreibgeschützt.|Der größte Wert für die Identitätsspalte. Er wird durch den Basisdatentyp der Spalte bestimmt.|  
    |**Inkrement**|Wert für ganze Zahl. Schreibgeschützt.|Die Zahl, um die sich eine Identitätsspalte bei jeder Einfügung erhöhen oder verringern sollte: in der Regel auf 1 festgelegt.|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-modify-identity-ranges-and-thresholds-after-a-table-is-published"></a>So ändern Sie Identitätsbereiche und Schwellenwerte nach dem Veröffentlichen einer Tabelle  
  
1.  Wählen Sie auf der Seite **Artikel** im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** eine Tabelle mit einer Identitätsspalte aus.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Artikels festlegen**.  
  
3.  Geben Sie im Dialogfeld **Artikeleigenschaften - **Artikel>** auf der Registerkarte \<Eigenschaften** im Abschnitt **Identitätsbereichsverwaltung** Werte für eine oder mehrere der folgenden Eigenschaften ein: **Bereichsgröße auf dem Verleger**, **Bereichsgröße auf dem Abonnenten** und **Prozentsatz für Bereichsschwellenwert**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Klicken Sie im Dialogfeld **Veröffentlichungseigenschaften - **Veröffentlichung>** auf \<OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Wenn ein Artikel erstellt wird, können Sie mithilfe gespeicherter Replikationsprozeduren Verwaltungsoptionen für Identitätsbereiche angeben.  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>So aktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)aus. Wenn die zu veröffentlichende Quelltabelle eine Identitätsspalte besitzt, geben Sie für **** identityrangemanagementoption** den Wert \@auto**, für **\@pub_identity_range** den dem Verleger zugewiesenen Bereich von Identitätswerten und für **\@identity_range** den jedem Abonnenten zugewiesenen Bereich von Identitätswerten an. Geben Sie für **\@threshold** den Prozentsatz der gesamten Identitätswerte an, die verwendet werden, bevor ein neuer Identitätsbereich zugewiesen wird. Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](define-an-article.md).  
  
    > [!NOTE]  
    >  Vergewissern Sie sich, dass der Datentyp der Identitätsspalte groß genug ist, um den gesamten, allen Abonnenten zugewiesenen Identitätsbereich zu unterstützen.  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>So deaktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)aus. Geben Sie für **** identityrangemanagementoption** den Wert \@manual** an. Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](define-an-article.md).  
  
2.  Weisen Sie auf dem Abonnenten Identitätsartikelspalten Bereiche zu, um zu verhindern, dass für Updateabonnenten Konflikte auftreten. Weitere Informationen finden Sie im Abschnitt zum Zuweisen von Bereichen bei der manuellen Verwaltung von Identitätsbereichen im Thema [Replizieren von Identitätsspalten](replicate-identity-columns.md).  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>So aktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)aus. Wenn die zu veröffentlichende Quelltabelle eine Identitätsspalte besitzt, geben Sie für **** identityrangemanagementoption** den Wert \@auto**, für **\@pub_identity_range** den einem Serverabonnement zugewiesenen Bereich von Identitätswerten und für **\@identity_range** den dem Verleger und jedem Clientabonnement zugewiesenen Bereich von Identitätswerten an. Geben Sie für **\@threshold** den Prozentsatz der gesamten Identitätswerte an, die verwendet werden, bevor ein neuer Identitätsbereich zugewiesen wird. Weitere Informationen dazu, wann neue Identitätsbereiche zugewiesen werden, finden Sie im Abschnitt zum Zuweisen von Identitätsbereichen im Thema [Replizieren von Identitätsspalten](replicate-identity-columns.md). Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](define-an-article.md).  
  
    > [!NOTE]  
    >  Vergewissern Sie sich, dass der Datentyp der Identitätsspalte groß genug ist, um den gesamten, allen Abonnenten zugewiesenen Identitätsbereich zu unterstützen. Dies gilt besonders bei Abonnenten mit Serverabonnements.  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>So deaktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)aus. Geben Sie einen der folgenden Werte für ** \@die identityrangemanagementoption**an:  
  
    -   **manuell: Identitäts** Bereiche müssen manuell für Update Abonnenten zugewiesen werden.  
  
    -   **None** : Identitäts Spalten auf dem Verleger werden auf dem Abonnenten nicht als Identitäts Spalten definiert.  
  
     Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](define-an-article.md).  
  
2.  Weisen Sie auf dem Abonnenten Identitätsartikelspalten Bereiche zu, um zu verhindern, dass für Updateabonnenten Konflikte auftreten.  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>So ändern Sie die Einstellungen für die automatische Identitätsbereichsverwaltung für einen vorhandenen Artikel in einer Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql) aus, und achten Sie auf den Wert von **identityrangemanagementoption** im Resultset. Ist dieser Wert **0**, ist die automatische Identitätsbereichsverwaltung nicht aktiviert.  
  
2.  Wenn der Wert von **identityrangemanagementoption** im Resultset **1**ist, ändern Sie die Einstellungen wie folgt:  
  
    -   Um die zugewiesenen Identitätsbereiche zu ändern, führen Sie [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie für **** property** den Wert **identity_range** oder \@pub_identity_range** und für **\@value** den neuen Bereichswert an.  
  
    -   Um den Schwellenwert zu ändern, bei dessen Überschreiten neue Identitätsbereiche zugewiesen werden, führen Sie [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie für **** property** den Wert \@threshold** und für **\@value** den neuen Schwellenwert an.  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-merge-publication"></a>So ändern Sie die Einstellungen für die automatische Identitätsbereichsverwaltung für einen vorhandenen Artikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) aus, und achten Sie auf den Wert von **identity_support** im Resultset. Ist dieser Wert **0**, ist die automatische Identitätsbereichsverwaltung nicht aktiviert.  
  
2.  Wenn der Wert von **identity_support** im Resultset **1**ist, ändern Sie die Einstellungen wie folgt:  
  
    -   Um die zugewiesenen Identitätsbereiche zu ändern, führen Sie [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie für **** property** den Wert **identity_range** oder \@pub_identity_range** und für **\@value** den neuen Bereichswert an.  
  
    -   Um den Schwellenwert zu ändern, bei dessen Überschreiten neue Identitätsbereiche zugewiesen werden, führen Sie [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie für **** property** den Wert \@threshold** und für **\@value** den neuen Schwellenwert an. Weitere Informationen dazu, wann neue Identitätsbereiche zugewiesen werden, finden Sie im Abschnitt zum Zuweisen von Identitätsbereichen im Thema [Replizieren von Identitätsspalten](replicate-identity-columns.md).  
  
    -   Um die automatische Verwaltung von Identitätsbereichen zu deaktivieren, führen Sie [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie den Wert **identityrangemanagementoption** für **\@property** und entweder **manual** oder **none** für **\@value** an.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Peer-to-Peer Transactional Replication](../transactional/peer-to-peer-transactional-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Replizieren von Identitätsspalten](replicate-identity-columns.md)  
  
  
