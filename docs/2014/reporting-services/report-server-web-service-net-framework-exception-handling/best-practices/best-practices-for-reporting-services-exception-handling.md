---
title: Reporting Services 异常处理的最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ac285135f3ae444f222008e9e8b28ffbdd2c9823
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248057"
---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Reporting Services 异常处理的最佳实践
  当开发 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 应用程序时，可以使用多种方法来消除或减少异常的发生。 当确实发生异常时，请向用户提供明确和简洁的错误消息，并添加适当的异常处理以防止应用程序意外结束。  
  
 向报表服务器 Web 服务发送请求的应用程序应执行以下操作：  
  
-   通过尽量防止无效请求，以避免导致异常。  
  
-   尽可能捕获异常并提供有针对性的错误处理代码。  
  
-   处理不引发异常的错误情况。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[阻止无效请求](preventing-invalid-requests.md)|介绍防止将无效请求发送到报表服务器的方法。|  
|[使用 Try 和 Catch 块](using-try-and-catch-blocks.md)|介绍如何通过 try/catch 块进一步增强应用程序的可靠性。|  
|[处理不导致异常的警告和事例](handling-warnings-and-cases-that-do-not-cause-exceptions.md)|说明如何处理不会导致由 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 引发的异常的错误。|  
|[使用 Detail 属性处理特定错误](using-the-detail-property-to-handle-specific-errors.md)|说明如何通过使用 SoapException 对象的 Detail 属性以编程方式处理特定的错误。|  
  
## <a name="see-also"></a>请参阅  
 [Detail 属性](../soapexception-class/detail-property.md)   
 [介绍 Reporting Services 中的异常处理](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../soapexception-class/reporting-services-soapexception-class.md)  
  
  
