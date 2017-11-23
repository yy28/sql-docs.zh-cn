---
title: "授予 Web 服务器计算机的来宾权限 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3935d66bdd1dfb412f5410b245231036ae025823
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>来宾特权授予 Web 服务器计算机
匿名的 Web 服务器帐户 (IUSR_*ComputerName*) 必须添加到来宾本地 Web 服务器计算机上要使用的组 rds.  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>若要将 Web 服务器计算机的来宾特权授予  
  
1.  你的 Microsoft Windows 2000 Server 计算机上，单击**启动**，指向**程序**，指向**管理工具**，然后单击**计算机管理**。  
  
2.  在控制台树中，在**本地用户和组**，单击**组**。  
  
3.  选择**来宾**本地组。 从**操作**菜单上，选择**属性**。  
  
4.  在**来宾属性**对话框中，单击**添加**。  
  
5.  如果在列表中不显示匿名的 Web 服务器帐户**选择用户或组**对话框框中，键入其名称 (IUSR_*ComputerName*) 到底部空白框中，然后单击**添加**.  
  
6.  单击 **“确定”**。


