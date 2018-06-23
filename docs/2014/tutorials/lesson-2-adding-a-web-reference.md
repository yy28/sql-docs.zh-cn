---
title: 第 2 课： 添加 Web 引用 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a2c2b8b8-6b13-45ca-ab3b-1582447b6807
caps.latest.revision: 29
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ff574cf6ab00b4b368a7d372957b2348757ad0f5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123522"
---
# <a name="lesson-2-adding-a-web-reference"></a>第 2 课：添加 Web 引用
  Web 服务发现是客户端查找 Web 服务并获取其服务说明的过程。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的 Web 服务发现过程涉及询问网站是否遵循预定算法。 此过程的目的是查找服务说明，它是使用 Web 服务描述语言 (WSDL) 的一个 XML 文档。  
  
 服务说明介绍了哪些服务可用，以及如何与这些服务进行交互。 没有服务说明，就不可能通过编程方式与 Web 服务进行交互。  
  
 您的应用程序必须能够通过某种方式与 Web 服务通信并在运行时找到该服务。 添加对 Web 服务项目的 Web 引用可以做到这点，这种方法将生成与 Web 服务连接并提供 Web 服务的本地表示形式的代理类。 有关详细信息，请参阅 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 文档中的“如何生成 XML Web 服务代理”。  
  
### <a name="to-add-a-web-reference"></a>若要添加 Web 引用  
  
1.  上**项目**菜单上，单击**添加服务引用**。  
  
2.  在**添加服务引用**对话框中，单击**高级**。  
  
3.  在**服务引用设置**对话框中，单击**添加 Web 引用**。  
  
4.  在**URL**框**添加 Web 引用**对话框框中，键入 URL，若要获取的服务说明的报表服务器 Web 服务，如http://localhost/reportserver/reportservice2010.asmx。 然后单击**转**按钮以检索 Web 服务有关的信息。  
  
     \- 或 -  
  
     如果本地计算机上是否存在该报表服务器 Web 服务，请单击**本地计算机上的 Web 服务**在浏览器窗格中的链接。 然后在提供的列表中单击 ReportService2010 Web 服务的链接。  
  
5.  在**Web 引用名称**框中，重命名 Web 参考 ReportService2010，这是你将用于此 Web 引用的命名空间。  
  
6.  单击**添加引用**添加目标 Web 服务的 Web 引用。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将下载服务说明并生成一个代理类，以在您的应用程序和报表服务器 Web 服务之间进行连接。 您还需要添加对 <xref:System.Web.Services> 命名空间的引用，Web 引用才能正常工作。  
  
7.  在项目菜单中，单击**添加引用**。  
  
8.  在**添加引用**对话框中，在 **.NET**选项卡上，选择**System.Web.Services**，然后单击**确定**。  
  
 有关详细信息，请参阅[访问 SOAP API](../reporting-services/report-server-web-service/accessing-the-soap-api.md)。  
  
## <a name="see-also"></a>请参阅  
 [报表服务器 Web 服务](../reporting-services/report-server-web-service/report-server-web-service.md)   
 [第 3 课： 访问 Web 服务](../../2014/tutorials/lesson-3-accessing-the-web-service.md)   
 [访问报表服务器 Web 服务使用 Visual Basic 或 Visual C&#35; &#40;SSRS 教程&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  