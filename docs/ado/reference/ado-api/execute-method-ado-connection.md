---
title: 执行方法 （ADO 连接） |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 05d1df49596da99bc98fba9cef7999772ea78f40
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="execute-method-ado-connection"></a>执行方法 （ADO 连接）
执行指定的查询、 SQL 语句、 存储的过程或提供程序特定的文本。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>返回值  
 返回[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)对象引用。  
  
#### <a name="parameters"></a>Parameters  
 *CommandText*  
 A**字符串**包含执行 SQL 语句、 存储的过程、 URL 或特定于提供程序的文本值。 **（可选)**，如果提供程序注意的 SQL，可以但仅使用表名称。 例如，如果表名称的"客户"则使用，ADO 将自动在前面添加标准的 SQL Select 语法，窗体，然后将"选择 * 从客户"为[!INCLUDE[tsql](../../../includes/tsql_md.md)]到提供程序的语句。  
  
 *RecordsAffected*  
 選擇性。 A**长**变量到该提供程序返回的操作所影响的记录数。  
  
 *Options*  
 選擇性。 A**长**值，该值指示提供程序应如何评估 CommandText 自变量。 可以是一个位屏蔽的一个或多个[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值。  
  
 **请注意**使用**ExecuteOptionEnum**值**adExecuteNoRecords**以提高性能，通过最小化内部处理和要从 Visual Basic 6.0 移植的应用程序。  
  
 不要使用**adExecuteStream**与**执行**方法**连接**对象。  
  
 不要使用与执行 adCmdFile 或 adCmdTableDirect 的 CommandTypeEnum 值。 这些值仅用作选项[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[Requery 方法](../../../ado/reference/ado-api/requery-method.md)方法**记录集**。  
  
## <a name="remarks"></a>注释  
 使用**执行**方法[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)对象执行任何查询，你将传递给方法 CommandText 参数中指定连接上。 如果 CommandText 参数指定返回行的查询，将执行生成任何结果存储在一个新**记录集**对象。 如果该命令不是要返回的结果 （例如，SQL 更新查询） 该提供程序返回**执行任何操作**只要选项**adExecuteNoRecords**指定; 否则将执行返回关闭**记录集**。  
  
 返回**记录集**对象始终是只读的、 只进游标。 如果你需要**记录集**对象具有更多的功能，请首先创建**记录集**对象具有所需的属性设置，然后使用**记录集**对象[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法以执行查询并返回所需的游标类型。  
  
 内容*CommandText*参数特定于提供程序，可以为标准的 SQL 语法或任何特殊命令格式提供程序支持。  
  
 此操作结束时，将发出 ExecuteComplete 事件。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
