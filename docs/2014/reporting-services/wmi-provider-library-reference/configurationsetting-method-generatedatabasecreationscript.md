---
title: GenerateDatabaseCreationScript 方法 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseCreationScript method
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
caps.latest.revision: 25
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 05560854358e95ce4beae1727e8c1aeb7be131d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016294"
---
# <a name="generatedatabasecreationscript-method-wmi-msreportserverconfigurationsetting"></a>GenerateDatabaseCreationScript 方法 (WMI MSReportServer_ConfigurationSetting)
  生成可用于创建报表服务器数据库的 SQL 脚本。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub GenerateDatabaseCreationScript(ByVal DatabaseName As String, _  
    ByVal Lcid As Int32, ByVal IsSharePointMode As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseCreationScript(string DatabaseName, Int32 Lcid,   
    Boolean IsSharePointMode, out string Script, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *Databasename*  
 包含要创建的报表服务器数据库名称的字符串。  
  
 *Lcid*  
 用于角色名称本地化的值。  
  
 *IsSharePointMode*  
 指示是以本机模式还是以 SharePoint 模式创建数据库。  
  
> [!IMPORTANT]  
>  从[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， *IsSharePointMode* = `True`不支持，因为在 SharePoint 模式下，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]是 SharePoint 共享服务，不控制的 WMI 提供程序。 你应始终将此参数设置为`False`。  
  
 *脚本*  
 [out] 包含所生成的 SQL 脚本的字符串。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 此方法将生成一个 SQL 脚本，创建适用于当前所连接的报表服务器版本的报表服务器数据库。  
  
 在 DatabaseName 参数中提供的值必须符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库命名约定。  
  
 生成脚本时，该方法不会检查该数据库是否存在。  
  
 生成脚本时，此方法不会检查报表服务器数据库是否存在。  
  
 生成的脚本支持 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  