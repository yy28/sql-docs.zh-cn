---
title: "使用 sqlcmd 连接 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b26f383b6e324681d561c0add4298c8f8084523
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-with-sqlcmd"></a>使用 sqlcmd 进行连接
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[Sqlcmd](http://go.microsoft.com/fwlink/?LinkID=154481)实用工具位于[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 和 macOS 上。
  
下面的命令演示如何使用 Windows 身份验证 (Kerberos) 和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]身份验证，分别：
  
```  
sqlcmd –E –Sxxx.xxx.xxx.xxx  
sqlcmd –Sxxx.xxx.xxx.xxx –Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>可用选项

在当前版本中，还提供以下选项：  
  
- -? 显示`sqlcmd`使用情况。  
  
- -a 请求的数据包大小。  
  
- -b 终止批处理作业如果没有错误。  
  
- -c *batch_terminator*指定批处理终止符。  
  
- -C 信任服务器证书。  

- -d *database_name*问题`USE ` *database_name*语句启动时`sqlcmd`。  

- -D 会导致值传递给`sqlcmd`-S 选项被解释为数据源名称 (DSN)。 有关详细信息，请参阅"中的 DSN 支持`sqlcmd`和`bcp`"本主题的末尾。  
  
- -e 写入标准输出设备 (stdout) 的输入的脚本。

- -E 使用可信的连接 （集成身份验证）。进行使用集成身份验证从 Linux 或 macOS 客户端的受信任的连接的详细信息，请参阅[使用集成身份验证](../../../connect/odbc/linux-mac/using-integrated-authentication.md)。

- -h *number_of_rows*指定要在列标题之间打印的行数。  
  
- -H 指定工作站的名称。  
  
- -i *input_file*[，*input_file*[，...]]标识包含一批 SQL 语句或存储过程的文件。  
  
- -I 集`SET QUOTED_IDENTIFIER`连接选项为 ON。  
  
- -k 删除或替换控制字符。  
  
- **-K***application_intent*  
连接到服务器时声明应用程序工作负荷类型。 目前唯一支持的值是 **ReadOnly**。 如果**-K**未指定，`sqlcmd`不支持连接到辅助副本的 AlwaysOn 可用性组中。 有关详细信息，请参阅[上 Linux 和 macOS 的高可用性和灾难恢复的 ODBC 驱动程序](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  
  
> [!NOTE]  
> **-K** 在适用于 SUSE Linux 的 CTP 中不受支持。 但是，可以指定**ApplicationIntent = ReadOnly** DSN 文件中的关键字传递给`sqlcmd`。 有关详细信息，请参阅"中的 DSN 支持`sqlcmd`和`bcp`"本主题的末尾。  
  
- -l*超时*指定之前的秒数`sqlcmd`当你尝试连接到服务器时，登录超时。

- -m *error_level*控制哪些错误消息发送到 stdout。  
  
- **-M***multisubnet_failover*  
在连接到 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 可用性组或 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 **-M**。 **-M**提供更快地检测故障转移和到 （当前） 活动服务器的连接。 如果不指定 **–M** ，则 **-M** 处于关闭状态。 有关详细信息[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]，请参阅[上 Linux 和 macOS 的高可用性和灾难恢复的 ODBC 驱动程序](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  
  
> [!NOTE]  
> **-M** 在适用于 SUSE Linux 的 CTP 中不受支持。 但是，可以指定**MultiSubnetFailover = Yes** DSN 文件中的关键字传递给`sqlcmd`。 有关详细信息，请参阅"中的 DSN 支持`sqlcmd`和`bcp`"本主题的末尾。  
  
- -N 对连接进行加密。  
  
- -o *output_file*标识接收输出的文件`sqlcmd`。  
  
- -p 打印性能统计信息为每个结果集的。  
  
- -P 指定用户密码。  
  
- -q *commandline_query*执行查询时`sqlcmd`启动，但不退出时查询运行完毕。  

- -Q *commandline_query*执行查询时`sqlcmd`启动。 `sqlcmd`在查询结束时，将退出。  

- -r 重定向到 stderr 的错误消息。

- -R 将导致驱动程序使用客户端区域设置来将货币和日期和时间数据转换为字符数据。 当前仅使用 en_US（美国英语）格式设置。
  
- -s *column_separator_char*指定列分隔符字符。  

- -S [*protocol*:] *server*[**,***port*]  
指定的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]要连接到或-D 是否使用，DSN。 在 Linux 和 macOS 上的 ODBC 驱动程序要求-s。 请注意， **tcp**是唯一有效的协议。  
  
- -t *query_timeout*指定的命令 （或 SQL 语句） 在超时之前等待的秒数。  
  
- -u 指定该 output_file 存储在 Unicode 格式，而不考虑 input_file 的格式。  
  
- -U *login_id*指定用户登录 id。  
  
- -V *error_severity_level*控制用于设置 ERRORLEVEL 变量的严重性级别。  
  
- -w *column_width*指定输出的屏幕宽度。  
  
- -W 从列删除尾随空格。  
  
- -x 禁用变量替换。  
  
- -X 禁用命令、 启动脚本和环境变量。  
  
- -y *variable_length_type_display_width*设置`sqlcmd`脚本变量`SQLCMDMAXFIXEDTYPEWIDTH`。
  
- -Y *fixed_length_type_display_width*设置`sqlcmd`脚本变量`SQLCMDMAXVARTYPEWIDTH`。


## <a name="available-commands"></a>可用的命令

在当前版本中，会出现以下命令：  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>不可用选项
在当前版本中，以下选项不可用：  

- -A 中登录到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]与专用的管理员连接 (DAC)。 有关如何建立专用的管理员连接 (DAC) 的信息，请参阅[编程准则](../../../connect/odbc/linux-mac/programming-guidelines.md)。  
  
- -f *code_page*指定的输入和输出的代码页。  
  
- -L 列出的本地配置的服务器计算机，以及在网络广播的服务器计算机的名称。  
  
- -v 创建`sqlcmd`可以在中使用的脚本变量`sqlcmd`脚本。  
  
你可以使用以下替代方法： 将参数放入一个文件，然后将追加到另一个文件内。 这将有助于你使用参数文件来替换值。 例如，创建名为的文件`a.sql`（参数文件） 包含以下内容：
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
然后创建名为的文件`b.sql`，替换的参数：  
  
    select $(ColumnName) from $(TableName)  

在命令行中，组合`a.sql`和`b.sql`到`c.sql`使用以下命令：  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
运行`sqlcmd`并用`c.sql`为输入文件：  
  
    slqcmd -S<…> -P<..> –U<..> -I c.sql  

- -z*密码*更改密码。  
  
- -Z*密码*更改密码并退出。  

## <a name="unavailable-commands"></a>不可用的命令

在当前版本中，以下命令不可用：  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>sqlcmd 和 bcp 中的 DSN 支持

你可以指定数据源名称 (DSN) 而不是中的服务器名称**sqlcmd**或**bcp** `-S`选项 (或**sqlcmd** ： 连接命令) 如果你指定-D. -D 导致**sqlcmd**或**bcp**连接到在 DSN 中通过-S 选项指定的服务器。  
  
在存储系统 Dsn `odbc.ini` ODBC SysConfigDir 目录中的文件 (`/etc/odbc.ini`标准安装上)。 用户 Dsn 存储在`.odbc.ini`中用户的主目录 (`~/.odbc.ini`)。
  
在 Linux 或 macOS 上 DSN 中支持的以下条目：

-   **ApplicationIntent = ReadOnly**  

-   **数据库 =***database_name*  
  
-   **驱动程序 = ODBC Driver 11 for SQL Server**或**驱动程序 = ODBC Driver 13 for SQL Server**
  
-   **MultiSubnetFailover = Yes**  
  
-   **服务器 =***server_name_or_IP_address*  
  
-   **Trusted_Connection=yes**|**no**  
  
在 DSN 中的驱动程序项是必需的但若要连接到服务器，`sqlcmd`或`bcp`需要服务器条目中的值。  

如果在这两个 DSN 中指定相同的选项和`sqlcmd`或`bcp`命令行中，命令行选项将重写在 DSN 中使用的值。 例如，如果 DSN 具有某一数据库项和`sqlcmd`命令行包括**-d**，传递给值**-d**使用。 如果**Trusted_Connection = yes** DSN，则使用身份验证的 Kerberos 和用户名称中指定 (**– U**) 和密码 (**– P**)，如果提供，将被忽略。

调用的现有脚本`isql`可以修改为使用`sqlcmd`通过定义以下别名： `alias isql="sqlcmd –D"`。  

## <a name="see-also"></a>另请参阅  
[使用连接**bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 

