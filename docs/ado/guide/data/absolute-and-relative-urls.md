---
title: 绝对和相对 Url |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bb960fc84dd1558589918096daedf4d36d18ebf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632165"
---
# <a name="absolute-and-relative-urls"></a>绝对和相对 URL
URL 指定存储在本地或网络计算机上的目标的位置。 目标可以是文件、 目录、 HTML 页、 图像、 程序和等等 *。*  
  
 *绝对 URL*包含定位资源所需的所有信息。  
  
 一个*相对 URL*定位使用绝对 URL 作为起始点的资源。 实际上，"完整的 URL"的目标是通过串联绝对和相对 Url 的指定。  
  
 *绝对 URL*使用以下格式： *scheme://server/path/resource*  
  
 相对 URL 通常仅包含*路径*，和 （可选），*资源*，但没有*方案*或者*server*。 下表定义了完整的 URL 格式的各个部分。  
  
 *scheme*  
 指定如何*资源*要访问。  
  
 服务器  
 指定的计算机的名称，*资源*所在。  
  
 path  
 指定目录指向目标的序列。 如果*资源*是省略，目标是中的最后一个目录*路径*。  
  
 *resource*  
 如果包含，*资源*是目标，而通常是文件的名称。 可能会更*简单的文件，* 包含单个二进制流的字节，或*结构化的文档*包含一个或多个存储和的字节二进制流。  
  
## <a name="url-scheme-registration"></a>注册 URL 方案  
 如果访问接口支持的 Url，该提供程序将注册一个或多个 URL 方案。 注册意味着使用方案的任何 Url 将自动调用已注册的提供程序。 例如， *http*方案已注册到[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 ADO 假定前缀为"http"的所有 Url 都表示的 Web 文件夹或文件，以用于 Internet 发布提供程序。 有关您的提供程序注册的架构信息，请参阅提供程序文档。  
  
## <a name="defining-context-with-a-url"></a>定义上下文使用的 URL  
 打开连接，由表示的一个函数[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，以限制对数据源的后续操作由表示该连接。 也就是说，连接定义后续操作的上下文。  
  
 使用 ADO 2.7 或更高版本中，绝对 URL 还可以定义一个上下文。 例如，当[记录](../../../ado/reference/ado-api/record-object-ado.md)使用绝对 URL，打开对象**连接**隐式创建对象来表示 URL 指定资源。  
  
 可以指定绝对 URL，用于定义上下文*ActiveConnection*的参数**记录**对象[打开](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 绝对 URL 还可以指定的值作为"URL**=**"中的关键字**连接**对象[打开](../../../ado/reference/ado-api/open-method-ado-connection.md)方法*ConnectionString*参数，并[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法*ActiveConnection*参数。  
  
 此外可以通过打开定义上下文**记录**或**记录集**对象，表示一个目录，因为这些对象已有隐式或显式声明**连接**指定上下文的对象。  
  
## <a name="scoped-operations"></a>作用域内的操作  
 上下文还定义了作用域 — 即，目录和子目录可以参与后续操作。 **记录**对象有多个作用域内的方法作用于一个目录和所有子目录。 这些方法包括[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)， [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)，并[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)。  
  
## <a name="relative-urls-as-command-text"></a>为命令文本的相对 Url  
 可以指定要通过键入字符串中的数据源上执行的命令*CommandText*的参数**连接**对象的[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法，并在*源*的参数**记录集**对象的[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。  
  
 可以在指定的相对 URL *CommandText*或*源*参数。 相对 URL 不实际表示命令，例如 SQL 命令;它只是指定的参数。 活动连接的上下文必须是绝对 URL，并*选项*参数必须设置为**adCmdTableDirect**。  
  
 例如，下面的代码示例显示如何打开**记录集**Winnt/system32 目录 Readme25.txt 文件：  
  
```  
recordset.Open "system32/Readme25.txt", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 在连接字符串中的绝对 URL 指定的服务器 (`YourServer`) 和路径 (`Winnt`)。 此 URL 还定义的上下文。  
  
 命令文本中的相对 URL 的绝对 URL 用作起始点，并指定路径的其余部分 (`system32`) 和要打开的文件 (`Readme25.txt`)。  
  
 选项字段 (`adCmdTableDirect`) 指示命令类型是相对 URL。  
  
 下面的代码将作为另一个示例中，打开**记录集**上的内容`Winnt`目录：  
  
```  
recordset.Open "", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB 提供程序提供的 URL 方案  
 完全限定 URL 的前导部分是*方案*用于访问 URL 的其余部分标识的资源。 示例包括 HTTP （超文本传输协议） 和 FTP （文件传输协议）。  
  
 ADO 支持 OLE DB 访问接口识别其自己的 URL 方案。 例如， [Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*，* 访问"published"Windows 2000 文件，可以识别现有 HTTP 方案。  
  
## <a name="see-also"></a>请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
