---
title: "ADO 历史记录 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ace4237c41b4a92b62e958970ebb49dcf2156d0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="ado-features-for-each-release"></a>每个版本的 ADO 功能
本主题列出每个版本的 ADO、 ADO MD 和 ADOX 引入的新功能。

## <a name="ado-60"></a>ADO 6.0
 在 Windows Vista 中，作为 Windows 数据访问组件 (Windows DAC) 6.0 的一部分包括 ADO 6.0。 ADO 6.0 在功能上等效于 ADO 2.8。

## <a name="ado-28"></a>ADO 2.8
 ADO 2.8 已包含在 Windows XP 和 Windows Server 2003 中，作为一部分的 Microsoft 数据访问组件 (MDAC) 2.8。 MDAC 2.8 的可再发行组件版本也是可用;请注意，此可再发行组件版本仅在 Windows 2000 上安装。 ADO 2.8 解决几个与安全相关的问题：

 *受信任区域之外不允许硬盘驱动器访问。*
在跨域脚本涉及非信任的站点，会禁用以下操作： **Stream.SaveToFile**， **Stream.LoadFromFile**， **Recordset.Save**，和**Recordset.Open**、 结合使用**adCmdFile**标志或与 Microsoft OLE DB 持久性提供程序 (MSPersist)。

 **Recordset.Open** *，***Recordset.Save** *，***Stream.SaveToFile** *，和* **Stream.LoadFromFile***物理的文件进行操作。        *
这些方法现在验证文件句柄指向仅限于物理文件。

 **Recordset.ActiveCommand***返回调用从 HTML/ASP 页时出错。  *
这可以防止**命令**被误用的对象。

 *数***记录集***返回嵌套***形状***命令具有上限。        *
嵌套的形状命令现在返回最多 512 个**记录集**。 这意味着，**形状**不再可以在任何深度嵌套命令。 相反，最大级别深度是 512，如果每个命令结果在一次 （子级）**记录集**。 如果是，在任何级别**形状**命令将返回多个**记录集**，最大深度级别将小于 512。

## <a name="ado-27"></a>ADO 2.7
 *64 位平台支持*ADO 2.7 引入了对 64 位处理器支持。

## <a name="ado-26"></a>ADO 2.6
 **CubDef.GetSchemaObject***方法*从 ADO 2.6 开始，ADO MD 检索对象，可以使用唯一的名称，作为指定的[UniqueName 属性 (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)。   父对象的名称不必已知的也不需父集合填充，以便检索的架构对象。 请参阅[GetSchemaObject 方法 (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)。

 *命令流***命令**对象支持命令以流格式作为使用的替代方法**CommandText**属性。 [CommandStream 属性 (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md)可以用来指定 XML 模板或作为 updategram**命令**带有 Microsoft OLE DB Provider for SQL Server 的输入。

 **方言***属性*[方言](../../ado/reference/ado-api/dialect-property.md)是一个新属性，定义的语法和一般规则提供程序使用来分析字符串或流。  

 **Command.Execute***方法*[执行方法](../../ado/reference/ado-api/execute-method-ado-command.md)的 ADO**命令**对象已得到增强，以用于输入和输出的流。  

 *字段 statusvalues*如果修改时，则在用户遇到 DB_E_ERRORSOCCURRED 错误**字段**的**记录集**，现在将填充 ADO **Field.Status**与相应的状态信息的属性，以便用户都具有有关发生的问题的详细信息。 请参阅[状态属性 （ADO 字段）](../../ado/reference/ado-api/status-property-ado-field.md)。

 **NamedParameters***属性* [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md)是的一个新属性**命令**对象，它指示提供程序应使用名为参数。  

 *在流的结果集*ADO 可以从数据源中返回的结果集**流**，而不是**记录集**对象。 适用于 SQL Server 使用的 Microsoft OLE DB 提供程序的最新版本，你可以获取 XML 结果从提供程序通过执行"XML"查询。 A**流**接收结果集中可以使用作为源的"XML"命令打开。 请参阅[到流中检索结果集](../../ado/guide/data/retrieving-resultsets-into-streams.md)。

 *单行结果集*ADO**记录**对象现在可以打开上的命令字符串或**命令**从提供程序返回的数据的一个行的对象。 这会导致与 MDAC 2.6 提供程序的改进性能。 请参阅[Open 方法 （ADO 记录）](../../ado/reference/ado-api/open-method-ado-record.md)。

## <a name="ado-25"></a>ADO 2.5
 **记录***对象*ADO 2.5 引入了**记录**对象来表示和管理中的行将**记录集**或数据提供程序或对象封装半结构化的数据，如文件或目录。

 **流***对象*ADO 2.5 还引入了**流**对象以代表二进制或文本数据的流。

 *URL 绑定*ADO 2.5 引入了一个 URL，将用作连接字符串和命令文本，名称数据存储对象的替代方法。 可以使用某 URL 与现有**连接**和**记录集**对象，以及与新一样**记录**和**流**对象。

 *数据访问接口支持 URL 绑定*ADO 2.5 支持识别 URL 方案的 OLE DB 提供程序。 这包括用于 Internet 发布，也不能访问 Windows 2000 文件系统可识别现有的 HTTP 方案的 OLE DB 提供程序。

