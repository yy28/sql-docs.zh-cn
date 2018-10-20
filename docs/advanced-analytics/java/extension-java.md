---
title: Java 语言扩展。 在 SQL Server 2019 |Microsoft Docs
description: 使用 Java 语言扩展的 SQL Server 2019 上运行 Java 代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/12/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2d69a255c56c3b15051a393b74eb1492a4f830f4
ms.sourcegitcommit: 93e3bb8941411b808e00daa31121367e96fdfda1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49359334"
---
# <a name="java-language-extension-in-sql-server-2019"></a>在 SQL Server 2019 Java 语言扩展 

从 SQL Server 2019 开始，你可以运行自定义 Java 代码[可扩展性框架](../concepts/extensibility-framework.md)作为数据库引擎实例的附加项。 

可扩展性框架是用于执行外部代码的体系结构： Java （从 SQL Server 2019）， [（从 SQL Server 2017） 的 Python](../concepts/extension-python.md)，并[R （从 SQL Server 2016 开始）](../concepts/extension-r.md)。 执行代码是独立于核心引擎进程，但与 SQL Server 的查询执行完全集成。 这意味着您可以将数据从任何 SQL Server 查询推送到外部运行时，并使用或持久保存回 SQL Server 中的结果。

使用任何编程语言扩展，如系统存储过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)是用于执行预编译的 Java 代码的接口。

## <a name="prerequisites"></a>必要條件

SQL Server 2019 是必需的。 早期版本不具有 Java 集成。 

Java 版本要求在 Windows 和 Linux 上可能有所不同。 Java Runtime Environment (JRE) 的最低要求，但 Jdk 非常有用，如果您需要 Java 编译器或开发包。 JDK 是全包含所有，如果安装了 JDK，因为不需要 JRE。

