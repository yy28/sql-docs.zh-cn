---
title: 命令元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Command Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.command
- Command
- urn:schemas-microsoft-com:xml-analysis#Command
- http://schemas.microsoft.com/analysisservices/2003/engine#Command
helpviewer_keywords:
- Command element
ms.assetid: 9abc14df-7cbe-46bc-ba0f-f0691c19afad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fd5362d84991a7880798763c9cfec760151ccf34
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163487"
---
# <a name="command-element-xmla"></a>Command 元素 (XMLA)
  包含要由执行的命令[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Execute>  
   ...  
   <Command>  
      <Alter>...</Alter>  
      <!-- or -->  
      <Backup>...</Backup>  
      <!-- or -->  
      <Batch>...</Batch>  
      <!-- or -->  
      <BeginTransaction>...</BeginTransaction>  
      <!-- or -->  
      <Cancel>...</Cancel>  
      <!-- or -->  
      <ClearCache>...</ClearCache>  
      <!-- or -->  
      <CommitTransaction>...</CommitTransaction>  
      <!-- or -->  
      <Create>...</Create>  
      <!-- or -->  
      <Delete>...</Delete>  
      <!-- or -->  
      <DesignAggregations>...</DesignAggregations>  
      <!-- or -->  
      <Drop>...</Drop>  
      <!-- or -->  
      <Insert>...</Insert>  
      <!-- or -->  
      <Lock>...</Lock>  
      <!-- or -->  
      <MergePartitions>...</MergePartitions>  
      <!-- or -->  
      <NotifyTableChange>...</NotifyTableChange>  
      <!-- or -->  
      <Process>...</Process>  
      <!-- or -->  
      <Restore>...</Restore>  
      <!-- or -->  
      <RollbackTransaction>...</RollbackTransaction>  
      <!-- or -->  
      <SetPasswordEncryptionKey>...</SetPasswordEncryptionKey>  
      <!-- or -->  
      <Statement>...</Statement>  
      <!-- or -->  
      <Subscribe>...</Subscribe>  
      <!-- or -->  
      <Synchronize>...</Synchronize>  
      <!-- or -->  
      <Unlock>...</Unlock>  
      <!-- or -->  
      <Update>...</Update>  
      <!-- or -->  
      <UpdateCells>...</UpdateCells>  
   </Command>  
   ...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[执行](../xml-elements-methods-execute.md)|  
|子元素|[Alter](../xml-elements-commands/alter-element-xmla.md)，[备份](../xml-elements-commands/backup-element-xmla.md)，[批处理](../xml-elements-commands/batch-element-xmla.md)， [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md)，[取消](../xml-elements-commands/cancel-element-xmla.md)， [ClearCache](../xml-elements-commands/clearcache-element-xmla.md)[CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md)，[创建](../xml-elements-commands/create-element-xmla.md)，[删除](../xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)，[删除](../xml-elements-commands/drop-element-xmla.md)，[插入](../xml-elements-commands/insert-element-xmla.md)，[锁](../xml-elements-commands/lock-element-xmla.md)， [MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)， [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md)，[过程](../xml-elements-commands/process-element-xmla.md)，[还原](../xml-elements-commands/restore-element-xmla.md)， [RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md)， [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e)，[语句](../xml-elements-commands/statement-element-xmla.md)， [订阅](../xml-elements-commands/subscribe-element-xmla.md)，[同步](../xml-elements-commands/synchronize-element-xmla.md)，[解锁](../xml-elements-commands/unlock-element-xmla.md)，[更新](../xml-elements-commands/update-element-xmla.md)， [UpdateCells](../xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Command` 方法使用 `Execute` 元素将命令转发到数据源。 虽然 XML for Analysis (XMLA) 1.1 规范只支持`Statement`命令， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支持许多新的 XMLA 命令。 有关支持的 XMLA 命令的详细信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[命令&#40;XMLA&#41;](../xml-elements-commands/xml-elements-commands.md)。  
  
## <a name="see-also"></a>请参阅  
 [XML 数据类型&#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
