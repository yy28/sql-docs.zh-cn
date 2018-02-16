---
title: "Oracle 补充日志记录脚本 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e6ee618-b89b-46c7-92ad-4fc5ef7b777a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4f97617decf23356dc663805494d5a2d9e2d72c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="oracle-supplemental-logging-script"></a>Oracle 补充日志记录脚本
  此对话框显示 Oracle 补充日志记录脚本。  
  
 在您准备供使用的 CDC 实例时，CDC 设计器将创建一个 Oracle SQL 脚本，该脚本为要捕获的表设置补充日志记录。 该补充日志记录脚本指示 Oracle 在更新特定表时，它写入事务日志的更改记录应包含所有有关列的数据，而不只是更改的列。  
  
 根据您的组织中的 Oracle DBA 策略，运行补充日志记录脚本可能要求 Oracle DBA 的审批。  
  
## <a name="options"></a>“常规”  
 以下是可用于执行脚本的选项。  
  
 **运行脚本**  
 对为 CDC 实例定义的表运行补充日志记录脚本。 若要运行该脚本，Oracle 用户必须对要捕获的所有表具有 ALTER TABLE 权限，并且对 DBA_LOG_GROUPS 视图具有 SELECT 权限。 此外，Oracle 用户必须具有凭据以便通过所需权限使用 Oracle 数据库。 您可以让程序提示您 Oracle 凭据，然后使用它运行该脚本。  
  
 **另存为**  
 将脚本保存到文本文件中。 这在 Oracle 数据库管理员 (DBA) 需要检查和执行补充日志记录脚本时很有用，程序会让您将该脚本保存到一个文本文件，您在以后可以通过电子邮件或其他方式将该文件发送给 Oracle DBA 以便执行（通过使用 SQL*Plus Oracle 实用工具或用于在 Oracle 数据库上运行脚本的其他工具）。  
  
 **复制**  
 将脚本复制到剪贴板。 在就绪后，在 Oracle 数据库管理员 (DBA) 需要检查和执行补充日志记录脚本时，您可以将该脚本粘贴到您需要的任何位置。  
  
## <a name="see-also"></a>另请参阅  
 [如何管理 CDC 实例](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [管理 CDC 实例](../../integration-services/change-data-capture/manage-a-cdc-instance.md)  
  
  
