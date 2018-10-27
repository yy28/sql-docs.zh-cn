### <a id="sampledata"></a> 加载示例数据

SQL Server 大数据群集教程使用一组通用的示例数据。 使用以下步骤在大数据群集上配置的示例数据：

1. 如果不具有 SQL Server 命令行工具 (**sqlcmd**并**bcp**) 安装，请首先安装这些工具与链接之一：

   * **Windows**:[在 Windows 上的安装 SQL Server 命令行工具](https://www.microsoft.com/download/details.aspx?id=53591)
   * **Linux**: [Linux 上的安装 SQL Server 命令行工具](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-tools)

1. 下载示例备份文件[tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak)到计算机。

1. 导航到 SQL Server 2019 大数据群集[示例目录](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)。

1. 下载[bootstrap 示例 db.sql](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql) Transact SQL 脚本。

1. 下载并从命令行运行以下两个示例脚本之一：

   * **Windows**: [bootstrap 示例 db.cmd](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd)
   * **Linux**: [bootstrap 示例 db.sh](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh)

   > [!TIP]
   > 可以通过不带任何参数运行该脚本获取使用情况的说明。

该脚本将示例数据库还原到 SQL Server 主实例，并且还将数据加载到 HDFS 中存储池。