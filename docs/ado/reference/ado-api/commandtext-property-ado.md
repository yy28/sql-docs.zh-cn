---
title: "CommandText 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 60ee83c7d1f667feb0b1fcb4985dcd50edfda27b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="commandtext-property-ado"></a>CommandText 属性 (ADO)
指示要对提供程序发出命令的文本。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 获取或设置**字符串**值，该值包含提供程序命令，如 SQL 语句、 表名称、 相对 URL 或存储的过程调用。 默认值为空字符串 ("")。  
  
## <a name="remarks"></a>注释  
 使用**CommandText**属性来设置或返回表示命令的文本[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。 通常这将是一个 SQL 语句，但也可以是任何其他类型的提供程序，如存储的过程调用识别的命令语句。 SQL 语句必须是特定语句或提供程序的查询处理器支持的版本。  
  
 如果[已准备](../../../ado/reference/ado-api/prepared-property-ado.md)属性**命令**对象设置为**True**和**命令**设置时，将对象绑定到打开的连接**CommandText**属性，ADO 准备查询 （即，已编译形式提供程序存储的查询） 当调用[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)或[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法。  
  
 具体取决于[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性设置，ADO 可能会更改**CommandText**属性。 你可以阅读**CommandText**在任何时候，若要查看实际命令文本的属性在执行期间将使用该 ADO。  
  
 使用**CommandText**属性来设置或返回指定的资源，如文件或目录的相对 URL。 资源是相对位置的绝对 URL，或打开通过隐式显式指定[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

