---
title: sp_upgrade_log_shipping （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_upgrade_log_shipping
- sp_upgrade_log_shipping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_upgrade_log_shipping
ms.assetid: ee01092f-9caf-4e88-888b-ec7b84223705
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e96326c97dde209f37104e66e562b66e96c8acd3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82809000"
---
# <a name="sp_upgrade_log_shipping-transact-sql"></a>sp_upgrade_log_shipping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sp_upgrade_log_shipping 存储过程会自动调用，以便升级特定于日志传送的元数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_upgrade_log_shipping  
```  
  
## <a name="arguments"></a>参数  
 无。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或1（否则为）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>备注  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级过程中会自动调用此存储过程，以升级用于日志传送的元数据。 您不需要显式执行此过程，除非在升级过程中元数据出现问题。  
  
 sp_upgrade_log_shipping 必须在主服务器、辅助服务器或监视服务器的 master 数据库中运行。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [关于 &#40;SQL Server 的日志传送&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
