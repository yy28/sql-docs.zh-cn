SA  帐户是在安装期间创建的 SQL Server 实例上的系统管理员。 创建 SQL Server 容器后，可以通过在容器中运行 `echo $MSSQL_SA_PASSWORD` 来发现指定的 `MSSQL_SA_PASSWORD` 环境变量。 出于安全考虑，请考虑更改 SA 密码：

1. 选择 SA 用户要使用的强密码。

1. 使用 `docker exec` 运行 sqlcmd  实用工具，以通过 Transact-SQL 语句来更改密码。 将 `<YourStrong!Passw0rd>` 和 `<YourNewStrong!Passw0rd>` 替换为你自己的密码值：

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
