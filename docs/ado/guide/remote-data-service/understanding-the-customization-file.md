---
title: 了解自定义文件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 581065868f408eca28f15ffe9fb703d53e16ae66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704135"
---
# <a name="understanding-the-customization-file"></a>了解自定义文件
自定义文件中的每个部分标头包含方括号 ( **[]** ) 包含类型和参数。 四个部分类型由文本的字符串指示**连接**， **sql**， **userlist**，或者**日志**。 参数是字符串、 默认值、 用户指定的标识符，或执行任何操作。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 因此，每个部分之一标记的以下部分标头：  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 部分标头有以下几个部分。  
  
|组成部分|Description|  
|----------|-----------------|  
|**connect**|修改连接字符串的文本字符串。|  
|**sql**|修改命令字符串的文本字符串。|  
|**userlist**|修改特定用户的访问权限的文本字符串。|  
|**logs**|一个文本字符串，指定日志文件记录操作错误。|  
|default |如果没有标识符指定或未找到，则使用一个文本字符串。|  
|*identifier*|与匹配的字符串的字符串**连接**或**命令**字符串。<br /><br /> -使用本部分中，如果部分标头包含**连接**和连接字符串中找到的标识符字符串。<br />-使用本部分中，如果部分标头包含**sql**和命令字符串中找到的标识符字符串。<br />-使用本部分中，如果部分标头包含**userlist**和标识符字符串匹配**连接**部分标识符。|  
  
 **DataFactory**调用处理程序，将客户端参数传递。 该处理程序将搜索整个字符串中的相应部分标头中的标识符进行匹配的客户端参数。 如果找到匹配项，则该节的内容应用于客户端参数。  
  
 在以下情况下使用特定的节：  
  
-   一个**连接**如果客户端的值部分连接字符串关键字，使用部分"**数据源 =** _值_"，匹配**连接**部分标识符 *。*  
  
-   **Sql**如果客户端命令字符串包含与匹配的字符串，则使用部分**sql**部分标识符。  
  
-   一个**连接**或**sql**如果没有匹配的标识符，则使用部分使用默认参数。  
  
-   一个**userlist**如果使用部分**userlist**部分标识符匹配**连接**部分标识符。 如果没有匹配项的内容**userlist**部分应用于受该连接**连接**部分。  
  
-   如果连接或命令字符串中的字符串不匹配任何标识符**连接**或**sql**部分标头，并且没有任何**连接**或**sql**部分使用默认参数的标头，则无需修改即可使用客户端字符串。  
  
-   **日志**使用部分每当**DataFactory**是在操作中。  
  
## <a name="see-also"></a>请参阅  
 [自定义文件 Connect 部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件 Logs 部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [所需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

