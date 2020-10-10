---
description: SqlErrorLogEvent 类
title: SqlErrorLogEvent 类
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7e106fa85ac8832782c339b115969e2ca8d4fad4
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891527"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent 类
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]
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
  
| 属性 | 说明 |
| -------- | ----------- |
|FileName|数据类型： **字符串**<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 错误日志文件的名称。|  
|InstanceName|数据类型： **字符串**<br /><br /> 访问类型：只读<br /><br /> 限定符：键<br /><br /> 日志文件所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|LogDate|数据类型： **datetime**<br /><br /> 访问类型：只读<br /><br /> 限定符：键<br /><br /> <br /><br /> 在日志文件中记录该事件的日期和时间。|  
|Message|数据类型： **字符串**<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 事件消息。|  
|ProcessInfo|数据类型： **字符串**<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 与事件的源服务器进程 ID (SPID) 有关的信息。|  
  
## <a name="remarks"></a>备注  
  
| 类型 | 名称 |
| ---- | ---- |
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|命名空间|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>示例  
 下面的示例显示如何检索指定的日志文件中所有记录的事件的值。 若要运行该示例，请将替换 \<*Instance_Name*> 为实例的名称（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 例如 "Instance1"），并将 "File_Name" 替换为错误日志文件的名称，如 "错误日志 1"。  
  
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
 如果 WQL 语句中未提供 *InstanceName* 或 *FileName* ，则查询将返回默认实例和当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志文件的信息。 例如，以下 WQL 语句将返回与来自默认实例 (MSSQLSERVER) 上当前日志文件 (ERRORLOG) 的所有日志事件有关的信息。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>安全  
 若要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过 WMI 连接到日志文件，您必须在本地和远程计算机上都具有以下权限：  
  
-   对 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空间的读取访问权限。 默认情况下，每个人都可以通过“启用帐户”权限获得读取权限。  
  
-   包含错误日志的文件夹的读取权限。 默认情况下，错误日志位于以下路径中 (其中 \<*Drive> * 表示你安装的驱动器 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， \<*InstanceName*> 是) 实例的名称 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：  
  
     ** \<Drive> ： \PROGRAM Files\Microsoft SQL Server\MSSQL13** **。 \<InstanceName>\MSSQL\Log**  
  
 如果您在通过防火墙进行连接，则请确保在防火墙中针对远程目标计算机上的 WMI 设置例外。 有关详细信息，请参阅 [从 Windows Vista 远程连接到 WMI](/windows/win32/wmisdk/connecting-to-wmi-remotely-starting-with-vista)。  
  
## <a name="see-also"></a>另请参阅  
 [SqlErrorLogFile 类](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [查看脱机日志文件](../../relational-databases/logs/view-offline-log-files.md)  
  
