---
title: 第 4 课：使用 SSIS 添加错误流重定向 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c0117f867363a9536887ff1b67e1960170317d8d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295938"
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>第 4 课：使用 SSIS 添加错误流重定向

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



为了处理在转换过程中可能发生的错误，[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 允许根据每个组件和每个列来决定如何处理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 无法转换的数据。 可以选择忽略“某些列中的失败”、“重定向整个失败的行”或“使组件失败”。 默认情况下，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中的组件配置为在发生错误时失败。 失败的组件反过来导致包失败，并使处理停止。  
  
可以配置和处理可能发生的处理错误，而不是让失败阻止包执行。 一种选择是完全忽略失败，以便包始终成功运行。 还可以将失败的行重定向到另一个处理路径，可在其中保留、检查或重新处理数据和错误。  
  
本课将创建在[第 3 课：使用 SSIS 添加日志记录](../integration-services/lesson-3-add-logging-with-ssis.md)中开发的包的副本。 使用此新包时，会创建一个示例数据文件的损坏版本。 运行包时，损坏的文件会导致出现处理错误。  
  
要处理错误数据，请添加和配置将任何失败的行写入错误文件的平面文件目标。 
  
在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将错误数据写入文件之前，需包括用于获取错误说明的脚本组件。 然后，重新配置 Lookup Currency Key 转换，以便将所有无法处理的数据重定向到脚本转换中。  
  
## <a name="prerequisites"></a>先决条件

> [!NOTE]
> 如果尚不具备必备条件，请参阅[第 1 课必备条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。
 
## <a name="lesson-task"></a>课程任务
本课程包含以下任务：  
  
-   [步骤 1：复制第 3 课包](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [步骤 2：创建损坏的文件](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [步骤 3：添加错误流重定向](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [步骤 4：添加平面文件目标](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [步骤 5：测试第 4 课教程包](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
[步骤 1：复制第 3 课包](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
