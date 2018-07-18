---
title: 提取行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 5e6dbe36-b682-464d-adfa-8e886f9bd452
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ef60069c801ed7000677122af6fba7b2e9f7c4a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415056"
---
# <a name="fetching-rows"></a>提取行
  **IRowset**接口是基础行集接口。 **IRowset**接口提供了用于按顺序提取行、 从这些行获得数据和管理行的方法。 使用者使用中的方法**IRowset**所有基本行集操作。 这包括提取和释放行以及获得列值。  
  
 使用者获得行集上的接口指针，第一步时，通常使用确定行集的功能**irowsetinfo:: Getproperties**方法。 这将返回行集所公开的接口的相关信息，以及未显示为非重复接口的行集的功能，例如最大活动行数和可以同时有挂起更新的行数。  
  
 使用者的下一步是确定行集中列的特征（即元数据）。 为此，它们使用**IColumnsInfo**简单列信息的方法或**IColumnsRowset**对扩展的列信息的方法。 **GetColumnInfo**方法将返回以下信息：  
  
-   结果集中的列数。  
  
-   DBCOLUMNINFO 结构的数组，每列一个。  
  
     结构的顺序是列在行集中出现的顺序。 每个 DBCOLUMNINFO 结构都包括列元数据，例如列名称、列的序号、列值的最大可能长度、列的数据类型、精度和长度。  
  
-   指向单个分配块中的所有字符串值的存储区的指针。  
  
 使用者通过元数据或基于生成该行集的文本命令来确定它需要哪些列。 它将确定返回的列信息进行排序所需的列的序号**IColumnsInfo**或从通过返回的列元数据行集中的序号**IColumnsRowset**。  
  
 **IColumnsInfo**并**IColumnsRowset**接口用于提取有关行集中的列信息。 **IColumnsInfo**接口返回一组有限的信息，而**IColumnsRowset**提供所有元数据。  
  
> [!NOTE]  
>  在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本 7.0 和更早版本，可选的元数据列 dbcolumn_computemode 会返回**icolumnsinfo:: Getcolumnsinfo**返回 DBSTATUS_S_ISNULL （而不是描述该列是否的值计算） 由于不能确定基础列是否为计算列。  
  
 序号用于指定到列的绑定。 绑定是将使用者的结构元素与列进行关联的结构。 绑定可以是对列的数据值、长度和状态值的绑定。  
  
 在取值函数中可收集一组绑定。 这通过创建**iaccessor:: Createaccessor**方法。 取值函数可以包含多个绑定，以便可以在单个调用中检索或设置多个列的数据。 使用者可以创建多个取值函数，以便在应用程序的不同部分匹配不同的使用模式。 它可以在行集仍然存在时创建和释放取值函数。  
  
 若要从数据库提取的行，使用者调用的方法，如**irowset:: Getnextrows**或**irowsetlocate:: Getrowsat**。 这些提取操作将行数据从服务器放入提供程序的行缓冲区中。 使用者不能直接访问提供程序的行缓冲区。 使用者使用**irowset:: Getdata**将数据从提供程序缓冲区复制到使用者缓冲区并**irowsetchange:: Setdata**将数据更改从使用者缓冲区复制到提供程序缓冲区。  
  
 使用者可调用**GetData**方法，并将该句柄传递到行、 句柄访问器中和使用者分配的缓冲区的指针。 **GetData**将数据转换并返回用于创建取值函数绑定中指定的列。 使用者可以调用**GetData**不止一次一行时，使用不同取值函数和缓冲区，因此使用者可以获得相同的数据的多个副本。  
  
 可以采用多种方式处理来自变长列的数据。 首先，可以将这样的列绑定到使用者的结构的有限部分。 这将导致当数据的长度超过缓冲区的长度时发生截断。 通过检查状态是否为 DBSTATUS_S_TRUNCATED，使用者可以确定是否已发生截断。 返回的长度始终是真实的字节长度，因此使用者还可以确定有多少数据被截断。  
  
 当使用者完成提取或更新行时，它将释放与它们**ReleaseRows**方法。 这将释放行集中行的副本所占的资源，并为新行腾出空间。 然后，使用者可以重复其提取或创建行并访问其中数据的循环。  
  
 使用者完成对行集时，它将调用**iaccessor:: Releaseaccessor**方法释放所有取值函数。 它将调用**iunknown:: Release**由要释放行集的行集公开的所有接口上的方法。 释放行集时，它将强制释放使用者可能持有的任何剩余的行或取值函数。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [下次提取位置](fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>请参阅  
 [行集](rowsets.md)  
  
  
