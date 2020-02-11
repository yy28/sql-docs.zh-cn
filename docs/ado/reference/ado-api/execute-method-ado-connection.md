---
title: Execute 方法（ADO 连接） |Microsoft Docs
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
ms.openlocfilehash: 4999b1e21ec145713cadae28ff7ee8a64dd460b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932895"
---
# <a name="execute-method-ado-connection"></a>Execute 方法（ADO 连接）
执行指定的查询、SQL 语句、存储过程或特定于提供程序的文本。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>返回值  
 返回[Recordset 对象（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)对象引用。  
  
#### <a name="parameters"></a>parameters  
 *CommandText*  
 一个**字符串**值，该值包含要执行的 SQL 语句、存储过程、URL 或特定于提供程序的文本。 **或者**，仅当提供程序可以识别 SQL 时，才可以使用表名。 例如，如果使用了表名 "Customers"，则 ADO 将自动预置标准 SQL Select 语法来形成，并将 "SELECT * FROM Customers" 作为[!INCLUDE[tsql](../../../includes/tsql-md.md)]语句传递给提供程序。  
  
 *RecordsAffected*  
 可选。 一个**长整型**变量，提供程序返回操作影响的记录数。  
  
 *选项*  
 可选。 一个**长整型**值，该值指示提供程序应如何计算 CommandText 参数。 可以是一个或多个[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值的位掩码。  
  
 **注意**使用**ExecuteOptionEnum**值**adExecuteNoRecords** ，通过最大程度地减少内部处理以及从 Visual Basic 6.0 迁移的应用程序来提高性能。  
  
 不要将**adExecuteStream**与**连接**对象的**Execute**方法一起使用。  
  
 不要将 adCmdFile 或 adCmdTableDirect 的 CommandTypeEnum 值用于 Execute。 这些值只能用作[开放式方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)和**记录集**的[方法](../../../ado/reference/ado-api/requery-method.md)方法的选项。  
  
## <a name="remarks"></a>备注  
 对[连接对象（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)对象使用**Execute**方法会执行您传递给指定连接上的 CommandText 参数中的方法的任何查询。 如果 CommandText 参数指定了返回行的查询，则执行生成的任何结果都存储在新的**记录集**对象中。 如果该命令不是为了返回结果（例如，SQL 更新查询），则只要指定了选项**adExecuteNoRecords** ，提供程序就不会返回**任何内容**;否则 Execute 将返回已关闭的**记录集**。  
  
 返回的**记录集**对象始终为只读、只进游标。 如果需要具有更多功能的**记录集**对象，请首先使用所需的属性设置创建**记录集**对象，然后使用**Recordset**对象的[Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法执行查询并返回所需的游标类型。  
  
 *CommandText*参数的内容特定于提供程序，可以是标准的 SQL 语法，也可以是提供程序支持的任何特殊命令格式。  
  
 此操作结束时，将发出 ExecuteComplete 事件。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>应用于  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
