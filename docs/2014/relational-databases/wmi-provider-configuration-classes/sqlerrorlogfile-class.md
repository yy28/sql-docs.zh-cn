---
title: SqlErrorLogFile 类 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c5c6f1998cffc268a57318e0124f74d3411a3b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63249318"
---
# <a name="sqlerrorlogfile-class"></a>SqlErrorLogFile 类
  提供用于查看与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志文件有关的信息的属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
class SQLErrorLogFile  
{  
   uint32ArchiveNumber;  
   stringInstanceName;  
   datetimeLastModified;  
   uint32LogFileSize;  
   stringName;  
  
};  
```  
  
## <a name="properties"></a>属性  
 SQLErrorLogFile 类定义以下属性。  
  
|||  
|-|-|  
|ArchiveNumber|数据类型：`uint32`<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 日志文件的存档号。|  
|InstanceName|数据类型：`string`<br /><br /> 访问类型：只读<br /><br /> 限定符：键<br /><br /> <br /><br /> 日志文件所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|LastModified|数据类型：`datetime`<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 上次修改日志文件的日期。|  
|LogFileSize|数据类型：`uint32`<br /><br /> 访问类型：只读<br /><br /> <br /><br /> 日志文件大小（字节）。|  
|名称|数据类型：`string`<br /><br /> 访问类型：只读<br /><br /> 限定符：键<br /><br /> <br /><br /> 日志文件名。|  
  
## <a name="remarks"></a>备注  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|命名空间|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>示例  
 下面的示例检索与指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志文件有关的信息。 若要运行该示例， \<请将*Instance_Name*> 替换为实例的名称，例如 "Instance1"。  
  
```  
on error resume next  
set strComputer = "."  
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")  
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")  
  
For Each logFile in LogFiles  
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _  
    & "Log File Name:  " & logFile.Name & vbNewLine _  
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _  
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _  
    & "Last Modified:  " & logFile.LastModified & vbNewLine _  
  
Next   
```  
  
## <a name="comments"></a>说明  
 如果 WQL 语句中未提供*InstanceName* ，则查询将返回默认实例的信息。 例如，以下 WQL 语句将返回与来自默认实例 (MSSQLSERVER) 的所有日志文件有关的信息。  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>安全性  
 若要通过 WMI [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接到日志文件，您必须在本地和远程计算机上都具有以下权限：  
  
-   对**Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空间的读取访问权限。 默认情况下，每个人都可以通过“启用帐户”权限获得读取权限。  
  
    > [!NOTE]  
    >  有关如何验证 WMI 权限的信息，请参阅主题中的 "[查看脱机日志文件](../logs/view-offline-log-files.md)" 的 "安全性" 部分。  
  
-   包含错误日志的文件夹的读取权限。 默认\<情况下，错误日志位于以下路径中（其中， *drive>* 表示安装了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的驱动器， \< *InstanceName*> 是实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名称）：  
  
     **驱动器>： \Program Files\Microsoft SQL Server\MSSQL11。 \<** **\<InstanceName> \MSSQL\Log**  
  
 如果您在通过防火墙进行连接，则请确保在防火墙中针对远程目标计算机上的 WMI 设置例外。 有关详细信息，请参阅[从 Windows Vista 远程连接到 WMI](https://go.microsoft.com/fwlink/?LinkId=178848)。  
  
## <a name="see-also"></a>另请参阅  
 [SqlErrorLogEvent 类](sqlerrorlogevent-class.md)   
 [查看脱机日志文件](../logs/view-offline-log-files.md)  
  
  
