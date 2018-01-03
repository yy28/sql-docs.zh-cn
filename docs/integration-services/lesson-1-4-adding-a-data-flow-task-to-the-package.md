---
title: "步骤 4：将数据流任务添加到包 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d67e1dc478ce982dc65ff7f0ed86ea3447395b84
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-1-4---adding-a-data-flow-task-to-the-package"></a>第 1-4 课 - 将数据流任务添加到包
为源数据和目标数据创建了连接管理器后，下一个任务是在包中添加一个数据流任务。 数据流任务将封装在源和目标之间移动数据的数据流引擎，并提供在移动数据时转换、清除和修改数据的功能。 大部分的数据提取、转换和加载 (ETL) 进程均在数据流任务中完成。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将数据流从控制流中分隔开来。  
  
### <a name="to-add-a-data-flow-task"></a>添加一个数据流任务  
  
1.  单击 **“控制流”** 选项卡。  
  
2.  在“SSIS 工具箱”中，展开“收藏夹”，并将一个“数据流任务”拖到“控制流”选项卡的设计图面上。  
  
    > [!NOTE]  
    > 如果“SSIS 工具箱”不可用，请在主菜单中依次选择“SSIS”和“SSIS 工具箱”，以显示“SSIS 工具箱”。  
  
3.  在“控制流”  设计图面中，右键单击新添加的“数据流任务” ，再单击“重命名” ，将名称更改为 **Extract Sample Currency Data**。  
  
    好的做法是为添加到设计图面的所有组件提供唯一的名称。 考虑到易用性和可维护性，名称应说明每个组件执行的功能。 按照这些命名指南， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包可以进行自我说明。 另一个说明包的方法是使用批注。 有关批注的详细信息，请参阅[在包中使用批注](../integration-services/use-annotations-in-packages.md)。  
  
4.  右键单击“数据流”任务，再单击“属性”，然后在“属性”窗口，确保已将“LocaleID”属性设置为“英语(美国)”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[步骤 5：添加并配置平面文件源](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>另请参阅  
[数据流任务](../integration-services/control-flow/data-flow-task.md)  
  
  
  
