---
title: 如何从 SQL-SQL Server 机器学习服务调用 Java
description: 了解如何使用 Java 编程语言扩展。 在 SQL Server 2019 中的 SQL Server 存储过程从调用的 Java 类。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 438c1096a933932e08c5cbf21722ba75874bb1dc
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644756"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>如何从 SQL Server 2019 预览调用 Java

使用时[Java 语言扩展](extension-java.md)，则[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系统存储的过程是用来调用 Java 运行时的接口。 针对数据库的权限适用于 Java 的代码执行。

本文介绍了 Java 类和 SQL 服务器执行的方法的实现详细信息。 一旦您熟悉这些详细信息，请查看[Java 示例](java-first-sample.md)作为下一步。

## <a name="basic-principles"></a>基本原则

* 已编译的自定义 Java 类必须存在于.class 文件或 Java 类路径中的.jar 文件。 [CLASSPATH 参数](#set-classpath)提供了已编译的 Java 文件的路径。 

* 正在调用的 Java 方法必须提供对存储过程在"脚本"参数中。

* 如果此类属于的包，"包名称"，需要提供。

* "params"用于将参数传递给一个 Java 类。 需要参数的方法不是支持调用，这使得将参数值传递给您的方法的唯一方法的参数。 

> [!Note]
> 本说明重述特定于 CTP 中的 Java 支持和不支持操作 2.x。
> * 针对存储过程支持的输入的参数。 不是输出参数。
> * 使用 sp_execute_external_script 参数传送视频流**@r_rowsPerRead**不受支持。
> * 使用分区**@input_data_1_partition_by_columns**不受支持。
> * 并行处理使用 **@parallel= 1**支持。

## <a name="call-spexecuteexternalscript"></a>调用 sp_execute_external_script

适用于 Windows 和 Linux [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系统存储的过程是用来调用 Java 运行时的接口。 下面的示例演示使用 Java 扩展和参数用于指定路径、 脚本和自定义代码 sp_execute_external_script。

```sql
DECLARE @myClassPath nvarchar(30)
DECLARE @param1 int

SET @myClassPath = N'/<my path>/program.jar'
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>.<methodName>'
, @input_data_1 = N'<Input Query>
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @param1
```

<a name="set-classpath"></a>

## <a name="set-classpath"></a>设置 CLASSPATH

编译你的 Java 类并在 Java classpath 中放置.class 文件或.jar 文件后，必须提供 SQL Server Java 扩展到类路径中的两个选项：

**选项 1:作为参数传递**

指定已编译的代码的路径所需的一种方法是通过将 CLASSPATH 设置为 sp_execute_external_script 过程的输入参数。 [Java 示例](java-first-sample.md#call-method)演示此技术。 如果您选择这种方法，并且有多个路径，请确保使用有效的基础操作系统的路径分隔符：

* 在 Linux 上，用冒号分隔类路径中的路径":"。
* Windows，在单独的类路径中的路径用分号";"

**选项 2:注册系统变量**

就像创建 JDK 可执行文件的系统变量，可以创建系统变量的代码路径。 若要此操作，创建名为"CLASSPATH"的系统环境变量

## <a name="class-requirements"></a>类要求

为了使 SQL Server 与 Java 运行时进行通信，需要在类中实现特定的静态变量。 SQL Server 然后可以执行中使用的 Java 语言扩展的 Java 类和 exchange 数据的方法。

> [!Note]
> 预期的实现详细信息，若要更改在即将推出的 Ctp，因为我们致力于改进开发人员的体验。

## <a name="method-requirements"></a>方法要求
若要将自变量传递，请使用**@param**在 sp_execute_external_script 的参数。 该方法本身不能具有任何参数。 返回类型必须为 void。  

```java
public static void test()  {}
```

## <a name="data-inputs"></a>数据输入 

本部分介绍如何将数据从 SQL Server 查询使用推送到 Java **InputDataSet** sp_execute_external_script 中。

对于每个输入列，您的 SQL 查询将推送到 Java，需要声明数组。

### <a name="inputdatacol"></a>inputDataCol

在当前版本的 Java 扩展插件**inputDataColN**变量是必需的其中*N*是列数。 

```java
public static <type>[] inputDataColN = new <type>[1]
```

必须初始化这些数组 （数组的大小必须是大于 0，并且没有以反映实际的列的长度）。

例如：`public static int[] inputDataCol1 = new int[1];`

将使用从 SQL server 查询的 Java 程序执行前正在调用的输入数据填充这些数组变量。

### <a name="inputnullmap"></a>inputNullMap

该扩展使用 null 映射了解哪些值均为 null。 此变量将包含 null 值有关的信息由 SQL Server 之前用户函数的执行。

用户仅需要初始化此变量 （和数组的大小必须是大于 0）。

```java
public static boolean[][] inputNullMap = new boolean[1][1];
```

## <a name="data-outputs"></a>数据输出 

本部分介绍**OutputDataSet**，从 Java 中，你可以将发送到和保留在 SQL Server 中返回的输出数据集。

> [!Note]
> 输出中的参数[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)不支持在此版本中。

### <a name="outputdatacoln"></a>outputDataColN

类似于**inputDataSet**，为 Java 程序将发送回 SQL Server 每个输出列，必须声明一个数组变量。 所有**outputDataCol**数组应具有相同的长度。 您需要确保这类执行完成时进行初始化。

```java
public static <type>[] outputDataColN = new <type>[]
```

### <a name="numberofoutputcols"></a>numberofOutputCols

将此变量设置为预期会有将用户的函数完成执行时的输出数据列的数量。

```java
public static short numberofOutputCols = <expected number of output columns>;
```

### <a name="outputnullmap"></a>outputNullMap

该扩展使用 null 映射以指示哪些值均为 null。 我们需要此因为基元类型不支持 null。 目前，我们也需要空映射为字符串类型，即使字符串可以为 null。 "True"来表示 null 值。

预期的列和要返回到 SQL Server 的行数，必须填充此 NullMap。

```java
public static boolean[][] outputNullMap
```
<a name="create-external-library"></a>


## <a name="next-steps"></a>后续步骤

+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)
+ [SQL Server 中的 Java 语言扩展](extension-java.md)
