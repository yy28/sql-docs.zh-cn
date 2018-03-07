---
title: "还原 SERVICE MASTER KEY (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE SERVICE MASTER KEY
- RESTORE_SERVICE_MASTER_KEY_TSQL
- LOAD SERVICE MASTER KEY
- LOAD_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- importing Service Master Keys
- copying Service Master Keys
- service master key [SQL Server], importing
- RESTORE SERVICE MASTER KEY statement
- transferring Service Master Keys
ms.assetid: a68fd0ee-70ce-4104-aca0-fcae5f41fc38
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f88ab43c6e452bbbb3b6cfa32e858ee1f091e366
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="restore-service-master-key-transact-sql"></a>RESTORE SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从备份文件中导入服务主密钥。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
RESTORE SERVICE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password' [FORCE]  
```  
  
## <a name="arguments"></a>参数  
 文件**=***path_to_file*  
 指定存储服务主密钥的完整路径（包括文件名）。 *path_to_file*可以是本地路径或网络位置的 UNC 路径。  
  
 密码**=***密码*  
 指定对从文件中导入的服务主密钥进行解密时所需的密码。  
  
 FORCE  
 即使存在数据丢失的风险，也要强制替换服务主密钥。  
  
## <a name="remarks"></a>注释  
 当还原服务主密钥时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将对所有已使用当前服务主密钥加密的密钥和机密内容进行解密，然后使用从备份文件中加载的服务主密钥对这些密钥和机密内容进行加密。  
  
 如果有任意一种解密操作失败，则还原操作将会失败。 您可以使用 FORCE 选项忽略错误，但是该选项会使无法进行解密的数据丢失。  
  
> [!CAUTION]  
>  服务主密钥为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加密层次结构的根。 服务主密钥直接或间接地保护树中的所有其他密钥。 如果在强制的还原过程中不能对某个相关密钥进行解密，则由该密钥所保护的数据便会丢失。  
  
 重新生成加密层次结构是一种消耗大量资源的操作。 您应当将该操作安排在资源需求较低的时段进行。  
  
## <a name="permissions"></a>Permissions  
 需要对服务器的 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 以下示例从备份文件中还原服务主密钥。  
  
```  
RESTORE SERVICE MASTER KEY   
    FROM FILE = 'c:\temp_backups\keys\service_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [服务主密钥](../../relational-databases/security/encryption/service-master-key.md)   
 [ALTER SERVICE MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact SQL &#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [加密层次结构](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
