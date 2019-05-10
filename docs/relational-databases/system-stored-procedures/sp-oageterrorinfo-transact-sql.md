---
title: sp_OAGetErrorInfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2f4ab09693234d72890524628f4def5afcf447ef
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65450084"
---
# <a name="spoageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  获取 OLE 自动化错误信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>参数  
 *objecttoken*  
 通过使用先前创建的 OLE 对象的对象令牌**sp_OACreate**或，则为 NULL。 如果*objecttoken*是指定，则返回该对象的错误信息。 如果指定为 NULL，则返回整个批处理的错误信息。  
  
 _源_ **输出**  
 错误信息的源。 如果指定，它必须是本地**char**， **nchar**， **varchar**，或者**nvarchar**变量。 必要时将截断返回值以适合局部变量的要求。  
  
 _描述_ **输出**  
 是错误的说明。 如果指定，它必须是本地**char**， **nchar**， **varchar**，或者**nvarchar**变量。 必要时将截断返回值以适合局部变量的要求。  
  
 _helpfile_ **输出**  
 OLE 对象的帮助文件。 如果指定，它必须是本地**char**， **nchar**， **varchar**，或者**nvarchar**变量。 必要时将截断返回值以适合局部变量的要求。  
  
 _helpid_ **输出**  
 帮助文件的上下文 ID。 如果指定，它必须是本地**int**变量。  
  
> [!NOTE]  
>  此存储过程的参数按位置（而不是按名称）指定。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零数字（失败），是由 OLE 自动化对象返回的 HRESULT 整数值。  
  
 有关 HRESULT 返回代码的详细信息，请参阅[OLE 自动化返回代码和错误信息](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="result-sets"></a>结果集  
 如果未指定输出参数，错误信息将作为结果集返回给客户端。  
  
|列名|数据类型|Description|  
|------------------|---------------|-----------------|  
|**错误**|**binary(4)**|错误号的二进制表示形式。|  
|**数据源**|**nvarchar(nn)**|错误的源。|  
|**说明**|**nvarchar(nn)**|错误的说明。|  
|**Helpfile**|**nvarchar(nn)**|错误源的帮助文件。|  
|**HelpID**|**int**|错误源帮助文件中的帮助上下文 ID。|  
  
## <a name="remarks"></a>备注  
 每次调用 OLE 自动化存储过程 (除**sp_OAGetErrorInfo**) 重置错误信息; 因此， **sp_OAGetErrorInfo**中获得最新 OLE 错误信息自动化存储过程调用。 请注意，由于**sp_OAGetErrorInfo**不重置的错误信息，它可以多次调用以获取相同的错误信息。  
  
 下表中列出了 OLE 自动化错误及其常见原因。  
  
|错误及 HRESULT|常见原因|  
|-----------------------|------------------|  
|**变量类型 (错误 0x80020008)**|数据类型[!INCLUDE[tsql](../../includes/tsql-md.md)]作为方法参数不匹配的值传递[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]作为方法参数传递的方法参数或为 NULL 值的数据类型。|  
|**未知的名称 (0x8002006)**|找不到指定对象的指定属性名或方法名。|  
|**类字符串无效 (0x800401f3)**|没有将指定的 ProgID 或 CLSID 没有注册为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 OLE 对象。 必须先注册自定义 OLE 自动化服务器，然后它们可以使用实例化**sp_OACreate**。 这可以通过用于进程内 (.dll) 服务器的 Regsvr32.exe 实用工具或 **/REGSERVER**本地 (.exe) 服务器的命令行开关。|  
|**服务器执行失败 (0x80080005)**|指定的 OLE 对象已注册为本地 OLE 服务器（.exe 文件），但无法找到或启动该 .exe 文件。|  
|**无法找到指定的模块 (0x8007007e)**|指定的 OLE 对象已注册为进程内 OLE 服务器（.dll 文件），但无法找到或半截该 .dll 文件。|  
|**类型不匹配 (0x80020005)**|用于存储返回的属性值或者方法返回值的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 局部变量的数据类型与属性或方法返回值的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 数据类型不匹配。 或者，要求属性或方法返回值，但该属性或方法未返回值。|  
|**数据类型或 sp_OACreate 的 'context' 参数的值无效。(0x8004275B)**|上下文参数的值应为之一：1、 4 或 5。|  
  
 有关处理 HRESULT 返回代码的详细信息，请参阅[OLE 自动化返回代码和错误信息](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定服务器角色或直接在此存储过程的执行权限。 `Ole Automation Procedures` 必须配置**启用**若要使用相关的 OLE 自动化到任何系统过程。  
  
## <a name="examples"></a>示例  
 以下示例将显示 OLE 自动化错误信息。  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>请参阅  
 [OLE 自动化存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 自动化脚本示例](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
