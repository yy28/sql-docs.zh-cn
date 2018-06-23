---
title: 第 2 课： 从 RDL 架构使用 xsd 工具生成的类 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
caps.latest.revision: 13
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 67cbc84882683fcb31d6b42f69274d5166556450
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137886"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>第 2 课：使用 xsd 工具从 RDL 架构生成类
  创建 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目后，下一步是检索报表定义架构的本地副本和运行 XML 架构定义工具 (Xsd.exe)。  
  
### <a name="to-generate-the-rdl-classes"></a>生成 RDL 类  
  
1.  打开的实例[!INCLUDE[msCoName](../includes/msconame-md.md)]Internet Explorer （或等效的 Web 浏览器） 并导航到以下 URL:  
  
    ```  
    http://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  RDL 架构已打开浏览器中，浏览到**文件**菜单，然后选择**另存为**。  
  
3.  浏览到您创建 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目的位置，使用文件名 ReportDefinition.xsd 保存该架构。  
  
4.  保存该文件后，打开的实例[!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]命令提示符。 若要打开命令提示符下的实例，请单击开始菜单，指向**所有程序**，指向**Microsoft Visual Studio 2010**，指向**Visual Studio Tools**单击**Visual Studio 命令提示 (2010)**。  
  
5.  将当前路径更改为 ReportDefinition.xsd 文件的保存位置：  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  用以下命令生成包含 RDL 架构的类的 ReportDefinition.cs 文件：  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     若要生成 ReportDefinition.vb 文件，请使用以下命令：  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  向您的项目添加 ReportDefinition.xsd。 从**项目**菜单上，单击**添加现有项**。 浏览到 ReportDefinition.xsd 文件的位置，选择 ReportDefinition.xsd，然后单击**添加**。  
  
    > [!NOTE]  
    >  ReportDefinition.xsd 文件添加到项目后你将中注意到**解决方案资源管理器**ReportDefinition.cs (.vb) 文件不会存在。 若要显示该文件，请单击 ReportDefinition.xsd 文件旁边的展开/折叠按钮。  
  
## <a name="next-lesson"></a>下一课  
 在下一课中，您将使用从 RDL 架构生成的类编写用于从报表服务器加载报表定义的代码。 请参阅[第 3 课： 从报表服务器加载报表定义](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [更新报表使用生成的 RDL 架构类&#40;SSRS 教程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [报表定义语言 (SSRS)](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  