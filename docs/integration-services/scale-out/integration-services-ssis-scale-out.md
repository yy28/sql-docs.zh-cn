---
title: "SQL Server Integration Services (SSIS) 横向扩展 |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ce7fb96901e8af4da74392fe0a0a85c6e2ec05a4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out"></a>Integration Services (SSIS) Scale Out
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 通过将执行分布到多台计算机，提供高性能包执行。 你可以提交在 SQL Server Management Studio 中的多个包执行的请求。 这些包将以 Scale Out 模式并行执行。  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]向外扩展组成[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]缩放出 Master 和一个或多个[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]横向扩展辅助进程。 Scale Out Master 负责 Scale Out 管理和接收来自用户的包执行请求。 Scale Out Worker 从 Scale Out Master 拉取执行任务，并完成包执行工作。 有关详细信息，请参阅 [Scale Out Master](integration-services-ssis-scale-out-master.md)、[Scale Out Worker](integration-services-ssis-scale-out-worker.md)。

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]向外扩展可以配置在一台计算机，一个出母版横向和横向扩展辅助进程设置好计算机上并行。 Scale Out 还可在多台计算机上运行，其中每个 Scale Out Worker 位于不同计算机上。
- [演练：设置 Integration Services Scale Out](walkthrough-set-up-integration-services-scale-out.md)

Scale Out 支持在 SSISDB 目录中并行运行多个包。 有关详细信息，请参阅[在 Scale Out 中运行包](run-packages-in-integration-services-ssis-scale-out.md)。

