---
title: "了解安全策略 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services], security policies
- Execution permission set
- custom assemblies [Reporting Services], security
- permission sets [Reporting Services]
- expressions [Reporting Services], security
- evidence [Reporting Services]
- FullTrust permission set
- security policies [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: a9bf043a-139a-4929-9a58-244815323df0
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 4c8fa977e2b9cdd596e3029be4954daea7fe239d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="understanding-security-policies"></a>了解安全策略
  由报表服务器执行的任何代码必须是特定的代码访问安全策略的一部分。 这些安全策略包含多个将证据映射到一组命名权限集的代码组。 通常，代码组与在该组中为代码指定可允许权限的命名权限集关联。 运行时使用受信任主机或加载程序所提供的证据来确定代码所属的代码组，从而确定要授予代码的权限。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]遵循此安全策略体系结构，由定义[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]公共语言运行时 (CLR)。 下面几节介绍了 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的各种代码类型以及与它们相关联的策略规则。  
  
## <a name="report-server-assemblies"></a>报表服务器程序集  
 报表服务器程序集是指那些包含作为 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 产品的一部分的代码的程序集。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 是用托管代码程序集编写的；所有这些程序集都采用了强命名模式（即数字签名模式）。 这些程序集的代码组的使用定义**StrongNameMembershipCondition**，该属性提供基于程序集的强名称的公共密钥信息的证据。 代码组被授予**FullTrust**权限集。  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>报表服务器扩展插件（呈现扩展插件、数据扩展插件、传递扩展插件和安全扩展插件）  
 报表服务器扩展插件是您或第三方为了扩展 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的功能而创建的自定义数据扩展插件、传递扩展插件、呈现扩展插件和安全扩展插件。 必须授予**FullTrust**对这些策略配置文件中的扩展或程序集代码与[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]组件扩展。 作为的一部分提供的扩展[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]使用报表服务器的公共密钥进行签名和接收**FullTrust**权限集。  
  
> [!IMPORTANT]  
>  必须修改[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]策略配置文件，以允许**FullTrust**的任何第三方扩展。 如果你不希望添加的代码组**FullTrust**的你自定义的扩展，它们不能由报表服务器。  
  
 有关中的策略配置文件的详细信息[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，请参阅[使用 Reporting Services Security Policy Files](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。  
  
## <a name="expressions-used-in-reports"></a>报表中使用的表达式  
 报表表达式是内联代码表达式或用户定义的方法中包含**代码**报表定义语言文件的元素。 没有代码授予的组已在策略文件中配置这些表达式**执行**默认设置的权限。 该代码组看起来如下所示：  
  
```  
<CodeGroup  
   class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="Execution"  
   Name="Report_Expressions_Default_Permissions"  
   Description="This code group grants default permissions for code in report expressions and Code element. ">  
    <IMembershipCondition  
       class="StrongNameMembershipCondition"  
       version="1"  
       PublicKeyBlob="002400..."  
    />  
</CodeGroup>  
```  
  
 **执行**权限使代码能够运行 （执行），但不是若要使用受保护的资源。 在报表中找到的所有表达式都编译为一个称作“表达式宿主”的程序集，该程序集作为已编译报表的一部分存储。 在执行报表时，报表服务器会加载并调用表达式宿主程序集以执行相应的表达式。 对表达式宿主程序集进行签名所用的密钥与为所有的表达式宿主定义代码组所用的密钥相同。  
  
 报表表达式引用报表对象模型集合（字段、参数等）并执行简单任务（如算术和字符串运算）。 执行这些简单的操作的代码只需要**执行**权限。 默认情况下，用户定义的方法中**代码**元素和任何自定义程序集被授予**执行**中的权限[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。 因此，对于大多数表达式来说，当前的配置不要求您修改任何安全策略文件。 若要向表达式宿主程序集授予额外的权限，管理员需要修改报表服务器和报表设计器的策略配置文件，并更改报表表达式代码组。 由于权限是全局设置，因此更改表达式宿主的默认权限会影响所有报表。 因此，极力建议您将需要额外安全性的所有代码放在一个自定义程序集内。 只有此程序集将被授予所需的权限。  
  
> [!IMPORTANT]  
>  用来调用外部程序集或受保护资源的代码应当合并到一个自定义程序集内以供报表使用， 这会使您对代码所请求和断言的权限进行更多的控制。 你不应调用内的安全方法**代码**元素。 执行此操作需要你授予**FullTrust**到报表表达式主机，并授予 CLR 访问完整的所有自定义代码。  
  
> [!CAUTION]  
>  不要授予**FullTrust**向报表表达式宿主的代码组。 否则将允许所有的报表表达式发出受保护的系统调用。  
  
## <a name="custom-assemblies-referenced-in-reports"></a>报表中引用的自定义程序集  
 某些报表表达式可以调用第三方代码程序集（在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中又称为自定义程序集）。 报表服务器需要这些程序集以至少具有**执行**策略配置文件中的权限。 默认情况下，策略的文件所附带[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]授予**执行**开始从我的电脑区域的所有程序集的权限。 您可以根据需要向自定义程序集授予额外的权限。  
  
 在某些情况下，您可能需要执行某个要求报表表达式中具有特定代码权限的操作。 通常，这意味着报表表达式需要调用受保护的 CLR 库方法（如用来访问文件或系统注册表的方法）。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 文档介绍了发出此安全调用所需的代码权限；若要执行此调用，必须向调用代码授予这些特定的安全权限。 如果你从发起呼叫的报表表达式或**代码**元素，表达式宿主程序集必须为授予适当的权限。 但是，在向表达式宿主授予相应的权限之后，在任何报表中的任何表达式中运行的所有代码现在都将被授予此特定权限。 从自定义程序集发出调用，并向该自定义程序集授予特定权限的操作要安全得多。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的代码访问安全性](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)   
 [安全开发 &#40;Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  

