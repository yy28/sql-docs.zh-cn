---
title: 在 SQL Server 2019-SQL Server 机器学习服务的 Java 语言扩展
description: 安装、 配置和验证 Linux 和 Windows 系统上 SQL Server 2019 的 Java 语言扩展。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a258573ff7506f2533c2f91edb5751cfd1121dc8
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431710"
---
# <a name="java-language-extension-in-sql-server-2019"></a>在 SQL Server 2019 Java 语言扩展 

从 Windows 和 Linux 上的 SQL Server 2019 预览版中开始，你可以运行自定义 Java 代码[可扩展性框架](../concepts/extensibility-framework.md)作为数据库引擎实例的附加项。 

可扩展性框架是用于执行外部代码的体系结构：（从 SQL Server 2019），Java [（从 SQL Server 2017） 的 Python](../concepts/extension-python.md)，并[R （从 SQL Server 2016 开始）](../concepts/extension-r.md)。 执行代码是独立于核心引擎进程，但与 SQL Server 的查询执行完全集成。 这意味着您可以将数据从任何 SQL Server 查询推送到外部运行时，并使用或持久保存回 SQL Server 中的结果。

使用任何编程语言扩展，如系统存储过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)是用于执行预编译的 Java 代码的接口。

## <a name="prerequisites"></a>先决条件

SQL Server 2019 预览实例是必需的。 早期版本不具有 Java 集成。 

Java 版本要求在 Windows 和 Linux 上可能有所不同。 Java Runtime Environment (JRE) 的最低要求，但 Jdk 非常有用，如果您需要 Java 编译器或开发包。 JDK 是全包含所有，如果安装了 JDK，因为不需要 JRE。

| 操作系统 | Java 版本 | JRE 下载 | JDK 下载 |
|------------------|--------------|--------------|--------------|
| Windows          | 1.10         | [JRE 10](https://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) | [JDK 10](https://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)  |
| Linux            | 1.8          |  [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) | [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  |  

在 Linux 上， **mssql server 扩展性 java**包会自动安装 JRE 1.8，如果尚未安装。 安装脚本还将 JVM 路径添加到名为 JAVA_HOME 的环境变量。

上 Windows，我们建议您安装的 JDK 下默认 /Program 文件 / 文件夹在可能的情况。 否则，需要额外配置，以授予对可执行文件的权限。 有关详细信息，请参阅[授予的权限 (Windows)](#perms-nonwindows)本文档中的部分。

> [!Note]
> 给定的 Java 是向后兼容，早期版本可能有效，但表中列出了对于此早期 CTP 版本的支持和测试版本。

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>在 Linux 上安装

你可以安装[数据库引擎和 Java 扩展一起](../../linux/sql-server-linux-setup-machine-learning.md#install-all)，或向现有实例中添加的 Java 支持。 下面的示例将 Java 扩展添加到现有安装。  

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

### <a name="grant-permissions-on-linux"></a>Linux 上的授予权限

若要向 SQL Server 提供有权执行的 Java 类，需要设置权限。

若要授予读取和执行 jar 文件或类文件的访问权限，请运行以下**chmod**命令上每个类或 jar 文件。 我们建议将类文件放在一个 jar，当您使用 SQL Server 时。 创建一个 jar 的帮助，请参阅[如何创建一个 jar 文件](#create-jar)。

```cmd
chmod ug+rx <MyJarFile.jar>
```
您还需要为 mssql_satellite 权限授予读取/执行的目录或 jar 文件。

* 如果你正在从 SQL Server 调用的类文件，mssql_satellite 将需要读取/执行权限*每个*在文件夹层次结构中，从根下的直接父目录。

* 如果你正在从 SQL Server 调用 jar 文件，它就足以 jar 文件本身上运行命令。

```cmd
chown mssql_satellite:mssql_satellite <directory>
```

```cmd
chown mssql_satellite:mssql_satellite <MyJarFile.jar>
```

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

  Java 1.8 中，将扩展路径才能到达 JDK (例如，"C:\Program Files\Java\jdk1.8.0_181\bin\server"在 Windows 上的 jvm.dll。 或者，你可以指向 JRE 基本文件夹："C:\Program Files\Java\jre1.8.0_181"。

2. 在控制面板中，打开**系统和安全**，打开**系统**，然后单击**高级系统属性**。

3. 单击**环境变量**。

4. 为 JAVA_HOME 创建新的系统变量。

   ![Java 主页中的环境变量](../media/java/env-variable-java-home.png "设置适用于 Java")

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>授予对非默认 JDK 文件夹 (仅 Windows) 访问权限

如果在默认文件夹中安装 JDK/JRE，可以跳过此步骤。 

对于非默认文件夹安装，运行**icacls**命令从*提升*行，以授予访问权限**SQLRUsergroup**和 SQL Server 服务帐户 （在**ALL_APPLICATION_PACKAGES**) 用于访问 JVM 和 Java classpath。 命令将以递归方式授予对所有文件和给定的目录路径下的文件夹的访问权限。

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup 的权限

对于命名实例，将实例名追加到 SQLRUsergroup (例如， `SQLRUsergroupINSTANCENAME`)。

```cmd
icacls "<PATH TO CLASS or JAR FILES>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

#### <a name="appcontainer-permissions"></a>AppContainer 权限

```cmd
icacls "PATH to JDK/JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

### <a name="add-the-jre-path-to-javahome"></a>将 JRE 路径添加到 JAVA_HOME
此外需要将该路径添加到 JRE JAVA_HOME 系统环境变量中。 如果您只需安装的 JRE，可以提供 JRE 文件夹路径。 但是，如果已安装 JDK，您需要 jvm，此类下 JDK、 JRE 文件夹中提供的完整路径："C:\Program Files\Java\jdk1.8.0_191\jre\bin\server"。

若要创建系统变量，请使用控制面板 > 系统和安全 > 系统访问**高级系统属性**。 单击**环境变量**然后针对 JAVA_HOME 创建新的系统变量。

![Java 主页中的环境变量](../media/java/env-variable-java-home.png "设置适用于 Java")

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

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>如何从类文件中创建的 jar 文件

导航到包含您的类文件的文件夹并运行以下命令：

```cmd
jar -cf <MyJar.jar> *.class
```

请确保路径**jar.exe**是系统 path 变量的一部分。 或者，指定 jar，其中可以下 /bin JDK 文件夹中找到的完整路径： `C:\Users\MyUser\Desktop\jdk-10.0.2\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>后续步骤

+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)