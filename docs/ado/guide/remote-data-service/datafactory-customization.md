---
title: 自定义 DataFactory |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bdc406778bea0d6355e747998d2517b841fc17b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922773"
---
# <a name="datafactory-customization"></a>自定义 DataFactory
远程数据服务 (RDS) 提供了一种方法轻松地在三层客户端/服务器系统中执行数据访问。 客户端数据控件指定远程数据源或连接字符串上执行查询的连接和命令的字符串参数和[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象参数，以执行更新。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 参数传递到服务器的程序，后者将执行对远程数据源的数据访问操作。 RDS 提供了默认的服务器程序调用[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象。 **提高**对象返回任何**记录集**对客户端的查询生成的对象。  
  
 但是，**提高**限制为执行查询和更新。 它不能执行任何验证或处理对连接或命令字符串。  
  
 使用 ADO 中，可以指定**DataFactory**与另一种名为的服务器程序一起工作*处理程序*。 它们用于访问数据源之前，该处理程序可以修改客户端连接和命令字符串。 此外，该处理程序可以强制执行访问权限，控制客户端读取，并将数据写入到数据源的功能。  
  
 自定义项文件的节中指定的参数处理程序使用来修改客户端参数和访问权限。  
  
 以下主题提供有关自定义的详细信息**DataFactory**对象。  
  
-   [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [自定义文件 Connect 部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [自定义文件 Logs 部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


