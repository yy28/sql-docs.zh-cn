---
title: SqlErrorLogEvent 类 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 558e60a5638ab3af75c5450e3f6fc22c6f9d9601
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62721066"
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
  
## <a name="remarks"></a>备注  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|命名空间|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>示例  
 下面的示例显示如何检索指定的日志文件中所有记录的事件的值。 若要运行该示例， \<请将*Instance_Name*> 替换为实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名称，例如 "Instance1"，并将 "File_Name" 替换为错误日志文件的名称，如 "错误日志文件 1"。  
  
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
  
## <a name="comments"></a>说明  
 如果 WQL 语句中未提供*InstanceName*或*FileName* ，则查询将返回默认实例和当前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志文件的信息。 例如，以下 WQL 语句将返回与来自默认实例 (MSSQLSERVER) 上当前日志文件 (ERRORLOG) 的所有日志事件有关的信息。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>安全性  
 若要通过 WMI [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接到日志文件，您必须在本地和远程计算机上都具有以下权限：  
  
-   对**Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空间的读取访问权限。 默认情况下，每个人都可以通过“启用帐户”权限获得读取权限。  
  
-   包含错误日志的文件夹的读取权限。 默认\<情况下，错误日志位于以下路径中（其中， *drive>* 表示安装了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的驱动器， \< *InstanceName*> 是实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名称）：  
  
     **驱动器>： \Program Files\Microsoft SQL Server\MSSQL12。 \<** **\<InstanceName> \MSSQL\Log**  
  
 如果您在通过防火墙进行连接，则请确保在防火墙中针对远程目标计算机上的 WMI 设置例外。 有关详细信息，请参阅[从 Windows Vista 远程连接到 WMI](https://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>另请参阅  
 [SqlErrorLogFile 类](sqlerrorlogfile-class.md)   
 [查看脱机日志文件](../logs/view-offline-log-files.md)  
  
  
