---
title: "SoapException 错误表 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SoapException class
ms.assetid: 3dbf1b5a-bd2a-4385-925d-5d095d72014c
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bce2a94413b1aa40c3c935da4ed8c8d70814028c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="soapexception-errors-table"></a>SoapException 错误表
  报表服务器基于在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中发生的错误在 SOAP 异常中生成错误和错误消息。 下表显示可从通过方法进行访问的错误**SoapException**报表服务器 Web 服务中。 该表按引发异常的方法组织。  
  
|方法|错误代码|  
|-----------------|----------------|  
|**ALL**|**rsEvaluationCopyExpired**|  
|**ALL**|**rsFailedToDecryptConfigInformation**|  
|**ALL**|**rsInvalidRSEditionConfiguration**|  
|**ALL**|**rsReportServerNotActivated**|  
|**ALL**|**rsServerBusy**|  
|**ALL**|**rsReportServerServiceUnavailable**|  
|**ALL**|**rsReportServerDisabled**|  
|**所有**除**GetPermissions**， **GetRenderResource**， **GetSystemPermissions**， **ListEvents**，和**ListSecureMethods**|**rsAccessDenied**|  
|**所有**除**CreateBatch**， **ExecuteBatch**， **GetSystemPolicies**， **GetSystemPermissions**， **GetSystemProperties**， **ListEvents**， **ListJobs**， **ListRoles**， **ListSchedules**， **ListSecureMethods**， **ListSubscriptions**， **ListSystemRoles**， **ListSystemTasks**， **ListTasks**|**rsMissingParameter**|  
|**CreateDataDrivenSubscription**， **CreateDataSource**， **CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateReportHistorySnapshot**， **CreateResource**， **CreateSubscription**， **DeleteItem**， **DeleteReportHistorySnapshot**， **DisableDataSource**， **EnableDataSource**， **FindItems**， **FlushCache**， **GetCacheOptions**， **GetDataSourceContents****GetExecutionOptions**， **GetPermissions**， **GetPolicies**， **GetProperties**， **GetReportDataSourcePrompts**， **GetReportDataSources**， **GetReportDefinition**， **GetReportHistoryLimit**， **GetReportHistoryOptions**， **GetReportLink**， **GetReportParameters**， **GetResourceContents**， **GetRoleProperties**， **GetServerDateTime**， **IheritParentSecurity**， **ListChildren**， **ListLinkedReports**， **ListReportHistory**， **ListReportsUsingDataSource**， **ListSchedules**， **ListSubscriptions**， **ListSubscriptionsUsingDataSource**， **MoveItem**，**呈现**， **RenderStream**， **SetCacheOptions**， **SetDataSourceContents**， **SetExecutionOptions**， **SetPolicies**， **SetProperties**， **SetReportDataSources**， **SetReportDefinition**， **SetReportHistoryLimit**， **SetReportHistoryOptions**， **SetReportLink**， **SetReportParameters**， **SetResourceContents**， **UpdateReportExecutionSnapshot**， **ValidateExtensionSettings**|**rsItemNotFound**|  
|**执行**， **CreateDataDrivenSubscription**， **CreateDataSource**， **CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateReportHistorySnapshot**， **CreateResource**， **CreateRole**， **CreateSchedule**， **CreateSubscription**， **DeleteItem**， **DeleteReportHistorySnapshot**， **DeleteRole**， **DeleteSchedule**， **DeleteSubscription**， **DisableDataSource**， **EnableDataSource**， **ExecuteBatch**， **FindItems**， **FlushCache**， **GetResourceContents**， **GetServerDateTime**， **MoveItem**， **PauseSchedule**， **ResumeSchedule**， **SetCacheOptions**， **SetDataDrivenSubscriptionProperties**， **SetDataSourceContents**， **SetExecutionOptions**， **SetPolicies**， **SetProperties**， **SetReportDataSources**， **SetReportDefinition**， **SetReportHistoryLimit**， **SetReportHistoryOptions**， **SetReportLink**， **SetReportParameters**， **SetResourceContents**， **SetRoleProperties**， **SetScheduleProperties**， **SetSubscriptionProperties**， **SetSystemPolicies**， **SetSystemProperties**， **UpdateReportExecutionSnapshot**， **ValidateExtensionSettings**|**rsBatchNotFound**|  
|**CreateDataDrivenSubscription**， **CreateDataSource**， **CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateReportHistorySnapshot**， **CreateResource**， **CreateSubscription**， **DeleteItem**， **DeleteReportHistorySnapshot**， **DisableDataSource**， **EnableDataSource**， **FindItems**， **FlushCache**， **GetCacheOptions**， **GetDataSourceContents****GetExecutionOptions**， **GetItemType**， **GetPermissions**， **GetPolicies**， **GetProperties**， **GetReportDataSourcePrompts**， **GetReportDataSources**， **GetReportDefinition**， **GetReportHistoryLimit**， **GetReportHistoryOptions**， **GetReportLink**， **GetResourceContents**， **GetServerDateTime**， **IheritParentSecurity**， **ListChildren**， **ListLinkedReports**， **ListReportHistory**， **ListSchedules**， **ListSubscriptionsUsingDataSource**， **MoveItem**，**呈现**， **RenderStream**， **SetCacheOptions**， **SetDataSourceContents**， **SetExecutionOptions**， **SetPolicies**， **SetProperties**， **SetReportDataSources**， **SetReportDefinition**， **SetReportHistoryLimit**， **SetReportHistoryOptions**， **SetReportLink**， **SetReportParameters**， **SetResourceContents**， **SetSubscriptionProperties**， **UpdateReportExecutionSnapshot**， **ValidateExtensionSettings**|**rsInvalidItemPath**|  
|**CreateDataDrivenSubscription**， **CreateDataSource**， **CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateReportHistorySnapshot**， **CreateResource**， **CreateSubscription**， **DeleteReportHistorySnapshot**， **DisableDataSource**， **EnableDataSource**， **FindItems**， **FlushCache**， **GetCacheOptions**， **GetDataSourceContents**， **GetExecutionOptions**， **GetReportDataSourcePrompts**， **GetReportDataSources**， **GetReportDefinition**， **GetReportHistoryLimit**， **GetReportHistoryOptions**， **GetReportLink**， **GetReportParameters**， **GetResourceContents**， **GetServerDateTime**， **GetSystemProperties**， **ListChildren**， **ListLinkedReports**， **ListReportHistory**， **ListReportsUsingDataSource****ListSchedules**， **ListSubscriptions**， **ListSubscriptionsUsingDataSource**， **MoveItem**，**呈现**， **RenderStream**， **SetCacheOptions**， **SetDataSourceContents**， **SetExecutionOptions**， **SetReportDataSources**， **SetReportDefinition**， **SetReportHistoryLimit**， **SetReportHistoryOptions**， **SetReportLink**， **SetReportParameters**， **SetResourceContents**， **UpdateReportExecutionSnapshot**， **ValidateExtensionSettings**|**rsWrongItemType**|  
|**CreateReport**， **CreateResource**， **DeleteReportHistorySnapshot**， **DeleteSchedule**， **DeleteSubscription**， **GetDataDrivenSubscriptionProperties**， **GetSubscriptionProperties**， **ListChildren**， **ListScheduledReports**， **PauseSchedule**，**呈现**， **RenderStream**， **ResumeSchedule**， **SetCacheOptions**， **SetDataDrivenSubscriptionProperties**， **SetReportHistoryLimit**， **SetReportHistoryOptions**， **SetScheduleProperties**， **SetSubscriptionProperties**|**rsParameterTypeMismatch**|  
|**CreateDataDrivenSubscription**， **CreateDataSource**， **CreateSchedule**， **CreateSubscription**， **FindItems**， **GetReportParameters**， **PrepareQuery**，**呈现**， **SetCacheOptions**， **SetDataDrivenSubscriptionProperties**， **SetDataSourceContents**， **SetPolicies**， **SetReportDataSources**， **SetReportParameters**， **SetScheduleProperties**， **SetSubscriptionProperties**， **SetSystemPolicies**|**rsMissingElement**|  
|**CreateDataDrivenSubscription**， **CreateDataSource**， **CreateSchedule**， **CreateSubscription**， **PrepareQuery**，**呈现**， **SetCacheOptions**， **SetDataDrivenSubscriptionProperties**， **SetDataSourceContents**， **SetProperties**， **SetReportDataSources**， **SetReportParameters**， **SetScheduleProperties**， **SetSubscriptionProperties**， **SetSystemProperties**|**rsInvalidElement**|  
|**CreateDataDrivenSubscription**， **CreateSchedule**， **CreateSubscription**， **FindItems**， **GetRenderResource**， **PrepareQuery**，**呈现**， **RenderStream**， **SetCacheOptions**， **SetDataDrivenSubscriptionProperties**， **SetExecutionOptions**， **SetProperties**， **SetReportHistoryOptions**， **SetReportParameters**， **SetScheduleProperties**， **SetSubscriptionProperties**， **SetSystemProperties**|**rsElementTypeMismatch**|  
|**CreateDataSource**， **CreateRole**， **GetDataDrivenSubscriptionProperties**， **GetRenderResource**， **ListExtensions**，**呈现**， **SetDataDrivenSubscriptionProperties**， **SetDataSourceContents**， **SetExecutionOptions**， **SetReportHistoryLimit**， **SetReportHistoryOptions**， **SetScheduleProperties**|**rsInvalidParameter**|  
|**CreateDataDrivenSubscription**， **CreateReportHistorySnapshot**， **CreateSubscription**， **PrepareQuery**， **SetDataDrivenSubscriptionProperties**， **SetExecutionOptions**， **SetReportHistoryOptions**， **SetSubscriptionProperties**|**rsInvalidDataSourceCredentialSetting**|  
|**CreateDataDrivenSubscriptionProperties**， **CreateReportHistorySnapshot**， **CreateSchedule**， **CreateSubscription**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**， **UpdateReportExecutionSnapshot**|**rsReportParameterValueNotSet**|  
|**CreateDataDrivenSubscription**， **CreateSubscription**， **GetExtensionSettings**， **GetRenderResource**，**呈现**， **RenderStream**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsMultipleExtensionsFoundInAssembly**|  
|**CreateDataDrivenSubscriptionProperties**， **CreateSubscription**，**呈现**， **SetCacheOptions**， **SetExecutionOptions**， **SetReportParameters**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsReportParameterTypeMismatch**|  
|**CreateSchedule**， **CreateSubscription**， **DeleteSchedule**， **PauseSchedule**， **ResumeSchedule**， **SetCacheOptions**， **SetExecutionOptions**， **SetScheduleProperties**， **SetSubscriptionProperties**|**rsSchedulerNotResponding**|  
|**DeleteSchedule**， **GetScheduleProperties**， **ListScheduledReports**， **PauseSchedule**， **ResumeSchedule**， **SetCacheOptions**， **SetExecutionOptions**， **SetScheduleProperties**|**rsScheduleNotFound**|  
|**CreateDataDrivenSubscriptionProperties**， **CreateSubscription**，**呈现**， **SetReportParameters**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsReadOnlyReportParameter**|  
|**CreateDataDrivenSubscriptionProperties**， **CreateSubscription**， **GetReportParameters**，**呈现**， **SetReportParameters**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsUnknownReportParameter**|  
|**DeleteSubscription**， **GetDataDrivenSubscriptionProperties**， **GetSubscriptionProperties**， **SetDataDrivenSubscriptionProperties**， **SetExecutionOptions**， **SetSubscriptionProperties**|**rsSubscriptionNotFound**|  
|**CreateDataDrivenSubscription**， **CreateSubscription**， **GetExtensionSettings**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsDeliveryExtensionNotFound**|  
|**CreateDataDrivenSubscription**， **CreateSubscription**， **GetExtensionSettings**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsDeliveryError**|  
|**CreateDataDrivenSubscription**， **GetDataDrivenSubscriptionProperties**， **PrepareQuery**， **SetDataDrivenSubscriptionProperties**|**rsSecureConnectionRequired**|  
|**CreateDataDrivenSubscription**， **CreateSubscription**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsCannotSubscribeToEvent**|  
|**CreateDataDrivenSubscription**， **CreateSubscription**， **FireEvent**， **SetDataDrivenSubscriptionProperties**， **SetSubscriptionProperties**|**rsUnknownEventType**|  
|**CreateDataSource**， **CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateResource**， **MoveItem**|**rsItemPathLengthExceeded**|  
|**CopyItem**， **CreateFolder**， **CreateReport**， **CreateResource**，**删除项**|**rsReservedItem**|  
|**CreateDataSource**， **SetDataSourceContents**， **SetReportDataSources**|**rsInvalidElementCombination**|  
|**SetCacheOptions**， **SetExecutionOptions**， **SetReportHistoryOptions**|**rsInvalidParameterCombination**|  
|**CreateDataSource**， **CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateResource**， **MoveItem**|**rsInvalidItemName**|  
|**CreateDataSource**， **CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateResource**， **MoveItem**|**rsItemAlreadyExists**|  
|**CreateFolder**， **CreateLinkedReport**， **CreateReport**， **CreateResource**， **SetProperties**|**rsReadOnlyProperty**|  
|**GetPolicies**， **GetSystemPolicies**， **SetPolicies**， **SetSystemPolicies**|**rsInvalidPolicyDefinition**|  
|**SetCacheOptions**， **SetDataSourceContents**， **SetReportDataSources**， **SetReportParameters**|**rsOperationPreventsUnattendedExecution**|  
|**CreateReportHistorySnapshot**，**呈现**， **PrepareQuery**， **UpdateReportExecutionSnapshot**|**rsInvalidDataSourceReference**|  
|**CreateReportHistorySnapshot**， **PrepareQuery**，**呈现**， **UpdateReportExecutionSnapshot**|**rsDataSourceDisabled**|  
|**CreateReport**， **PrepareQuery**， **SetReportDefinition**|**rsProcessingError**|  
|**GetRenderResource**，**呈现**， **RenderStream**|**rsInvalidReportLink**|  
|**DeleteReportHistorySnapshot**，**呈现**， **RenderStream**|**rsReportHistoryNotFound**|  
|**SetCacheOptions**， **SetExecutionOptions**， **SetReportHistoryOptions**|**rsReportMayNotBeScheduled**|  
|**CreateDataDrivenSubscription**， **GetDataDrivenSubscriptionProperties**， **SetDataDrivenSubscriptionProperties**|**rsOperationNotSupported**|  
|**CreateDataSource**， **SetDataSourceContents**， **SetReportDataSources**|**rsDataExtensionNotFound**|  
|**DeleteRole**， **SetPolicies**， **SetRoleProperties**|**rsRoleNotFound**|  
|**DeleteReportHistorySnapshot**，**呈现**， **RenderStream**|**rsParametersNotSpecified**|  
|**GetReportParameters**， **SetReportParameters**|**rsNotSupported**|  
|**SetReportParameters**， **UpdateReportExecutionSnapshot**|**rsReportSnapshotNotEnabled**|  
|**CreateSchedule**， **SetScheduleProperties**|**rsScheduleAlreadyExists**|  
|**CreateRole**， **SetRoleProperties**|**rsTaskNotFound**|  
|**CreateRole**， **SetRoleProperties**|**rsMixedTasks**|  
|**ListSubscriptions**， **SetPolicies**|**rsUnknownUserName**|  
|**MoveItem**|**rsInvalidMove**|  
|**RenderStream**|**rsStreamNotFound**|  
|**RenderStream**|**rsMissingSessionId**|  
|**Render**|**rsReportNotReady**|  
|**Render**|**rsAssemblyNotPermissioned**|  
|**SetExecutionOptions**|**rsReportSnapshotEnabled**|  
|**FindItems**|**rsInvalidSearchOperator**|  
|**SetReportDataSources**|**rsDataSourceNotFound**|  
|**PrepareQuery**，**呈现**|**rsDataSourceNoPrompt**|  
|**PrepareQuery**|**rsCannotPrepareQuery**|  
|**DeleteRole**|**rsReservedRole**|  
|**CreateRole**|**rsEmptyRole**|  
|**InheritParentSecurity**|**rsInheritedPolicy**|  
|**CreateRole**|**rsRoleAlreadyExists**|  
|**InheritParentSecurity**|**rsCannotDeleteRootPolicy**|  
|**CancelJob**|**rsJobWasCanceled**|  
|**ListSecureMethods**|**rsServerConfigurationError**|  
  
## <a name="see-also"></a>另请参阅  
 [引入了 Reporting Services 中的异常处理](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [错误和事件参考 &#40;Reporting Services &#41;](../../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)   
 [Reporting Services SoapException 类](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [使用的详细信息属性来处理特定的错误](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  

