---
title: "无人参与的安装在 Ubuntu 上的 SQL Server |Microsoft 文档"
description: "SQL Server 脚本示例-Ubuntu 上的无人参与安装"
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 9ab85f20c1bc8660c54d8d1a2ec946a2121f59f9
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---
# <a name="sample-unattended-sql-server-installation-script-for-ubuntu"></a>示例： 适用于 Ubuntu 的无人参与的 SQL Server 安装脚本

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

此示例 Bash 脚本上 Ubuntu 16.04 中安装 SQL Server 自 2017 年，而无需交互式输入。 它提供的安装数据库引擎、 SQL Server 命令行工具，SQL Server 代理的示例，并执行安装后步骤。 或者，你可以安装全文搜索，并创建一个管理用户。

> [!TIP]
> 如果不需要的无人参与的安装脚本，安装 SQL Server 的最快方法是遵循[适用于 Ubuntu 的快速入门教程](quickstart-install-connect-ubuntu.md)。 有关安装程序的其他信息，请参阅[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>先决条件

- 你需要至少 3.25 GB 的内存来运行在 Linux 上的 SQL Server。
- 文件系统必须是**XFS**或**EXT4**。 其他文件系统，如**BTRFS**，均不受支持。
- 其他系统要求，请参阅[在 Linux 上的 SQL Server 的系统需求](sql-server-linux-setup.md#system)。

## <a name="sample-script"></a>示例脚本

```bash
#!/bin/bash

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list)"
sudo add-apt-repository "${repoargs}"
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
sudo add-apt-repository "${repoargs}"

echo Running apt-get update -y...
sudo apt-get update -y

echo Installing SQL Server...
sudo apt-get install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo apt-get install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo apt-get install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring UFW to allow traffic on port 1433...
sudo ufw allow 1433/tcp
sudo ufw reload

# Optional example of post-installation configuration.
# Trace flags 1204 and 1222 are for deadlock tracing.
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after installing:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 3s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

### <a name="running-the-script"></a>运行脚本

运行该脚本

1. 将示例粘贴到你最喜欢的文本编辑器，并将其保存具有记忆的名称，如`install_sql.sh`。

1. 自定义`MSSQL_SA_PASSWORD`， `MSSQL_PID`，和任何你想要更改的其他变量。

1. 将标记为可执行文件的脚本

   ```bash
   chmod +x install_sql.sh
   ```

1. 运行脚本

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>了解脚本
Bash 脚本执行的第一个操作是设置几个变量。 这些可以是脚本变量，如示例中或环境变量。 变量``` MSSQL_SA_PASSWORD ```是**必需**通过 SQL Server 安装其他类型是为脚本创建的自定义变量。 示例脚本将执行以下步骤：

1. 导入的公钥的 Microsoft GPG 密钥。

1. 注册 SQL Server 和命令行工具的 Microsoft 存储库。

1. 更新本地存储库

1. 安装 SQL Server

1. 配置与 SQL Server```MSSQL_SA_PASSWORD```并自动接受最终用户许可协议。

1. 自动接受 SQL Server 命令行工具的最终用户许可协议、 安装它们，并安装 unixodbc 开发人员包。

1. 将 SQL Server 命令行工具添加到易于使用的路径。

1. 安装 SQL Server 代理，如果脚本变量```SQL_INSTALL_AGENT```，在默认设置。

1. 如果选择安装 SQL Server 全文搜索变量```SQL_INSTALL_FULLTEXT```设置。

1. 取消阻止 tcp 在系统防火墙上，从另一个系统连接到 SQL Server 所需的端口 1433年。

1. 可以选择设置死锁跟踪的跟踪标志。 （需要对行取消注释）

1. 现已安装 SQL Server，才能让其生效，重新启动此过程。

1. 验证 SQL Server 安装正确，，而隐藏任何错误消息。

1. 如果创建新的服务器管理员用户```SQL_INSTALL_USER```和```SQL_INSTALL_USER_PASSWORD```都设置。

## <a name="next-steps"></a>后续步骤

简化多个无人参与的安装，并创建独立的 Bash 脚本，用于设置适当的环境变量。 你可以删除的任何变量的示例脚本使用，并将它们放在其自己的 Bash 脚本。

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

然后运行 Bash 脚本，如下所示：
```bash
. ./my_script_name.sh
```

在 Linux 上 SQL Server 的详细信息，请参阅[Linux 概述上的 SQL Server](sql-server-linux-overview.md)。
