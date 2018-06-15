---
title: 数据源向导屏幕 3 (ODBC Driver for SQL Server) |Microsoft 文档
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbbedb76089ffb508f6ce521bd831b213ba90fc5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851972"
---
# <a name="data-source-wizard-screen-3"></a>数据源向导屏幕 3

指定默认数据库、将由驱动程序使用的各种 ANSI 选项和镜像服务器的名称。

## <a name="options"></a>选项

### <a name="change-the-default-database-to"></a>更改默认的数据库为

指定使用该数据源建立的任何连接的默认数据库的名称。 清除此框后，连接将使用在服务器上为登录 ID 定义的默认数据库。 选择此框后，在框中命名的数据库将覆盖为登录 ID 定义的默认数据库。 如果**附加数据库文件名**框中具有主文件的名称、 使用中指定的数据库名称的数据库作为附加的主文件所描述的数据库**将默认数据库更改为**框。

使用登录 ID 的默认数据库比在 ODBC 数据源中指定默认数据库更有效。

### <a name="mirror-server"></a>镜像服务器

指定要镜像的数据库的故障转移伙伴的名称。 如果数据库名称中不会显示**更改默认的数据库为**框中或显示的名称是默认数据库，**镜像服务器**灰显。

您还可以指定镜像服务器的服务器主体名称 (SPN)。 镜像服务器的 SPN 用于在客户端和服务器之间相互进行身份验证。

### <a name="attach-database-filename"></a>附加数据库文件名

指定可附加数据库的主文件的名称。 该数据库作为数据源的默认数据库附加和使用。 指定主文件的完整路径和文件名。 中指定的数据库名称**更改默认的数据库为**框使用作为附加的数据库的名称。

### <a name="use-ansi-quoted-identifiers"></a>使用带引号的标识符的 ANSI

指定 QUOTED_IDENTIFIERS 集上的 ODBC driver for SQL Server 连接时。 选中此复选框后，SQL Server 强制实施有关引号内的 ANSI 规则。 双引号只能用于标识符，如列和表名称。 字符串必须用单引号引起来：

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

清除此复选框后，使用引用标识符的应用程序（如 Microsoft Excel 附带的 Microsoft Query 实用工具）将在生成带有引用标识符的 SQL 语句时出错。

### <a name="use-ansi-nulls-paddings-and-warnings"></a>使用 ANSI nulls、 填充和警告

指定当 ODBC Driver for SQL Server 连接时，在设置 ANSI_NULLS 和 ANSI_WARNINGS，ANSI_PADDINGS 选项。

在 ANSI_NULLS 设置为开启时，服务器将执行与比较列是否为 NULL 有关的 ANSI 规则。 在所有 NULL 比较中，必须使用 ANSI 语法“IS NULL”或“IS NOT NULL”。 不支持 Transact-SQL 语法“= NULL”。

与 ANSI_WARNINGS 设置上，SQL Server 会发出警告消息的违反 ANSI 规则，但不是会违反 TRANSACT-SQL 的规则的条件。 此类错误的示例为执行 INSERT 或 UPDATE 语句时数据截断，或在执行聚合函数时遇到 Null 值。 

以 ansi_padding 为其设置、 尾随空格上**varchar**值和上尾随零**varbinary**值也不会自动剪裁。

### <a name="application-intent"></a>应用程序意向

连接到服务器时声明应用程序工作负荷类型。 可能的值为**ReadOnly**和**ReadWrite**。

### <a name="multi-subnet-failover"></a>多子网故障转移。

如果你的应用程序连接到高可用性、 灾难恢复 （AlwaysOn 可用性组） 可用性组 (AG) 在不同子网上，启用**多子网故障转移。** 配置 ODBC Driver for SQL Server，以便更快地检测和到 （当前） 活动服务器的连接。

### <a name="transparent-network-ip-resolution"></a>透明网络 IP 解析。

将的行为更改为**多子网故障转移**以便在故障转移期间更快地重新连接。 请参阅[使用透明网络 IP 解析](../../../connect/odbc/using-transparent-network-ip-resolution.md)有关详细信息。

### <a name="column-encryption"></a>列加密。

启用自动解密和加密的数据传输到和使用加密的列从[始终加密](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)位于 SQL Server 2016 及更高版本的功能。

### <a name="use-fmtonly-metadata-discovery"></a>使用 FMTONLY 元数据发现：

在连接到 SQL Server 2012 或更高版本时，请使用旧的 SET FMTONLY 元数据发现方法。 只有在使用不支持的查询时，才启用此[sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)，例如那些包含临时表。 

### <a name="next"></a>Next

转到向导的下一个屏幕。

### <a name="back"></a>返回

返回到向导的上一屏幕。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)

[数据源向导屏幕 4](../../../connect/odbc/windows/dsn-wizard-4.md)
