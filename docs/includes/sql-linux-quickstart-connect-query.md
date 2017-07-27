## <a name="connect-locally"></a>本地连接

以下步骤使用 sqlcmd 本地连接到新的 SQL Server 实例。

1. 使用 SQL Server 名称 (-S)，用户名 (-U) 和密码 (-P) 的参数运行 sqlcmd。 在本教程中，用户进行本地连接，因此服务器名称为 `localhost`。 用户名为 `SA`，密码是在安装过程中为 SA 帐户提供的密码。

   ```bash
   sqlcmd -S localhost -U SA -P '<YourPassword>'
   ```

   > [!TIP]
   > 可以省略命令行上提示要输入的密码。

   > [!TIP]
   > 如果以后决定进行远程连接，请指定 -S 参数的计算机名称或 IP 地址，并确保防火墙上的端口 1433 已打开。

1. 如果成功，应会显示 sqlcmd 命令提示符：`1>`。

1. 如果连接失败，请首先尝试根据错误消息诊断问题。 然后查看[连接故障排除建议](../linux/sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="create-and-query-data"></a>创建和查询数据
以下部分将引导你使用 sqlcmd 和 Transact-SQL 完成新建数据库、添加数据并运行简单查询的整个过程。

### <a name="create-a-new-database"></a>新建数据库

以下步骤创建一个名为 `TestDB` 的新数据库。

1. 在 sqlcmd 命令提示符中，粘贴以下 Transact-SQL 命令以创建测试数据库：

   ```sql
   CREATE DATABASE TestDB
   ```

1. 在下一行中，编写一个查询以返回服务器上所有数据库的名称：

   ```sql
   SELECT Name from sys.Databases
   ```

1. 前两个命令没有立即执行。 必须在新行中键入 `GO` 才能执行以前的命令：

   ```sql
   GO
   ```

### <a name="insert-data"></a>插入数据

接下来创建一个新表 `Inventory`，然后插入两个新行。

1. 在 sqlcmd 命令提示符中，将上下文切换到新的 `TestDB` 数据库：

   ```sql
   USE TestDB
   ```

1. 创建名为 `Inventory` 的新表：

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. 将数据插入新表：

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. 要执行上述命令的类型 `GO`：

   ```sql
   GO
   ```

### <a name="select-data"></a>选择数据

现在，运行查询以从 `Inventory` 表返回数据。

1. 在 sqlcmd 命令提示符中，输入一个可从 `Inventory` 表返回行的查询，该表中的行数量大于 152：

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. 执行命令：

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>退出 sqlcmd 命令提示符

要结束 sqlcmd 会话，请键入 `QUIT`：

```sql
QUIT
```

## <a name="connect-from-windows"></a>从 Windows 进行连接

请务必注意，将 Windows 上的 SQL Server 工具连接到 Linux 上的 SQL Server 实例时，操作方式与连接任何远程 SQL Server 实例完全相同。

如果有一台可以连接到 Linux 计算机的 Windows 计算机，请从运行 sqlcmd 的 Windows 命令提示符尝试执行本主题中的相同步骤。 仅验证所使用的是目标 Linux 计算机名称或 IP 地址，而非 localhost，并确保 TCP 端口 1433 已打开。 如果从 Windows 进行连接存在任何问题，请参阅[连接故障排除建议](../linux/sql-server-linux-troubleshooting-guide.md#connection)。

有关在 Windows 上运行，但连接到 Linux 上的 SQL Server 的其他工具，请参阅：

- [SQL Server Management Studio (SSMS)](../linux/sql-server-linux-develop-use-ssms.md)
- [Windows PowerShell](../linux/sql-server-linux-manage-powershell.md)
- [SQL Server Data Tools (SSDT)](../linux/sql-server-linux-develop-use-ssdt.md)

## <a name="next-steps"></a>后续步骤

如果不熟悉 T-SQL，请参阅[ 教程：编写 Transact-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)和 [Transact-SQL 引用（数据库引擎）](../t-sql/language-reference.md)。

要了解连接和管理 SQL Server 的其他方法，请参阅 [Visual Studio Code](../linux/sql-server-linux-develop-use-vscode.md) 和 [SQL Server Management Studio](../linux/sql-server-linux-develop-use-ssms.md)。