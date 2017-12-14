---
title: SQL Server Integration Services (SSIS) Scale Out | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0277d312ce4dab14e7ba64529e3eb2251a0d2d02
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-scale-out"></a>Integration Services (SSIS) Scale Out
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 通过将执行分布到多台计算机，提供高性能包执行。 可在 SQL Server Management Studio 中提交多个包执行的请求。 这些包将以 Scale Out 模式并行执行。  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out 包括一个 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out Master 和一个或多个 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out Worker。 Scale Out Master 负责 Scale Out 管理和接收来自用户的包执行请求。 Scale Out Worker 从 Scale Out Master 拉取执行任务，并完成包执行工作。 有关详细信息，请参阅 [Scale Out Master](integration-services-ssis-scale-out-master.md)、[Scale Out Worker](integration-services-ssis-scale-out-worker.md)。

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可在一台计算机上配置 Scale Out，其中 Scale Out Master 和 Scale Out Worker 在计算机上并行设置。 Scale Out 还可在多台计算机上运行，其中每个 Scale Out Worker 位于不同计算机上。
- [演练：设置 Integration Services Scale Out](walkthrough-set-up-integration-services-scale-out.md)

Scale Out 支持在 SSISDB 目录中并行运行多个包。 有关详细信息，请参阅[在 Scale Out 中运行包](run-packages-in-integration-services-ssis-scale-out.md)。
