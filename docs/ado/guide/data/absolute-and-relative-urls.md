---
title: "绝对和相对 Url |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f0bbd79ff71ffe17c9fb33903501ab7302766fbf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="absolute-and-relative-urls"></a>绝对和相对 Url
URL 指定存储在本地或网络的计算机上的目标的位置。 目标可以是文件、 目录、 HTML 页、 图像、 程序和等等*。*  
  
 *绝对 URL*包含所有定位资源所需的信息。  
  
 A*相对 URL*查找资源使用作为起始点的绝对 URL。 实际上，"完整的 URL"的目标是通过串联绝对和相对 Url 的指定。  
  
 *绝对 URL*使用以下格式： *scheme://server/path/resource*  
  
 相对 URL 通常仅包含*路径*，和 （可选）*资源*，但不*方案*或*服务器*。 下表定义的各个部分的完整的 URL 格式。  
  
 *方案*  
 指定如何*资源*是访问。  
  
 服务器  
 指定的计算机的名称其中*资源*所在。  
  
 *路径*  
 指定目录，从而导致目标的序列。 如果*资源*是省略，目标为中的最后一个目录*路径*。  
  
 *资源*  
 如果包含，*资源*是目标，并且通常是文件的名称。 它可能是*简单文件*包含单个二进制流的字节，或*结构化的文档，*包含一个或多个存储和的字节的二进制流。  
  
## <a name="url-scheme-registration"></a>URL 方案注册  
 如果提供程序支持 Url，该提供程序将注册一个或多个 URL 方案。 注册意味着使用方案的任何 Url 将自动调用已注册的提供程序。 例如， *http*方案已注册到[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 ADO 假定所有的 Url 前缀为"http"表示 Web 文件夹或文件，才能用于 Internet 发布提供程序。 有关注册你的提供程序的方案的信息，请参阅提供程序文档。  
  
## <a name="defining-context-with-a-url"></a>定义上下文提供一个 URL  
 一个函数的打开的连接，由表示[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，以限制到数据源的后续操作由该连接。 也就是说，连接定义为后续的操作上下文。  
  
 用 ADO 2.7 或更高版本，绝对 URL 还可以定义上下文。 例如，当[记录](../../../ado/reference/ado-api/record-object-ado.md)对象将打开，其中一个绝对 URL，**连接**隐式创建对象来表示 URL 指定资源。  
  
 可以在指定定义的上下文的绝对 URL *ActiveConnection*参数**记录**对象[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 也可以作为的值指定一个绝对 URL"URL**=**"中的关键字**连接**对象[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法*ConnectionString*参数，与[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法*ActiveConnection*参数。  
  
 也可通过打开定义上下文**记录**或**记录集**对象，表示一个目录，因为这些对象已具有隐式或显式声明**连接**指定上下文的对象。  
  
## <a name="scoped-operations"></a>指定了作用域的操作  
 上下文还定义作用域-即，目录和在后续操作可以参与及其子目录。 **记录**对象具有在目录运行的多个指定了作用域的方法和所有子目录。 这些方法包括[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)，[移动记录](../../../ado/reference/ado-api/moverecord-method-ado.md)，和[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)。  
  
## <a name="relative-urls-as-command-text"></a>作为命令文本的相对 Url  
 你可以指定用于通过键入中的字符串在数据源上执行的命令*CommandText*参数**连接**对象的[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法，并在*源*参数**记录集**对象的[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。  
  
 可以在指定的相对 URL *CommandText*或*源*参数。 相对 URL 不实际表示一个命令，如 SQL 命令;它只是指定的参数。 活动连接的上下文必须是绝对 URL，与*选项*参数必须设置为**adCmdTableDirect**。  
  
 例如，下面的代码示例显示如何打开**记录集**Winnt/system32 目录 Readme25.txt 文件：  
  
```  
recordset.Open "system32/Readme25.txt", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 连接字符串中的绝对 URL 指定的服务器 (`YourServer`) 和路径 (`Winnt`)。 此 URL 还定义的上下文。  
  
 命令文本中的相对 URL 用作起始点的绝对 URL，并指定路径的其余部分 (`system32`) 和要打开的文件 (`Readme25.txt`)。  
  
 选项字段 (`adCmdTableDirect`) 指示命令类型是相对 URL。  
  
 再举一例，以下代码将打开**记录集**上的内容`Winnt`目录：  
  
```  
recordset.Open "", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB 访问接口提供的 URL 方案  
 完全限定 URL 的前导部分是*方案*用于访问 URL 的剩余部分标识的资源。 示例包括 HTTP （超文本传输协议） 和 FTP （文件传输协议）。  
  
 ADO 支持识别它们自己的 URL 方案的 OLE DB 提供程序。 例如， [Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*，*访问"已发布"Windows 2000 文件，识别现有 HTTP 方案。  
  
## <a name="see-also"></a>另请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
