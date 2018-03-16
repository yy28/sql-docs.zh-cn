---
title: APP_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b2b65f2380cc52c7a1d084dedad5fdb744d377bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="appname-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回当前会话的应用程序名称（如果应用程序进行了设置）。
  
> [!IMPORTANT]  
>  应用程序名称由客户端提供，并不以任何方式进行验证。 请不要使用 APP_NAME 作为安全检查的一部分。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>返回类型  
**nvarchar(128)**
  
## <a name="remarks"></a>Remarks  
如果想针对不同应用程序执行不同的操作，请使用 APP_NAME。 例如，针对不同应用程序进行不同的日期格式化，或返回信息性消息到某些应用程序。
  
要在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中设置应用程序名称，在“连接到数据库引擎”对话框中单击“选项”。 在“其他连接参数”选项卡上，提供 app 属性，格式为 `;app='application_name'`
  
## <a name="examples"></a>示例  
以下示例检查了初始化该进程的客户端应用程序是否是一个 `SQL Server Management Studio` 会话，并且提供 US 或 ANSI 格式的日期。
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>另请参阅
[系统函数 (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[函数](../../t-sql/functions/functions.md)
  
  
