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
author: rothja
ms.author: jroth
ms.openlocfilehash: 934b982004bf27e28a8daeed09061101886ce444
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749881"
---
# <a name="customization-file-sql-section"></a>自定义文件 SQL 部分
**Sql**部分可以包含替换客户端命令字符串的新 sql 字符串。 如果部分中没有 SQL 字符串，则将忽略该部分。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 新的 SQL 字符串可能已*参数化*。 也就是说， **sql**部分 sql 字符串中的参数（由 "？" 字符指定）可以由客户端命令字符串中的*标识符*（用括号括起以逗号分隔的列表指定）中的相应参数替换。 标识符和参数列表的行为类似于函数调用。  
  
 例如，假设客户端命令字符串为 `"CustomerByID(4)"` ，SQL 节标头为 `[SQL CustomerByID]` ，而新的 SQL 部分字符串为，则 `"SELECT * FROM Customers WHERE CustomerID = ?".` 处理程序将生成 `"SELECT * FROM Customers WHERE CustomerID = 4"` 并使用该字符串来查询数据源。  
  
 如果新 SQL 语句为空字符串（""），则忽略该部分。  
  
 如果新的 SQL 语句字符串无效，则语句的执行将失败。 有效地忽略客户端参数。 您可以通过指定以下内容来特意 "关闭" 所有客户端 SQL 命令：  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>语法  
 替换 SQL 字符串条目的格式如下：  
  
 **SQL =**   
 ***sqlString***  
  
|组成部分|说明|  
|----------|-----------------|  
|**SQL**|指示这是一个 SQL 节条目的文字字符串。|  
|***sqlString***|替换客户端字符串的 SQL 字符串。|  
  
## <a name="see-also"></a>另请参阅  
 [自定义文件连接部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件日志部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


