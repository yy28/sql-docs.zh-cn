---
title: 加密的数据库与 AlwaysOn 可用性组 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bafd990a7c115a6108b699a61897f9e587e83c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124177"
---
# <a name="encrypted-databases-with-alwayson-availability-groups-sql-server"></a>加密的数据库与 AlwaysOn 可用性组 (SQL Server)
  本主题包含有关在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中将当前加密或最近解密的数据库与 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]一起使用的信息。  
  
 **本主题内容：**  
  
-   [限制和局限](#Restrictions)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="Restrictions"></a> 限制和局限  
  
-   如果数据库进行了加密或者数据库甚至包含数据库加密密钥 (DEK)，则您无法使用 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 或 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 将该数据库添加到某一可用性组。 即使已对加密的数据库进行了解密，其日志备份也可能包含加密的数据。 在此情况下，在该数据库上完整的初始数据同步可能会失败。 其原因在于，还原日志操作可能要求数据库加密密钥 (DEK) 使用的证书，但该证书可能不可用。  
  
     为使解密的数据库可添加到某一可用性组，请使用向导：  
  
    1.  创建主数据库的日志备份。  
  
    2.  创建主数据库的完整数据库备份。  
  
    3.  在承载辅助副本的服务器实例上，还原数据库备份。  
  
    4.  从主数据库创建新的日志备份。  
  
    5.  在辅助数据库上还原此日志备份。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [使用可用性组向导 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“将数据库添加到可用性组向导”(SQL Server Management Studio)](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [透明数据加密 (TDE)](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
