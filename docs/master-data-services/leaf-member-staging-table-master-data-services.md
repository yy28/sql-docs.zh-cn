---
title: "叶成员临时表 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "成员临时表 [Master Data Services]"
  - "数据库 [Master Data Services], 成员临时表"
ms.assetid: a8c953da-ec20-47dc-8656-ed5f0dfed89b
caps.latest.revision: 14
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# 叶成员临时表 (Master Data Services)
  使用临时表 (stg.name_Leaf) 中的叶成员 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库来创建、 更新、 停用和删除叶成员。 您还可以使用它更新叶成员的属性值。  
  
##  <a name="TableColumns"></a> 表列  
 下表说明 Leaf 临时表中每个字段的用途。  
  
|列名|说明|值|  
|-----------------|-----------------|------------|  
|**ID**|自动分配的标识符。|不要在此字段中输入值。 如果尚未处理此批次，则此字段为空。|  
|**ImportType**<br /><br /> 必需|确定临时数据与 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中已存在的数据匹配时执行何种操作。|**0**：创建新成员。 使用临时数据替换现有的 MDS 数据，但是仅限临时数据不为 NULL 时。 忽略 NULL 值。 若要将某个字符串属性值设置为 NULL，请将其设置为 **~NULL~**。 若要将某个数字属性值更改为 NULL，请将其设置为 **-98765432101234567890**。 若要将日期时间属性值更改为 NULL，请将其设置为 **5555-11-22T12:34:56**。<br /><br /> **1**：仅创建新成员。 对现有 MDS 数据的任何更新都将失败。<br /><br /> **2**：创建新成员。 使用临时数据替换现有的 MDS 数据。 如果导入了 NULL 值，它们将覆盖现有的 MDS 值。<br /><br /> **3**：基于 Code 值停用成员。 维护所有属性、层次结构和集合成员身份以及事务，但是在 UI 中已无法使用。 如果成员用作另一个成员的基于域的属性值，则无法停用。 请参阅 **ImportType5** 的一种替代方法。<br /><br /> **4**：基于 Code 值永久删除成员。 永久删除所有属性、层次结构和集合成员身份以及事务。 如果成员用作另一个成员的基于域的属性值，则无法删除。 请参阅 **ImportType6** 的一种替代方法。<br /><br /> **5**：基于 **Code** 值停用成员。 维护所有属性、层次结构和集合成员身份以及事务，但是在 UI 中已无法使用。 如果成员用作其他成员的基于域的属性值，则相关值将设置为 NULL。 ImportType 5 仅用于叶成员。<br /><br /> **6**：基于 **Code** 值永久删除成员。 永久删除所有属性、层次结构和集合成员身份以及事务。 如果成员用作其他成员的基于域的属性值，则相关值将设置为 NULL。 ImportType 6 仅用于叶成员。|  
|**ImportStatus_ID**<br /><br /> 必需|导入过程的状态。|**0**- 指定此值表示记录已经准备好临时存储。<br /><br /> **1**- 自动分配的值，表示记录的暂存过程已成功。<br /><br /> **2**- 自动分配的值，表示记录的临时过程已失败。|  
|**Batch_ID**<br /><br /> 仅对 Web 服务为必需的|自动分配的标识符，该标识符将记录分组以便临时存储。 将为此批次中的所有成员分配此标识符，此标识符显示在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 用户界面中的 **ID** 列。|如果尚未处理此批次，则此字段为空。|  
|**BatchTag**<br /><br /> 必需，但是 Web 服务除外|批次的唯一名称，最多包含 50 个字符。||  
|**ErrorCode**|显示错误代码。 有关包含的所有记录 **ImportStatus_ID** 的 **2**, ，请参阅 [临时过程错误 & #40;Master Data Services & #41;](../master-data-services/staging-process-errors-master-data-services.md)。||  
|**代码**<br /><br /> 必需的除生成代码时自动为 **ImportType1** 或 **2**; 请参阅 [自动创建代码 & #40;Master Data Services & #41;](../master-data-services/automatic-code-creation-master-data-services.md) 有关详细信息|成员的唯一代码。||  
|**名称**<br /><br /> 可选|成员的名称。||  
|**NewCode**|仅当要更改成员代码时才使用。||  
|\< 属性名称>|实体中的每个属性对应的列。 对于 **ImportType** 为 **0** 或 **2**时使用它。 对于自由格式属性，请为该属性指定新的文本或字符串值。 对于基于域的属性，请为将要成为属性的成员指定代码。 对于链接属性，该 URL 必须以开头 **http://**。<br /><br /> 注意：不能暂存文件属性。||  
  
## 另请参阅  
 [概述︰ 从表和 #40; 导入数据Master Data Services & #41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [查看在临时 & #40; 过程中发生的错误Master Data Services & #41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [临时过程错误 & #40;Master Data Services & #41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  