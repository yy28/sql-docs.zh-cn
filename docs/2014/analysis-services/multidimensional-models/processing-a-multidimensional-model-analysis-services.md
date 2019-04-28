---
title: 多维模型对象处理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- online mode [Analysis Services]
- processing objects [Analysis Services]
- partitions [Analysis Services], processing
- jobs [Analysis Services]
- objects [Analysis Services], processing
- reprocessing objects
- impact analysis [Analysis Services]
- dimensions [Analysis Services], processing
- project mode [Analysis Services]
- cubes [Analysis Services], processing
ms.assetid: 625aa5a6-aa09-4bac-be8a-778fa81c5a61
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3877278e26b6373c9121ad6b5c7e8249b73dc166
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62736914"
---
# <a name="multidimensional-model-object-processing"></a>多维模型对象处理
  处理是 Analysis Services 将数据从关系数据源加载到多维模型的一个步骤或一系列步骤。 对于使用 MOLAP 存储的对象，数据将保存到磁盘的数据库文件所在文件夹中。 对于 ROLAP 存储，按需执行处理，以响应对象的 MDX 查询。 对于使用 ROLAP 存储的对象，处理是指在返回查询结果之前更新缓存。  
  
 默认情况下，当您将解决方案部署到服务器时进行处理。 您还可以处理解决方案的全部或一部分，无论是使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]等工具进行即席处理还是使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 SQL Server 代理按计划处理。 对模型进行结构上的更改（如删除维度或更改兼容级别）时，您需要重新处理以同步模型的物理和逻辑方面。  
  
 本主题包含以下各节：  
  
 [先决条件](#bkmk_prereq)  
  
 [选择工具或方法](#bkmk_tool)  
  
 [处理对象](#bkmk_proc)  
  
 [Reprocessing Objects](#bkmk_reproc)  
  
##  <a name="bkmk_prereq"></a> 先决条件  
  
-   处理需要对 Analysis Services 实例的管理权限。 如果正在从 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]以交互方式进行处理，您必须是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上服务器管理员角色的成员。 对于以无人参与方式运行的处理，例如使用通过 SQL Server 代理计划运行的 SSIS 包，用于运行该包的帐户必须是服务器管理员角色的成员。 有关设置管理员权限的详细信息，请参阅[授予服务器管理员权限&#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
-   用于检索数据的帐户在数据源对象中作为模拟选项（如果使用 Windows 身份验证）或连接字符串中的用户名（如果使用数据库身份验证）指定。 该帐户必须具有对模型使用的关系数据源的读取权限。  
  
-   必须先部署项目或解决方案，然后才能处理任何对象。  
  
     最初，在模型开发的早期阶段，部署和处理一起进行。 但是，您可以设置选项来在部署解决方案后再处理模型。 有关部署的详细信息，请参阅[部署 Analysis Services 项目 (SSDT)](deploy-analysis-services-projects-ssdt.md)。  
  
##  <a name="bkmk_tool"></a> 选择工具或方法  
 您可以使用客户端应用程序（如 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]）或是作为 SQL Server 代理作业或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包运行的脚本操作，以交互方式处理对象。  
  
 根据模型是正处于开发阶段还是已投入使用，处理数据库的方式会大有不同。 一旦将模型部署到生产服务器，就必须严格控制处理，确保多维数据的完整性和可用性。 由于对象相互依存，处理通常对整个模型具有连锁影响，因为处理某个对象时也会处理或取消处理其他对象。 如果有对象未处理，针对该数据的查询将无法求解，从而破坏使用它的任何报表或应用程序。 制定用于处理生产数据库的策略时，请考虑使用已经过调试和测试的脚本或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包，以避免运算符错误或忽略的步骤。  
  
 有关详细信息，请参阅[用于处理的工具和方法 (Analysis Services)](tools-and-approaches-for-processing-analysis-services.md)。  
  
##  <a name="bkmk_proc"></a> 处理对象  
 处理会影响以下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象：度量值组、分区、维度、多维数据集、挖掘模型、挖掘结构和数据库。 如果某个对象包含一个或多个对象，处理最高级别的对象将引起对所有低级别对象的级联处理。 例如，多维数据集通常包含一个和多个度量值组（每个度量值组包含一个或多个分区）和维度。 处理多维数据集会引起处理该多维数据集中的所有度量值组和当前处于未处理状态的组成维度。 有关处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的详细信息，请参阅 [处理 Analysis Services 对象](processing-analysis-services-objects.md)。  
  
 处理作业运行时，可以访问受影响的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象以进行查询。 在事务中运行处理作业，并且可以提交或回滚该事务。 如果处理作业失败，则将回滚事务。 如果处理作业成功，则提交更改时会在该对象上放置一个排他锁，表示该对象暂时不可用于查询或处理。 在事务提交阶段，仍然可以向对象发送查询，但查询将进行排队，等待完成提交。  
  
 处理作业时，是否处理对象以及如何处理对象都取决于为该对象设置的处理选项。 有关可应用于每个对象的特定处理选项的详细信息，请参阅[处理选项和设置 (Analysis Services)](processing-options-and-settings-analysis-services.md)。  
  
##  <a name="bkmk_reproc"></a> Reprocessing Objects  
 必须先重新处理包含未处理元素的多维数据集，然后才能浏览。 必须先处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中包含度量值组和分区的多维数据集，然后才能查询该多维数据集。 如果多维数据集的组成维度处于未处理状态，则处理多维数据集会引起 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 处理这些组成维度。 对象经首次处理后，出现下列情况之一时，必须部分或全部重新处理：  
  
-   该对象的结构会改变，例如在事实数据表中删除列。  
  
-   对象的聚合设计发生变化。  
  
-   对象中的数据需要更新。  
  
 处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的对象时，可以选择处理选项，也可以由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 确定处理的适当类型。 可用的处理方法随对象的类型不同而有差异。 此外，可用的方法取决于对象在上一次处理后又发生了什么变化。 如果允许 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自动选择处理方法，则将使用以最少时间将对象返回已完全处理状态的方法。 有关详细信息，请参阅[处理选项和设置 (Analysis Services)](processing-options-and-settings-analysis-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [逻辑体系结构（Analysis Services - 多维数据）](olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象（Analysis Services - 多维数据）](olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
