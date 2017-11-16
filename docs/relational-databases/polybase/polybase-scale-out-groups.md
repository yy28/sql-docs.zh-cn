---
title: "PolyBase 横向扩展组 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 05/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
caps.latest.revision: "20"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 989b6a52d4a0e26b32f292fad44a5ad1caf0b71b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="polybase-scale-out-groups"></a>PolyBase 横向扩展组
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  在处理 Hadoop 或 Azure Blob 存储中的大型数据集时，具有 PolyBase 的独立 SQL Server 实例可能成为性能瓶颈。 PolyBase 组功能允许你创建 SQL Server 实例的群集来处理来自外部数据源的大型数据集（如 Hadoop 或 Azure Blob 存储），从而通过一种扩展的方式提高查询性能。  
  
 请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md) 和 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)。  
  
 ![PolyBase 横向扩展组](../../relational-databases/polybase/media/polybase-scale-out-groups.png "PolyBase 横向扩展组")  
  
## <a name="overview"></a>概述  
  
### <a name="head-node"></a>头节点  
 头节点包含 PolyBase 查询提交到的 SQL Server 实例。 每个 PolyBase 组只能有一个头节点。 头节点是 SQL Server 实例上 SQL 数据库引擎、PolyBase 引擎和 PolyBase 数据移动服务的逻辑组。  
  
### <a name="compute-node"></a>计算节点  
 计算节点包含协助扩展查询处理外部数据的 SQL Server 实例。 计算节点是 SQL Server 和 SQL Server 实例上的 PolyBase 数据移动服务的逻辑组。 PolyBase 组可以有多个计算节点。  
  
### <a name="distributed-query-processing"></a>分布式查询处理  
 PolyBase 查询会提交到头节点上的 SQL Server。 查询中引用外部表的那部分会移交给 PolyBase 引擎。  
  
 PolyBase 引擎是 PolyBase 查询背后的关键组件。 它对外部数据查询进行分析、生成查询计划并将工作分发到计算节点上的数据移动服务以便执行。 完成工作后，它将接收来自计算节点的结果，并将其提交给 SQL Server 进行处理并返回到客户端。  
  
 PolyBase 数据移动服务接收来自 PolyBase 引擎的指令，并在 HDFS 和 SQL Server 之间以及头节点和计算节点上的 SQL Server 实例之间传输数据。  
  
### <a name="editions-availability"></a>版本可用性  
 在设置 SQL Server 后，可以将该实例指定为头节点或计算节点。  选择结果取决于运行 PolyBase 的 SQL Server 的版本。 在 Enterprise Edition 安装中，可将该实例指定为头节点或计算节点。 在 Standard Edition 中，只能将该实例指定为计算节点。  
  
## <a name="to-configure-a-polybase-group"></a>若要配置 PolyBase 组  
  
### <a name="prerequisites"></a>先决条件  
  
-   N 台机器位于同一域中  
  
-   使用域用户帐户来运行 PolyBase 服务  
  
### <a name="steps"></a>步骤  
  
1.  在 N 台机器上安装具有 PolyBase 的 SQL Server。  
  
2.  选择一个 SQL Server 实例作为头节点。 只能在运行 SQL Server Enterprise 的实例上指定头节点。  
  
3.  使用 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md) 将剩余的 SQL Server 实例添加为计算节点。  
  
4.  使用 [sys.dm_exec_compute_nodes (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) 监视组中的节点。  
  
5.  可选。 使用 [sp_polybase_leave_group (Transact-SQL)](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md) 从 删除计算节点。  
  
## <a name="example-walk-through"></a>示例演练  
 它将演示使用以下内容配置 PolyBase 组的步骤：  
  
1.  域 *PQTH4A* 中的两台计算机，计算机名称为：  
  
    -   PQTH4A-CMP01  
  
    -   PQTH4A-CMP02  
  
2.  域帐户：PQTH4A\PolybaseUser  
  
#### <a name="step-1-install-sql-server-with-polybase-on-all-machines"></a>第 1 步：在所有机器上安装具有 PolyBase 的 SQL Server  
  
1.  运行 setup.exe。  
  
2.  在“功能选择”页中，选择“针对外部数据的 PolyBase 查询服务” 。  
  
3.  在“服务器配置”页上，对 SQL Server PolyBase 引擎和 SQL Server PolyBase 数据移动服务使用**域账户** PQTH4A\PolybaseUser。  
  
4.  在“PolyBase 配置”页中，选择“将 SQL Server 实例用作 PolyBase 横向扩展组的一部分”选项。 这将打开防火墙以允许 PolyBase 服务的传入连接。  
  
5.  安装完成后，运行“services.msc” 。 验证 SQL Server、PolyBase 引擎和 PolyBase 数据移动服务是否在运行。  
  
     ![PolyBase 服务](../../relational-databases/polybase/media/polybase-services.png "PolyBase 服务")  
  
#### <a name="step-2-select-one-sql-server-as-head-node"></a>第 2 步：选择一个 SQL Server 作为头节点  
  
-   安装完成后，两台计算机都可充当 PolyBase 组头节点。 在此示例中，我们将选择 PQTH4A-CMP01 上的“MSSQLSERVER”作为头节点。  
  
#### <a name="step-3-add-other-sql-server-instances-as-compute-nodes"></a>第 3 步：将其他 SQL Server 实例添加为计算节点  
  
1.  连接到 PQTH4A-CMP02 上的 SQL Server。  
  
2.  运行存储过程 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)。  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
3.  在计算节点 (PQTH4A-CMP02) 上运行 services.msc。  
  
4.  关闭 PolyBase 引擎并重启 PolyBase 数据移动服务。  
  
#### <a name="optional-remove-a-compute-node"></a>可选：删除计算节点  
  
1.  连接到计算节点 SQL Server (PQTH4A-CMP02)。  
  
2.  运行存储过程 sp_polybase_leave_group。  
  
    ```  
    EXEC sp_polybase_leave_group;  
    ```  
  
3.  在正在删除的计算节点 (PQTH4A-CMP02) 上运行 services.msc。  
  
4.  启动 PolyBase 引擎。 重启 PolyBase 数据移动服务。  
  
5.  验证是否已通过运行 DMV sys.dm_exec_compute_nodes on PQTH4A-CMP01 删除该节点。 现在，PQTH4A-CMP02 将充当独立头节点  
  
## <a name="next-steps"></a>后续步骤  
 有关故障排除，请参阅 [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)。  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)   
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)  
  
  
