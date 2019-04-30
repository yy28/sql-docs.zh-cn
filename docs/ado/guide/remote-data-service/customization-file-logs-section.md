---
title: 自定义项文件记录了部分 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- logs section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: a368e264-865c-41ee-be00-d9097255c2ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71a9130c385032acfad7c0c1040b293486bff525
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214906"
---
# <a name="customization-file-logs-section"></a>自定义文件 Logs 部分
**日志**部分包含的日志文件条目，用于指定的操作过程中记录错误的文件的名称**DataFactory**。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 日志文件条目的形式：  
  
```console
  
err=  
FileName  
  
```  
  
## <a name="remarks"></a>备注  
  
|组成部分|描述|  
|----------|-----------------|  
|**err**|文本字符串，用于指示这是一个日志文件条目。|  
|*FileName*|完整的路径和文件名的名称。 典型的文件名称是**c:\msdfmap.log**。|  
  
 日志文件将包含用户名、 HRESULT、 日期和时间的每个错误。  
  
## <a name="see-also"></a>请参阅  
 [自定义文件 Connect 部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [所需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义项文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


