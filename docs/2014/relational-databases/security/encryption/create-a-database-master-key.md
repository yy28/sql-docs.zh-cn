---
title: 创建数据库主密钥 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.reviewer: carlrab
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 86f74710e99079d0acd28db09bcf1e4ba7c57865
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957241"
---
# <a name="create-a-database-master-key"></a>Create a Database Master Key

本主题说明如何使用`master` [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)]在中的数据库中创建数据库主密钥。

**本主题中的**

- **开始之前：**

  [安全](#Security)

- [使用 Transact-SQL 创建数据库主密钥](#TsqlProcedure)

## <a name="BeforeYouBegin"></a>开始之前

### <a name="Security"></a>安全

#### <a name="Permissions"></a>访问

要求对数据库具有 CONTROL 权限。

## <a name="TsqlProcedure"></a>使用 Transact-sql

### <a name="to-create-a-database-master-key"></a>创建数据库主密钥

1. 选择密码来对存储于该数据库中的主密钥副本进行加密。
2. 在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。
3. 展开“系统数据库”，右键单击 **，然后单击“新建查询”**`master`****。
4. 将以下示例复制并粘贴到查询窗口中，然后单击“执行” ****。

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

有关详细信息，请参阅 [CREATE MASTER KEY (Transact-SQL)](/sql/t-sql/statements/create-master-key-transact-sql)。
