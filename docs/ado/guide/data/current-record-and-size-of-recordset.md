---
title: 当前记录和记录集的大小 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a01e17ea9c786a724e5869a28bf4d8927b58ac81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925696"
---
# <a name="current-record-and-size-of-recordset"></a>当前记录和记录集的大小
本部分介绍如何在此示例中找到光标的当前位置**记录集**中[JScript 代码示例返回一个记录集](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)。  
  
## <a name="current-record"></a>当前记录  
 在数据集中的当前记录对应于指向的光标的位置的**记录集**对象。 当**记录集**对象从数据源返回调用的结果作为**Recordset.Open**， **Command.Execute**，或**Connection.Execute** (包括**Connection.NamedCommand**并**Connection.StoredProcedure**)，将光标设置为指向第一条记录。 在示例数据集，初始的当前记录是"Uncle Bob 有机 Dried 梨"项。  
  
## <a name="size-of-recordset"></a>记录集的大小  
 若要查看的大小**记录集**对象，获取的值**Recordset.RecordCount**属性。 此值是一个长整数，指示中的记录数**记录集**。 如果数据集从 OLEDB 访问接口返回适用于 Microsoft SQL Server，此值将使返回的行数。 读取**RecordCount**属性对已关闭**记录集**将导致错误。  
  
 如果不确定的记录数，该属性的值为-1。  
  
 值**RecordCount**属性还依赖于提供程序和使用的游标类型的功能。 对于只进游标，值为-1。 对于静态或键集游标，值是实际返回中的记录数**记录集**对象。 对于动态游标，值为-1 或的记录，具体取决于数据源的实际数目。  
  
 支持的游标**Recordcount**必须工作更难，因此要求更高计算能力，不是游标不支持**Recordcount**。 如果不需要知道的记录数，使用不同的游标类型可能有助于提高应用程序的性能，尤其是当必须处理大型数据集。  
  
 在某些情况下，提供程序或光标是无法确定**RecordCount**而无需第一个数据源中提取所有记录的值。 若要确保准确计数，请调用**记录集**。**MoveLast**方法之前调用**Recordset.RecordCount**。  
  
 该示例**记录集**对象使用获取[JScript 代码示例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)使用只进游标，因此调用**RecordCount**对此对象始终会为-1。 如果您更改的调用的代码行**记录集**。**打开**方法，如以下示例所示**RecordCount**属性将返回实际提取的记录数。  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 这是因为静态游标[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支持**RecordCount**。 在此示例中，有五个记录，因此**RecordCount**应产生值为 5。  
  
 本部分包含以下主题。  
  
 [记录集的边界](../../../ado/guide/data/boundaries-of-a-recordset.md)
