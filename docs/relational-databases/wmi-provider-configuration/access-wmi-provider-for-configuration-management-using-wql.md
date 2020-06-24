---
title: 使用 WQL 访问 WMI 提供程序
description: 使用此示例来了解如何在 SQL Server 中为计算机管理的 WMI 提供程序运行 Windows Management Instrumentation 查询语言语句。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8b9fa96f19bc0675a1e83db858e16605338b3899
ms.sourcegitcommit: bf5e9cb3a2caa25d0a37f401b3806b7baa5adea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2020
ms.locfileid: "85295440"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>使用 WQL 访问用于配置管理的 WMI 提供程序
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本节描述如何根据用于计算机管理的 WMI 提供程序执行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Management Instrumentation 查询语言 (WQL) 语句。  
  
 该示例使用 WQL 编辑器 WBEMtest.exe 根据 WMI 提供程序运行 WQL 查询，以枚举 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务、网络协议和别名。  
  
### <a name="querying-services-using-wbemtest"></a>使用 WBEMtest 查询服务  
  
1.  从 "**开始**" 菜单中，单击 "**运行**"，然后输入**WBEMtest**。  
  
2.  将出现 WBEMtest.exe 对话框。 单击“连接”。  
  
3.  在第一个文本字段中，键入计算机管理命名空间的 WMI 提供程序：root\Microsoft\SqlServer\ComputerManagement11。 单击“连接”。  
  
4.  单击 **“查询”**。 键入返回本地计算机上运行的当前服务的查询： ** \* 从 SqlService 中选择。** 单击“应用”。  
  
5.  通过添加**ServiceName = "MSSQLSERVER"，** 进一步细化查询。  
  
  
