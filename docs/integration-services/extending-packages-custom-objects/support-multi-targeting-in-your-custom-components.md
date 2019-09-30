---
title: 支持自定义组件中的多目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 91524408998df8be0df4ee5d4ede0b641dbaa2a4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71287229"
---
# <a name="support-multi-targeting-in-your-custom-components"></a>支持自定义组件中的多目标

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 现在可以在 SQL Server Data Tools (SSDT) 中使用 SSIS 设计器来创建、维护和运行面向 SQL Server 2016、SQL Server 2014 或 SQL Server 2012 的包。 若要获取用于 Visual Studio 2015 的 SSDT，请参阅[下载最新的 SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md)。 

 在解决方案资源管理器中，右键单击 Integration Services 项目并选择“属性”  以打开该项目的属性页。 在“配置属性”  的“常规”  选项卡上，选择“TargetServerVersion”  属性，然后选择 SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
   
 ![项目属性对话框中的 TargetServerVersion 属性](../../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>自定义组件的多版本支持和多目标
 
五种 SSIS 自定义扩展都支持多目标。
-   连接管理器
-   “任务”
-   枚举器
-   日志提供程序
-   数据流组件

对于托管扩展，SSIS 设计器会为指定的目标版本加载扩展版本。 例如：
-   如果目标版本为 SQL Server 2012，设计器会加载扩展的 2012 版本。
-   如果目标版本为 SQL Server 2016，设计器则加载扩展的 2016 版本。

COM 扩展不支持多目标。 无论指定的目标版本是什么，SSIS 设计器始终为当前版本的 SQL Server 加载 COM 扩展。

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>添加对多版本和多目标的基本支持

有关基本指南，请参阅 [Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)（让 SSIS 自定义扩展获得用于 SQL Server 2016 的 SSDT 2015 多版本支持的支持）。 此博客文章介绍了以下步骤或要求。

-   将程序集部署到相应的文件夹。

-   为 SQL Server 2014 和较高版本创建扩展映射文件。

## <a name="add-code-to-switch-versions"></a>添加代码以切换版本

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>在自定义连接管理器、任务、枚举器或日志提供程序中切换版本

对于自定义连接管理器、任务、枚举器或日志提供程序，在 **SaveToXML** 方法中添加降级逻辑。

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>在自定义数据流组件中切换版本

对于自定义连接管理器、任务、枚举器或日志提供程序，在新的 **PerformDowngrade** 方法中添加降级逻辑。

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>常见错误

### <a name="invalidcastexception"></a>InvalidCastException

**错误消息。** 无法将类型为 "System.__ComObject" 的 COM 对象强制转换为接口类型 "Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100"。 此操作失败的原因是对 IID 为“{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}”的接口的 COM 组件调用 QueryInterface 因以下错误而失败：不支持此类接口(异常来自 HRESULT:0x80004002 (E_NOINTERFACE))。 (Microsoft.SqlServer.DTSPipelineWrap)。

**解决方案。** 如果自定义扩展引用 Microsoft.SqlServer.DTSPipelineWrap 或 Microsoft.SqlServer.DTSRuntimeWrap 等 SSIS 互操作程序集，将“嵌入互操作类型”  属性的值设置为“False”  。

![嵌入互操作类型](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>当目标版本为 SQL Server 2012 时无法加载某些类型

此问题会影响某些类型，比如 IErrorReportingService 或 IUserPromptService。

**错误消息（示例）。** 未能从程序集 "Microsoft.DataWarehouse, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" 中加载类型 "Microsoft.DataWarehouse.Design.IErrorReportingService"。

**解决方法。** 当目标版本为 SQL Server 2012 时，不使用这些接口，而改用 MessageBox。

