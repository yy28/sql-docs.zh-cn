---
title: "自定义工作流 XML 描述 (Master Data Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ca6f208bab4ed0b7932d3bd5f7e9a911b8b2c8af
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---xml-description"></a>创建自定义的工作流的 XML 描述
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 中，当工作流启动时，<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 方法由 SQL Server MDS Workflow Integration Service 调用。 此方法将有关触发工作流业务规则的项的元数据和数据作为 XML 块接收。 有关示例代码实现工作流处理程序，请参阅[自定义工作流示例 &#40;Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 下面的示例说明发送到工作流处理程序的 XML 可能类似以下形式：  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 下表描述此 XML 所包含的一些标记：  
  
|标记|Description|  
|---------|-----------------|  
|\<类型 >|在输入的文本**工作流类型**文本框中[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]来标识要加载哪些自定义工作流程序集。|  
|\<SendData >|一个布尔值，由控制**消息中包括成员数据**中的复选框[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。 值为 1 意味着\<MemberData > 部分是发送; 否则为\<MemberData > 部分不会发送。|  
|< Server_URL >|在输入的文本**工作流站点**文本框中[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|  
|< Action_ID >|在输入的文本**工作流名称**文本框中[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|  
|\<MemberData >|包含触发工作流操作的成员的数据。 仅当，这是包含的值\<SendData > 为 1。|  
|\<输入*xxx*>|这组标记包含有关创建成员的元数据，例如，何时创建该成员或该成员的创建者。|  
|\<LastChg*xxx*>|这组标记包含有关对成员所作最后更改的元数据，例如，所作更改及更改者。|  
|\<名称 >|已更改的成员的第一个属性。 此示例成员仅包含 Name 和 Code 属性。|  
|\<代码 >|已更改的成员的下一个属性。 如果此示例成员包含更多属性，它们将遵循这一属性。|  
  
## <a name="see-also"></a>另请参阅  
 [创建自定义工作流 &#40;Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [自定义工作流示例 &#40;Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
