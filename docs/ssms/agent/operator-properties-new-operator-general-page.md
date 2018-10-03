---
title: 操作员属性 - 新建操作员（“常规”页）| Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.operator.general.f1
ms.assetid: c036d1c9-83d1-4a95-b67e-29d283b1a046
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 253d1630db6cc6c16166226b89d6d8705d88a9ac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673195"
---
# <a name="operator-properties---new-operator-general-page"></a>操作员属性 - 新建操作员（“常规”页）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此页可查看和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理操作员的常规属性。  
  
## <a name="options"></a>选项  
**名称**  
更改操作员的名称。  
  
**已启用**  
启用操作员。 在未启用时，不会向操作员发送通知。  
  
**电子邮件名称**  
指定操作员的电子邮件地址。  
  
**Net send 地址**  
指定用于 **net send**的地址。  
  
**寻呼电子邮件名称**  
指定用于操作员的寻呼程序的电子邮件地址。  
  
**寻呼值班计划**  
设置寻呼程序处于活动状态的时间。  
  
**星期一 - 星期日**  
选择寻呼程序在一周中的哪些天处于活动状态。  
  
**工作日开始**  
选择一天之中的特定时间， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在该时间之后才可向寻呼程序发送消息。  
  
**工作日结束**  
选择一天之中的特定时间， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在该时间之后不再向寻呼程序发送消息。  
  
## <a name="see-also"></a>另请参阅  
[运算符](../../ssms/agent/operators.md)  
  
