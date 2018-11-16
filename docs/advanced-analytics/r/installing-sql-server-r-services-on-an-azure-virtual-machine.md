---
title: 在 Azure 虚拟机上使用 R 和 Python 安装 SQL Server 机器学习服务 |Microsoft Docs
description: R 和 Python 的数据科学和机器学习解决方案在 Azure 云中的 SQL Server 虚拟机上运行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e416b99c3d4597cb2fe9346819184be43cd98402
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512692"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>在 Azure 虚拟机上使用 R 和 Python 安装 SQL Server 机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 Azure 中，消除了安装和配置任务的 SQL Server 虚拟机上，可以使用机器学习服务安装 R 和 Python 集成。 虚拟机部署后，功能是可供使用。
 
有关分步说明，请参阅[如何预配 Windows SQL Server 虚拟机在 Azure 门户中](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)。

[配置 SQL server 设置](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#4-configure-sql-server-settings)步是在其中将机器学习添加到你的实例。

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>取消阻止防火墙

默认情况下，Azure 虚拟机上的防火墙包含阻止网络访问本地用户帐户的规则。

必须禁用此规则，以确保可以访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从远程数据科学客户端的实例。  否则，不能在使用虚拟机的工作区的计算上下文中执行机器学习代码。

若要启用从远程数据科学客户端的访问权限：

1. 在虚拟机上打开“高级安全 Windows 防火墙”。
2. 选择“出站规则”。
3. 禁用以下规则：
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>启用远程客户端的 ODBC 回调

如果希望客户端调用服务器需要发出 ODBC 查询作为其机器学习解决方案的一部分，则必须确保快速启动板可以代表远程客户端的 ODBC 调用。 

为此，必须允许 Launchpad 使用的 SQL 辅助角色帐户登录到实例。 有关详细信息，请参阅[作为数据库用户添加 SQLRUserGroup](../security/add-sqlrusergroup-to-database.md)。

<a name="network"></a>

## <a name="add-network-protocols"></a>添加网络协议

+ 启用命名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 对客户端与服务器计算机之间的连接以及某些内部连接使用命名管道协议。 如果未启用命名管道，必须同时在 Azure 虚拟机以及连接到服务器的任何数据科学客户端上安装并启用命名管道。
  
+ 启用 TCP/IP

  TCP/IP 是环回连接所必需的。 如果收到错误"DBNETLIB;SQL Server 不存在或访问被拒绝"，在支持该实例的虚拟机上启用 TCP/IP。