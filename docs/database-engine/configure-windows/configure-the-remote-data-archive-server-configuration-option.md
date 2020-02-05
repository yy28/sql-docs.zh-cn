---
title: 配置 remote data archive 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
author: rothja
ms.author: jroth
ms.openlocfilehash: fda2594b2dc61a78eb5900ef6d1b735dac5b44e4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012327"
---
# <a name="configure-the-remote-data-archive-server-configuration-option"></a>配置远程数据存档服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 **remote data archive** 选项，可以指定能否为服务器上的数据库和表启用延伸。 有关详细信息，请参阅 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)。  
  
 **remote data archive** 选项可以具有下列值。  
  
|值|说明|  
|-----------|-----------------|  
|0|不可以为服务器上的数据库和表启用延伸。|  
|1|可以为服务器上的数据库和表启用延伸。|  
  
 必须具有 sysadmin 或 serveradmin 权限，才能运行 **sp_configure** 来设置 **远程数据存档** 选项的值。  
  
## <a name="example"></a>示例  
 下面的示例先显示 **remote data archive** 选项的当前设置。 然后，此示例通过将 **remote data archive** 选项的值设置为 1 来启用这个选项。  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 若要禁用该选项，请将此值设置为 0。  
  
## <a name="see-also"></a>另请参阅  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
