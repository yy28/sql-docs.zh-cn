---
title: 在 Integration Services 包中执行 MERGE | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- MERGE statement [SQL Server]
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bea006d7e58931d16b1ea8728d4f979de56c6d32
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918512"
---
# <a name="merge-in-integration-services-packages"></a>在 Integration Services 包中执行 MERGE
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的当前版本中，执行 SQL 任务中的 SQL 语句可以包含 MERGE 语句。 使用此 MERGE 语句可以在一个语句中完成多个 INSERT、UPDATE 和 DELETE 操作。  
  
 若要在包中使用 MERGE 语句，请执行下列步骤：  
  
-   创建用于将源数据加载、转换和保存到临时表的数据流任务。  
  
-   创建包含 MERGE 语句的执行 SQL 任务。  
  
-   将数据流任务连接到执行 SQL 任务，并将临时表中的数据用作 MERGE 语句的输入。  
  
    > [!NOTE]  
    >  尽管在此方案中，MERGE 语句通常需要临时表，但 MERGE 语句的性能通常优于由查找转换执行的逐行查找的性能。 当查找表很大以致需要有足够多的内存供查找转换缓存其引用表时，MERGE 也非常有用。  
  
 本主题的其余部分将讨论 MERGE 语句的一些其他用法。  
  
 有关支持使用 MERGE 语句的示例目标组件，请参阅 CodePlex 社区示例 [MERGE Destination](https://go.microsoft.com/fwlink/?LinkId=141215)（MERGE 目标）。  
  
## <a name="using-merge"></a>使用 MERGE  
 通常，当需要应用包括从一个表到另一个表的插入、更新和删除等更改时，可使用 MERGE 语句。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]之前，此过程需要一个查找转换和多个 OLE DB 命令转换。 查找转换执行逐行查找，以确定每一行是新行还是经过更改的行。 OLE DB 命令转换然后会执行必要的 INSERT、UPDATE 和 DELETE 操作。 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]开始，一个 MERGE 语句即可替代查找转换和相应的 OLE DB 命令转换。  
  
### <a name="merge-with-incremental-loads"></a>用于增量加载的 MERGE  
 变更数据捕获功能是 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中的新增功能，使用该功能可以方便可靠地对数据仓库执行增量加载。 除了使用参数化的 OLE DB 命令转换来执行插入和更新之外，还可以使用 MERGE 语句来合并这两项操作。  
  
 有关详细信息，请参阅 [将变更应用到目标](../change-data-capture/apply-the-changes-to-the-destination.md)。  
  
#### <a name="merge-in-other-scenarios"></a>在其他情况下的 MERGE  
 在以下情况下，可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的外部或内部使用 MERGE 语句。 不过，从多个异类源加载此数据以及随后合并和清除该数据通常都需要 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 因此，为了使用方便和便于维护，可以考虑在包中使用 MERGE 语句。  
  
##### <a name="track-buying-habits"></a>跟踪购买习惯  
 数据仓库中的 FactBuyingHabits 表会跟踪客户购买指定产品的最后日期。 该表由 ProductID、CustomerID 和 PurchaseDate 列组成。 事务性数据库每周都会生成一个包括该周采购情况的 PurchaseRecords 表。 目标是使用一个 MERGE 语句将 PurchaseRecords 表中的信息合并到 FactBuyingHabits 表中。 对于不存在的产品-客户对，MERGE 语句将插入新行。 对于已存在的产品-客户对，MERGE 语句会更新最近的购买日期。  
  
###### <a name="track-price-history"></a>跟踪价格历史记录  
 DimBook 表表示某书商库存中的图书列表，并标识每本书的价格历史记录。 此表包括以下列：ISBN、ProductID、Price、Shelf 和 IsCurrent。 此表还将书的每个价格显示为一行。 其中一行显示的是当前价格。 为了指示哪一行包含当前价格，该行的 IsCurrent 列的值设置为 1。  
  
 该数据库每周会生成一个 WeeklyChanges 表，其中包含该周的价格更改以及该周添加的新书。 使用一个 MERGE 语句可以将 WeeklyChanges 表中的更改应用到 DimBook 表中。 MERGE 语句会为新添加的书插入新行，对于价格已更改的现有书的行，MERGE 语句会将这些行的 IsCurrent 列更新为 0。 MERGE 语句还会为价格已更改的书插入新行，并会将这些新行的 IsCurrent 列的值设置为 1。  
  
### <a name="merge-a-table-with-new-data-against-the-old-table"></a>将具有新数据的表与旧表合并  
 该数据库使用“开放式架构”（即，包含各属性的名称-值对的表）对对象的属性进行建模。 Properties 表具有三列：EntityID、PropertyID 和 Value。 NewProperties 表是 Properties 表的更新版本，应与 Properties 表保持同步。 若要同步这两个表，可以使用一个 MERGE 语句执行以下操作：  
  
-   从 Properties 表中删除 NewProperties 表中不存在的属性。  
  
-   使用 NewProperties 表中找到的新值更新 Properties 表中的属性值。  
  
-   插入在 NewProperties 表中存在但在 Properties 表中不存在的新属性。  
  
 此方法在类似复制方案的方案中非常有用，此方案的目标是使两台服务器上的两个表中的数据保持一致。  
  
### <a name="track-inventory"></a>跟踪库存  
 Inventory 数据库具有一个 ProductsInventory 表，该表具有 ProductID 列和 StockOnHand 列。 具有 ProductID、CustomerID 和 Quantity 列的 Shipments 表跟踪对客户的产品发货情况。 ProductInventory 表应根据 Shipments 表中的信息每天更新。 根据发货情况，一个 MERGE 语句可以降低 ProductInventory 表中的库存。 如果某产品的库存已降低为 0，该 MERGE 语句还可以从 ProductInventory 表中删除该产品行。  
  
  
