---
title: "自定义文件连接部分 |Microsoft 文档"
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
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0b18fd84d31e95aa2973dd0d5377fbc8f51fafe4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="customization-file-connect-section"></a>自定义文件连接部分
处理程序的默认行为是拒绝所有连接。 **连接**节指定该行为的例外情况。 例如，如果所有**连接**节都不存在或为空，则默认情况下无法不建立任何连接。  
  
 **连接**部分可以包含：  
  
-   指定默认值的默认访问项读取和写入允许对此连接执行操作。 如果部分中没有任何默认访问项，则将忽略该节。  
  
-   一个新的连接字符串，将客户端的连接字符串。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 默认访问条目的格式为：  
  
```  
  
Access=  
accessRight  
  
```  
  
 替换连接字符串条目的格式为：  
  
```  
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Remarks  
  
|组成部分|Description|  
|----------|-----------------|  
|**“连接”**|一个文本字符串，指示这是连接字符串条目。|  
|***connectionString***|一个字符串，将整个客户端的连接字符串。|  
|**访问**|一个文本字符串，指示这是访问条目。|  
|***种***|以下的访问权限之一：<br /><br /> -   **NoAccess** -用户将无法访问数据源。<br />-   **ReadOnly** -用户可以读取的数据源。<br />-   **ReadWrite** -用户可以读取或写入到数据源。|  
  
 如果你想要允许任何连接 （实际上，禁用默认处理程序行为），在中设置的访问项**连接默认**部分到`Access=ReadWrite`，并删除或注释掉任何其他**连接***标识符*部分。  
  
## <a name="see-also"></a>另请参阅  
 [自定义文件日志部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自定义项](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



