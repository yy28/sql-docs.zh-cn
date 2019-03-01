---
title: 在 SQL Server 2019-SQL Server 机器学习服务的 Java 语言扩展
description: 安装、 配置和验证 Linux 和 Windows 系统上 SQL Server 2019 的 Java 语言扩展。
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a18886ea4daff3fb87853a556b67ad0562c2efd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017833"
---
# <a name="java-language-extension-in-sql-server-2019"></a>在 SQL Server 2019 Java 语言扩展 

从 Windows 和 Linux 上的 SQL Server 2019 预览版中开始，你可以运行自定义 Java 代码[可扩展性框架](../concepts/extensibility-framework.md)作为数据库引擎实例的附加项。 

可扩展性框架是用于执行外部代码的体系结构：（从 SQL Server 2019），Java [（从 SQL Server 2017） 的 Python](../concepts/extension-python.md)，并[R （从 SQL Server 2016 开始）](../concepts/extension-r.md)。 执行代码是独立于核心引擎进程，但与 SQL Server 的查询执行完全集成。 这意味着您可以将数据从任何 SQL Server 查询推送到外部运行时，并使用或持久保存回 SQL Server 中的结果。

使用任何编程语言扩展，如系统存储过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)是用于执行预编译的 Java 代码的接口。

<a name="prerequisites"></a>

## <a name="prerequisites"></a>先决条件

SQL Server 2019 预览实例是必需的。 早期版本不具有 Java 集成。

支持 Java 8。 Java Runtime Environment (JRE) 的最低要求，但 Jdk 非常有用，如果您需要 Java 编译器或开发包。 JDK 是全包含所有，如果安装了 JDK，因为不需要 JRE。

可以使用你的首选的 Java 8 分发。 以下是两个建议的分布：

| Distribution | Java 版本 | 操作系统 | JDK | JRE |
|-|-|-|-|-|
| [Oracle Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) | 8 | Windows 和 Linux | 用户帐户控制 | 用户帐户控制 |
| [Zulu OpenJDK](https://www.azul.com/downloads/zulu/) | 8 | Windows 和 Linux | 用户帐户控制 | 否 |

在 Linux 上， **mssql server 扩展性 java**包会自动安装 JRE 8，如果尚未安装。 安装脚本还将 JVM 路径添加到名为 JAVA_HOME 的环境变量。

在 Windows 中，我们建议安装下默认 JDK`/Program Files/`文件夹在可能的情况。 否则，需要额外配置，以授予对可执行文件的权限。 有关详细信息，请参阅[授予的权限 (Windows)](#perms-nonwindows)本文档中的部分。

> [!Note]
> 给定的 Java 是向后兼容，早期版本可能有效，但此早期 CTP 版本的支持和测试版本是 Java 8。 

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>在 Linux 上安装

你可以安装[数据库引擎和 Java 扩展一起](../../linux/sql-server-linux-setup-machine-learning.md#install-all)，或向现有实例中添加的 Java 支持。 下面的示例将 Java 扩展添加到现有安装。  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# SUSE install commands
sudo zypper install mssql-server-extensibility-java
```

当你安装**mssql server 扩展性 java**，如果尚未安装包将自动安装 JRE 8。 它还将添加到名为 JAVA_HOME 的环境变量的 JVM 路径。

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

1. 请确保安装了支持的 Java 版本。 有关详细信息，请参阅[先决条件](#prerequisites)。

2. [运行安装程序](../install/sql-machine-learning-services-windows-install.md)安装 SQL Server 2019。

3. 转到功能选择后，选择**机器学习服务 （数据库内）**。 

   虽然 Java 集成不附带机器学习库，这是提供可扩展性框架的安装程序中的选项。 如果您愿意，可以省略 R 和 Python。

4. 完成安装向导，然后继续执行下面的两个任务。

### <a name="add-the-javahome-variable"></a>添加 JAVA_HOME 变量

JAVA_HOME 是一个环境变量，指定 Java 解释器的位置。 在此步骤中，系统环境变量为其创建在 Windows 上。

1. 查找并复制 JDK/JRE 路径 (例如， `C:\Program Files\Java\jdk1.8.0_201`)。

    具体取决于你的首选 Java 分发，你的 JRE 的 JDK 的位置可能不同于上面的示例路径。

2. 在控制面板中，打开**系统和安全**，打开**系统**，然后单击**高级系统属性**。

3. 单击**环境变量**。

4. 创建新的系统变量用于`JAVA_HOME`JDK/JRE 路径 （在步骤 1 中找到） 的值。

5. 重新启动[快速启动板](../concepts/extensibility-framework.md#launchpad)。

    1. 打开 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。

    2. 在 SQL Server 服务、 右键单击 SQL Server 快速启动板，然后选择**重新启动**。

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

## <a name="differences-in-ctp-23"></a>CTP 2.3 中的差异

如果你已熟悉机器学习服务，扩展的授权和隔离模型已在此版本中更改。 有关详细信息，请参阅[SQL Server 机器 2019年学习服务安装中的差异](../install/sql-machine-learning-services-ver15.md)。

## <a name="limitations-in-ctp-23"></a>CTP 2.3 中的限制

* 输入和输出缓冲区中值的数目不能超过`MAX_INT (2^31-1)`，因为它是可以在 Java 中的数组中分配的元素的最大数目。

* 输出中的参数[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)不支持在此版本中。

* 使用 sp_execute_external_script 参数传送视频流@r_rowsPerRead此 CTP 中不受支持。

* 分区使用 sp_execute_external_script 参数@input_data_1_partition_by_columns此 CTP 中不受支持。

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>如何从类文件中创建的 jar 文件

导航到包含您的类文件的文件夹并运行以下命令：

```cmd
jar -cf <MyJar.jar> *.class
```

请确保路径**jar.exe**是系统 path 变量的一部分。 或者，指定 jar，其中可以下 /bin JDK 文件夹中找到的完整路径： `C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>后续步骤

+ [如何在 SQL Server 中调用 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 示例](java-first-sample.md)
+ [Java 和 SQL Server 数据类型](java-sql-datatypes.md)