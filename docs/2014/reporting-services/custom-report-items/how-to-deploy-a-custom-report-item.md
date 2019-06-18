---
title: 如何：部署自定义报表项 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2b41519ee6a6d31be33d92c8fbdf2ab503c93ec1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63265083"
---
# <a name="how-to-deploy-a-custom-report-item"></a>如何：部署自定义报表项
  若要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中部署自定义报表项，必须修改报表服务器配置文件，并将设计时和运行时组件程序集复制到报表设计器和报表服务器的相应应用程序文件夹中。  
  
### <a name="to-deploy-a-custom-report-item"></a>部署自定义报表项  
  
1.  编辑 Rsreportdesigner.config 文件，以配置供在相应设计器中使用的自定义报表项运行时组件和设计时组件。 请注意，`ReportItemName` 条目必须与 `CustomReportItemAttribute` 类中使用的 `CustomReportItemDesigner` 属性匹配。 例如：  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  编辑 Rsreportserver.config 文件以注册自定义报表项运行时组件。 例如：  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  编辑 Rsssrvpolicy.config 文件以添加用于为相应自定义报表项授予合适权限的 `CodeGroup`。 例如：  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  将相应自定义报表项运行时组件 DLL 复制到 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 和 \Program Files\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin 目录下。  
  
5.  将相应自定义报表项设计时组件 DLL 复制到 %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 目录下。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置文件](../report-server/reporting-services-configuration-files.md)   
 [自定义报表项类库](custom-report-item-class-libraries.md)  
  
  
