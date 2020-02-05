---
title: TRUSTWORTHY 数据库属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database property
ms.assetid: 64b2a53d-4416-4a19-acc0-664a61b45348
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ec745810697b325b8f1e1b2d5e67871136b9f089
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68126821"
---
# <a name="trustworthy-database-property"></a>TRUSTWORTHY 数据库属性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  TRUSTWORTHY 数据库属性用于指明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例是否信任该数据库以及其中的内容。 默认情况下，此设置为 OFF，但是可以使用 ALTER DATABASE 语句将其设置为 ON。 例如，`ALTER DATABASE AdventureWorks2012 SET TRUSTWORTHY ON;` 。  
  
> [!NOTE]  
>  必须是 **sysadmin** 固定服务器角色的成员才能设置此选项。  
  
 此属性可用于减少附加数据库所带来的某些隐患，该数据库包含下列对象之一：  
  
-   带有 EXTERNAL_ACCESS 或 UNSAFE 权限设置的有害程序集。 有关详细信息，请参阅 [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md)。  
  
-   所定义的、作为高特权用户执行的有害模块。 有关详细信息，请参阅 [EXECUTE AS 子句 (Transact-SQL)](../../t-sql/statements/execute-as-clause-transact-sql.md)。  
  
 这两种情况均要求具有特定程度的权限，并且在已附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的数据库的上下文中使用这两种情况时，应采取相应的机制保护这两种情况。 但是，如果数据库脱机，则对数据库文件具有访问权限的用户可能会将其附加到其选择的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，并将有害内容添加到数据库中。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中分离和附加数据库时，将对限制访问数据库文件的数据和日志文件设置某些权限。  
  
 因为无法立即信任附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据库，所以不允许数据库访问超出数据库范围的资源，直到数据库已显式标记为可信。 因此，如果备份或分离 TRUSTWORTHY 选项设置为 ON 的数据库并将该数据库附加或还原到同一个或另一个 SQL Server 实例，则附加/还原完成后 TRUSTWORTHY 属性将设置为 OFF。 此外，旨在访问数据库以外资源的模块和带有 EXTERNAL_ACCESS 或 UNSAFE 权限设置的程序集还需要其他条件才能成功运行。  
  
## <a name="related-content"></a>相关内容  
 [SQL Server 数据库引擎和 Azure SQL Database 的安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
