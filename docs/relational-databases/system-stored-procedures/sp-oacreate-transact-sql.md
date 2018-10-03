---
title: sp_OACreate (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e7ddb90a20b8d7d3c5aab323b803ca9fe3fcecf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605235"
---
# <a name="spoacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建 OLE 对象的实例。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>参数  
 *progid*  
 要创建的 OLE 对象的编程标识符 (ProgID)。 此字符串说明该 OLE 对象的类，采用以下格式： **'***OLEComponent***。***对象*****  
  
 *OLEComponent*是 OLE 自动化服务器的组件名称和*对象*是 OLE 对象的名称。 指定的 OLE 对象必须有效，并且必须支持**IDispatch**接口。  
  
 例如，SQLDMO。SQLServer 是 SQL DMO 的 ProgID **SQLServer**对象。 SQL-DMO 具有的组件名称为 SQLDMO， **SQLServer**对象是否有效，并且 （如所有 SQL-DMO 对象） **SQLServer**对象支持**IDispatch**。  
  
 *clsid*  
 要创建的 OLE 对象的类标识符 (CLSID)。 此字符串说明该 OLE 对象的类，采用以下格式： **{***nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn***}**。 指定的 OLE 对象必须有效，并且必须支持**IDispatch**接口。  
  
 例如，{00026BA1-0000-0000-C000-000000000046} 是 SQL-DMO 的 CLSID **SQLServer**对象。  
  
 *objecttoken* **输出**  
 返回的对象令牌，并且必须是数据类型的局部变量**int**。该对象令牌用于标识所创建的 OLE 对象，并用于调用其他 OLE 自动化存储过程。  
  
 *context*  
 指定要运行新创建的 OLE 对象的执行上下文。 如果指定，则该值必须为下列值之一：  
  
 **1** = 仅进程内 (.dll) OLE 服务器。  
  
 **4** = 本地 (.exe) OLE 服务器仅。  
  
 **5** = 允许进程内和本地 OLE 服务器  
  
 如果未指定，默认值是**5**。 此值将作为传递*dwClsContext*到调用的参数**CoCreateInstance**。  
  
 如果允许进程内 OLE 服务器 (通过使用上下文值为**1**或**5**或者不指定的上下文值)，它可以访问的内存和其他资源拥有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 进程内 OLE 服务器可能会破坏 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内存或资源并导致不可预知的结果，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问违规。  
  
 当指定的上下文值**4**，本地 OLE 服务器不具有任何访问权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]资源，因而不能破坏[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内存或资源。  
  
> [!NOTE]  
>  此存储过程的参数按位置指定，而不是按名称指定。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零数字（失败），是由 OLE 自动化对象返回的 HRESULT 整数值。  
  
 有关 HRESULT 返回代码的详细信息，请参阅[OLE 自动化返回代码和错误信息](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="remarks"></a>备注  
 如果启用 OLE automation procedures 时，调用**sp_OACreate**将会启动 OLE 自动化共享的执行环境。 有关启用 OLE 自动化的详细信息，请参阅[Ole Automation Procedures 服务器配置选项](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)。  
  
 已创建的 OLE 对象在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句批处理结束时会自动破坏。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-progid"></a>A. 使用 ProgID  
 下面的示例创建的 SQL-DMO **SQLServer**通过使用其 ProgID 的对象。  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate 'SQLDMO.SQLServer', @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
### <a name="b-using-clsid"></a>B. 使用 CLSID  
 下面的示例创建的 SQL-DMO **SQLServer**对象使用的 CLSID。  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate '{00026BA1-0000-0000-C000-000000000046}',  
    @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [OLE 自动化存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ole Automation Procedures 服务器配置选项](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [OLE 自动化脚本示例](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
