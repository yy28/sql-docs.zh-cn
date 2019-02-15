---
title: 连接到 Azure SQL 数据库 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d948e4a790933e6f703232e3f642241395bbb410
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736978"
---
# <a name="connecting-to-an-azure-sql-database"></a>连接到 Azure SQL 数据库

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文章讨论使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 连接到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 时遇到的问题。 有关连接到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 的详细信息，请参阅：  
  
- [SQL Azure 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)  
  
- [如何使用 JDBC 连接到 SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)  

- [使用 Azure Active Directory 身份验证连接](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>详细信息

当连接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，则应连接到 master 数据库以调用**SQLServerDatabaseMetaData.getCatalogs**。  
[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 不支持从用户数据库中返回整个目录集。 **SQLServerDatabaseMetaData.getCatalogs**使用 sys.databases 视图获取目录。 中的权限的讨论，请参阅[sys.databases （SQL Azure 数据库）](https://go.microsoft.com/fwlink/?LinkId=217396)若要了解**SQLServerDatabaseMetaData.getCatalogs**上的行为[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]。  
  
## <a name="connections-dropped"></a>删除的连接

连接到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 时，空闲连接在处于不活动状态一定时间后可能被某个网络组件（如防火墙）终止。 在此上下文中，有两种类型的空闲连接：  

- TCP 层出现空闲，在此情形下，任意数量的网络设备都可以删除连接。  

- SQL Azure 网关出现空闲，在此情形下，可能会发生 TCP keepalive 消息（使连接从 TCP 的角度看不再空闲），但在 30 分钟内没有活动的查询。 在这种情况下，网关将确定 TDS 连接处于空闲状态已有 30 分钟，因此将中止连接。  
  
为了避免网络组件删除空闲连接，应在加载驱动程序的操作系统上设置以下注册表设置（或非 Windows 的等效设置）：  
  
|注册表设置|推荐值|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ TcpMaxDataRetransmissions|10|  
  
重启计算机，注册表设置才能生效。  

为此，在 Windows Azure 中运行时，创建一个启动任务来添加注册表项。  例如，将以下启动任务添加到服务定义文件：  

```xml
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```

然后将 AddKeepAlive.cmd 文件添加到您的项目。 将“复制到输出目录”设置为“始终复制”。 以下是一个 AddKeepAlive.cmd 文件示例：  

```bat
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```

## <a name="appending-the-server-name-to-the-userid-in-the-connection-string"></a>将服务器名称追加到连接字符串中的 UserId  

在 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 之前的版本中，连接到 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 时，要求将服务器名称追加到连接字符串中的 UserId。 例如， user@servername。 从 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 版本开始，不再要求将 @@servername 追加到连接字符串中的 UserId。  

## <a name="using-encryption-requires-setting-hostnameincertificate"></a>使用加密要求设置 hostNameInCertificate

之前的版本 7.2 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，连接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，则应指定**hostNameInCertificate**如果你指定**加密 = true** （如果在连接中的服务器名称字符串是*短名称*。*domainName*，将**hostNameInCertificate**属性设置为\*。*domainName*。)。 此属性是可选自版本 7.2 的驱动程序。

例如：

```java
jdbc:sqlserver://abcd.int.mscds.com;databaseName=myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate=*.int.mscds.com;
```

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
