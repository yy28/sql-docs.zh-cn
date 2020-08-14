---
title: 导入基于策略的管理策略 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54e0ca12595b0ce8bdde128c9261918c910ffdcf
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934342"
---
# <a name="import-a-policy-based-management-policy"></a>导入基于策略的管理策略
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中导入基于策略的管理策略实例。  
  
## <a name="permissions"></a>权限
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。

  
##  <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
  
### <a name="to-import-a-policy-instance"></a>导入策略实例  
  
1.  在“对象资源管理器” **** 中，单击加号以展开新导入的策略实例要存储到的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”**。  
  
4.  右键单击“策略”**** 文件夹，然后选择“导入策略”****。  
  
5.  在“导入”**** 对话框中，键入该文件的路径和名称；或者使用“浏览”按钮 (**...**) 查找包含策略的 XML 文件，然后选择该文件。 有关 **“导入”** 对话框中可用选项的详细信息，请参阅 [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md)。  
  
6.  完成后，单击 **“确定”** 。  


## <a name="example-policies"></a>示例策略
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中没有示例策略，但你可安装 [SQL Server Management Studio v17](../../ssms/release-notes-ssms.md#previous-ssms-releases) 来访问之前分发的示例策略。  安装 SQL Server Management Studio v17 后，可在 `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Policies` 中找到示例策略。 可导入这些策略，并将其用作你自己基于策略的管理策略的基础。
