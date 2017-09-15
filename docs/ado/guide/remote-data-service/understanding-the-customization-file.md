---
title: "了解自定义文件 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cadf89ac579b11ab829ecd288fec77df81eb0603
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-the-customization-file"></a>了解自定义文件
自定义文件中的每个部分标头包含方括号 (**[]**) 包含的类型和参数。 文字字符串由指示四个部分类型**连接**， **sql**， **userlist**，或**日志**。 该参数是文字字符串、 默认值、 用户指定的标识符，或执行任何操作。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 因此，每个部分将标有以下部分标头之一：  
  
```  
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 节标头包含以下部分。  
  
|组成部分|Description|  
|----------|-----------------|  
|**连接**|修改连接字符串的文本字符串。|  
|**sql**|修改的命令字符串的文本字符串。|  
|**用户列表**|修改的特定用户的访问权限的文本字符串。|  
|**日志**|一个文本字符串，指定录制操作的错误日志文件。|  
|**默认值**|如果没有标识符指定或未找到，则使用一个文本字符串。|  
|*标识符*|与中的字符串匹配的字符串**连接**或**命令**字符串。<br /><br /> -使用本部分，如果部分标头包含**连接**和连接字符串中找到的标识符字符串。<br />-使用本部分，如果部分标头包含**sql**和命令字符串中找到的标识符字符串。<br />-使用本部分，如果部分标头包含**userlist**和标识符字符串匹配**连接**部分标识符。|  
  
 **DataFactory**调用处理程序，传递客户端参数。 处理程序搜索整个字符串中匹配相应的部分标头中的标识符的客户端参数。 如果找到匹配项，则该节的内容应用于客户端参数。  
  
 在下列情况下使用特定的部分：  
  
-   A**连接**如果客户端的值部分连接字符串关键字，使用部分"**数据源 =***值*"，与匹配**连接**部分标识符*。*  
  
-   **Sql**如果客户端命令字符串包含与匹配的字符串，则使用部分**sql**部分标识符。  
  
-   A**连接**或**sql**没有匹配的标识符是否使用带默认参数的部分。  
  
-   A **userlist**如果使用节**userlist**部分标识符匹配**连接**部分标识符。 如果没有匹配项的内容**userlist**部分应用于受连接**连接**部分。  
  
-   如果连接或命令字符串中的字符串不匹配中任何标识符**连接**或**sql**部分标头，并且没有任何**连接**或**sql**部分带默认参数，标头，则无需修改使用客户端字符串。  
  
-   **日志**使用节每当**DataFactory**正在运行。  
  
## <a name="see-also"></a>另请参阅  
 [自定义文件连接部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件日志部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自定义项](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)





















