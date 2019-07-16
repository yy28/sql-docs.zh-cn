---
title: 自定义工作流 XML 说明 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cd291d1615920c3b576386b3f026a4b4d7f29dd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901676"
---
# <a name="create-a-custom-workflow---xml-description"></a>创建自定义工作流 - XML 说明

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 中，当工作流启动时，<xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 方法由 SQL Server MDS Workflow Integration Service 调用。 此方法将有关触发工作流业务规则的项的元数据和数据作为 XML 块接收。 有关实现工作流处理程序的代码示例，请参阅[自定义工作流示例 &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)。  
  
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
  
|标记|描述|  
|---------|-----------------|  
|\<Type>|在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的“工作流类型”文本框中输入的文本，用于标识要加载的自定义工作流程序集  。|  
|\<SendData>|由 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中的“消息中包括成员数据”复选框控制的一个布尔值  。 值 1 表示发送 \<MemberData> 部分；否则表示未发送 \<MemberData> 部分。|  
|<Server_URL>|在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中的“工作流站点”文本框中输入的文本  。|  
|<Action_ID>|在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中的“工作流名称”文本框中输入的文本  。|  
|\<MemberData>|包含触发工作流操作的成员的数据。 仅当 \<SendData> 的值为 1 时才包括此项。|  
|\<Enter*xxx*>|这组标记包含有关创建成员的元数据，例如，何时创建该成员或该成员的创建者。|  
|\<LastChg*xxx*>|这组标记包含有关对成员所作最后更改的元数据，例如，所作更改及更改者。|  
|\<Name>|已更改的成员的第一个属性。 此示例成员仅包含 Name 和 Code 属性。|  
|\<Code>|已更改的成员的下一个属性。 如果此示例成员包含更多属性，它们将遵循这一属性。|  
  
## <a name="see-also"></a>请参阅  
 [创建自定义工作流 &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [自定义工作流示例 &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
