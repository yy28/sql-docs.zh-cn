---
title: 在添加或修改可用性副本时指定端点 URL （SQL Server） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- endpoints [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], endpoint
- Endpoint URLs (HADR)
ms.assetid: d7520c13-a8ee-4ddc-9e9a-54cd3d27ef1c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 524f9d4b3173a70d3491f2efc0f00f4061c4d6b4
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797965"
---
# <a name="specify-the-endpoint-url-when-adding-or-modifying-an-availability-replica-sql-server"></a>在添加或修改可用性副本时指定端点 URL (SQL Server)
  若要为某一可用性组承载可用性副本，服务器实例必须拥有数据库镜像端点。 该服务器实例使用此端点来侦听来自其他服务器实例承载的可用性副本的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 消息。 若要为某一可用性组定义可用性副本，您必须指定将承载该副本的服务器实例的端点 URL。 “端点 URL”标识数据库镜像端点的传输协议 - TCP、服务器实例的系统地址以及与端点关联的端口号。  
  
> [!NOTE]  
>  “端点 URL”一词是“服务器网络地址”一词的同义词，由数据库镜像的用户界面和文档使用。  
  
-   [端点 URL 的语法](#SyntaxOfURL)  
  
-   [查找系统的完全限定域名](#Finding_FQDN)  
  
-   [相关任务](#RelatedTasks)  
  
-   [相关内容](#RelatedContent)  
  
##  <a name="SyntaxOfURL"></a> 端点 URL 的语法  
 端点 URL 的语法采用以下形式：  
  
 TCP<strong>://</strong> *\<system-address>* <strong>:</strong> *\<port>*  
  
 其中  
  
-   \<system-address> 是明确标识目标计算机系统的字符串。 通常，服务器地址是系统名称（如果各系统都在同一个域中）、完全限定域名或 IP 地址：  
  
    -   因为 Windows Server 故障转移群集 (WSFC) 群集的节点处于相同的域，所以，您可以使用计算机系统的名称，例如 `SYSTEM46`。  
  
    -   若要使用 IP 地址，则该地址在您环境中必须是唯一的。 建议只使用静态的 IP 地址。 IP 地址可以是 IP 版本 4 (IPv4) 或 IP 版本 6 (IPv6)。 必须用方括号将 IPv6 地址括起，例如： **[** _<IPv6_address>_ **]** 。  
  
         若要了解系统的 IP 地址，则在 Windows 命令提示符处，输入 **ipconfig** 命令。  
  
    -   保证完全限定域名的有效性。 它是在不同位置具有不同形式的本地定义的地址字符串。 通常（但并不总是），完全限定域名是一个复合名称，包含计算机名称和一系列句点分隔的域段，其格式为：  
  
         _computer_name_ **。** _domain_segment_[... **.** _domain_segment_]  
  
         其中， *computer_name*是运行服务器实例的计算机的网络名称， *domain_segment*[... **.** _domain_segment_] 是服务器的其余域信息；例如： `localinfo.corp.Adventure-Works.com`。  
  
         在公司或组织内确定域段的内容和数量。 有关详细信息，请参阅本主题后面的 [查找完全限定域名](#Finding_FQDN)。  
  
-   \<port> 是合作伙伴服务器实例的镜像终结点所使用的端口号。  
  
     数据库镜像端点可以使用计算机系统上的任意可用端口。 每个端口号只能与一个端点相关联，而每个端点与一个服务器实例相关联；这样，同一服务器上的不同服务器实例便可使用不同端口来侦听各个端点。 因此，在您指定可用性副本时在端点 URL 中指定的端口会始终将传入消息定向到其端点与该端口关联的服务器实例。  
  
     在端点 URL 中，只有端口号才能标识与目标计算机上的镜像端点相关联的服务器实例。 下图显示了一台计算机上两个服务器实例的端点 URL。 默认实例使用端口 `7022` ，命名实例使用端口 `7033`。 这两个服务器实例的端点 URL 分别为： `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` 和 `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`。 请注意，地址中不包含服务器实例名。  
  
     ![默认实例的服务器网络地址](../../media/dbm-2-instances-ports-1-system.gif "默认实例的服务器网络地址")  
  
     若要标识当前与服务器实例的数据库镜像端点关联的端口，请使用以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句：  
  
    ```sql
    SELECT type_desc, port FROM sys.TCP_endpoints  
    ```  
  
     找到 **type_desc** 值为“DATABASE_MIRRORING”的行，然后使用对应的端口号。  
  
### <a name="examples"></a>示例  
  
#### <a name="a-using-a-system-name"></a>A. 使用系统名称  
 以下端点 URL 指定系统名称 `SYSTEM46`和端口 `7022`。  
  
 `TCP://SYSTEM46:7022`  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>B. 使用完全限定域名  
 以下端点 URL 指定完全限定域名 `DBSERVER8.manufacturing.Adventure-Works.com`和端口 `7024`。  
  
 `TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024`  
  
#### <a name="c-using-ipv4"></a>C. 使用 IPv4  
 以下端点 URL 指定 IPv4 地址 `10.193.9.134`和端口 `7023`。  
  
 `TCP://10.193.9.134:7023`  
  
#### <a name="d-using-ipv6"></a>D. 使用 IPv6  
 以下端点 URL 包含 IPv6 地址 `2001:4898:23:1002:20f:1fff:feff:b3a3`和端口 `7022`。  
  
 `TCP://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022`  
  
##  <a name="Finding_FQDN"></a> 查找系统的完全限定域名  
 若要查找系统的完全限定域名，请在该系统的 Windows 命令提示符下，输入：  
  
 **IPCONFIG /ALL**  
  
 若要形成完全限定的域名，请将 *<host_name>* 和 *<Primary_Dns_Suffix>* 的值连接一起，如下所示：  
  
 _<host_name>_ **.** _<Primary_Dns_Suffix>_  
  
 例如，IP 配置  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 等同于以下完全限定域名：  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
> [!NOTE]  
>  如果您需要与完全限定域名有关的详细信息，请与系统管理员联系。  
  
##  <a name="RelatedTasks"></a>相关任务  
 **配置数据库镜像端点**  
  
-   [为 AlwaysOn 可用性组&#40;创建数据库镜像端点 SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [使用数据库镜像终结点证书 (Transact-SQL)](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [允许数据库镜像终结点将证书用于入站连接 (Transact-SQL)](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [指定服务器网络地址（数据库镜像）](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [删除 SQL Server&#41;AlwaysOn 可用性组&#40;配置的疑难解答](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
 **查看有关数据库镜像端点的信息**  
  
-   [sys.database_mirroring_endpoints (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **添加可用性副本**  
  
-   [将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [将辅助副本联接到可用性组 (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [Microsoft SQL Server AlwaysOn 解决方案指南以实现高可用性和灾难恢复](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>另请参阅  
 [创建和配置可用性组 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)   
 [ &#40;AlwaysOn 可用性组 SQL Server&#41;   概述](overview-of-always-on-availability-groups-sql-server.md)  
 [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql)  
