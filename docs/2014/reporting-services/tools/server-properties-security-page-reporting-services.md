---
title: 服务器属性（“安全性”页）- Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a49f56c4e898b0189ce0f8bf5008873e13dc6223
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099559"
---
# <a name="server-properties-security-page---reporting-services"></a>服务器属性（“安全性”页）- Reporting Services
  使用此页可以关闭有可能会危及报表服务器安全的功能。 关闭这些功能将限制某个功能，但是可以通过缓解特定的威胁来改进报表服务器的总体安全性。  
  
 若要打开此页，请启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到报表服务器实例，右键单击报表服务器名称，然后选择“属性”。 单击 **“安全性”** 将此页打开。  
  
## <a name="options"></a>选项  
 **对报表数据源启用 Windows 集成安全性**  
 指定是否可以使用请求报表的用户的 Windows 安全令牌与报表数据源建立连接。  
  
 如果关闭此功能，报表数据源属性页中的 Windows 集成安全性功能将不可用。 如果为数据源配置了 Windows 集成安全性，随后又关闭了此功能，报表服务器将立即更新所有的数据源连接属性以提示输入凭据。  
  
 **启用特别报告**  
 指定用户是否可以从报表生成器报表执行即席查询，当用户单击相关数据时，会自动在报表生成器报表中生成新报表。  
  
 设置此选项将确定报表服务器的 `EnableLoadReportDefinition` 属性是设置为 `True` 还是 `False`。 如果清除此选项，则该属性将设置为 `False`，报表服务器将不会生成在数据浏览过程中创建的点击链接型报表。 将阻止对 `LoadReportDefinition` 方法的所有调用。  
  
 如果关闭此选项，则会缓解恶意用户通过用 `LoadReportDefinition` 请求使报表服务器重载来启动拒绝服务攻击的威胁。  
  
## <a name="see-also"></a>请参阅  
 [设置报表服务器属性 (Management Studio)](set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](connect-to-a-report-server-in-management-studio.md)   
 [指定凭据和报表数据源的连接信息](../report-data/specify-credential-and-connection-information-for-report-data-sources.md[报表服务器在 Management Studio 的 F1 帮助](report-server-in-management-studio-f1-help.md)  
  
  
