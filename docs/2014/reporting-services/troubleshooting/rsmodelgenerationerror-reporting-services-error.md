---
title: rsModelGenerationError - Reporting Services 错误 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 713de57f0f2957983966f8ef0345bb374c311781
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099221"
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|rsRenderingError|  
|事件源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|生成模型时出错。 (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>说明  
 不能生成报表模型。 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 及更早版本中，当 system.object 对象无法处理数据库架构内的表或关系时（例如，当在表中的同一列上定义了两个外键时），很可能会显示此错误。  
  
## <a name="user-action"></a>用户操作  
 若要确定导致出现此消息的具体原因，请查看报表服务器日志文件，该文件位于 \Microsoft SQL Server\\<SQL Server Instance\>\Reporting Services\LogFiles。  
  
## <a name="internal-only"></a>仅内部  
  
