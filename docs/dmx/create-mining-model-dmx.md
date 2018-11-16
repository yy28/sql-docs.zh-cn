---
title: 创建挖掘模型 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2ea71a918ab9ceb1afba41e5af0148212f33044b
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607137"
---
# <a name="create-mining-model-dmx"></a>CREATE MINING MODEL (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在数据库中同时创建新的挖掘模型和挖掘结构。 通过在语句中定义新模型，或者通过使用预测模型标记语言 (PMML)，均可以创建模型。 第二种选择只适用于高级用户。  
  
 挖掘结构的命名方式是在模型名称后追加 "_structure"，这样可以确保将结构名称与模型名称进行区分。  
  
 若要创建现有挖掘结构的挖掘模型，请使用[ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md)语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE [SESSION] MINING MODEL <model>  
(  
    [(<column definition list>)]  
)  
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH]  
CREATE MINING MODEL <model> FROM PMML <xml string>  
```  
  
## <a name="arguments"></a>参数  
 *model*  
 模型的唯一名称。  
  
 *列定义列表*  
 列定义的逗号分隔列表。  
  
 *算法*  
 当前提供程序定义的数据挖掘算法的名称。  
  
> [!NOTE]  
>  可以通过检索当前提供程序支持的算法的列表[DMSCHEMA_MINING_SERVICES 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)。 若要查看支持的当前实例中的算法[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，请参阅[数据挖掘属性](../analysis-services/server-properties/data-mining-properties.md)。  
  
 *参数列表*  
 可选。 由提供程序定义的算法所需参数的逗号分隔列表。  
  
 *XML 字符串*  
 （仅适用于高级用户。）XML 编码的模型 (PMML)。 字符串必须以单引号 (') 引起。  
  
 **会话**子句允许您创建在连接关闭或会话超时时时自动删除从服务器的挖掘模型。**会话**挖掘模型非常有用，因为它们不需要用户以数据库管理员，并且它们仅使用的磁盘空间，只要连接处于打开状态。  
  
 **WITH DRILLTHROUGH**子句可以对新的挖掘模型的钻取。 只有在创建模型时，才能启用钻取功能。 对于某些模型类型，在自定义查看器中浏览模型时需要进行钻取。 对于预测或使用 Microsoft 一般内容树查看器浏览，钻取则不是必需的。  
  
 **CREATE MINING MODEL**语句创建新的挖掘模型基于列定义列表、 算法和算法参数列表。  
  
### <a name="column-definition-list"></a>列定义列表  
 通过包含各列的以下信息，可以使用列定义列表定义模型的结构：  
  
-   名称（必选）  
  
-   日期类型（必需）  
  
-   Distribution  
  
-   建模标志列表  
  
-   内容类型（必需）  
  
-   预测请求，用于指示算法对该列进行预测，为由**PREDICT**或**PREDICT_ONLY**子句  
  
-   与属性列 （强制仅在适用） 的关系由**RELATED TO**子句  
  
 使用以下列定义列表的语法，定义单个列：  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 使用以下列定义列表的语法，定义嵌套表列：  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 除了建模标志外，只能使用特定组的一个子句来定义列。 可以为一个列定义多个建模标志。  
  
 有关可用于定义列的一组数据类型、内容类型、列分布和建模标志，请参阅下列主题：  
  
-   [数据类型（数据挖掘）](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [内容类型（数据挖掘）](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [列分布（数据挖掘）](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [建模标志（数据挖掘）](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 您可以向语句中添加子句，说明两个列之间的关系。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持以下使用\<列关系 > 子句。  
  
 **与相关**  
 此窗体指示值的层次结构。 RELATED TO 列的目标可以是嵌套表的键列、事例行中具有离散值的列或另一个包含 RELATED TO 子句并指示更深层次结构的列。  
  
 使用预测子句可以说明使用预测列的方式。 下表列出了两种可以使用的子句。  
  
|\<预测 > 子句|Description|  
|---------------------------|-----------------|  
|**PREDICT**|该列可以由模型预测，并且可以在输入事例中提供，以预测其他可预测列的值。|  
|**PREDICT_ONLY**|此列可以由模型预测，但其值不可用于输入事例来预测其他可预测列的值。|  
  
### <a name="parameter-definition-list"></a>参数定义列表  
 可以使用参数列表调整挖掘模型的性能和功能。 参数列表语法如下：  
  
```  
[<parameter> = <value>, <parameter> = <value>,…]  
```  
  
 有关与每种算法关联的参数的列表，请参阅[数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
## <a name="remarks"></a>备注  
 如果要创建具有内置测试数据集的模型，则应当使用 CREATE MINING STRUCTURE 语句，然后再使用 ALTER MINING STRUCTURE 语句。 但是，并非所有挖掘模型类型都支持维持数据集。 有关详细信息，请参阅 [CREATE MINING STRUCTURE (DMX)](../dmx/create-mining-structure-dmx.md)。  
  
 有关如何使用 CREATEMODEL 语句创建挖掘模型的演练，请参阅[时序预测 DMX 教程](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2)。  
  
## <a name="naive-bayes-example"></a>Naive Bayes 示例  
 以下示例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 算法创建新的挖掘模型。 Bike Buyer 列定义为可预测属性。  
  
```  
CREATE MINING MODEL [NBSample]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE PREDICT  
)  
USING Microsoft_Naive_Bayes  
```  
  
## <a name="association-model-example"></a>关联模型示例  
 以下示例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 关联算法创建新的挖掘模型。 该语句通过使用表列，充分利用了在模型定义中嵌套表的能力。 通过修改模型*MINIMUM_PROBABILITY*并*MINIMUM_SUPPORT*参数。  
  
```  
CREATE MINING MODEL MyAssociationModel (  
    OrderNumber TEXT KEY,  
    [Products] TABLE PREDICT (  
        [Model] TEXT KEY  
    )  
)  
USING Microsoft_Association_Rules (Minimum_Probability = 0.1, MINIMUM_SUPPORT = 0.01)  
```  
  
## <a name="sequence-clustering-example"></a>顺序分析和聚类分析示例  
 以下示例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法创建新的挖掘模型。 将使用两个键来定义模型。 OrderNumber 列用作事例键，指定各个订单。 LineNumber 列用作嵌套表键，指定项添加到订单的顺序。  
  
```  
CREATE MINING MODEL BuyingSequence (  
    [Order Number] TEXT KEY,  
    [Products] TABLE   
     (  
        [Line Number] LONG KEY SEQUENCE,  
        [Model] TEXT DISCRETE PREDICT  
    )  
)  
USING Microsoft_Sequence_Clustering  
```  
  
## <a name="time-series-example"></a>时间序列示例  
 下面的示例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法和 ARTxp 算法创建新的挖掘模型。 ReportingDate 是时序的键列，ModelRegion 是数据序列的键列。 在此示例中，假定数据出现的频率为每 12 个月一次。 因此， *PERIODICITY_HINT*参数设置为 12。  
  
> [!NOTE]  
>  必须指定*PERIODICITY_HINT*参数使用大括号字符。 此外，由于值是一个字符串，则必须用单引号引起来:"{\<数值 >}"。  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;数据定义语句](../dmx/dmx-statements-data-definition.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
