---
title: 自定义文件 Connect 部分 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 627bbbafd272b6bb7682b776132445041207f8e1
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133327"
---
# <a name="customization-file-connect-section"></a>自定义文件 Connect 部分
该处理程序的默认行为是拒绝所有连接。 **连接**节指定该行为的例外情况。 例如，如果所有**连接**部分已不存在或为空，则默认情况下无法不建立任何连接。  
  
 **连接**部分可以包含：  
  
-   默认访问项的指定的默认读取和写入操作允许对此连接。 如果在部分中没有任何默认访问权限条目，将忽略该节。  
  
-   新的连接字符串，用于替换客户端连接字符串。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 默认访问项的形式：  
  
```console
  
Access=  
accessRight  
  
```  
  
 替换连接字符串条目的形式：  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>备注  
  
|组成部分|Description|  
|----------|-----------------|  
|**“连接”**|文本字符串，用于指示这是一个连接字符串条目。|  
|**_ConnectionString_**|一个字符串，将整个客户端的连接字符串。|  
|**访问**|文本字符串，用于指示这是访问项。|  
|**_种_**|以下访问权限之一：<br /><br /> -   **NoAccess** -用户无法访问数据源。<br />-   **ReadOnly** -用户可以读取的数据源。<br />-   **ReadWrite** -用户可以读取或写入到数据源。|  
  
 如果你想要允许任何连接 （实际上，禁用默认处理程序行为），在中设置的访问权限条目**连接默认**部分`Access=ReadWrite`，然后删除或注释掉任何其他**连接**_标识符_部分。  
  
## <a name="see-also"></a>请参阅  
 [自定义文件 Logs 部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [所需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义项文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



