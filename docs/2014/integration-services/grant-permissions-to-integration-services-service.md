---
title: 向 Integration Services 服务授予权限 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c2caa68-7834-4ea0-bd77-4f3a7c86d634
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 32b8ee36951ec828340de5c6d581f0b8d8bc919a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124821"
---
# <a name="grant-permissions-to-integration-services-service"></a>授予 Integration Services 服务权限
  在以前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中，在您安装了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 后，默认情况下 Users 组中的所有用户都已对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务具有访问权限。 在您安装当前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]时，用户无权访问 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。 该服务默认是安全的。 在安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 后，管理员必须授予对服务的访问权限。  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>授予对 Integration Services 服务的访问权限  
  
1.  运行 Dcomcnfg.exe。 Dcomcnfg.exe 提供用于修改注册表中的某些设置的用户界面。  
  
2.  在“组件服务”对话框中，展开“组件服务 > 计算机 > 我的电脑 > DCOM 配置”节点。  
  
3.  右键单击**Microsoft SQL Server Integration Services 12.0**，然后单击**属性**。  
  
4.  在 **“安全性”** 选项卡上，在 **“启动和激活权限”** 区域中单击 **“编辑”** 。  
  
5.  添加用户并分配适当的权限，然后单击“确定”。  
  
6.  对于访问权限重复步骤 4 和 5。  
  
7.  重新启动 SQL Server Management Studio。  
  
8.  重新启动 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务。  
  
  