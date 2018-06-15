---
title: 更新 PowerPivotSystemService cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f09c45944b15f474bf9454303924c759ac6f6e9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028268"
---
# <a name="update-powerpivotsystemservice-cmdlet"></a>Update-PowerPivotSystemService cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  升级场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务的父对象。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
Update-PowerPivotSystemService [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 **Update-PowerPivotSystemService** cmdlet 对场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务父对象、实例和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序运行一系列升级操作。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署中的所有中间层服务和应用程序都必须运行在相同的功能级别。 此 cmdlet 对所有这些对象运行升级操作。  
  
 在运行 SQL Server 安装程序以便安装新版本的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或对服务器应用了累积更新后，运行此 cmdlet。 若要检查是否需要升级，请运行 `Get-PowerPivotSystemService` 以查看 **NeedsUpgrade** 属性。 如果 **NeedsUpgrade** 为 true，则应运行此 cmdlet 以升级场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中间层对象。  
  
 由于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署包括中间层和后端数据服务，因此在运行 **Update-PowerPivotEngineService** 时必须运行 **Update-PowerPivotSystemService** 以确保这两个层在场中为相同版本。  
  
 升级不能回滚到以前的版本。 如果你必须还原到以前的版本，则必须从 SharePoint 场中删除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ，然后重新安装该软件。 若要确认升级操作已成功，请运行 `Get-PowerPivotSystemService` 以查看版本信息的全局属性并确认 **NeedsUpgrade** 不再设置为 true。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-confirm-switch"></a>确认\<切换 >  
 在执行命令前提示您进行确认。 默认情况下将启用该值。 若要在命令中跳过确认响应，请在命令中指定 Confirm:$false。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下参数：  
  
-   Verbose  
  
-   调试  
  
-   ErrorAction  
  
-   ErrorVariable  
  
-   WarningAction  
  
-   WarningVariable  
  
-   OutBuffer  
  
-   OutVariable  
  
 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|无。|  
|输出|无。|  
  
  
