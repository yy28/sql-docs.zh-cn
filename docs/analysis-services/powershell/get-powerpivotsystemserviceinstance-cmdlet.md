---
title: "Get-PowerPivotSystemServiceInstance cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 56027a8e-1949-4349-b616-68c8b1d2963c
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Get-PowerPivotSystemServiceInstance cmdlet
  返回在场中的应用程序服务器上运行的一个或多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例。  
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## 语法  
  
```  
Get-PowerPivotSystemServiceInstance [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 Get-PowerPivotSystemServiceInstance cmdlet返回在场中运行的一个或多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例的属性。 该 cmdlet 报告应用程序类型、状态（联机或脱机）和标识。 若要查看特定实例的其他属性，请向该 cmdlet 添加 Identity 参数和 format-list 选项。  
  
## Parameters  
  
### -Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 指定要获取的服务实例。 该值必须是一个有效的 GUID，用于唯一标识场中的对象。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### \<CommonParameters>  
 此 cmdlet 支持以下常用参数：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)  
  
## 输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|无。|  
|输出|无。|  
  
## 示例 1  
  
```  
C:\PS>Get-PowerPivotSystemServiceInstance -Identity 1234567-890a-bcde-fghijklm | format-list| format-list  
```  
  
 此示例返回指定的实例的其他属性，包括服务器名称、版本和升级状态。  
  
  