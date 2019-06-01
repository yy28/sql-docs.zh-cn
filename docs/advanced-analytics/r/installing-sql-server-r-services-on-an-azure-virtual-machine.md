---
title: Azure 虚拟机的 SQL Server 机器学习服务上安装 R 语言和 Python 功能
description: R 和 Python 的数据科学和机器学习解决方案在 Azure 云中的 SQL Server 虚拟机上运行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 65c6afcf3f74e320237c1f345ad643752fde6ae0
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454759"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>在 Azure 虚拟机上使用 R 和 Python 安装 SQL Server 机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

可以在 Azure 中的 SQL Server 虚拟机上安装 R 和 Python 与机器学习服务的集成，这样就不需执行安装和配置任务。 一旦虚拟机部署好，这些功能就可以使用了。
 
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

为此，必须允许 Launchpad 使用的 SQL 辅助角色帐户登录到实例。 有关详细信息，请参阅[作为数据库用户添加 SQLRUserGroup](../security/create-a-login-for-sqlrusergroup.md)。

<a name="network"></a>

## <a name="add-network-protocols"></a>添加网络协议

+ 启用命名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 对客户端与服务器计算机之间的连接以及某些内部连接使用命名管道协议。 如果未启用命名管道，必须同时在 Azure 虚拟机以及连接到服务器的任何数据科学客户端上安装并启用命名管道。
  
+ 启用 TCP/IP

  TCP/IP 是环回连接所必需的。 如果收到错误"DBNETLIB;SQL Server 不存在或访问被拒绝"，在支持该实例的虚拟机上启用 TCP/IP。