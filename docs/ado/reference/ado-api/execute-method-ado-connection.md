---
title: Execute 方法 （ADO 连接） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a52ca419f3f06e4156c278cb0ba8999c24e09ac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680021"
---
# <a name="execute-method-ado-connection"></a>Execute 方法（ADO 连接）
执行指定的查询，SQL 语句、 存储的过程或特定于提供程序的文本。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>返回值  
 返回[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)对象引用。  
  
#### <a name="parameters"></a>Parameters  
 *CommandText*  
 一个**字符串**值，该值包含执行 SQL 语句、 存储的过程、 URL 或特定于提供程序的文本。 **可以选择**，可以但仅使用表名称，如果提供程序注意 SQL。 有关使用例如，如果表名称的"客户"，ADO 将自动在前面添加标准的 SQL Select 语法，以形成，并通过"选择 * 从客户"作为[!INCLUDE[tsql](../../../includes/tsql-md.md)]到提供程序的语句。  
  
 *RecordsAffected*  
 可选。 一个**长**变量向其提供程序返回的操作所影响的记录数。  
  
 *选项*  
 可选。 一个**长**值，该值指示提供程序应该如何评估 CommandText 参数。 可以是一个或多个的位掩码[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值。  
  
 **请注意**使用**ExecuteOptionEnum**值**adExecuteNoRecords**通过最小化内部处理并将从 Visual Basic 6.0 迁移的应用程序来提高性能。  
  
 不要使用**adExecuteStream**与**Execute**方法**连接**对象。  
  
 不要使用与 Execute 的 adCmdFile 或 adCmdTableDirect CommandTypeEnum 值。 这些值仅用作选项与[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)并[Requery 方法](../../../ado/reference/ado-api/requery-method.md)方法**记录集**。  
  
## <a name="remarks"></a>备注  
 使用**Execute**方法[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)对象执行将传递给方法的 CommandText 参数中指定连接上任何查询。 如果 CommandText 参数指定返回行的查询，将执行生成任何结果存储在一个新**记录集**对象。 如果该命令不返回结果 （例如，SQL 更新查询） 访问接口将返回**Nothing**只要选项**adExecuteNoRecords**指定; 否则执行返回关闭**记录集**。  
  
 返回**记录集**对象始终是只读的、 只进游标。 如果你需要**记录集**对象具有更多功能，请首先创建**记录集**对象使用所需的属性设置，然后使用**记录集**对象[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法以执行查询并返回所需的游标类型。  
  
 内容*CommandText*参数特定于提供程序，可以是标准的 SQL 语法或提供程序支持的任何特殊的命令格式。  
  
 此操作结束时，将发出 ExecuteComplete 事件。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
