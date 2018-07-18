---
title: 客户端和服务器端 XML 格式化 (SQLXML 4.0) 的体系结构 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], XML formatting architecture
- SQLOLEDB provider
- client-side XML formatting
- data providers [SQLXML], XML formatting architecture
- SQLNCLI, XML
- server-side XML formatting
- SQL Server Native Client, XML
- SQLXMLOLEDB Provider, XML formatting architecture
ms.assetid: 52440d9e-89fd-4c15-a008-a1ea99f41387
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 32fd7cf959e5dbf87b0052e32f796428ede3f040
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38035549"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>客户端和服务器端 XML 格式的体系结构 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  下图显示服务器端的 XML 格式的体系结构。  
  
 ![服务器端 XML 格式的体系结构。](../../../relational-databases/sqlxml/formatting/media/serversidexml.gif "服务器端体系结构的 XML 格式。")  
  
 在该示例中，在客户端上指定的命令将发送到服务器。 服务器生成 XML 文档，并将它返回到客户端。 在这种情况下，服务器具有的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 利用服务器端 XML 格式，可以使用 SQLXMLOLEDB 访问接口或 SQLOLEDB 访问接口。  SQLXMLOLEDB 访问接口使用 Sqlxml4.dll，后者包含在 SQLXML 4.0 中。 使用 SQLOLEDB 访问接口时，默认情况下您将获得由 Sqlxmlx.dll 提供的 SQLXML 功能，该 DLL 随 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 提供或者随附在 Microsoft 数据访问组件 (MDAC) 2.6 或更高版本中。 若要配合使用 Sqlxml4.dll 和 SQLOLEDB，必须在 SQLOLEDB 连接对象上设置为"SQLXML.4.0"SQLXML Version 属性。 在这两种情况下，服务器都将生成 XML 文档，并将它发送到客户端。  
  
> [!NOTE]  
>  XPath 查询和 Updategram 将在客户端上进行分析。 若要获得 SQLXML 4.0 中的 XPath 模板或 Updategram 功能，请使用 Sqlxml4.dll。  
  
 下图显示客户端的 XML 格式的体系结构：  
  
 ![在客户端 XML 格式的体系结构。](../../../relational-databases/sqlxml/formatting/media/clientsidexml.gif "客户端上的体系结构的 XML 格式。")  
  
 在该示例中，客户端使用 SQLXMLOLEDB 访问接口。 连接字符串中的数据提供程序属性必须设置为 SQLOLEDB。 （在 SQLXML 4.0 中这是唯一接受的值。）在客户端上执行的命令将发送到服务器。 在服务器上生成的行集则发送到客户端。 由行集转换至 XML 文档的格式设置操作将在客户端上执行。  
  
 在 SQLXML 4.0 中，可以将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) 或 SQLOLEDB 访问接口用作数据访问接口。 您应当可以访问任何数据源。 只要查询返回单个行集，就可以在客户端应用 XML 转换。  
  
  
