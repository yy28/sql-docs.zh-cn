---
title: Always Encrypted 向导 | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a202d9dfb063979fbae76d6402909674bd163033
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39549693"
---
# <a name="always-encrypted-wizard"></a>始终加密向导
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

使用 **始终加密向导** 帮助保护存储在 SQL Server 数据库中的敏感数据。 始终加密允许客户端对客户端应用程序内的敏感数据进行加密，并且永远不向 SQL Server 显示加密密钥。 因此，始终加密分隔了拥有数据（且可以查看它）的人员与管理数据（但没有访问权限）的人员。  有关此功能的完整说明，请参阅 [Always Encrypted（数据库引擎）](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)。  
 
 - 有关显示如何使用向导配置始终加密并在客户端应用程序中使用它的端对端演练，请参阅 [SQL 数据库教程：使用始终加密保护敏感数据](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)。  
 
 - 有关包括使用该向导的视频，请参阅 [使用始终加密保持敏感数据的安全](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)。 此外，还可参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全团队博客 [SSMS Encryption Wizard - Enabling Always Encrypted in a Few Easy Steps](http://blogs.msdn.com/b/sqlsecurity/archive/2015/11/01/ssms-encryption-wizard-enabling-always-encrypted-made-easy.aspx)（SSMS 加密向导 - 用几个简单的步骤启用 Always Encrypted）。  
 
 - **权限：** 若要查询加密列并使用此向导选择密钥，则必须具有 `VIEW ANY COLUMN MASTER KEY DEFINITION` 和 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 权限。 若要创建新密钥，还必须具有 `ALTER ANY COLUMN MASTER KEY` 和 `ALTER ANY COLUMN ENCRYPTION KEY` 权限。  
 
 #### <a name="to-open-the-always-encrypted-wizard"></a>打开始终加密向导  
 
 1.  使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的对象资源管理器组件连接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
   
 2.  右键单击数据库，指向“任务”，然后单击“加密列”。  
   
 ## <a name="column-selection-page"></a>列选择页  
 - 找到表和列，然后选择加密类型（确定性的或随机的）和已选择列的加密密匙。 若要解密当前已加密的列，选择“纯文本” 。 若要旋转列加密密匙，请选择不同的加密密匙，向导将解密列并使用新密钥重新加密列。 （ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持加密临时表和内存中表，但不能通过此向导进行配置。）  
 
## <a name="master-key-configuration-page"></a>主密匙配置页  
 - 在 Windows 证书商店或 Azure 密匙保管库中创建新的列主密匙。 有关详细信息，请参阅下面位于密匙存储下的链接。  
 
 - 如果在“列选择”页中选择了自动生成的列加密密匙，则必须配置加密生成的列加密密匙所用的列主密匙。 如果你有已经在数据库中定义了的列主密匙，则可以选择它。 （若要使用现有的列主密匙，用户必须具有访问密匙的权限。）或者，可以在已选择的密匙存储（Windows 证书商店或 Azure 密匙保管库）中生成列主密匙，然后在数据库中定义该密匙。  
 
 ### <a name="key-storage"></a>**密匙存储**  
 
 - 选择将存储列主密匙的位置。  
 
   - **将主密匙存储在 Windows 证书中** 有关详细信息，请参阅 [使用证书商店](https://msdn.microsoft.com/library/windows/desktop/aa388160.aspx)  
 
   - **将主密钥存储在 AKV 中** 有关详细信息，请参阅 [Azure 密钥保管库入门](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)。  
 
 - 若要在 Azure 密匙保管库中生成列主密匙，用户必须具有密匙保管库的 **WrapKey**、 **UnwrapKey**、 **Verify**和 **Sign** 权限。 用户可能还需要 **Get**、 **List**、 **Create**、 **Delete**、 **Update**、 **Import**、 **Backup**和 **Restore** 权限。 有关详细信息，请参阅 [什么是 Azure 密匙保管库？](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) 和   [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx)。  
 
 - 该向导仅支持两个选项。 必须使用 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 配置硬件安全模块和客户商店。  
 
 ## <a name="always-encrypted-terms"></a>始终加密术语  
 
 - **确定性加密** 使用一种对任何给定的纯文本值始终生成相同的加密值的方法。 使用确定性加密不仅允许分组、按等式筛选和根据加密值加入表，还允许未经授权的用户通过检查加密列中的模式来猜测加密值的相关信息。 当存在小部分可能的加密值时（如 True/False 或北部/南部/东部/西部地区），此漏洞会增大。 确定性加密必须使用具有字符列的 binary2 排序顺序的列排序规则。  
 
 - **随机加密** 使用一种以更不可预测地方式加密数据的方法。 随机加密更加安全，但不支持对加密列进行等式搜索、分组、索引和链接。  

 - **列主密匙** 保护用于加密列加密密匙的密匙。 列主密匙必须存储在受信任的密匙存储中。 有关列主密匙（包括它们的位置）的信息存储在系统目录视图中的数据库中。  

 - **列加密密钥** 用于加密存储在数据库列中的敏感数据。 可以使用单个列加密密匙加密列中的所有值。 列加密密钥的加密值存储在系统目录视图中的数据库中。 应在一个安全的/受信任的位置存储列加密密钥以用于备份。  

 ## <a name="see-also"></a>另请参阅  
 - [Always Encrypted（数据库引擎）](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [使用 Azure 密钥保管库的可扩展密钥管理 (SQL Server)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
