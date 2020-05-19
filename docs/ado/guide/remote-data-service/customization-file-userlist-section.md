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
author: rothja
ms.author: jroth
ms.openlocfilehash: 002bb8b92105547086ea8649a877b4a9d6f71d3b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749799"
---
# <a name="customization-file-userlist-section"></a>自定义文件 UserList 部分
**Userlist**部分适用于具有相同节*标识符*参数的**connect**部分。  
  
 此部分可以包含一个*用户访问条目*，该条目指定指定用户的访问权限，并覆盖匹配**连接**部分中的*默认**访问条目*。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 用户访问条目的格式为：  
  
 _用户名_**=**   
 **_accessRights_**  
  
|组成部分|说明|  
|----------|-----------------|  
|*用户名*|采用此连接的人员的*用户名*。 有效用户名与 IIS **Service Manager**对话框建立在一起。|  
|**_accessRights_**|以下访问权限之一：<br /><br /> -   **NoAccess** -用户无法访问数据源。<br />-   **ReadOnly** -用户可以读取数据源。<br />-   **ReadWrite** -用户可以读取或写入数据源。|  
  
## <a name="see-also"></a>另请参阅  
 [自定义文件连接部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件日志部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


