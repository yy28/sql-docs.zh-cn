---
title: Resource 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- system objects [SQL Server]
- read-only databases
- mssqlsystemresource.mdf file
- Resource database [SQL Server]
ms.assetid: d592b2b4-bc36-4eb9-9385-8fe4dff0dced
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5f6b63e0ff79f44b2900fb0f727436ed36401ee2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127461"
---
# <a name="resource-database"></a>Resource 数据库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Resource 数据库为只读数据库，它包含了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的所有系统对象。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统对象（如 sys.objects）在物理上保留在 Resource 数据库中，但在逻辑上却显示在每个数据库的 sys 架构中。 Resource 数据库不包含用户数据或用户元数据。  
  
 Resource 数据库可比较轻松快捷地升级到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，进行升级需要删除和创建系统对象。 由于 Resource 数据库文件包含所有系统对象，因此，现在仅通过将单个 Resource 数据库文件复制到本地服务器便可完成升级。  
  
## <a name="physical-properties-of-resource"></a>Resource 的物理属性  
 Resource 数据库的物理文件名为 mssqlsystemresource.mdf 和 mssqlsystemresource.ldf。 这些文件位于 \<*drive*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\，不应移动。 每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例都具有一个（也是唯一的一个）关联的 mssqlsystemresource.mdf 文件，并且实例间不共享此文件。  
  
> [!WARNING]  
>  有时，升级和服务包会提供安装到 BINN 文件夹的新资源数据库。 不支持或建议更改资源数据库的位置。  
  
## <a name="backing-up-and-restoring-the-resource-database"></a>备份和还原 Resource 数据库  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能备份 Resource 数据库。 通过将 mssqlsystemresource.mdf 文件作为二进制 (.EXE) 文件而不是作为数据库文件，可以执行您自己的基于文件的备份或基于磁盘的备份，但是不能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还原所做的备份。 只能手动还原 mssqlsystemresource.mdf 的备份副本，并且必须谨慎，不要使用过时版本或可能不安全的版本覆盖当前的 Resource 数据库。  
  
> [!IMPORTANT]  
>  还原 mssqlsystemresource.mdf 的备份之后，必须重新应用所有后续更新。  
  
## <a name="accessing-the-resource-database"></a>访问 Resource 数据库  
 Resource 数据库仅应由 Microsoft 客户支持服务部门 (CSS) 的专家修改或在其指导下进行修改。 Resource 数据库的 ID 始终为 32767。 与 Resource 数据库相关联的其他重要值是版本号和数据库的上次更新时间。  
  
 **若要确定** Resource **数据库的版本号，请使用**：  
  
```  
SELECT SERVERPROPERTY('ResourceVersion');  
GO  
```  
  
 **若要确定** Resource **数据库的上次升级时间，请使用**：  
  
```  
SELECT SERVERPROPERTY('ResourceLastUpdateDateTime');  
GO  
```  
  
 **若要访问系统对象的 SQL 定义，请使用 OBJECT_DEFINITION 函数：**  
  
```  
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.objects'));  
GO  
```  
  
## <a name="related-content"></a>相关内容  
 [系统数据库](../../relational-databases/databases/system-databases.md)  
  
 [用于数据库管理员的诊断连接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
 [OBJECT_DEFINITION (Transact-SQL)](../../t-sql/functions/object-definition-transact-sql.md)  
  
 [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)  
  
 [在单用户模式下启动 SQL Server](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
