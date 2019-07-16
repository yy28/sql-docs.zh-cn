---
title: ADO 历史记录 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a84ccbb97c26ea92f31212933aac79bde2784b72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927160"
---
# <a name="ado-features-for-each-release"></a>对于每个版本的 ADO 功能

本主题列出了每个版本的 ADO、 ADO MD 和 ADOX 引入的新功能。

## <a name="ado-60"></a>ADO 6.0

 ADO 6.0 包含在 Windows Vista，Windows 数据访问组件 (Windows DAC) 6.0 的一部分。 ADO 6.0 是功能上等效于 ADO 2.8。

## <a name="ado-28"></a>ADO 2.8

 ADO 2.8 已包含在 Windows XP 和 Windows Server 2003 中，作为一部分的 Microsoft 数据访问组件 (MDAC) 2.8。 MDAC 2.8 的可再发行组件版本也是可用;请注意，此可再发行组件版本仅在 Windows 2000 上安装。 ADO 2.8 解决几个与安全相关的问题：

 *外部受信任的区域不允许硬盘驱动器访问。*
在跨域脚本涉及非信任的站点，将禁用以下操作：**Stream.SaveToFile**， **Stream.LoadFromFile**， **Recordset.Save**，并且**Recordset.Open**、 与结合使用**adCmdFile**标志或使用 Microsoft OLE DB 永久性提供程序 (MSPersist)。

 **Recordset.Open** _，_ **Recordset.Save** _，_ **Stream.SaveToFile** _，和_ **Stream.LoadFromFile** _对仅限物理文件进行操作。_
现在，这些方法验证文件句柄指向仅限物理文件。

 **Recordset.ActiveCommand** _返回错误时调用的 HTML/ASP 页中。_
这可以防止**命令**对象被误用。

 _数_**记录集**_返回嵌套_**形状**_命令的上限。_
嵌套的形状命令现在返回最多为 512**记录集**。 这意味着**形状**命令不再可以嵌套在任何深度。 相反，级别的最大深度是 512，如果每个命令导致 （子级） 的单个**记录集**。 如果在任何级别**形状**命令返回多个**记录集**，深度的最大级别将为小于 512。

## <a name="ado-27"></a>ADO 2.7

 *64 位平台支持*ADO 2.7 引入了对 64 位处理器的支持。

## <a name="ado-26"></a>ADO 2.6

 **CubDef.GetSchemaObject**_方法_从 ADO 2.6 开始，ADO MD 对象可以使用检索的唯一名称，由指定[UniqueName 属性 (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md)。 无需已知的父对象的名称和父集合无需填充要检索的架构对象。 请参阅[GetSchemaObject 方法 (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md)。

 *命令流* **命令**对象作为一种方式使用流格式支持命令**CommandText**属性。 [CommandStream 属性 (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md)可用于指定 XML 模板或 updategram 作为**命令**与 Microsoft OLE DB Provider for SQL Server 的输入。

 **方言**_属性_[方言](../../ado/reference/ado-api/dialect-property.md)是一个新属性，定义的语法和提供程序使用来分析该字符串或流的一般规则。

 **Command.Execute**_方法_ [Execute 方法](../../ado/reference/ado-api/execute-method-ado-command.md)的 ADO**命令**对象已经过增强，用于输入和输出流。

 *字段 statusvalues*如果用户修改时遇到了 DB_E_ERRORSOCCURRED 错误**字段**的**记录集**，现在将填充 ADO **Field.Status**与相应的状态信息的属性，以便用户将包含有关错误原因的详细信息。 请参阅[Status 属性 （ADO 字段）](../../ado/reference/ado-api/status-property-ado-field.md)。

 **NamedParameters**_属性_ [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md)是新的属性**命令**对象，它指示提供程序应使用名为参数。

 *流中的结果集*ADO 可以从数据源中返回的结果集**Stream**，而非**记录集**对象。 使用适用于 SQL Server 的 Microsoft OLE DB 访问接口的最新版本，可以获取从提供程序 XML 结果通过执行"XML"查询。 一个**Stream**用于接收结果集可以使用作为源的"XML"命令打开。 请参阅[到流中检索结果集](../../ado/guide/data/retrieving-resultsets-into-streams.md)。

 *单行结果集*ADO**记录**对象现在可以打开上一个命令字符串或**命令**从提供程序返回一个数据行的对象。 这会导致与 MDAC 2.6 提供改进的性能。 请参阅[Open 方法 （ADO 记录）](../../ado/reference/ado-api/open-method-ado-record.md)。

## <a name="ado-25"></a>ADO 2.5

 **记录**_对象_ADO 2.5 引入了**记录**对象用于表示和管理中的行将**记录集**或数据提供程序，或对象封装半结构化的数据，例如文件或目录。

 **Stream** _对象_ADO 2.5 还引入了**Stream**对象来表示二进制或文本数据的流。

 *URL 绑定*ADO 2.5 引入了一个 URL，用作连接字符串和命令文本，来命名数据存储区对象的替代方法。 可以与现有使用某 URL**连接**和**记录集**对象，也与新一样**记录**并**Stream**对象。

 *数据访问接口支持 URL 绑定*ADO 2.5 支持 OLE DB 访问接口识别的 URL 方案。 用于 Internet 发布，也不能访问 Windows 2000 的文件系统可以识别现有 HTTP 方案，这包括 OLE DB 访问接口。
