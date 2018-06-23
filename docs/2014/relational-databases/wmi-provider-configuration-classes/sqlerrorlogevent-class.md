---
title: SqlErrorLogEvent 类 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 95588b82a36bb5d7d5d520a5f54ca968a9198112
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024750"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent 类
  提供用于查看指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志文件中的事件的属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>属性  
 SQLErrorLogEvent 类定义以下属性。  
  
|||  
|-|-|  
|FileName|数据类型：`string`<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 错误日志文件的名称。|  
|InstanceName|数据类型：`string`<br /><br /> 访问类型：只读<br /><br /> 限定符：键<br /><br /> 日志文件所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|LogDate|数据类型：`datetime`<br /><br /> 访问类型：只读<br /><br /> 限定符：键<br /><br /> <br /><br /> 在日志文件中记录该事件的日期和时间。|  
|消息|数据类型：`string`<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 事件消息。|  
|ProcessInfo|数据类型：`string`<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 与事件的源服务器进程 ID (SPID) 有关的信息。|  
  
## <a name="remarks"></a>Remarks  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|命名空间|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>示例  
 下面的示例显示如何检索指定的日志文件中所有记录的事件的值。 若要运行该示例，请替换\< *Instance_Name*> 的实例的名称与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如 Instance1 和文件名同名的错误日志文件，如 ERRORLOG.1 替换。  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>注释  
 当*InstanceName*或*FileName*查询将返回的默认实例和当前信息在 WQL 语句中，未提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志文件。 例如，以下 WQL 语句将从默认实例 (MSSQLSERVER) 上的当前日志文件 （错误日志） 返回所有日志事件。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Security  
 若要连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志文件通过 WMI，必须在本地和远程计算机上具有以下权限：  
  
-   读取访问权限**Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空间。 默认情况下，每个人都可以通过“启用帐户”权限获得读取权限。  
  
-   包含错误日志的文件夹的读取权限。 默认情况下，错误日志文件位于以下路径 (其中\<*驱动器 >* 代表你的安装位置的驱动器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和\< *InstanceName*> 是实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<驱动器 >: files\microsoft SQL Server\MSSQL12** **。\<InstanceName > \MSSQL\Log**  
  
 如果您在通过防火墙进行连接，则请确保在防火墙中针对远程目标计算机上的 WMI 设置例外。 有关详细信息，请参阅[连接到 WMI 远程从 Windows Vista 开始](http://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>请参阅  
 [SqlErrorLogFile 类](sqlerrorlogfile-class.md)   
 [查看脱机日志文件](../logs/view-offline-log-files.md)  
  
  