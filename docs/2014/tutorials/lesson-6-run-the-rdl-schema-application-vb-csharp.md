---
title: 第 6 课： 运行 RDL 架构应用程序 (VB-C#) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a2cd2386-2df8-4b69-ab81-9ad1a31f6d27
caps.latest.revision: 15
author: craigg-msft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a56a29edc9b30577dca3db245d3ace5e4c7814d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169788"
---
# <a name="lesson-6-run-the-rdl-schema-application-vb-c"></a>第 6 课： 运行 RDL 架构应用程序 (VB-C#)
  
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 提供了两种从集成开发环境 (IDE) 生成和运行控制台应用程序的方法：  
  
-   开始执行（调试）  
  
-   开始执行（不调试）  
  
### <a name="to-build-and-run-the-samplerdlschema-application"></a>生成并运行 SampleRDLSchema 应用程序  
  
1.  从**调试**菜单上，单击**启动但不调试**。 该操作可确保控制台窗口在程序执行完毕后保持打开状态。  
  
     应用程序将以下输出内容打印到控制台：  
  
    ```  
    Loading Report Definition  
    Updating Report Definition  
    - Old Description: <Old Report Description>  
    - New Description: <New Report Description>  
    Publishing Report Definition  
    ```  
  
2.  按任意键关闭控制台。  
  
    > [!NOTE]  
    >  发生的所有错误都将写入控制台。  
  
3.  示例应用程序完成运行时，经过更新的该报表副本将保存至报表服务器。  
  
## <a name="see-also"></a>请参阅  
 [使用从 RDL 架构生成的类更新报表&#40;SSRS 教程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [报表定义语言 (SSRS)](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
