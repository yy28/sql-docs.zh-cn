---
title: 数据连接使用 Windows 身份验证并且无法对用户凭据进行委托。 以下连接无法刷新： PowerPivot 数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d2006df1-d244-4786-b272-49d8996cc88c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9611bc9d922caee25f841b709ee8a743cd539357
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547749"
---
# <a name="the-data-connection-uses-windows-authentication-and-user-credentials-could-not-be-delegated-the-following-connections-failed-to-refresh-powerpivot-data"></a>数据连接使用 Windows 身份验证并且无法对用户凭据进行委托。 以下连接无法刷新：PowerPivot 数据
  对于包含 PowerPivot 数据的 Excel 工作簿，如果 Excel Services 无法连接到 SharePoint 中的 PowerPivot 服务器实例，则会返回此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|PowerPivot for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|在尝试使用 PowerPivot 数据访问接口时出现连接错误。|  
|消息正文|数据连接使用 Windows 身份验证并且无法对用户凭据进行委托。 以下连接无法刷新：PowerPivot 数据|  
  
## <a name="explanation"></a>说明  
 有多个原因会导致出现此错误消息。 但所有这些原因都具有一个共性，就是 Excel Services 无法从 SharePoint 的声明令牌中获取有效的 Windows 用户标识。 在 Excel 工作簿包含 PowerPivot 数据时，如果以下任何条件成立，都会出现此错误：  
  
-   Claims to Windows Token Service 未运行。 您可以通过查看 SharePoint 日志文件确认导致此错误的原因。 如果 SharePoint 日志包括消息“The pipe endpoint 'net.pipe://localhost/s4u/022694f3-9fbd-422b-b4b2-312e25dae2a2' could not be found on your local machine”，则 Claims to Windows Token Service 未运行。 若要启动该服务，请使用管理中心，然后在“服务”控制台应用程序中确认该服务正在运行。  
  
-   域控制器不可用于确认用户标识。 Claims to Windows Token Service 不使用缓存凭据。 它会验证每个连接的用户标识。 您可以通过查看 SharePoint 日志文件确认导致此错误的原因。 如果 SharePoint 日志包括消息“Failed to get WindowsIdentity from IClaimsIdentity”，则无法对该用户标识进行身份验证。  
  
-   计算机必须是同一域中的成员，或者必须处于具有双向信任关系的域中。  
  
-   您必须使用 Windows 域用户帐户。 这些帐户必须具有通用主体名称 (UPN)。  
  
-   Excel Services 服务帐户必须具有 Active Directory 权限以便查询对象。  
  
## <a name="user-action"></a>用户操作  
 使用以下说明可以查看 Claims to Windows Token Service 的状态。  
  
 对于所有其他情况，请与您的网络管理员联系。  
  
#### <a name="enable-claims-to-windows-token-service"></a>启用 Claims to Windows Token Service  
  
1.  在管理中心的 "系统设置" 中，单击 "**管理服务器上的服务**"。  
  
2.  选择 **“Claims to Windows Token Service”**，然后单击 **“开始”**。  
  
3.  验证服务是否也在“服务”控制台上运行：  
  
    1.  在“管理工具”中，单击“服务”。  
  
    2.  如果 Claims to Windows Token Service 未运行，则启动它。  
  
## <a name="see-also"></a>另请参阅  
 [配置 PowerPivot 服务帐户](configure-power-pivot-service-accounts.md)  
  
  
