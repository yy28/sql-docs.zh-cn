---
title: "当前记录和记录集的大小 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb50826230e46cc71106a2b17d01914eae024f47
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="current-record-and-size-of-recordset"></a>当前记录和记录集的大小
本部分介绍如何在此示例中找到光标的当前位置**记录集**中[JScript 代码示例，以返回一个记录集](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)。  
  
## <a name="current-record"></a>当前记录  
 在数据集中的当前记录对应于所指向的光标的位置**记录集**对象。 当**记录集**形式调用的结果从数据源返回对象**Recordset.Open**， **Command.Execute**，或**Connection.Execute** (包括**Connection.NamedCommand**和**Connection.StoredProcedure**)，光标设置为指向第一条记录。 在示例数据集，初始的当前记录是"位置 Bob 环保 Dried 梨"项。  
  
## <a name="size-of-recordset"></a>记录集的大小  
 若要了解的大小**记录集**对象，获取的值**Recordset.RecordCount**属性。 此值是一个长整数，指示中的记录数**记录集**。 如果从 OLEDB 提供程序中数据集返回适用于 Microsoft SQL Server 时，此值将使返回的行数。 读取**RecordCount**属性关闭**记录集**会导致错误。  
  
 如果不确定的记录数，属性的值为 1。  
  
 值**RecordCount**属性又依赖于提供程序和使用的游标的类型的功能。 对于只进游标，值为-1。 对于静态或键集游标，则这是中返回的记录的实际数目**记录集**对象。 对于动态游标，值为-1 或实际的记录，具体取决于数据源数。  
  
 支持的游标**Recordcount**必须工作更难一些，因此需要比游标不支持的更高计算能力**Recordcount**。 如果不需要知道的记录数，使用不同的游标类型可能有助于提高应用程序的性能，尤其是当必须处理大型数据集。  
  
 在某些情况下，提供程序或光标是无法确定**RecordCount**不带第一个从数据源提取所有记录值。 若要确保准确计数，调用**记录集**。**MoveLast**方法之前调用**Recordset.RecordCount**。  
  
 示例**记录集**获取使用对象[JScript 代码示例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)使用只进游标，因此调用**RecordCount**对此对象始终会为-1。 如果你更改的调用的代码行**记录集**。**打开**方法，如以下示例所示**RecordCount**属性将返回的实际提取的记录数。  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 这是因为静态游标与[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支持**RecordCount**。 在此示例中，有 5 个记录，因此**RecordCount**应产生 5 的值。  
  
 本部分包含以下主题。  
  
 [记录集的边界](../../../ado/guide/data/boundaries-of-a-recordset.md)

