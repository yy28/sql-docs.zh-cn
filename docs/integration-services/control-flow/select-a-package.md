---
title: 选择包 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f19490ea376b4a0aa8ecae8fdaae251376a56b3c
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334771"
---
# <a name="select-a-package"></a>选择包
  可以使用 **“选择包”** 对话框，指定消息队列任务可从中接收消息的包。  
  
## <a name="static-options"></a>静态选项  
 **位置**  
 指定包的位置。 此属性具有下表所列的选项。  
  
|ReplTest1|描述|  
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
  
 **User name**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则在登录服务器时应提供要使用的用户名。  
  
 **Password**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
### <a name="location--dtsx-file"></a>位置 = DTSX 文件  
 **File name**  
 提供包的路径，或单击浏览按钮 **(…)** 并查找包。  
  
## <a name="see-also"></a>另请参阅  
 [消息队列任务](../../integration-services/control-flow/message-queue-task.md)  
  
  
