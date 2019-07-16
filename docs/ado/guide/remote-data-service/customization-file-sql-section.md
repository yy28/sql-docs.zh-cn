---
title: 自定义文件 SQL 部分 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6163a5b5fd0999e17e17961639e0a1fee3e8fa4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922787"
---
# <a name="customization-file-sql-section"></a>自定义文件 SQL 部分
**Sql**部分可以包含一个新的 SQL 字符串，将客户端的命令字符串。 是否存在任何 SQL 字符串的部分中，将忽略该节。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 新的 SQL 字符串可能*参数化*。 它是中的参数**sql**部分 SQL 字符串 (由？ 字符) 可以替换为中的相应参数*标识符*客户端命令字符串中 (由指定以逗号分隔的列表在括号中）。 标识符和参数列表类似于函数调用。  
  
 例如，假定客户端命令字符串是`"CustomerByID(4)"`，SQL 部分标头`[SQL CustomerByID]`，并且新的 SQL 部分字符串`"SELECT * FROM Customers WHERE CustomerID = ?".`处理程序将生成`"SELECT * FROM Customers WHERE CustomerID = 4"`并使用该字符串来查询数据源。  
  
 如果新的 SQL 语句是空字符串 ("")，则忽略该节。  
  
 如果新的 SQL 语句字符串不是有效的该语句的执行将失败。 有效地忽略客户端参数。 要做到这有意来"关闭"客户端的所有 SQL 命令通过指定：  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>语法  
 替换 SQL 字符串条目的形式：  
  
 **SQL=**    
 ***sqlString***  
  
|组成部分|描述|  
|----------|-----------------|  
|**SQL**|文本字符串，用于指示这是一个 SQL 部分实体。|  
|***sqlString***|将客户端的字符串为 SQL 字符串。|  
  
## <a name="see-also"></a>请参阅  
 [自定义文件 Connect 部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件 Logs 部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [所需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义项文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


