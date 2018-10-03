---
title: 审核转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce5a320baf91ddf028e93ea9560cc9f8c5add5cd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770632"
---
# <a name="audit-transformation"></a>审核转换
  通过进行审核转换，包中的数据流可以包含有关运行包的环境的数据。 例如，包、计算机和操作员的名称可添加到数据流中。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中包含了提供这些信息的系统变量。  
  
## <a name="system-variables"></a>系统变量  
 下表介绍了审核转换可以使用的系统变量。  
  
|系统变量|索引|描述|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|标识包的执行实例的 GUID。|  
|**PackageID**|1|包的唯一标识符。|  
|**PackageName**|2|包名称。|  
|**VersionID**|3|包的版本。|  
|**ExecutionStartTime**|4|包开始运行的时间。|  
|**MachineName**|5|计算机名称。|  
|**UserName**|6|启动包的人员的登录名。|  
|**TaskName**|7|与审核转换相关联的数据流任务的名称。|  
|**TaskId**|8|数据流任务的唯一标识符。|  
  
## <a name="configuration-of-the-audit-transformation"></a>审核转换的配置  
 您可以通过提供要添加到转换输出的新输出列的名称，然后将系统变量映射到该输出列，来配置审核转换。 可以将单个系统变量映射到多个列。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="audit-transformation-editor"></a>审核转换编辑器
  通过进行审核转换，包中的数据流可以包含有关运行包的环境的数据。 例如，包、计算机和操作员的名称可添加到数据流中。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中包含了提供这些信息的系统变量。  
  
### <a name="options"></a>选项  
 **输出列的名称**  
 为包含审核信息的新输出列提供名称。  
  
 **审核类型**  
 选择用于提供审核信息的可用系统变量。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**执行实例 GUID**|插入唯一标识包的执行实例的 GUID。|  
|**包 ID**|插入唯一标识包的 GUID。|  
|**包名称**|插入包名称。|  
|**版本 ID**|插入唯一标识包版本的 GUID。|  
|**执行开始时间**|插入包执行的开始时间。|  
|**计算机名称**|插入启动包的计算机的名称。|  
|**User name**|插入启动包的用户的登录名。|  
|**任务名称**|插入与审核转换相关联的数据流任务的名称。|  
|**任务 ID**|插入唯一标识与审核转换相关联的数据流任务的 GUID。|  
  
  
