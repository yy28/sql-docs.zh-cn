1. **在所有 SQL Server 上，为 Pacemaker 创建 Server 登录名**。 以下 Transact-SQL 创建登录名：

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

   或者，可以在更精细的级别设置权限。 Pacemaker 登录需要 ALTER、CONTROL 和 VIEW DEFINITION 权限。 有关详细信息，请参阅 [GRANT 可用性组权限 (Transact-SQL)](http://msdn.microsoft.com/library/hh968934.aspx)。

   以下 Transact-SQL 仅授予 Pacemaker 登录所需的权限。 在下面的语句中，“ag1”是将添加为群集资源的可用性组的名称。

   ```Transact-SQL
   GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO pacemakerLogin
   ```

1. **在所有 SQL Server 上，保存 SQL Server 登录名的凭据**。

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
