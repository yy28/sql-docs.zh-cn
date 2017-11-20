---
title: "支持在自定义组件的多目标 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: dc111f1d884a3553156b55ab490afef2f8df9d61
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="support-multi-targeting-in-your-custom-components"></a>支持在自定义组件的多目标
 你现在可以使用 SSIS 设计器在 SQL Server Data Tools (SSDT) 来创建、 维护和运行包，该目标 SQL Server 2016、 SQL Server 2014 或 SQL Server 2012。 若要获取 Visual Studio 2015 的 SSDT，请参阅[下载最新 SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md)。 

 在解决方案资源管理器中，右键单击 Integration Services 项目并选择“属性”  以打开该项目的属性页。 在“配置属性”  的“常规” 选项卡上，选择“TargetServerVersion”  属性，然后选择 SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
   
 ![在项目属性对话框中的 TargetServerVersion 属性](../../integration-services/media/targetserverversion2.png "TargetServerVersion 属性在项目属性对话框中")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>多个版本支持和多目标的自定义组件
 
所有五种类型的 SSIS 自定义扩展插件支持多目标。
-   连接管理器
-   “任务”
-   枚举器
-   日志提供程序
-   数据流组件

对于托管扩展，SSIS 设计器加载指定的目标版本的扩展版本。 例如：
-   当目标版本 SQL Server 2012 时，设计器加载该扩展的 2012年版本。
-   当目标版本 SQL Server 2016 时，设计器加载该扩展的 2016年版本。

COM 扩展不支持多目标。 SSIS 设计器始终加载 SQL Server，无论何种指定的目标版本的当前版本的 COM 扩展。

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>添加对多个版本和多目标的基本支持

基本指南，请参阅[获取 SSIS 自定义扩展以支持的 SQL Server 2016 SSDT 2015 的多版本支持](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)。 此博客文章介绍了以下步骤或要求。

-   将你的程序集部署到相应的文件夹。

-   为 SQL Server 2014 和高版本创建扩展映射文件。

## <a name="add-code-to-switch-versions"></a>添加代码以切换版本

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>切换在自定义连接管理器、 任务、 枚举器或日志提供程序的版本

对于自定义连接管理器、 任务、 枚举器或日志提供程序，将添加在降级逻辑**SaveToXML**方法。

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

### <a name="switch-versions-in-a-custom-data-flow-component"></a>自定义数据流组件中的交换机版本

对于自定义连接管理器、 任务、 枚举器或日志提供程序，在新添加降级逻辑**PerformDowngrade**方法。

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

**错误消息。** 找不到类型的对象强制转换 COM 接口的 System.__ComObject 键入 Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100。 此操作失败，因为具有 IID {BE8C48A3-155B-4810-BA5C-BDF68A659E9E} 的接口的 COM 组件的 QueryInterface 调用失败由于以下错误： 不支持此接口 (异常来自 HRESULT: 0x80004002 (E_NOINTERFACE))。 (Microsoft.SqlServer.DTSPipelineWrap)。

**解决方案。** 如果你自定义的扩展引用 SSIS 如 Microsoft.SqlServer.DTSPipelineWrap 或 Microsoft.SqlServer.DTSRuntimeWrap 的互操作程序集，将的值设置**嵌入互操作类型**属性设置为 * * False"。

![嵌入互操作类型](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>无法加载某些类型，如果目标版本，则 SQL Server 2012

此问题会影响某些类型如 IErrorReportingService 或 IUserPromptService。

**错误消息 （例如）。** 无法从程序集加载类型 Microsoft.DataWarehouse.Design.IErrorReportingService Microsoft.DataWarehouse，Version = 13.0.0.0，区域性 = neutral，PublicKeyToken = 89845dcd8080cc91。

**解决方法。** SQL Server 2012 的目标版本时，请使用一个消息框而不是这些接口。


