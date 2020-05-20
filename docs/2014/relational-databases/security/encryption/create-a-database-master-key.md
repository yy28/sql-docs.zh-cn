---
title: 创建数据库主密钥 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.reviewer: carlrab
ms.openlocfilehash: cc0b3e0dccd1ecf674d583e4d1b7adc1a85341d2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758883"
---
# <a name="create-a-database-master-key"></a>创建数据库主密钥

本主题说明如何 `master` 使用在中的数据库中创建数据库主密钥 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] 。

**本主题内容**

- **开始之前：**

  [安全性](#Security)

- [使用 Transact-SQL 创建数据库主密钥](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前

### <a name="security"></a><a name="Security"></a> Security

#### <a name="permissions"></a><a name="Permissions"></a> 权限

要求对数据库具有 CONTROL 权限。

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL

### <a name="to-create-a-database-master-key"></a>创建数据库主密钥

1. 选择密码来对存储于该数据库中的主密钥副本进行加密。
2. 在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的实例。
3. 展开“系统数据库”，右键单击 `master`，然后单击“新建查询”********。
4. 将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

有关详细信息，请参阅 [CREATE MASTER KEY (Transact-SQL)](/sql/t-sql/statements/create-master-key-transact-sql)。
