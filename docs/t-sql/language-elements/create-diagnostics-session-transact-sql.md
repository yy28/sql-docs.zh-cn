---
title: "创建诊断会话 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71f3463ad4d91bd117c322e9e63c0b331b07ca9f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-diagnostics-session-transact-sql"></a>创建诊断会话 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  诊断会话可让你以保存对系统或查询的性能、 用户定义的详细诊断信息。  
  
 若要调试的特定查询性能，或以在设备操作过程中监视的特定设备组件的行为，通常使用诊断会话。  
  
> [!NOTE]  
>  你应该熟悉 XML 才能使用诊断会话。  
  
## <a name="syntax"></a>语法  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N’{<session_xml>}’;  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name=”event_name”/>  
         [ <Where>\<filter_property_name Name=”value” ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name=”property_name”/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>参数  
 *diagnostics_name*  
 诊断会话的名称。 诊断会话名称只能包含字符 a 到 z、 A 到 Z 和 0-9 仅。 此外，诊断会话名称必须以字符开头。 *diagnostics_name*仅限于 127 个字符。  
  
 *max_item_count_num*  
 要在视图中保留的事件数。 例如，如果指定 100，则将到诊断会话中存在匹配的筛选条件的 100 个最新事件。 如果找到少于 100 匹配事件，诊断会话将包含少于 100 个事件。 *max_item_count_num*必须至少 100 且小于或等于 100000。  
  
 *event_name*  
 定义要在诊断会话中收集的实际事件。  *event_name*是中列出的事件之一[sys.pdw_diag_events](http://msdn.microsoft.com/en-us/d813aac0-cea1-4f53-b8e8-d26824bc2587)其中`sys.pdw_diag_events.is_enabled='True'`。  
  
 *filter_property_name*  
 限制结果所依据的属性名称。 例如，如果你想要限制基于会话 id *filter_property_name*应*SessionId*。 请参阅*property_name*下面有关的潜在值列表*filter_property_name*。  
  
 *值*  
 一个值，以评估针对*filter_property_name*。 值类型必须与匹配的属性类型。 例如，如果该属性类型是十进制的一种*值*必须为十进制。  
  
 *comp_type*  
 比较类型中。 可能值是： 等于、 EqualsOrGreaterThan、 EqualsOrLessThan、 GreaterThan、 LessThan、 NotEquals、 Contains、 正则表达式  
  
 *property_name*  
 一个与事件相关的属性。  属性名称可以是捕获标记的一部分，也用作筛选条件的一部分。  
  
|属性名称|Description|  
|-------------------|-----------------|  
|UserName|用户 （登录名） 名称。|  
|SessionId|会话 id。|  
|QueryId|查询 id。|  
|CommandType|命令类型。|  
|CommandText|处理的命令中的文本。|  
|OperationType|个事件的操作类型。|  
|Duration|事件的持续时间。|  
|SPID|服务进程 id。|  
  
## <a name="remarks"></a>注释  
 允许每个用户最多 10 个并发的诊断会话。 请参阅[sys.pdw_diag_sessions](http://msdn.microsoft.com/en-us/ca111ddc-2787-4205-baf0-1a242c0257a9)有关的当前会话和任何不需要的会话使用的下拉列表`DROP DIAGNOSTICS SESSION`。  
  
 诊断会话将继续收集之前删除的元数据。  
  
## <a name="permissions"></a>Permissions  
 需要**更改服务器状态**权限。  
  
## <a name="locking"></a>锁定  
 在诊断会话表上采用共享的锁。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-diagnostics-session"></a>A. 创建诊断会话  
 此示例创建一个诊断会话，以便记录的数据库引擎性能度量值。 该示例创建用于侦听的引擎查询运行/结束事件和阻止的 DMS 事件诊断会话。 返回的内容是命令文本、 计算机名、 请求 id (查询 id) 和创建该事件的会话。  
  
```  
CREATE DIAGNOSTICS SESSION MYDIAGSESSION AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:EngineQueryRunningEvent" />  
      <Event Name="DmsCoreInstrumentation:DmsBlockingQueueEnqueueBeginEvent" />  
      <Where>  
         <SessionId Value="381" ComparisonType="NotEquals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Query.CommandText" />  
      <Property Name="MachineName" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Alias" />  
      <Property Name="Duration" />  
      <Property Name="Session.SessionId" />  
   </Capture>  
</Session>';  
```  
  
 创建后的诊断会话，运行查询。  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 通过选择从 sysdiag 架构，然后查看诊断会话结果。  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 请注意 sysdiag 架构包含名为你的诊断会话名称的视图。  
  
 若要查看仅为你的连接活动，添加`Session.SPID`属性并添加`WHERE [Session.SPID] = @@spid;`到查询。  
  
 当你完成诊断会话时，使用删除该表**删除诊断**命令。  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. 替代的诊断会话  
 一个具有略有不同的属性的第二个示例。  
  
```  
-- Determine the session_id of your current session  
SELECT TOP 1 session_id();  
-- Replace \<*session_number*> in the code below with the numbers in your session_id  
CREATE DIAGNOSTICS SESSION PdwOptimizationDiagnostics AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:MemoGenerationBeginEvent" />  
      <Event Name="EngineInstrumentation:MemoGenerationEndEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationBeginEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationEndEvent" />  
      <Event Name="DSQLInstrumentation:BuildRelOpContextTreeBeginEvent" />  
      <Event Name="DSQLInstrumentation:PostPlanGenModifiersEndEvent" />  
      <Where>  
         <SessionId Value="\<*session_number*>" ComparisonType="Equals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Session.SessionId" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Query.CommandText" />  
      <Property Name="Name" />  
      <Property Name="DateTimePublished" />  
      <Property Name="DateTimePublished.Ticks" />  
  </Capture>  
</Session>';  
```  
  
 运行查询，如：  
  
```  
USE ssawPDW;  
GO  
SELECT * FROM dbo.FactFinance;  
```  
  
 以下查询返回的授权计时：  
  
```  
SELECT *   
FROM master.sysdiag.PdwOptimizationDiagnostics   
ORDER BY DateTimePublished;  
```  
  
 当你完成诊断会话时，使用删除该表**删除诊断**命令。  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  

