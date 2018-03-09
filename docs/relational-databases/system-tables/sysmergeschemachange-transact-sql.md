---
title: "sysmergeschemachange (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f42fbeba8639216d5a95414430099fbd5bde0b07
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含有关快照代理生成的已发布项目的信息。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|发布 ID。|  
|**artid**|**uniqueidentifier**|文章的 ID。|  
|**schemaversion**|**int**|最后一个架构更改的编号。|  
|**schemaguid**|**uniqueidentifier**|最后一个架构的唯一 ID。|  
|**schematype**|**int**|架构更改的类型：<br /><br /> **为-1** = 不有效。<br /><br /> **1** = SQL 命令。<br /><br /> **2** = 架构脚本。<br /><br /> **3** = 本机大容量复制程序实用工具 (BCP)。<br /><br /> **4** = 字符 BCP。<br /><br /> **5** = 最后一次记录生成。<br /><br /> **6** = 最后一次发送的生成。<br /><br /> **7** = 目录。<br /><br /> **8** = 优先级。<br /><br /> **9** = 保持期。<br /><br /> **10** = 触发器脚本。<br /><br /> **11** = Alter table。<br /><br /> **12** = 重新初始化所有。<br /><br /> **13** = ALTER TABLE (非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。<br /><br /> **14**与上载 = 重新初始化。<br /><br /> **15** = 约束和索引的脚本。<br /><br /> **16** = 元数据清理。<br /><br /> **17** = 更新上次发送的生成。<br /><br /> **18** = 向后兼容性级别。<br /><br /> **19** = 验证订阅服务器信息。<br /><br /> **20** = 也已分区。<br /><br /> **21** = 自定义冲突解决程序。<br /><br /> **22** = 项目处理顺序。<br /><br /> **23** = 事务发布中的已发布。<br /><br /> **24** = Compensate 是否有错误。<br /><br /> **25** = 备用快照文件夹。<br /><br /> **26** = 仅限下载。<br /><br /> **27** = 删除跟踪。<br /><br /> **40** = 预创建快照脚本。<br /><br /> **45** = 后创建快照脚本。<br /><br /> **46** = 按需用户脚本。<br /><br /> **50** = 快照标头开始。<br /><br /> **51** = 快照标头结束。<br /><br /> **52** = 快照预告片。<br /><br /> **53** = 文件传输协议 (FTP) 地址。<br /><br /> **54** = FTP 端口。<br /><br /> **55** = FTP 子目录。<br /><br /> **56** = 压缩的快照。<br /><br /> **57** = FTP 登录名。<br /><br /> **58** = FTP 密码。<br /><br /> **60** = 系统预创建脚本。<br /><br /> **61** = 存储过程架构。<br /><br /> **62** = 视图架构。<br /><br /> **63** = 用户定义函数的架构。<br /><br /> **64** = 视图索引。<br /><br /> **65** = 扩展属性。<br /><br /> **66** = 验证。<br /><br /> **67** = 快照前 SQL 命令。<br /><br /> **71** = 动态快照验证。<br /><br /> **80** = 系统表本机 BCP 9.0。<br /><br /> **81** = 系统表字符 BCP 9.0。<br /><br /> **82** = 系统表本机 BCP 9.0 （全局仅）。<br /><br /> **83** = 系统表字符 BCP 9.0 （全局仅）。<br /><br /> **84** = 系统表本机 BCP 9.0 （轻型）。<br /><br /> **85** = 系统表字符 BCP 9.0 （轻型）。<br /><br /> **128** = 动态 BCP （位）。<br /><br /> **131** = 动态本机 BCP。<br /><br /> **132** = 动态字符 BCP。<br /><br /> **208** = 动态系统表本机 BCP 9.0。<br /><br /> **209** = 动态系统表字符 BCP 9.0。<br /><br /> **210** = 动态系统表本机 BCP 9.0 （全局仅）。<br /><br /> **211** = 动态系统表字符 BCP 9.0 （全局仅）。<br /><br /> **212** = 动态系统表本机 BCP 9.0 （轻型）。<br /><br /> **213** = 动态系统表字符 BCP 9.0 （轻型）。<br /><br /> **300** = 数据定义语言 (DDL) 操作。<br /><br /> **1024** = 增量快照控件。<br /><br /> **1049** = 增量快照文件夹。<br /><br /> **1074** = 增量快照开始标头。<br /><br /> **1075** = 增量快照结束标头。<br /><br /> **1076** = 增量快照预告片。<br /><br /> **1077** = 增量 FTP 地址。<br /><br /> **1078** = 增量 FTP 端口。<br /><br /> **1079** = 增量 FTP 子目录。<br /><br /> **1080** = 增量压缩的快照。<br /><br /> **1081** = 增量 FTP 登录名。<br /><br /> **1082** = 增量 FTP 密码。|  
|**schematext**|**nvarchar(2000)**|脚本文件名，或包含文件名的命令|  
|**schemastatus**|**tinyint**|表示是否为项目挂起架构更改，可以是下列值之一：<br /><br /> **0** = 处于非活动状态。<br /><br /> **1** = 活动。<br /><br /> 挂起架构更改时，此值设置为**1**。|  
|**schemasubtype**|**int**|架构更改的子类型：<br /><br /> **1** = ADDCOLUMN<br /><br /> **2** = DROPCOLUMN<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = ADDPRIMARYKEY<br /><br /> **5** = ADDUNIQUE<br /><br /> **6** = ADDREFERENCE<br /><br /> **7** = DROPCONSTRAINT<br /><br /> **8** = ADDDEFAULT<br /><br /> **9** = ADDCHECK<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
