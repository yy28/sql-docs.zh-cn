---
title: "PolyBase 安装 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase, installation
ms.assetid: 3a1e64be-9bfc-4408-accd-35990e1a6b52
caps.latest.revision: 25
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f5b029907f25811131e08d2f7ade1f050e3a18d5
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="polybase-installation"></a>PolyBase 安装
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  若要安装 SQL Server 试用版，请转到 [SQL Server 评估](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)。 
  
## <a name="prerequisites"></a>先决条件  
  
-   64 位 SQL Server 评估版  
  
-   Microsoft .NET Framework 4.5。  
  
-   Oracle Java SE RunTime Environment (JRE) 版本 7.51 或更高版本（64 位）（ [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 或 [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) 均可）。 转到 [Java SE 下载](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。 如果不存在 JRE，安装程序将失败。  
  
-   最小内存：4GB  
  
-   最小硬盘空间：2GB  
  
-   必须启用 TCP/IP 连接。 （请参阅 [启用或禁用服务器网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。）  
  
 **说明**  
  
 在每台计算机上仅可在一个 SQL Server 实例上安装 PolyBase。  
  
## <a name="single-node-or-polybase-scaleout-group"></a>单节点或 PolyBase 横向扩展组
开始在 SQL Server 实例上安装 PolyBase 之前，最好规划一下你是需要单节点安装还是需要 PolyBase 横向扩展组。 对于 PolyBase 横向扩展组，你将需要确保： 
- 所有计算机都位于同一域中。
- 你在安装期间使用相同的服务帐户和密码。
- 你的 SQL Server 实例彼此之间可以通过网络进行通信。

无论是以独立模式还是以横向扩展组模式安装 PolyBase，在安装后都无法更改。 若要更改此设置，你必须卸载并重新安装该功能。

## <a name="install-using-the-installation-wizard"></a>使用安装向导进行安装  
  
1.  运行“SQL Server 安装中心”。 插入 SQL Server 安装介质，然后双击“Setup.exe”。  
  
2.  单击“安装”，然后单击“全新独立 SQL Server 安装或添加功能”。  
  
3.  在功能选择页上，选择“针对外部数据的 PolyBase 查询服务” 。  
  
4.  在服务器配置页上，将“SQL Server PolyBase 引擎服务”和“SQL Server PolyBase 数据移动服务”配置为在同一帐户下运行。  
  
    > **重要说明!!** 在 PolyBase 扩展组中，所有节点上的 PolyBase 引擎和 PolyBase 数据移动服务必须在同一个域帐户下运行。  
    > 请参阅“扩展 PolyBase”。  
  
5.  在“PolyBase 配置页” 上，选择两个选项之一。 有关详细信息，请参阅 [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md)（PolyBase 扩展组）。  
  
    -   将 SQL Server 实例用作已启用 PolyBase 的独立实例。  
  
         选择此选项可将 SQL Server 实例用作独立的头节点。  
  
    -   将 SQL Server 实例作为 PolyBase 扩展组的一部分使用。  选择此选项将打开防火墙，以允许与 SQL Server 数据库引擎、SQL Server PolyBase 引擎、SQL Server PolyBase 数据移动服务和 SQL Browser 建立传入连接。 打开防火墙，以允许来自 PolyBase 扩展组中其他节点的传入连接。  
  
         选择此选项还将启用 Microsoft 分布式事务处理协调器 (MSDTC) 防火墙连接并修改 MSDTC 注册表设置。  
  
6.  在“PolyBase 配置页” 上，指定具有至少六个端口的端口范围。 SQL Server 安装程序将分配该范围中的前六个可用端口。  
  
##  <a name="installing"></a> 使用命令提示符进行安装  
 使用此表中的值来创建安装脚本。 **SQL Server PolyBase 引擎** 和 **SQL Server PolyBase 数据移动服务** 这两项服务必须在同一帐户下运行。 在 PolyBase 扩展组中，所有节点上的 PolyBase 服务必须在同一个域帐户下运行。  
  
|SQL Server 组件 (SQL Server component)|参数和值|说明|  
|--------------------------|--------------------------|-----------------|  
|SQL Server 安装程序控件|**必需**<br /><br /> /FEATURES=PolyBase|选择 PolyBase 功能。|  
|SQL Server PolyBase 引擎|**可选**<br /><br /> /PBENGSVCACCOUNT|指定引擎服务的帐户。 默认为 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase 引擎|**可选**<br /><br /> /PBENGSVCPASSWORD|指定引擎服务帐户的密码。|  
|SQL Server PolyBase 引擎|**可选**<br /><br /> /PBENGSVCSTARTUPTYPE|指定 PolyBase 引擎服务的启动模式：自动（默认值）、禁用和手动|  
|SQL Server PolyBase 数据移动服务|**可选**<br /><br /> /PBDMSSVCACCOUNT|指定数据移动服务的帐户。 默认为 **NT Authority\NETWORK SERVICE**。|  
|SQL Server PolyBase 数据移动服务|**可选**<br /><br /> /PBDMSSVCPASSWORD|指定数据移动帐户的密码。|  
|SQL Server PolyBase 数据移动服务|**可选**<br /><br /> /PBDMSSVCSTARTUPTYPE|指定数据移动服务的启动模式：自动（默认值）、禁用和手动|  
|PolyBase|**可选**<br /><br /> /PBSCALEOUT|指定是否将 SQL Server 实例用作 PolyBase 扩展计算组的一部分。 <br />支持的值： **True**、 **False**|  
|PolyBase|**可选**<br /><br /> /PBPORTRANGE|使用最少 6 个端口为 PolyBase 服务指定端口范围。 例如：<br /><br /> `/PBPORTRANGE=16450-16460`|  
  
 **示例**  
  
 这将显示一个示例安装程序脚本。  
  
```  
  
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,Polybase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
  
```  
  
## <a name="post-installation-notes"></a>安装后说明  
 PolyBase 安装三个用户数据库：DWConfiguration、DWDiagnostics 和 DWQueue。   这些数据库供 PolyBase 使用，不得更改或删除。  
  
### <a name="how-to-confirm-installation"></a>如何确认安装  
 运行以下命令。 如果已安装 PolyBase，则返回 1；否则返回 0。  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
### <a name="firewall-rules"></a>防火墙规则  
 SQL Server PolyBase 安装程序将在计算机上创建以下防火墙规则。  
  
-   SQL Server PolyBase – 数据库引擎 - \<SQLServerInstanceName> (TCP-In)  
  
-   SQL Server PolyBase – PolyBase 服务 - \<SQLServerInstanceName> (TCP-In)  
  
-   SQL Server PolyBase - SQL Browser - (UDP-In)  
  
 安装时，如果选择将 SQL Server 实例作为 PolyBase 扩展组的一部分使用，则将启用这些规则，并打开防火墙以允许与 SQL Server 数据库引擎、SQL Server PolyBase 引擎、SQL Server PolyBase 数据移动服务和 SQL Browser 建立传入连接。 但是，如果在安装期间未运行计算机上的防火墙服务，SQL Server 安装程序将无法启用这些规则。 在这种情况下，你必须在计算机上启动防火墙服务并启用这些安装后规则。  
  
#### <a name="to-enable-the-firewall-rules"></a>启用防火墙规则的步骤  
  
-   打开“控制面板” 。  
  
-   单击“系统和安全” ，然后单击“Windows 防火墙” 。  
  
-   单击“高级设置” ，然后单击“入站规则” 。  
  
-   右键单击已禁用的规则，然后单击“启用规则”。  
  
### <a name="polybase-service-accounts"></a>PolyBase 服务帐户
若要更改的 PolyBase 引擎和 PolyBase 数据移动服务的服务帐户，请卸载并重新安装 PolyBase 功能。
   
## <a name="next-steps"></a>后续步骤  
 请参阅 [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md)。  
  
  

