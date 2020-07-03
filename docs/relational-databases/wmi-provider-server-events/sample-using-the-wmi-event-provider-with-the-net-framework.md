---
title: 示例：在 .NET 中使用 WMI 事件提供程序
description: '示例 c # 应用程序使用 WMI 事件提供程序返回 SQL Server 实例上发生的所有数据定义语言事件的事件数据。'
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Server Events, samples
- sample applications [WMI]
- managed code [WMI]
ms.assetid: 3d7aa7e9-0bb3-4a5b-9a3c-047f3240a6f8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a863d0c6130821c9a495b8e92332342e90005689
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888183"
---
# <a name="sample-using-the-wmi-event-provider-with-the-net-framework"></a>示例：与 .NET Framework 结合使用 WMI 事件提供程序
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  下面的示例用 C# 创建使用 WMI 事件提供程序返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认安装实例上发生的所有数据定义语言 (DDL) 事件的事件数据的应用程序。  
  
## <a name="example"></a>示例  
 该示例使用以下命令文件进行编译：  
  
```  
set compiler_path=C:\WINNT\Microsoft.NET\Framework\v2.0.50110  
  
%compiler_path%\csc %1  
```  
  
```  
using System;  
using System.Management;  
  
class SQLWEPExample   
{  
    public static void Main(string[] args)  
    {  
        string query =  @"SELECT * FROM DDL_EVENTS " ;  
        // Default namespace for default instance of SQL Server   
        string managementPath =  
            @"\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER";  
        ManagementEventWatcher  watcher =   
            new ManagementEventWatcher(new WqlEventQuery (query));  
        ManagementScope scope = new ManagementScope (managementPath);  
        scope.Connect();  
        watcher.Scope = scope;  
        Console.WriteLine("Watching...");  
        while (true)  
        {  
            ManagementBaseObject obj = watcher.WaitForNextEvent();  
            Console.WriteLine("Event!");  
            foreach (PropertyData data in obj.Properties)  
            {  
                Console.Write("{0}:", data.Name);  
                if (data.Value == null)  
                {  
                    Console.WriteLine("<null>");  
                }  
                else  
                {  
                    Console.WriteLine(data.Value.ToString());  
                }  
            }  
            Console.WriteLine("-----");  
            Console.WriteLine();  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [WMI Provider for Server Events 的概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