| 操作系统 | Java 版本 | JRE 下载 | JDK 下载 |
|------------------|--------------|--------------|--------------|
| Windows          | 1.10         | [JRE 10](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) | [JDK 10](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)  |
| Linux            | 1.8          |  [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) | [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  |  

在 Linux 上， **mssql server 扩展性 java**包会自动安装 JRE 1.8，如果尚未安装。 安装脚本还将 JVM 路径添加到名为 JAVA_HOME 的环境变量。

上 Windows，我们建议您安装的 JDK 下默认 /Program 文件 / 文件夹在可能的情况。 否则，需要额外配置，以授予对可执行文件的权限。 有关详细信息，请参阅[授予的权限 (Windows)](#perms-nonwindows)本文档中的部分。

> [!Note]
> 给定的 Java 是向后兼容，早期版本可能有效，但表中列出了对于此早期 CTP 版本的支持和测试版本。

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>在 Linux 上安装

你可以安装[数据库引擎和 Java 扩展一起](../../linux/sql-server-linux-setup-machine-learning.md#chained-installation)，或向现有实例中添加的 Java 支持。 下面的示例将 Java 扩展添加到现有安装。  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility-java
```

当你安装**mssql server 扩展性 java**，如果尚未安装包将自动安装 JRE 1.8。 它还将添加到名为 JAVA_HOME 的环境变量的 JVM 路径。

完成安装后下, 一步是[配置外部脚本执行](#configure-script-execution)。

> [!Note]
> 与 internet 连接的设备，在包的依赖项下载和安装作为主包安装的一部分。 有关详细信息，包括脱机安装程序，请参阅[安装在 Linux 上 SQL Server 机器学习](../../linux/sql-server-linux-setup-machine-learning.md)。

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>在 Windows 上安装

1. [运行安装程序](../install/sql-machine-learning-services-windows-install.md)安装 SQL Server 2019。

2. 转到功能选择后，选择**机器学习服务 （数据库内）**。 

   虽然 Java 集成不附带机器学习库，这是提供可扩展性框架的安装程序中的选项。 如果您愿意，可以省略 R 和 Python。

3. 完成安装向导，然后继续执行下面的两个任务。

### <a name="add-the-javahome-variable"></a>添加 JAVA_HOME 变量

JAVA_HOME 是一个环境变量，指定 Java 解释器的位置。 在此步骤中，系统环境变量为其创建在 Windows 上。

1. 找到并复制/JRE JDK 安装路径 (例如，C:\Program Files\Java\jdk-10.0.2)。

  在 CTP 2.0 中，将 JAVA_HOME 设置为基的 jdk 文件夹仅适用于 Java 1.10。 

  Java 1.8 中，将扩展路径才能到达 JDK (例如，"C:\Program Files\Java\jdk1.8.0_181\bin\server"在 Windows 上的 jvm.dll。 或者，你可以指向 JRE 基本文件夹:"C:\Program Files\Java\jre1.8.0_181"。

2. 在控制面板中，打开**系统和安全**，打开**系统**，然后单击**高级系统属性**。

3. 单击**环境变量**。

4. 为 JAVA_HOME 创建新的系统变量。

   ![Java 主页中的环境变量](../media/java/env-variable-java-home.png "设置适用于 Java")

<a name="perms-nonwindows"></a>

### <a name="grant-permissions-to-java-executables"></a>授予对 Java 可执行文件的权限

默认情况下，外部进程在其下运行的帐户没有访问到 JRE 或 JDK 文件。 在本部分中，运行以下 PowerShell 脚本授予权限以允许访问。

1. 找到并复制的 JDK 或 JRE 安装位置。 例如，它可能是 C:\Program Files\Java\jdk-10.0.2。

2. 使用管理员权限打开 PowerShell。 如果您不熟悉此任务，请参阅[这篇文章](https://www.top-password.com/blog/5-ways-to-run-powershell-as-administrator-in-windows-10/)提示和技巧。

3. 运行以下脚本，授予**SQLRUserGroup** Java 可执行文件的权限。 

  **SQLRUserGroup**指定的权限下运行的外部进程。 默认情况下，此组的成员有权 R 和 Python 程序安装的 SQL Server，但不是 Java 文件。 若要运行 Java 可执行文件，您必须授予**SQLRUserGroup**权限执行此操作。

   ```powershell
   $Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
   $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
   $Acl.SetAccessRule($Ar)
   Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
   ```
4. 运行以下脚本，授予**所有应用程序包**以及权限。 

  在 SQL Server 2019 容器辅助角色帐户作为隔离机制中，将替换为下快速启动板服务帐户，这是成员的标识的容器中运行的进程**SQLRUserGroup**。 有关详细信息，请参阅[安装 SQL Server 2019 之间的差异](../install/sql-machine-learning-services-ver15.md)。

   ```powershell
   $Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
   $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
   $Acl.SetAccessRule($Ar) 
   Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
   ```

5. 重复前面的两个步骤包含你想要在 SQL Server 上运行的.class 或.jar 文件的任何 Java 类路径文件夹上。 例如，如果您将保留路径，如 C:\JavaPrograms\my-app 编译的程序，请授予**SQLRUserGroup**并**ALL APPLICATION PACKAGES**文件夹的权限，以便可以加载程序。

  请务必授予权限的完整路径，在根文件夹开始。 只需包含文件夹的权限不会足以满足加载你的代码。

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>配置脚本执行

此时，已基本准备好在 Linux 或 Windows 上运行 Java 代码。 作为最后一个步骤中，切换到 SQL Server Management Studio 或运行 TRANSACT-SQL 脚本，以启用外部脚本执行的其他工具。

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>验证安装

若要确认安装是否正常工作，请创建并运行[示例应用程序](java-first-sample.md)使用您刚安装，将文件放在之前配置的类路径中的 JDK。

## <a name="differences-in-ctp-20"></a>CTP 2.0 中的差异

如果你已熟悉机器学习服务，扩展的授权和隔离模型已在此版本中更改。 有关详细信息，请参阅[SQL Server 机器 2019年学习服务安装中的差异](../install/sql-machine-learning-services-ver15.md)。

## <a name="limitations-in-ctp-20"></a>CTP 2.0 中的限制

* 输入和输出缓冲区中值的数目不能超过`MAX_INT (2^31-1)`，因为它是可以在 Java 中的数组中分配的元素的最大数目。

* 输出中的参数[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)不支持在此版本中。

* 在此版本中的输入和输出数据集没有 LOB 数据类型支持。 请参阅[Java 和 SQL Server 数据类型](java-sql-datatypes.md)有关哪些数据类型支持在此 CTP 中的详细信息。

* 使用 sp_execute_external_script 参数传送视频流@r_rowsPerRead此 CTP 中不受支持。

* 分区使用 sp_execute_external_script 参数@input_data_1_partition_by_columns此 CTP 中不受支持。

## <a name="next-steps"></a>后续步骤

+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)