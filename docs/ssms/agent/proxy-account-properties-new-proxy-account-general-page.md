---
title: 代理帐户属性 - 新建代理帐户（“常规”页）| Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f0d7a1ce8d98c6817b831cf858a2012cf9736169
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>代理帐户属性 - 新建代理帐户（“常规”页）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此页可以查看或更改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理帐户的属性。  
  
## <a name="options"></a>“常规”  
**代理名称**  
键入代理的名称。  
  
**凭据名称**  
键入代理的凭据名称。  
  
> [!NOTE]  
> 提供的凭据名称必须是一个现有凭据的名称。 有关创建凭据的详细信息，请参阅 [如何创建代理 (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/c1e77e91-2a69-40d9-b8b3-97cffc710586)。  
  
**...**  
启动“选择凭据”对话框。  
  
**Description**  
键入代理的说明。  
  
**对以下子系统有效**  
选择该代理帐户可以访问的子系统。  
  
**将作业步骤重新分配给**  
选择要将作业步骤重新分配给的代理。 在撤消对代理以前可访问的某个子系统的访问权限后，将启用此列表。  
  
## <a name="see-also"></a>另请参阅  
[创建 SQL Server 代理的代理帐户](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
