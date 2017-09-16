---
title: "连接到 Azure SQL 数据库 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6115941051862c9979db90b1aa8a58ac3c9b220
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-to-an-azure-sql-database"></a>连接到 Azure SQL 数据库
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主题讨论了问题，在使用时[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]连接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]。 有关连接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，请参阅：  
  
-   [SQL Azure 数据库](http://go.microsoft.com/fwlink/?LinkID=202490)  
  
-   [如何： 连接到使用 JDBC 的 SQL Azure](http://msdn.microsoft.com/library/gg715284.aspx)  
  
-   [使用用 Java SQL Azure](http://msdn.microsoft.com/library/windowsazure/hh749029(VS.103).aspx)

-   [使用 Azure Active Directory 身份验证进行连接](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>详细信息  
 连接到时[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，你应连接到 master 数据库才能调用**SQLServerDatabaseMetaData.getCatalogs**。  
 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]不支持从用户数据库中返回整个集的目录。 **SQLServerDatabaseMetaData.getCatalogs**使用 sys.databases 视图来获取目录。 中的权限的讨论，请参阅[sys.databases （SQL Azure 数据库）](http://go.microsoft.com/fwlink/?LinkId=217396)了解**SQLServerDatabaseMetaData.getCatalogs**行为[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]。  
  
 删除的连接  
 连接到时[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，处于非活动状态一段时间后 （例如防火墙） 的网络组件都可能终止空闲连接。 在此上下文中，有两种类型的空闲连接：  
  
-   TCP 层出现空闲，在此情形下，任意数量的网络设备都可以删除连接。  
  
-   SQL Azure 网关，空闲其中 TCP **keepalive**消息可能 （建立的连接从 TCP 透视不空闲），发生，但未在 30 分钟内进行活动查询。 在这种情况下，网关将确定 TDS 连接处于空闲状态已有 30 分钟，因此将中止连接。  
  
 为了避免网络组件删除空闲连接，应在加载驱动程序的操作系统上设置以下注册表设置（或非 Windows 的等效设置）：  
  
|注册表设置|推荐值|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ 参数 \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ 参数 \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ 参数 \ TcpMaxDataRetransmissions|10|  
  
 然后必须重新启动计算机，注册表设置才能生效。  
  
 为此，在 Windows Azure 中运行时，创建一个启动任务来添加注册表项。  例如，将以下启动任务添加到服务定义文件：  
  
```  
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```  
  
 然后将 AddKeepAlive.cmd 文件添加到您的项目。 将“复制到输出目录”设置为“始终复制”。 以下是一个 AddKeepAlive.cmd 文件示例：  
  
```  
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```  
  
 将服务器名称追加到连接字符串中的 UserId  
 之前的 4.0 版本[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，当连接到[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，你需要服务器名称追加到连接字符串中的用户 Id。 例如， user@servername。 从 4.0 版开始[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，不再需要要追加@servername到连接字符串中的用户 Id。  
  
 使用加密要求设置 hostNameInCertificate  
 连接到时[!INCLUDE[ssAzure](../../includes/ssazure_md.md)]，应指定**hostNameInCertificate**如果指定**加密 = true**。 (如果连接字符串中的服务器名称是*短名称*。*domainName*，将其设置**hostNameInCertificate**属性\*。*domainName*。)  
  
 例如：  
  
```  
jdbc:sqlserver://abcd.int.mscds.com;databaseName= myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate= *.int.mscds.com;  
```  
  
## <a name="see-also"></a>另请参阅  
 [连接到 SQL Server 使用 JDBC 驱动程序](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
