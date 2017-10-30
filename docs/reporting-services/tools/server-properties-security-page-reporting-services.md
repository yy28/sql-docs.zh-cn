---
title: "服务器属性（“安全性”页）- Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8da36c90d2eb22600ad6560a37367e68de933971
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="server-properties-security-page---reporting-services"></a>服务器属性（“安全性”页）- Reporting Services
  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的此 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 页可以关闭有可能会危及报表服务器安全的功能。 关闭这些功能将限制某个功能，但是可以通过缓解特定的威胁来改进报表服务器的总体安全性。  
  
 若要打开此页，请执行以下操作：
 1) 启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 2) 连接到报表服务器实例。
 3) 右键单击报表服务器名称，然后选择“属性”。 
 4) 单击 **“安全性”** 将此页打开。  
  
## <a name="options"></a>选项  
 **对报表数据源启用 Windows 集成安全性**  
 指定是否可以使用请求报表的用户的 Windows 安全令牌与报表数据源建立连接。  
  
 如果关闭此功能，报表数据源属性页中的 Windows 集成安全性功能将不可用。 如果为数据源配置了 Windows 集成安全性，随后又关闭了此功能，报表服务器将立即更新所有的数据源连接属性以提示输入凭据。  
  
 **启用特别报告**  
 指定用户是否可以从报表生成器报表执行即席查询，当用户单击相关数据时，会自动在报表生成器报表中生成新报表。  
  
 设置此选项将确定报表服务器的 **EnableLoadReportDefinition** 属性是设置为 **True** 还是 **False**。 如果清除此选项，则该属性将设置为 **False** ，报表服务器将不会生成在数据浏览过程中创建的点击链接型报表。 将阻止对 **LoadReportDefinition** 方法的所有调用。  
  
 如果关闭此选项，则会缓解恶意用户通过用 **LoadReportDefinition** 请求使报表服务器重载来启动拒绝服务攻击的威胁。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表服务器属性 &#40;Management Studio &#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [连接到在 Management Studio 中的报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [指定凭据和报表数据源的连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Management Studio F1 帮助中的报表服务器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  

