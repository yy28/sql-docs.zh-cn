---
title: 模拟 Oracle 包变量
description: 介绍 Oracle SQL Server 迁移助手（SSMA）如何在 SQL Server 中模拟 Oracle 包变量。
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 9a8ca5c7dfdda98e1c005c3851d061957cf67449
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "76762821"
---
# <a name="emulating-oracle-package-variables"></a>模拟 Oracle 包变量

Oracle 支持将变量、类型、存储过程和函数封装到包中。 转换 Oracle 包时，需要转换：

* 过程和函数-公共和私有
* 变量
* 游标
* 初始化例程

本文介绍了 Oracle SQL Server 迁移助手（SSMA）如何将包变量转换为 SQL Server。

## <a name="conversion-basics"></a>转换基础知识

若要存储包变量，Oracle 的 SSMA 将使用驻留在特殊`ssma_oracle`架构中的存储过程`ssma_oracle.db_storage`和表。 该表按`SPID` （会话标识符）和登录时间筛选。 此筛选使你可以区分不同会话的变量。

每个已转换的包过程开始时，SSMA 会调用`ssma_oracle.db_check_init_package`特殊过程，该过程将检查是否初始化了包，并在需要时对其进行初始化。 每个初始化过程将清理存储表，并为每个包变量设置默认值。

## <a name="example"></a>示例

请考虑以下用于转换多个包变量的示例：

```sql
CREATE OR REPLACE PACKAGE MY_PACKAGE
IS
    space varchar(1) := ' ';
    unitname varchar(128) := 'My Simple Package';
    ts date := sysdate;
END;
```

SSMA 将其转换为以下 Transact-sql 代码：

```sql
CREATE PROCEDURE dbo.MY_PACKAGE$SSMA_Initialize_Package
AS
BEGIN
    EXECUTE ssma_oracle.db_clean_storage

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'SPACE',
        ' '

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'UNITNAME',
        'My Simple Package'

    DECLARE
        @temp datetime2

    SET @temp = sysdatetime()

    EXECUTE sysdb.ssma_oracle.set_pv_datetime2
      DB_NAME(),
      'DBO',
      'MY_PACKAGE',
      'TS',
      @temp
END
```

## <a name="emulating-get-and-set-methods-for-package-variables"></a>为包变量模拟 Get 和 Set 方法

Oracle 对`Get`包`Set`变量使用和方法，以避免让其他 subprograms 直接读取和写入它们。 如果需要在同一会话中保留 subprogram 调用之间可用的某些变量，则这些变量将被视为全局变量。

为克服此范围规则，SSMA for Oracle 使用的存储过程`ssma_oracle.set_pv_varchar`与每个变量的类型相同。 为了访问这些变量，SSMA 使用一组独立于`get_*`事务的和`set_*`过程和函数。

| Oracle 中的数据类型 | SSMA `Set`过程           |
| ------------------- | ------------------------------ |
| VARCHAR             | `ssma_oracle.set_pv_varchar`   |
| DATE                | `ssma_oracle.set_pv_datetime2` |
| CHAR                | `ssma_oracle.set_pv_varchar`   |
| INT                 | `ssma_oracle.set_pv_float`     |
| FLOAT               | `ssma_oracle.set_pv_float`     |

为了区分不同会话中的变量，SSMA 会将变量连同其`SPID` （会话标识符）和会话的登录时间一起存储。 因此`get_*` ，和`set_*`过程会使变量独立于运行它们的会话。
