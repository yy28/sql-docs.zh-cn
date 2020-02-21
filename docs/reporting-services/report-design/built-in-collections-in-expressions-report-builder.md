---
title: 表达式中的内置集合（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 684f8dd2b74597b96018449492abe3786e0acba0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581789"
---
# <a name="built-in-collections-in-expressions-report-builder"></a>表达式中的内置集合（报表生成器）
  在报表的表达式中，可以添加对下列内置集合的引用：ReportItems、Parameters、Fields、DataSets、DataSources、Variables，以及适用于全局信息（如报表名称）的内置字段。 并非所有集合都显示在 **“表达式”** 对话框中。 DataSets 和 DataSources 集合只有在运行时报表将发布到报表服务器之后才可用。 ReportItems 集合是报表区域中的文本框集合，例如页面或页眉中的文本框。  
  
 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Collections"></a> 了解内置集合  
 下表列出了在您撰写表达式时可用的内置集合。 无论是否能够使用“表达式”对话框以交互方式添加对集合、示例和包含可用的初始化集合值的说明的引用，每行都包括集合的区分大小写编程名称。  
  
|内置集合|“表达式”对话框中的类别|示例|说明|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|**全局**|内置字段|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|表示对报表有用的全集变量，如报表名称或页码。 始终可用。<br /><br /> 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。|  
|**用户**|内置字段|`=User.UserID`<br /><br /> - 或 -<br /><br /> `=User.Language`|表示与运行报表的用户有关的数据的集合，如语言设置或用户 ID。 始终可用。<br /><br /> 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。|  
|**参数**|parameters|`=Parameters("ReportMonth").Value`<br /><br /> - 或 -<br /><br /> `=Parameters!ReportYear.Value`|表示报表参数的集合，每个参数都可为单值或多值参数。 直到处理初始化完成之后才可用。 有关详细信息，请参阅[集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)。|  
|**Fields(** *\<Dataset>* **)**|字段|`=Fields!Sales.Value`|表示可用于报表的数据集的字段集合。 将数据从数据源检索到数据集中之后可用。 有关详细信息，请参阅[数据集字段集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)。|  
|**DataSet**|不显示|`=DataSets("TopEmployees").CommandText`|表示从报表定义的主体中引用的数据集的集合。 不包括仅在页眉或页脚中使用的数据源。 无法在本地预览中使用。 有关详细信息，请参阅 [DataSources 和 DataSets 集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md)。|  
|**DataSources**|不显示|`=DataSources("AdventureWorks2012").Type`|表示从报表的主体中引用的数据源集合。 不包括仅在页眉或页脚中使用的数据源。 无法在本地预览中使用。 有关详细信息，请参阅 [DataSources 和 DataSets 集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md)。|  
|**变量**|`Variables`|`=Variables!CustomTimeStamp.Value`|表示报表变量和组变量的集合。 有关详细信息，请参阅[报表和组变量集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)。|  
|**ReportItems**|不显示|`=ReportItems("Textbox1").Value`|表示报表项中的文本框集合。 此集合可以用于汇总页面中的项，包括页眉或页脚。 有关详细信息，请参阅 [ReportItems 集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-reportitems-collection-references-report-builder.md)。|  
  
##  <a name="Syntax"></a> 在表达式中使用集合语法  
 若要从表达式中引用某个集合，可将标准的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 语法用于集合中的项。 下表显示集合语法的示例。  
  
|语法|示例|  
|------------|-------------|  
|*Collection!ObjectName.Property*|`=Fields!Sales.Value`|  
|*Collection!ObjectName("Property")*|`=Fields!Sales("Value")`|  
|*Collection("ObjectName").Property*|`=Fields("Sales").Value`|  
|*Collection("Member")*|`=User("Language")`|  
|*Collection.Member*|`=User.Language`|  
  
## <a name="see-also"></a>另请参阅  
 [添加表达式（报表生成器和 SSRS）](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
