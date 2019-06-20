---
title: CommandText 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7ebc6a783aa8520c3ab16465143acdf1a6bf6628
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698947"
---
# <a name="commandtext-property-ado"></a>CommandText 属性 (ADO)
指示要对提供程序发出的命令的文本。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 获取或设置**字符串**值，该值包含提供程序命令，例如 SQL 语句、 表名称、 相对 URL 或存储的过程调用。 默认值为空字符串 ("")。  
  
## <a name="remarks"></a>备注  
 使用**CommandText**属性设置或返回由表示命令的文本[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。 通常，这将为 SQL 语句，但也可以是任何其他类型的识别的提供程序，例如存储的过程调用的命令语句。 SQL 语句必须是特定语句或提供程序的查询处理器支持的版本。  
  
 如果[已准备](../../../ado/reference/ado-api/prepared-property-ado.md)的属性**命令**对象设置为**True**并**命令**设置时，将对象绑定到打开的连接**CommandText**属性，ADO 准备查询 （即，已编译的存储提供程序的查询形式） 时调用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)或[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法。  
  
 具体取决于[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性设置，则 ADO 可能会更改**CommandText**属性。 可以读取**CommandText**任何时候若要查看实际的命令文本的属性在执行期间将使用该 ADO。  
  
 使用**CommandText**属性来设置或返回指定的资源，如文件或目录的相对 URL。 资源是相对于显式指定绝对 URL，或隐式打开位置[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
