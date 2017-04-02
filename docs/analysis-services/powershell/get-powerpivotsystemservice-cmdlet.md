---
title: "Get-PowerPivotSystemService cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 33231250-3880-4d75-936b-d70662a01855
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Get-PowerPivotSystemService cmdlet
  返回场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务对象的全局属性。  
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## 语法  
  
```  
Get-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 Get-PowerPivotSystemService cmdlet 返回 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务对象的全局属性。 每个场只有一个父对象，但每个场可以有多个在场中各应用程序服务器上运行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例。 父对象显示不会按实例而改变的场级别设置。 如果场中包括多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安装，则实例的以逗号分隔的列表将指示在场中有多少个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务实例。  
  
## Parameters  
  
### -Identity \<PowerPivotMidTierServicePipeBind>  
 指定要获取的父对象。 该值必须是一个有效的 GUID，用于唯一标识场中的对象。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### \<CommonParameters>  
 此 cmdlet 支持以下常用参数：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## 输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|无。|  
|输出|无。|  
  
## 示例 1  
  
```  
C:\PS>Get-PowerPivotSystemService  
```  
  
 此示例返回父对象的全局属性，并且显示场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务的所有实例共享的属性。  
  
  