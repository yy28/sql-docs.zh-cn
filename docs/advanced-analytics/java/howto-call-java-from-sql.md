---
title: 如何从 SQL-SQL Server 机器学习服务调用 Java
description: 了解如何使用 Java 编程语言扩展。 在 SQL Server 2019 中的 SQL Server 存储过程从调用的 Java 类。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a75878ccc4f14d03f84102dd48bfd43a6e04daea
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473555"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>如何从 SQL Server 2019 预览调用 Java

使用时[Java 语言扩展](extension-java.md)，则[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系统存储的过程是用来调用 Java 运行时的接口。 针对数据库的权限适用于 Java 的代码执行。

本文介绍了 Java 类和 SQL 服务器执行的方法的实现详细信息。 一旦您熟悉这些详细信息，请查看[Java 示例](java-first-sample.md)作为下一步。

有两种方法来调用 SQL Server 中的 Java 类：

1. 请将.class 或.jar 文件放在[Java classpath](#classpath)。 这是适用于 Windows 和 Linux。

2. 上传的.jar 文件和为数据库，并使用其他依赖项中的已编译的类[外部库](#external-library)DDL。 此选项是适用于 Windows 和 Linux 从 CTP 2.4。

> [!NOTE]
> 作为一般建议，使用.jar 文件和不是单个.class 文件。 这是在 Java 中常见的做法，轻松地整体体验。 请参阅：[如何从类文件中创建的 jar 文件](extension-java.md#create-jar)。

<a name="classpath"></a>

## <a name="classpath"></a>Classpath

### <a name="basic-principles"></a>基本原则

* 已编译的自定义 Java 类必须存在于.class 文件或 Java 类路径中的.jar 文件。 [CLASSPATH 参数](#set-classpath)提供了已编译的 Java 文件的路径。 

* 正在调用的 Java 方法必须提供对存储过程在"脚本"参数中。

* 如果此类属于的包，"包名称"，需要提供。

* "params"用于将参数传递给一个 Java 类。 需要参数的方法不是支持调用，这使得将参数值传递给您的方法的唯一方法的参数。 

> [!Note]
> 本说明重述特定于 CTP 中的 Java 支持和不支持操作 2.x。
> * 针对存储过程支持的输入的参数。 不是输出参数。
> * 使用 sp_execute_external_script 参数传送视频流@r_rowsPerRead不受支持。
> * 分区使用@input_data_1_partition_by_columns不受支持。
> * 并行处理使用@parallel= 1 受支持。

### <a name="call-java-class"></a>调用 Java 类

适用于 Windows 和 Linux [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系统存储的过程是用来调用 Java 运行时的接口。 下面的示例演示使用 Java 扩展和参数用于指定路径、 脚本和自定义代码 sp_execute_external_script。

> [!NOTE]
> 请注意，无需定义要调用的方法。 默认情况下调用的方法**执行**调用。 这意味着您需要按照 SDK，并在 Java 类中实现一个 execute 方法。

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>设置 CLASSPATH

一次已编译你的 Java 类，并在 Java classpath 中创建的 jar 文件，必须提供 SQL Server Java 扩展到类路径中的两个选项：

**选项 1:使用外部库**最简单的选项是使 SQL Server 自动通过创建外部库，并指向 jar 库中查找您的类。 [使用用于 Java 的外部库](howto-call-java-from-sql.md#external-library)

**选项 2:注册系统环境变量**

就像你创建的 Java 运行时的系统环境变量，可以创建系统环境变量，并提供到包含的类将 jar 文件的路径。 若要执行此操作，需要创建名为"CLASSPATH"的系统环境变量。

<a name="external-library"></a>

## <a name="external-library"></a>外部库

在 SQL Server 2019 CTP 2.4，可以在 Windows 和 Linux 上的 Java 语言使用外部库。 可以将您的类编译到一个.jar 文件并上传的.jar 文件和为数据库，并使用其他依赖项[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL。

如何上传具有外部库的.jar 文件的示例：

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

通过创建外部库，SQL Server 将自动有权访问的 Java 类并不需要设置为类路径中的任何特殊权限。

作为外部库上载的包从类中调用方法的示例：

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

有关详细信息，请参阅[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="next-steps"></a>后续步骤

+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)
+ [SQL Server 中的 Java 语言扩展](extension-java.md)
