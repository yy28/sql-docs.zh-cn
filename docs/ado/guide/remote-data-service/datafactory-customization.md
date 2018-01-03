---
title: "DataFactory 自定义 |Microsoft 文档"
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
helpviewer_keywords: DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11a52b760227f8dad9400c24fe6118703aea3f5f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="datafactory-customization"></a>DataFactory 自定义项
远程数据服务 (RDS) 使您能够轻松地在三层客户端/服务器系统中执行数据访问。 客户端数据控件指定连接和命令字符串参数在远程数据源或连接字符串上执行查询和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象参数，以便执行更新。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 参数进行传递到服务器的程序，后者将执行远程数据源上的数据访问操作。 RDS 提供默认的服务器程序调用[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。 **提高**对象返回任何**记录集**由对客户端的查询的对象。  
  
 但是，**提高**也仅限于执行查询和更新。 对连接或命令字符串，它不能执行任何验证或处理。  
  
 用 ADO，你可以指定**DataFactory**工作与其他类型的调用的服务器程序结合*处理程序*。 在使用访问数据源之前，该处理程序可以修改客户端连接和命令字符串。 此外，该处理程序可以强制执行访问权限，控制客户端读取和写入到数据源的数据的能力。  
  
 自定义文件的各节中指定的参数处理程序使用来修改客户端参数和访问权限。  
  
 以下主题提供有关自定义的详细信息**DataFactory**对象。  
  
-   [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [自定义文件 Connect 部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [自定义文件 Logs 部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


