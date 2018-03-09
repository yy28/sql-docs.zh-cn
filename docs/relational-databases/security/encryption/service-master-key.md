---
title: "服务主密钥 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fbbd6923b2d0bc7158266df1b3d27ecf2c8397cf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="service-master-key"></a>服务主密钥
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 服务主密钥是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密层次结构的根。 服务主密钥是首次需要它来加密其他密钥时自动生成的。 默认情况下，服务主密钥使用 Windows 数据保护 API 和本地计算机密钥进行加密。 只有创建服务主密钥的 Windows 服务帐户或有权访问服务帐户名称和密码的主体能够打开服务主密钥。  
  
 重新生成或还原服务主密钥涉及解密和重新加密完整的加密层次结构的操作。 除非危及到该密钥的安全性，否则应该在需求较低的时间段内安排这种占用大量资源的操作。  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 使用 AES-256 加密算法来保护服务主密钥 (SMK) 和数据库主密钥 (DMK)。 AES 是一种比早期版本中使用的 3DES 更新的加密算法。 在将[!INCLUDE[ssDE](../../../includes/ssde-md.md)]实例升级到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 后，应重新生成 SMK 和 DMK 以便将主密钥升级到 AES。 有关重新生成 SMK 的详细信息，请参阅 [ALTER SERVICE MASTER KEY (Transact-SQL)](../../../t-sql/statements/alter-service-master-key-transact-sql.md) 和 [ALTER MASTER KEY (Transact-SQL)](../../../t-sql/statements/alter-master-key-transact-sql.md)。  
  
## <a name="best-practice"></a>最佳实践  
 备份服务主密钥并将备份副本存储在另外一个安全位置。  
  
## <a name="related-tasks"></a>相关任务  
 [BACKUP SERVICE MASTER KEY (Transact-SQL)](../../../t-sql/statements/backup-service-master-key-transact-sql.md)  
  
 [RESTORE SERVICE MASTER KEY (Transact-SQL)](../../../t-sql/statements/restore-service-master-key-transact-sql.md)  
  
 [ALTER SERVICE MASTER KEY (Transact-SQL)](../../../t-sql/statements/alter-service-master-key-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [加密层次结构](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
