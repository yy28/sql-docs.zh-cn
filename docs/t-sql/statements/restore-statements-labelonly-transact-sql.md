---
title: "RESTORE LABELONLY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LABELONLY
- RESTORE_LABELONLY_TSQL
- LABELONLY_TSQL
- RESTORE LABELONLY
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE LABELONLY statement
- backup media [SQL Server], content information
ms.assetid: 7cf0641e-0d55-4ffb-9500-ecd6ede85ae5
caps.latest.revision: 46
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f69efb096931108fdaea084b337fcb319f7cfb6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="restore-statements---labelonly-transact-sql"></a>还原语句的 LABELONLY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个结果集，它包含给定备份设备识别的备份介质的相关信息。  
  
> [!NOTE]  
>  自变量的说明，请参阅[RESTORE 参数 &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
RESTORE LABELONLY   
FROM <backup_device>   
[ WITH   
 {  
--Media Set Options  
   MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>参数  
 RESTORE LABELONLY 自变量的说明，请参阅[RESTORE 参数 &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>结果集  
 RESTORE LABELONLY 的结果集包含提供下列信息的一个行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**MediaName**|**nvarchar （128)**|介质的名称。|  
|**MediaSetId**|**uniqueidentifier**|介质集的唯一标识号。|  
|**FamilyCount**|**int**|在介质集中的介质簇数。|  
|**FamilySequenceNumber**|**int**|此介质簇的序号。|  
|**MediaFamilyId**|**uniqueidentifier**|介质簇的唯一标识号。|  
|**MediaSequenceNumber**|**int**|此介质在介质簇中的序号。|  
|**MediaLabelPresent**|**tinyint**|介质说明中是否包含：<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)]磁带格式介质标签<br /><br /> **0** = 介质说明|  
|**MediaDescription**|**nvarchar(255)**|介质说明（自由格式的文本）或磁带格式介质标签。|  
|**SoftwareName**|**nvarchar （128)**|写入标签的备份软件名称。|  
|**SoftwareVendorId**|**int**|写入备份的软件供应商的唯一供应商标识号。|  
|**MediaDate**|**datetime**|标签的写入日期和时间。|  
|**Mirror_Count**|**int**|介质集中的镜像服务器数 (1-4)。<br /><br /> 注意： 为一组中的不同镜像编写标签是相同的。|  
|**IsCompressed**|**bit**|备份是否已压缩：<br /><br /> 0 = 不压缩<br /><br /> 1 = 已压缩|  
  
> [!NOTE]  
>  如果为介质集定义了密码，则只有在命令的 MEDIAPASSWORD 选项中指定了正确的介质密码时，RESTORE LABELONLY 才会返回信息。  
  
## <a name="general-remarks"></a>一般备注  
 执行 RESTORE LABELONLY 是一种查找备份介质所含内容的快速方法。 由于 RESTORE LABELONLY 只读取介质标头，因此，即使使用高容量磁带设备，该语句的执行速度也会非常快。  
  
## <a name="security"></a>安全性  
 备份操作可以有选择地指定介质集的密码。 如果为介质集定义了密码，则必须在 RESTORE 语句中指定正确的密码。 密码防止未经授权的还原操作和未经授权的媒体使用的备份集追加[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]工具。 但是，密码不会阻止使用 BACKUP 语句的 FORMAT 选项覆盖介质。  
  
> [!IMPORTANT]  
>  此密码提供的安全性较低。 它旨在防止经过授权的用户或未经授权的用户使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具执行不正确的还原操作。 但是不能防止通过其他方式或通过替换密码来读取备份数据。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]保护备份的最佳做法是在一个安全位置或备份到磁盘保护的文件，由足够的访问控制列表 (Acl) 来存储备份的磁带。 ACL 应设置在创建备份的根目录下。  
  
### <a name="permissions"></a>Permissions  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，获取有关备份集或备份设备的信息要求具有 CREATE DATABASE 权限。 有关详细信息，请参阅 [GRANT 数据库权限 (Transact-SQL)](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [媒体集、媒体簇和备份集 (SQL Server)](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY (Transact-SQL)](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY (Transact-SQL)](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)   
 [备份历史记录和标头信息 (SQL Server)](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
