---
title: 自定义文件 UserList 部分 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b499f06254a482deea2c90f2fc570b8bb7c9d43e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516746"
---
# <a name="customization-file-userlist-section"></a>自定义文件 UserList 部分
**Userlist**部分是关于**连接**的相同部分与部分*标识符*参数。  
  
 此部分可以包含*用户访问权限条目*，它指定访问权限为指定的用户和重写*默认**访问项*匹配中**连接**部分。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 用户访问项的形式：  
  
 *userName* **=**   
 ***accessRights***  
  
|组成部分|Description|  
|----------|-----------------|  
|*userName*|*用户名*表示使用此连接的人员。 有效的用户名称与 IIS 建立**Service Manager**对话框。|  
|***accessRights***|以下访问权限之一：<br /><br /> -   **NoAccess** -用户无法访问数据源。<br />-   **ReadOnly** -用户可以读取的数据源。<br />-   **ReadWrite** -用户可以读取或写入到数据源。|  
  
## <a name="see-also"></a>请参阅  
 [自定义文件 Connect 部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件 Logs 部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [所需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义项文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


