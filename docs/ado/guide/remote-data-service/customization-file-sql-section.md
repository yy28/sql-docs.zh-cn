---
title: 自定义文件 SQL 部分 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f6cc8d75883f06acf449aba74341f86a8ae017b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274166"
---
# <a name="customization-file-sql-section"></a>自定义文件 SQL 部分
**Sql**部分可以包含一个新的 SQL 字符串，将客户端的命令字符串。 如果部分中没有任何 SQL 字符串，则将忽略该节。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 新的 SQL 字符串可能*参数化*。 即中的参数**sql**部分 SQL 字符串 (由？ 字符) 可由中相应自变量替换*标识符*中客户端命令字符串 (由以逗号分隔列表在括号中）。 标识符和自变量列表的行为与函数调用。  
  
 例如，假定客户端命令字符串是`"CustomerByID(4)"`，SQL 部分标头是`[SQL CustomerByID]`，而且该新的 SQL 部分字符串`"SELECT * FROM Customers WHERE CustomerID = ?".`处理程序将生成`"SELECT * FROM Customers WHERE CustomerID = 4"`并使用该字符串来查询数据源。  
  
 如果新的 SQL 语句是空字符串 ("")，则将忽略该节。  
  
 如果新的 SQL 语句字符串不是有效的则该语句的执行将失败。 有效地忽略客户端参数。 你可以这样做有意来"关闭"客户端的所有 SQL 命令通过指定：  
  
```  
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>语法  
 替换 SQL 字符串条目的格式为：  
  
 **SQL=**   
 ***sqlString***  
  
|组成部分|Description|  
|----------|-----------------|  
|**SQL**|一个文本字符串，指示这是 SQL 部分条目。|  
|***sqlString***|SQL 字符串，将客户端的字符串。|  
  
## <a name="see-also"></a>请参阅  
 [自定义文件连接部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件日志部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自定义项](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


