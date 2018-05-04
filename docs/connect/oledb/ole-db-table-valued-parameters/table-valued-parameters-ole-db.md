---
title: 表值参数 (OLE DB) |Microsoft 文档
description: 表值参数 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 91478e575fdde15b6bbd1f82185f7c32d5e38daa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="table-valued-parameters-ole-db"></a>表值参数 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本部分介绍对 SQL Server 的 OLE DB 驱动程序中的表值参数的支持。 其他的概述信息，请参阅[表值参数&#40;OLE DB 驱动程序的 SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)。 有关示例，请参阅[使用表值参数&#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>注释  
 目前，你可以多行将数据发送到服务器作为带参数集的过程的参数 (中的 DBPARAMS 参数**ICommand::Execute**)。 使用参数集时，该参数集中的每个元素都必须通过单独的远程过程调用 (RPC) 请求发送到服务器。 表值参数提供类似的功能，但可以与服务器更好地集成。 它减少了 RPC 请求数，并允许在服务器上基于集的操作。  
  
 作为 OLE DB 的 SQL Server 的 OLE DB 驱动程序中支持表值参数**行集**对象。 任何**行集**对象可以提供由使用者 （即，客户端应用程序使用 SQL Server 的 OLE DB 驱动程序） 作为占位符表值参数参数。 表值参数的处理方式与其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 参数类型相似。 创建、 发现、 规范、 绑定和架构接口，提供了 SQL Server 的 OLE DB 驱动程序。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [创建表值参数行集](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [表值参数类型发现](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [执行包含表值参数的命令](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [向表值参数中插入数据](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [为 OLE DB 表值参数更改的架构行集](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 表值参数类型支持](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 表值参数类型支持&#40;方法&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 表值参数类型支持&#40;属性&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 编程的 OLE DB 驱动程序](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [使用表值参数 & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
