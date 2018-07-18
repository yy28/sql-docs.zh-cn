---
title: 运行故障转移群集实例-Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e48f0e7150fa24361c8b854ced6f90b22448a68b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001680"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>运行故障转移群集实例-Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章介绍了如何运行在 Linux 上的 SQL Server 故障转移群集实例 (FCI)。 如果你尚未在 Linux 上创建 SQL Server FCI，请参阅[配置故障转移群集实例-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)。 

## <a name="failover"></a>故障转移

针对 Fci 的故障转移是类似于 Windows Server 故障转移群集 (WSFC)。 如果承载 FCI 的群集节点遇到某种形式的故障，FCI 应自动故障转移到另一个节点。 与不同的 WSFC，没有任何方法可设置首选的所有者，使 Pacemaker 选取将为 FCI 的新主机的节点。

有些的时候你可能想要手动故障到另一个节点 FCI。 进程不与 Fci 在 WSFC 上相同。 在 WSFC 故障转移在角色级别的资源。 Pacemaker 中, 选择要移动的资源，假定所有约束正确都无误，其他所有内容会将也。 

故障转移到的方式取决于 Linux 分发版。 按照 linux 分发版的说明。

- [RHEL 或 Ubuntu](#rhelFailover)
- [SLES](#slesFailover)

## <a name = "#rhelFailover"></a> 手动故障转移 （RHEL 或 Ubuntu）

若要执行的手动故障转移，在 Red Hat Enterprise Linux (RHEL) 或 Ubuntu 服务器，请执行以下步骤。
1.  发出以下命令： 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > 是 SQL Server FCI 的 Pacemaker 资源名称。

   \<NewHostNode > 是你想要承载 FCI 的群集节点的名称。 

   不会获得任何确认。

2.  在手动故障转移时，Pacemaker 创建选择的目的是手动移动资源的位置约束。 若要查看此约束，请运行`sudo pcs constraint`。

3.  在故障转移完成后，删除该约束通过发出`sudo pcs resource clear <FCIResourceName>`。 

\<FCIResourceName > 是在 FCI 的 Pacemaker 资源名称。 

## <a name = "#slesFailover"></a> 手动故障转移 (SLES)


在 Suse Linux Enterprise Server (SLES)，使用`migrate`命令手动故障转移到 SQL Server FCI。 例如：

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > 是故障转移群集实例的资源名称。 

\<NewHostNode > 是新的目标主机的名称。 


<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
--->

## <a name="next-steps"></a>后续步骤

- [配置故障转移群集实例-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
