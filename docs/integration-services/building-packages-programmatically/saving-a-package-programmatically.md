---
title: "以编程方式保存包 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: f6b99377f6eaf720b9511b560e5cf563ede2b869
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="saving-a-package-programmatically"></a>以编程方式保存包
  以编程方式生成新包或修改现有包后，通常要保存更改。  
  
 本主题中的使用以保存包的方法的所有需要引用**Microsoft.SqlServer.ManagedDTS**程序集。 新项目中添加引用后，导入<xref:Microsoft.SqlServer.Dts.Runtime>具有命名空间**使用**或**导入**语句。  
  
## <a name="saving-a-package-programmatically"></a>以编程方式保存包  
 若要以编程方式保存包，请调用以下方法之一[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]<xref:Microsoft.SqlServer.Dts.Runtime.Application>类：  
  
|存储位置|调用的方法|  
|----------------------|--------------------|  
|文件|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS 包存储区|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> 或<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  <xref:Microsoft.SqlServer.Dts.Runtime.Application> 类中用于处理 SSIS 包存储区的方法只支持“.”或本地服务器的服务器名称。 不能使用“(local)”或“localhost”。  
  
## <a name="see-also"></a>另請參閱  
 [保存包](../../integration-services/save-packages.md)  
  
  
