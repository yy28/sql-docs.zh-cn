---
title: "多维模型中的操作 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- actions [Analysis Services], creating
- report actions [Analysis Services]
- drillthrough actions [Analysis Services]
- cubes [Analysis Services], actions
ms.assetid: b9fee2b9-05a5-4077-848d-d8457326dc27
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c68c3d8eba2ec1519c38a89c7a1b0b71f3be4e3
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="actions-in-multidimensional-models"></a>多维模型中的操作
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
操作是指最终用户针对所选多维数据集或其个部分启动的操作。 操作可以通过将所选项目作为参数来启动应用程序，也可以检索有关所选项目的信息。 有关操作的详细信息，请参阅[操作（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 使用多维数据集设计器的 **“操作”** 选项卡可以为多维数据集生成操作。 指定下列各项：  
  
 **名称**  
 选择用于标识操作的名称。  
  
 **操作目标**  
 选择操作所附加到的对象。 一般情况下，在客户端应用程序中，当最终用户选中了目标对象后就会显示该操作；但是，最终用户的何种行为会导致操作的显示，取决于客户端应用程序。 对于 **“目标类型”**，请从以下对象中选择：  
  
-   属性成员  
  
-   单元  
  
-   多维数据集  
  
-   维度成员  
  
-   层次结构  
  
-   层次结构成员  
  
-   Level  
  
-   级别成员  
  
 选择目标对象类型后，请在 **“目标对象”**下面选择指定类型的多维数据集对象。  
  
 **条件(可选)**  
 指定其结果为布尔值的可选“多维表达式 (MDX)”表达式。 如果值是 **True**，则对指定目标执行操作。 如果值是 **False**，则不执行操作。  
  
 **操作内容**  
 选择操作的类型。 下表总结了可用的类型。  
  
|类型|Description|  
|----------|-----------------|  
|数据集|检索数据集。|  
|专有|使用除此表列出的这些类型以外的其他接口执行操作。|  
|行集|检索行集。|  
|。|运行 OLE DB 命令。|  
|URL|在 Internet 浏览器中显示可变页。|  
  
 对于 **“操作表达式”**，请指定运行操作时所传递的参数。 该语法的计算结果必须为字符串，并且必须包含以 MDX 编写的表达式。 例如，MDX 表达式可以指示该语法所包含的多维数据集的一部分。 MDX 表达式在传递参数之前得到取值。 MDX 生成器也可以帮助生成 MDX 表达式。  
  
 **附加属性**  
 选择属性。 下表总结了可用的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**调用**|指定如何运行操作。 “交互”（默认）指定在用户访问对象时运行操作。 可能的设置是：<br /><br /> 批处理<br /><br /> 交互<br /><br /> 处于打开状态|  
|**应用程序**|说明操作的应用程序。|  
|**Description**|说明操作。|  
|**Caption**|提供为操作显示的标题。 如果标题是 MDX，请将 **“标题是 MDX”** 指定为 **True**。|  
|**True**|如果标题是 MDX，请指定 **True** ，如果不是，则指定 **False** 。|  
  
> [!NOTE]  
>  必须使用 Analysis Services 脚本语言 (ASSL) 或分析管理对象 (AMO)，才能定义 HTML 和命令行操作类型。 有关详细信息，请参阅 [Action 元素 (ASSL)](../../analysis-services/scripting/objects/action-element-assl.md)、[Type 元素 (Action) (ASSL)](../../analysis-services/scripting/properties/type-element-action-assl.md) 和 [AMO OLAP 高级对象的编程](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)。  
  
## <a name="creating-a-reporting-action"></a>创建报表操作  
 报表服务器会对基于 URL 的报表请求作出响应。 若要创建报表操作，请在 **“多维数据集”** 菜单上单击 **“新建报表操作”**。 下面是特定于报表操作的选项。  
  
 **报表服务器**  
 下表说明的属性是为报表服务器指定的。  
  
|属性|Description|  
|--------------|-----------------|  
|**服务器名称**|运行报表服务器的计算机的名称。|  
|**服务器路径**|报表服务器所显示的路径。|  
|**报表格式**|HTML5、HTML3、Excel 或 PDF。|  
  
> [!NOTE]  
>  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，可在服务器名称属性中指定传输层安全性 (https:)。  
  
 **参数(可选)**  
 创建操作时，参数将作为 URL 字符串的一部分发送到服务器。 它们包括 **“参数名称”** 和 **“参数值”**，后者是 MDX 表达式。  
  
 报表服务器 URL 的构造如下所示：  
  
```  
  
http://  
host  
/  
virtualdirectory  
/Path&  
parametername1  
=  
parametervalue1  
& ...  
```  
  
 例如：  
  
```  
http://localhost/ReportServer/Sales/YearlySalesByCategory?rs:Command=Render&Region=West  
```  
  
## <a name="creating-a-drillthrough-action"></a>创建钻取操作  
 钻取操作由行集操作定义，它将作为钻取语句返回到客户端应用程序。 操作目标是度量值组的成员。 若要创建新的钻取操作，请在 **“多维数据集”** 菜单上单击 **“新建钻取操作”**。 下面是特定于钻取操作的选项：  
  
 **钻取列**  
 选择一个或多个维度以及每个维度的、由该操作返回到客户端应用程序的钻取列。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的多维数据集](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
