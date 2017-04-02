---
title: "Integration Services (SSIS) Scale Out | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Integration Services (SSIS) Scale Out
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scale Out 通过将执行分布到多台计算机，提供高性能包执行。 能够在 SQL Server Management Studio 中提交多个包执行的请求。 这些包将以 Scale Out 模式并行执行。  


## <a name="ssis-scale-out-master-and-scale-out-worker"></a>SSIS Scale Out Master 和 Scale Out Worker
[!INCLUDE[ssIS_md](../includes/ssis-md.md)] Scale Out 包括一个 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] Scale Out Master 和几个 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] Scale Out Worker。 Scale Out Master 负责 Scale Out 管理和接收来自用户的包执行请求。 Scale Out Worker 从 Scale Out Master 拉取执行任务，并完成包执行工作。 有关详细信息，请参阅 [Scale Out Master](../integration-services/integration-services-ssis-scale-out-master.md)、[Scale Out Worker](../integration-services/integration-services-ssis-scale-out-worker.md)。


## <a name="how-to-set-up-scale-out"></a>如何设置 Scale Out
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scale Out 可在一台计算机上运行，其中 Scale Out Master 和 Scale Out Worker 在计算机上并行设置。 Scale Out 还可在多台计算机上运行，其中每个 Scale Out Worker 位于不同计算机上。
- [演练：设置 Integration Services Scale Out](../integration-services/walkthrough-set-up-integration-services-scale-out.md)


## <a name="run-packages-in-scale-out"></a>在 Scale Out 中运行包
Scale Out 支持在 SSISDB 目录中并行运行多个包。 有关详细信息，请参阅[在 Scale Out 中运行包](../integration-services/run-packages-in-integration-services-ssis-scale-out.md)。

