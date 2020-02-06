---
title: Ole Automation Procedures 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cb13d9b50c78ff3d067d97b2d5dd1b763e024608
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67997960"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Ole Automation Procedures 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 **Ole Automation Procedures** 选项可指定是否可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中实例化 OLE Automation 对象。 还可以使用基于策略的管理或者 **sp_configure** 存储过程来配置这一选项。 有关详细信息，请参阅 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)。  
  
 可以将 **Ole Automation Procedures** 选项设置为以下值。  
  
 0  
 禁用 OLE Automation Procedures。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]新实例的默认值。  
  
 1  
 启用 OLE Automation Procedures。  
  
 当启用 OLE Automation Procedures 时，对 **sp_OACreate** 的调用将会启动 OLE 共享执行环境。  
  
 可以使用 **sp_configure** 系统存储过程来查看和更改 **Ole Automation Procedures** 选项的当前值。  
  
## <a name="examples"></a>示例  
 以下示例显示了如何查看 OLE Automation Procedures 的当前设置。  
  
```  
EXEC sp_configure 'Ole Automation Procedures';  
GO  
```  
  
 以下示例显示了如何启用 OLE Automation Procedures。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Ole Automation Procedures', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [外围应用配置器](../../relational-databases/security/surface-area-configuration.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
