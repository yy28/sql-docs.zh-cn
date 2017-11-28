---
title: "提取行 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 5e6dbe36-b682-464d-adfa-8e886f9bd452
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2e3cb9f50806d4796d9f65b05c269f610bd33933
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="fetching-rows"></a>提取行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRowset**接口是基行集接口。 **IRowset**接口可提供用于按顺序读取行、 从这些行，获取数据和管理行的方法。 使用者使用中的方法**IRowset**所有基本行集操作。 这包括提取和释放行以及获得列值。  
  
 当使用者获得行集上的接口指针时，第一步是通常使用来确定的行集的功能**IRowsetInfo::GetProperties**方法。 这将返回行集所公开的接口的相关信息，以及未显示为非重复接口的行集的功能，例如最大活动行数和可以同时有挂起更新的行数。  
  
 使用者的下一步是确定行集中列的特征（即元数据）。 为此，它们使用**IColumnsInfo**简单列信息的方法或**IColumnsRowset**扩展的列信息的方法。 **GetColumnInfo**方法返回以下信息：  
  
-   结果集中的列数。  
  
-   DBCOLUMNINFO 结构的数组，每列一个。  
  
     结构的顺序是列在行集中出现的顺序。 每个 DBCOLUMNINFO 结构都包括列元数据，例如列名称、列的序号、列值的最大可能长度、列的数据类型、精度和长度。  
  
-   指向单个分配块中的所有字符串值的存储区的指针。  
  
 使用者通过元数据或基于生成该行集的文本命令来确定它需要哪些列。 它确定从返回的列信息的排序所需的列的序号**IColumnsInfo**或从中返回的列元数据行集序号**IColumnsRowset**。  
  
 **IColumnsInfo**和**IColumnsRowset**接口用于提取有关行集中的列信息。 **IColumnsInfo**接口返回一组有限的信息，而**IColumnsRowset**提供所有元数据。  
  
> [!NOTE]  
>  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本 7.0 及更早版本，通过返回的可选元数据列 DBCOLUMN_COMPUTEMODE **IColumnsInfo::GetColumnsInfo**返回是 DBSTATUS_S_ISNULL （而不是描述该列是否的值计算） 因为无法确定是否计算基础列。  
  
 序号用于指定到列的绑定。 绑定是将使用者的结构元素与列进行关联的结构。 绑定可以是对列的数据值、长度和状态值的绑定。  
  
 在取值函数中可收集一组绑定。 这通过使用创建**IAccessor::CreateAccessor**方法。 取值函数可以包含多个绑定，以便可以在单个调用中检索或设置多个列的数据。 使用者可以创建多个取值函数，以便在应用程序的不同部分匹配不同的使用模式。 它可以在行集仍然存在时创建和释放取值函数。  
  
 若要从数据库提取行，使用者调用方法，如**irowset:: Getnextrows**或**IRowsetLocate::GetRowsAt**。 这些提取操作将行数据从服务器放入提供程序的行缓冲区中。 使用者不能直接访问提供程序的行缓冲区。 使用者使用**irowset:: Getdata**将从提供程序的缓冲区的数据复制到使用者缓冲区和**IRowsetChange::SetData**将从使用者缓冲区的数据更改复制到提供程序缓冲区。  
  
 使用者调用**GetData**方法，并将该句柄传递到行、 访问器中的句柄和指向使用者分配缓冲区的指针。 **GetData**将数据转换，并返回用于创建取值函数的绑定中指定的列。 使用者可以调用**GetData**不止一次一行时，使用不同的访问器和缓冲区，因此单击使用者可以获得相同的数据的多个副本。  
  
 可以采用多种方式处理来自变长列的数据。 首先，可以将这样的列绑定到使用者的结构的有限部分。 这将导致当数据的长度超过缓冲区的长度时发生截断。 通过检查状态是否为 DBSTATUS_S_TRUNCATED，使用者可以确定是否已发生截断。 返回的长度始终是真实的字节长度，因此使用者还可以确定有多少数据被截断。  
  
 当使用者完成提取或更新行时，它会释放它们与**ReleaseRows**方法。 这将释放行集中行的副本所占的资源，并为新行腾出空间。 然后，使用者可以重复其提取或创建行并访问其中数据的循环。  
  
 当使用者是完成与行集时，它将调用**IAccessor::ReleaseAccessor**方法来释放任何访问器。 它调用**iunknown:: Release**公开要释放行集的行集的所有接口上的方法。 释放行集时，它将强制释放使用者可能持有的任何剩余的行或取值函数。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [下次提取位置](../../relational-databases/native-client-ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
