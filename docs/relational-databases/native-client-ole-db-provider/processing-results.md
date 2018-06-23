---
title: 处理结果 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-provider
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [SQL Server Native Client]
ms.assetid: 20887ac4-f649-4e7f-92e6-f929e2e70952
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 18dddb9c3244a50a81d64b25fa200ca16e634284
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35699948"
---
# <a name="processing-results"></a>处理结果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  如果行集对象是由执行命令或直接从访问接口生成的，则使用者需要检索和访问行集中的数据。  
  
 行集是使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口能够以表格格式提供数据的核心对象。 从概念上说，行集是指其中的每行都拥有列数据的行的集合。 行集对象公开的接口，如**IRowset** （包含用于按顺序在行集中提取行的方法）， **IAccessor** (允许的一组列绑定描述的定义方式表格数据绑定到使用者程序变量）， **IColumnsInfo** （提供在行集中的列的信息），和**IRowsetInfo** （提供有关行集的信息）。  
  
 使用者可以调用**irowset:: Getdata**方法来从行集中的数据行检索到的缓冲区。 之前**GetData**是调用，使用者描述使用一组 DBBINDING 结构的缓冲区。 每个绑定都说明了行集中的列在使用者缓冲区中的存储方式并包含以下内容：  
  
-   应用绑定的列（或参数）的序号。  
  
-   有关绑定内容的信息（例如，数据值、数据长度及其绑定状态）。  
  
-   有关缓冲区中到这些部分中每个部分的偏移量的信息。  
  
-   数据值存在于使用者缓冲区中时的长度和类型。  
  
 获取数据时，访问接口将使用每个绑定中的信息来确定从使用者缓冲区的何处以及如何检索数据。 设置使用者缓冲区中的数据时，访问接口将使用每个绑定中的信息来确定在使用者缓冲区的何处以及如何返回数据。  
  
 指定 DBBINDING 结构后，创建取值函数 (**IAccessor::CreateAccessor**)。 取值函数是一个绑定集合，可用于获取或设置使用者缓冲区中的数据。  
  
## <a name="see-also"></a>请参阅  
 [创建 SQL Server Native Client OLE DB 提供程序应用程序](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [OLE DB 操作指南主题](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
