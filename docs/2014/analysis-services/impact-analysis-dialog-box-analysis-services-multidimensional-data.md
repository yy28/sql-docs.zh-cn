---
title: "\"影响分析\" 对话框（Analysis Services 多维数据） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0c08690cd2f5b77471392cab3aad1587b4cb0f9a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080744"
---
# <a name="impact-analysis-dialog-box-analysis-services---multidimensional-data"></a>“影响分析”对话框（Analysis Services - 多维数据）
  如果 **“处理”** 对话框中列出的对象已处理，则使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 **“影响分析”** 对话框来标识和处理受影响的依赖对象。 通过在 **“处理”** 对话框中单击 **“影响分析”** ，可以显示 **“影响分析”** 对话框。  
  
> [!NOTE]  
>  如果某个对象在多个方面受到影响，则该对象将显示多次。  
  
## <a name="options"></a>选项  
 **对象列表**  
 在网格中显示依赖对象的列表。 该网格包含以下列：  
  
 **Object Name**  
 显示可能需要处理的依赖对象的名称。 名称左侧的图标指示对象类型。  
  
 **类型**  
 显示可能需要处理的依赖对象的类型。  
  
 **影响类型**  
 显示处理“处理”**** 对话框中的对象对依赖对象的影响。 下表列出了处理的可能影响，并说明每种影响将导致警告还是错误：  
  
|影响|消息|  
|------------|-------------|  
|将清除对象（不处理）|警告|  
|对象将无效|错误|  
|将删除聚合|警告|  
|将删除灵活的聚合|警告|  
|将删除索引|警告|  
|将处理非子对象|警告|  
  
 **处理对象**  
 选择要使用处理操作处理的依赖对象。 必须在处理操作完成后处理未选中的依赖对象。 否则，将无法使用这些对象。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 ["处理" 对话框 &#40;Analysis Services 多维数据&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
