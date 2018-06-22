---
title: 以编程方式保存包 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b003cd2b5f6aed93af6e5f695aa972338179e59b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015292"
---
# <a name="saving-a-package-programmatically"></a>以编程方式保存包
  以编程方式生成新包或修改现有包后，通常要保存更改。  
  
 本主题中使用的保存包的所有方法都需要引用 `Microsoft.SqlServer.ManagedDTS` 程序集。 新项目中添加引用后，导入<xref:Microsoft.SqlServer.Dts.Runtime>具有命名空间`using`或`Imports`语句。  
  
## <a name="saving-a-package-programmatically"></a>以编程方式保存包  
 若要以编程方式保存包，可调用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application> 类的以下方法之一：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|文件|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> 或多个<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  <xref:Microsoft.SqlServer.Dts.Runtime.Application> 类中用于处理 SSIS 包存储区的方法只支持“.”或本地服务器的服务器名称。 不能使用“(local)”或“localhost”。  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新集成服务** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的集成服务页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [保存包](../save-packages.md)  
  
  