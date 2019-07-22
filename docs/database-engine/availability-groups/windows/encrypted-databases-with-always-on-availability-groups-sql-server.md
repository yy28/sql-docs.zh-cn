---
title: 将加密数据库添加到可用性组
description: 将加密（或最近解密的）数据库添加到 Always On 可用性组的步骤。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
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
ms.openlocfilehash: b5e86fe6a4f37e4ac21afb3a9aa72d80d48f3544
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000195"
---
# <a name="add-an-encrypted-database-to-an-always-on-availability-group"></a>将加密数据库添加到 Always On 可用性组
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题包含有关在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中将当前加密或最近解密的数据库与 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]一起使用的信息。  
  
 
##  <a name="Restrictions"></a> 限制和局限  
  
-   如果数据库进行了加密或者数据库甚至包含数据库加密密钥 (DEK)，则您无法使用 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 或 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 将该数据库添加到某一可用性组。 即使已对加密的数据库进行了解密，其日志备份也可能包含加密的数据。 在此情况下，在该数据库上完整的初始数据同步可能会失败。 其原因在于，还原日志操作可能要求数据库加密密钥 (DEK) 使用的证书，但该证书可能不可用。  
  
     为使解密的数据库可添加到某一可用性组，请使用向导：  
  
    1.  创建主数据库的日志备份。  
  
    2.  创建主数据库的完整数据库备份。  
  
    3.  在承载辅助副本的服务器实例上，还原数据库备份。  
  
    4.  从主数据库创建新的日志备份。  
  
    5.  在辅助数据库上还原此日志备份。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [为可用性组手动准备辅助数据库 (SQL Server)](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [使用可用性组向导 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“将数据库添加到可用性组向导”(SQL Server Management Studio)](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [透明数据加密 (TDE)](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
