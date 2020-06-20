---
title: 客户端和服务器端 XML 格式的体系结构（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ae1a9c60a7a7966f4eff2a08b4557487f5aec58c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065713"
---
# <a name="architecture-of-client-side-and-server-side-xml-formatting-sqlxml-40"></a>客户端和服务器端 XML 格式的体系结构 (SQLXML 4.0)
  下图显示服务器端的 XML 格式的体系结构。  
  
 ![服务器端 XML 格式的体系结构。](../../../database-engine/dev-guide/media/serversidexml.gif "服务器端 XML 格式的体系结构。")  
  
 在该示例中，在客户端上指定的命令将发送到服务器。 服务器生成 XML 文档，并将它返回到客户端。 在这种情况下，服务器有一个实例 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 利用服务器端 XML 格式，可以使用 SQLXMLOLEDB 访问接口或 SQLOLEDB 访问接口。  SQLXMLOLEDB 访问接口使用 Sqlxml4.dll，后者包含在 SQLXML 4.0 中。 使用 SQLOLEDB 访问接口时，默认情况下您将获得由 Sqlxmlx.dll 提供的 SQLXML 功能，该 DLL 随 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 提供或者随附在 Microsoft 数据访问组件 (MDAC) 2.6 或更高版本中。 若要将 Sqlxml4.dll 与 SQLOLEDB 一起使用，必须将 SQLOLEDB 版本属性设置为 SQLOLEDB 连接对象上的 "SQLXML. 4.0"。 在这两种情况下，服务器都将生成 XML 文档，并将它发送到客户端。  
  
> [!NOTE]  
>  XPath 查询和 Updategram 将在客户端上进行分析。 若要获得 SQLXML 4.0 中的 XPath 模板或 Updategram 功能，请使用 Sqlxml4.dll。  
  
 下图显示客户端的 XML 格式的体系结构：  
  
 ![客户端 XML 格式的体系结构。](../../../database-engine/dev-guide/media/clientsidexml.gif "客户端 XML 格式的体系结构。")  
  
 在该示例中，客户端使用 SQLXMLOLEDB 访问接口。 在连接字符串中，数据访问接口属性必须设置为 SQLOLEDB。 （这是 SQLXML 4.0 中唯一接受的值。）在客户端上执行的命令将发送到服务器。 在服务器上生成的行集则发送到客户端。 由行集转换至 XML 文档的格式设置操作将在客户端上执行。  
  
 在 SQLXML 4.0 中，可以将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) 或 SQLOLEDB 访问接口用作数据访问接口。 您应当可以访问任何数据源。 只要查询返回单个行集，就可以在客户端应用 XML 转换。  
  
  
