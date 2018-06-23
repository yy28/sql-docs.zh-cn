---
title: 表值参数 (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1a3a4e683887022c905fd2faf45cf5ff36b57a3a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128961"
---
# <a name="table-valued-parameters-ole-db"></a>表值参数 (OLE DB)
  本节介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口中的表值参数支持。 其他的概述信息，请参阅[表值参数&#40;SQL Server Native Client&#41;](../native-client/features/table-valued-parameters-sql-server-native-client.md)。 有关示例，请参阅[使用表值参数&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>Remarks  
 当前，您可以将多行数据作为带有参数集的过程的参数（如 `ICommand::Execute` 中的 DBPARAMS 参数）发送到服务器。 使用参数集时，该参数集中的每个元素都必须通过单独的远程过程调用 (RPC) 请求发送到服务器。 表值参数提供类似的功能，但可以与服务器更好地集成。 这可以减少 RPC 请求数，并在服务器上启用基于集的操作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将表值参数作为 OLE DB `Rowset` 对象提供支持。 使用者（即使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口的客户端应用程序）可以将任意 `Rowset` 对象作为表值参数的占位符提供。 表值参数的处理方式与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 参数类型相似。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口提供创建、发现、规范、绑定和架构接口。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [创建表值参数行集](table-valued-parameter-rowset-creation.md)  
  
-   [表值参数类型发现](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md)  
  
-   [执行包含表值参数的命令](executing-commands-containing-table-valued-parameters.md)  
  
-   [向表值参数中插入数据](inserting-data-into-table-valued-parameters.md)  
  
-   [为 OLE DB 表值参数更改的架构行集](schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 表值参数类型支持](ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 表值参数类型支持&#40;方法&#41;](ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 表值参数类型支持&#40;属性&#41;](ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用表值参数&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  