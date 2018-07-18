---
title: 审核转换 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittrans.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4cbe349fb83fea587874271c340853f8f38d2197
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176124"
---
# <a name="audit-transformation"></a>审核转换
  通过进行审核转换，包中的数据流可以包含有关运行包的环境的数据。 例如，包、计算机和操作员的名称可添加到数据流中。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中包含了提供这些信息的系统变量。  
  
## <a name="system-variables"></a>系统变量  
 下表介绍了审核转换可以使用的系统变量。  
  
|系统变量|索引|Description|  
|---------------------|-----------|-----------------|  
|`ExecutionInstanceGUID`|0|标识包的执行实例的 GUID。|  
|`PackageID`|@shouldalert|包的唯一标识符。|  
|`PackageName`|2|包名称。|  
|`VersionID`|3|包的版本。|  
|`ExecutionStartTime`|4|包开始运行的时间。|  
|`MachineName`|5|计算机名称。|  
|`UserName`|6|启动包的人员的登录名。|  
|`TaskName`|7|与审核转换相关联的数据流任务的名称。|  
|**TaskId**|8|数据流任务的唯一标识符。|  
  
## <a name="configuration-of-the-audit-transformation"></a>审核转换的配置  
 您可以通过提供要添加到转换输出的新输出列的名称，然后将系统变量映射到该输出列，来配置审核转换。 可以将单个系统变量映射到多个列。  
  
 此转换有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“审核转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Audit Transformation Editor](../../audit-transformation-editor.md)。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../../common-properties.md)  
  
-   [转换自定义属性](transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
