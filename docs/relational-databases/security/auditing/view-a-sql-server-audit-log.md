---
title: 查看 SQL Server 审核日志 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1b1f2528b4dd6c247c37f7c1d33b91ce32b52366
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="view-a-sql-server-audit-log"></a>查看 SQL Server 审核日志
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中查看 SQL Server 审核日志。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要查看 SQL Server 审核日志，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 **CONTROL SERVER** 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>查看 SQL Server 审核日志  
  
1.  在对象资源管理器中，展开“安全性”文件夹。  
  
2.  展开“审核”文件夹。  
  
3.  右键单击要查看的审核日志，然后选择“查看审核日志”。 这将打开“日志文件查看器 - server_name”对话框。 有关详细信息，请参阅 [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md)。  
  
4.  完成后，单击“关闭”。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议通过使用日志文件查看器查看审核日志。 但是，如果你要创建自动监视系统，则可以使用 [sys.fn_get_audit_file (Transact-SQL)](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) 函数直接读取审核文件中的信息。 直接读取该文件将以略有不同的（未处理的）格式返回数据。 有关详细信息，请参阅 **sys.fn_get_audit_file** 。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Audit（数据库引擎）](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [将 SQL Server 审核事件写入安全日志](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
