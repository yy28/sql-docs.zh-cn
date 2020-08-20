---
description: 设置或更改服务器排序规则
title: 设置或更改服务器排序规则 | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
ms.reviewer: carlrab
ms.openlocfilehash: fbcfa1ad33ef986bcd8e6cfc621758f632118ba0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465556"
---
# <a name="set-or-change-the-server-collation"></a>设置或更改服务器排序规则

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  服务器排序规则用作与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例一起安装的所有系统数据库以及任何新创建的用户数据库的默认排序规则。 应仔细选择服务器级排序规则，因为它会影响：
 - `=`、`JOIN`、`ORDER BY` 和其他比较文本数据的运算符的排序和比较规则。
 - 系统视图、系统函数和 TempDB 中的对象（例如临时表）中 `CHAR`、`VARCHAR`、`NCHAR` 和 `NVARCHAR` 列的排序规则。
 - 变量、游标和 `GOTO` 标签的名称。 如果服务器级排序规则区分大小写，则变量 @pi 和 @PI 被视为不同变量，如果服务器级排序规则不区分大小写，则将这两个变量视为相同变量。
  
## <a name="setting-the-server-collation-in-sql-server"></a>设置 SQL Server 中的服务器排序规则

  服务器排序规则是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装期间指定的。 默认服务器级排序规则基于操作系统的区域设置。 例如，使用美国英语 (en-US) 的系统的默认排序规则是 SQL_Latin1_General_CP1_CI_AS。 无法将仅限 Unicode 的排序规则指定为服务器级排序规则。 有关详细信息（包括 OS 区域设置到默认排序规则映射的列表），请参阅[排序规则和 Unicode 支持](collation-and-unicode-support.md#Server-level-collations)的“服务器级排序规则”部分。

> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express LocalDB 的服务器级排序规则为 SQL_Latin1_General_CP1_CI_AS，并且不能在安装期间或之后更改。  

## <a name="changing-the-server-collation-in-sql-server"></a>更改 SQL Server 中的服务器排序规则

 更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的默认排序规则的操作可能会比较复杂，包括以下步骤：  
  
- 确保具有重新创建用户数据库及这些数据库中的所有对象所需的全部信息或脚本。  
  
- 使用工具（例如 [bcp Utility](../../tools/bcp-utility.md)）导出所有数据。 有关详细信息，请参阅[批量导入和导出数据 (SQL Server)](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
- 删除所有用户数据库。  
  
- 重新生成在 **setup** 命令的 SQLCOLLATION 属性中指定新的排序规则的 master 数据库。 例如：  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]
    /SQLCOLLATION=CollationName  
    ```  
  
     有关详细信息，请参阅 [重新生成系统数据库](../../relational-databases/databases/rebuild-system-databases.md)。  
  
- 创建所有数据库及这些数据库中的所有对象。  
  
- 导入所有数据。  
  
> [!NOTE]  
> 可以通过 `CREATE DATABASE` 和 `ALTER DATABASE` 语句的 `COLLATE` 子句，为创建的每个新数据库指定默认排序规则，而不更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的默认排序规则。 有关详细信息，请参阅 [Set or Change the Database Collation](set-or-change-the-database-collation.md)。  
  
## <a name="setting-the-server-collation-in-managed-instance"></a>设置托管实例中的服务器排序规则
可以在创建实例时指定 Azure SQL 托管实例中的服务器级别排序规则，以后不能更改。 创建实例时，可通过 [Azure 门户](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started#create-a-managed-instance)或 [PowerShell 和资源管理器模板](https://docs.microsoft.com/azure/sql-database/scripts/sql-managed-instance-create-powershell-azure-resource-manager-template)设置服务器级别排序规则。 默认服务器级排序规则为 SQL_Latin1_General_CP1_CI_AS。 无法将仅限 Unicode 的排序规则和新的 UTF-8 排序规则指定为服务器级排序规则。
如果要将数据库从 SQL Server 迁移到托管实例，请使用 `SERVERPROPERTY(N'Collation')` 函数检查源 SQL Server 中的服务器排序规则，并创建与 SQL Server 排序规则匹配的托管实例。 使用不匹配的服务器级排序规则将数据库从 SQL Server 迁移到托管实例可能会导致查询中出现多个意外错误。 不能更改现有托管实例的服务器级排序规则。

## <a name="see-also"></a>另请参阅

 [排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)   
 [设置或更改数据库排序规则](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [设置或更改列排序规则](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [重新生成系统数据库](../../relational-databases/databases/rebuild-system-databases.md)  
 
