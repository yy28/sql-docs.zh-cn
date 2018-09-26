---
title: Java 语言扩展。 在 SQL Server 2019 |Microsoft Docs
description: 使用 Java 语言扩展的 SQL Server 2019 上运行 Java 代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8acb0a72435306cdec8740ffb41ff499eea61fac
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714901"
---
# <a name="java-language-extension-in-sql-server-2019"></a>在 SQL Server 2019 Java 语言扩展 

从 SQL Server 2019 开始，你可以运行自定义 Java 代码[可扩展性框架](../concepts/extensibility-framework.md)作为数据库引擎实例的附加项。 

可扩展性框架是用于执行外部代码的体系结构： Java （从 SQL Server 2019）， [（从 SQL Server 2017） 的 Python](../concepts/extension-python.md)，并[R （从 SQL Server 2016 开始）](../concepts/extension-r.md)。 执行代码是独立于核心引擎进程，但与 SQL Server 的查询执行完全集成。 这意味着您可以将数据从任何 SQL Server 查询推送到外部运行时，并使用或持久保存回 SQL Server 中的结果。

使用任何编程语言扩展，如系统存储过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)是用于执行预编译的 Java 代码的接口。

## <a name="1---feature-installation"></a>1-功能安装

若要安装 Java 语言扩展的 Windows 或 Linux 上运行 SQL Server 2019 安装程序。 SQL Server 2019 数据库引擎实例是必需的。 不能将 Java 集成添加到早期版本。

在 Windows 中，开始[安装向导](../install/sql-machine-learning-services-windows-install.md)。 在功能选择中选择**机器学习服务 （数据库内）**。 虽然 Java 集成不附带机器学习库，这是提供可扩展性框架的安装程序中的选项。 如果您愿意，可以省略 R 和 Python。

在 Linux 上，安装[数据库引擎](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)，并将[扩展性包和 Java 扩展包](../../linux/sql-server-linux-setup-machine-learning.md)。

以下示例说明了每个 Linux 操作系统的语法。

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility
sudo zypper install mssql-server-extensibility-java
```

## <a name="2---configuration"></a>2-配置

使用 SQL Server Management Studio 或其他工具运行 TRANSACT-SQL 脚本，数据库引擎实例上配置外部脚本执行。

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="3---bring-your-own-java"></a>3-将您自己的 Java

从 R 和 Python 等的上一个语言集成的一个区别是，你可以控制与 SQL Server 一起使用 JVM。

| Java 版本 | 操作系统 |
|--------------|------------------|
| [Java 1.10](http://jdk.java.net/10/)   | Windows |
| Java 1.8   | Linux | 

给定的 Java 是向后兼容，早期版本可能有效，但表中列出了对于此早期 CTP 版本的支持和测试版本。

> [!Note]
>若要使用 SQL Server 中运行 Java，从技术上讲仅需要[Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html)安装 (JRE)。 JDK 是开发工具包包括 Java 编译器和其他开发相关的包。 如果你已有一个开发环境，并且只需要在服务器计算机上的 Java 运行时，可以忽略的 JDK 安装说明并仅安装 JRE。

## <a name="jdk-on-windows"></a>在 Windows 上的 JDK

下载 Windows 版本[Java SE 开发工具包 (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)。

安装的 JDK 下默认 /Program 文件 / 文件夹，如果你想要避免无需授予读取权限**所有应用程序包**并**SQLRUserGroup**上备用位置的安全组. 相同的指南适用于您的 Java classpath 文件夹，其中保留.class 或.jar 文件的访问权限。 

> [!Note]
> 在此版本中，扩展的授权和隔离模型已更改。 有关详细信息，请参阅[SQL Server 机器 2019年学习服务安装中的差异](../install/sql-machine-learning-services-ver15.md)。

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>授予对非默认 JDK 文件夹 (仅 Windows) 访问权限

如果在默认文件夹中安装 JDK/JRE，可以跳过此步骤。 对于非默认文件夹安装，运行以下 PowerShell 脚本，以授予访问权限**SQLRUsergroup**和 SQL Server 服务帐户 （在 ALL_APPLICATION_PACKAGES) 用于访问 JVM 和 Java classpath。

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup 的权限

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
$Acl.SetAccessRule($Ar)
Set-Acl ""<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

#### <a name="appcontainer-permissions"></a>AppContainer 权限

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
$Acl.SetAccessRule($Ar) 
Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

### <a name="add-the-jdk-path-to-javahome"></a>将 JDK 路径添加到 JAVA_HOME
此外需要将 JDK/JRE 安装路径 (例如，"C:\Program Files\Java\jdk-10.0.2") 添加到系统环境变量名称"JAVA_HOME"。 

若要创建系统变量，请使用控制面板 > 系统和安全 > 系统访问**高级系统属性**。 单击**环境变量**然后针对 JAVA_HOME 创建新的系统变量。

![Java 主页中的环境变量](../media/java/env-variable-java-home.png "设置适用于 Java")

## <a name="jdk-on-linux"></a>Linux 上的 JDK

在 Linux 上的 mssql server 扩展性 java 包会自动安装 JRE 1.8 如果尚未安装。 它还将添加到名为 JAVA_HOME 的环境变量的 JVM 路径。

## <a name="limitations-in-ctp-20"></a>CTP 2.0 中的限制

* 输入和输出缓冲区中值的数目不能超过`MAX_INT (2^31-1)`，因为它是可以在 Java 中的数组中分配的元素的最大数目。

* 在此版本中不支持在 sp_execute_external_script 中的输出参数。

* 在此版本中的输入和输出数据集没有 LOB 数据类型支持。 请参阅[Java 和 SQL Server 数据类型](java-sql-datatypes.md)有关哪些数据类型支持在此 CTP 中的详细信息。

* 使用 sp_execute_external_script 参数传送视频流@r_rowsPerRead此 CTP 中不受支持。

* 分区使用 sp_execute_external_script 参数@input_data_1_partition_by_columns此 CTP 中不受支持。

## <a name="next-steps"></a>后续步骤

+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)