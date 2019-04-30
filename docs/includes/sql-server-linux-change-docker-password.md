---
ms.openlocfilehash: 70c86c40f290c26db5bcbc3526d66466c20504d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468921"
---
SA  帐户是安装过程中在 SQL Server 实例上创建的系统管理员。 创建 SQL Server 容器后，通过在容器中运行 `echo $MSSQL_SA_PASSWORD`，可发现指定的 `MSSQL_SA_PASSWORD` 环境变量。 出于安全考虑，请考虑更改 SA 密码。

1. 选择 SA 用户要使用的强密码。

1. 使用 `docker exec` 运行sqlcmd，以使用 Transact-SQL 更改密码。 将 `<YourStrong!Passw0rd>` 和 `<YourNewStrong!Passw0rd>` 替换为自己的密码值。

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
