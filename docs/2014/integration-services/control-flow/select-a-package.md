---
title: 选择包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 026c588f2fc35a6cb256a63046ad91e5d1b5641a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388295"
---
# <a name="select-a-package"></a>选择包
  可以使用 **“选择包”** 对话框，指定消息队列任务可从中接收消息的包。  
  
## <a name="static-options"></a>静态选项  
 **位置**  
 指定包的位置。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|将位置设置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 选择此值将显示以下动态选项： **Server**、 **Use Windows Authentication**、 **Use SQL Server Authentication**、 **User name**和 **Password**。|  
|DTSX 文件|将位置设置为 DTSX 文件。 选择此值将显示动态选项 **File name**。|  
  
## <a name="location-dynamic-options"></a>位置动态选项  
  
### <a name="location--sql-server"></a>位置 = SQL Server  
 **包名称**  
 选择指定服务器上存储的包。  
  
 **Server**  
 提供服务器名称或从列表中选择一个服务器。  
  
 **Use Windows Authentication**  
 单击此项可使用 Windows 身份验证。  
  
 **Use SQL Server Authentication**  
 单击此项可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。  
  
 **用户名**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则在登录服务器时应提供要使用的用户名。  
  
 **Password**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
### <a name="location--dtsx-file"></a>位置 = DTSX 文件  
 **文件名**  
 提供包的路径，或单击浏览按钮“(…)”并查找包。  
  
## <a name="see-also"></a>请参阅  
 [消息队列任务](message-queue-task.md)  
  
  
