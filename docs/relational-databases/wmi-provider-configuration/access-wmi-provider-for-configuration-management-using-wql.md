---
title: "访问 WMI 提供程序的配置管理使用 WQL |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e56590202577f6be6c9009237137b4a6909c9542
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>使用 WQL 访问用于配置管理的 WMI 提供程序
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本节描述如何根据用于计算机管理的 WMI 提供程序执行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Management Instrumentation 查询语言 (WQL) 语句。  
  
 该示例使用 WQL 编辑器 WBEMtest.exe 根据 WMI 提供程序运行 WQL 查询，以枚举 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、网络协议和别名。  
  
### <a name="querying-services-using-wbemtest"></a>使用 WBEMtest 查询服务  
  
1.  从**启动**菜单上，单击**运行**，然后输入**WBEMtest**。  
  
2.  将出现 WBEMtest.exe 对话框。 单击 **“连接”**。  
  
3.  在第一个文本字段中，键入计算机管理命名空间的 WMI 提供程序：root\Microsoft\SqlServer\ComputerManagement11。 单击 **“连接”**。  
  
4.  单击**查询**。 键入该查询将返回本地计算机上运行的当前服务：**选择\*从 SqlService。** 单击 **“应用”**。  
  
5.  通过添加进一步细化查询**其中 ServiceName ="MSSQLSERVER"**。  
  
  
