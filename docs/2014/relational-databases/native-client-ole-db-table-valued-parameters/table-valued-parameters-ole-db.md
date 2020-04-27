---
title: 表值参数 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9c58b1837eb017a3cc51652ff404b37690b3849
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046422"
---
# <a name="table-valued-parameters-ole-db"></a>表值参数 (OLE DB)
  本节介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口中的表值参数支持。 有关其他概述信息，请参阅[表值参数 &#40;SQL Server Native Client&#41;](../native-client/features/table-valued-parameters-sql-server-native-client.md)。 有关示例，请参阅[使用表值参数 (OLE DB)](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>备注  
 当前，您可以将多行数据作为带有参数集的过程的参数（如 `ICommand::Execute` 中的 DBPARAMS 参数）发送到服务器。 使用参数集时，该参数集中的每个元素都必须通过单独的远程过程调用 (RPC) 请求发送到服务器。 表值参数提供类似的功能，但可以与服务器更好地集成。 这可以减少 RPC 请求数，并在服务器上启用基于集的操作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将表值参数作为 OLE DB `Rowset` 对象提供支持。 使用者（即使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口的客户端应用程序）可以将任意 `Rowset` 对象作为表值参数的占位符提供。 表值参数的处理方式与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 参数类型相似。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口提供创建、发现、规范、绑定和架构接口。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [创建表值参数行集](table-valued-parameter-rowset-creation.md)  
  
-   [表值参数类型发现](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md)  
  
-   [执行包含表值参数的命令](executing-commands-containing-table-valued-parameters.md)  
  
-   [向表值参数中插入数据](inserting-data-into-table-valued-parameters.md)  
  
-   [为 OLE DB 表值参数更改的架构行集](schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 表值参数类型支持](ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 表值参数类型支持（方法）](ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 表值参数类型支持（属性）](ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用表值参数 (OLE DB)](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
