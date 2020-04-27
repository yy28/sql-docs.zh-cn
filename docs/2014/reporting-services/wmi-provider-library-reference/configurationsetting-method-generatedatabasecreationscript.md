---
title: GenerateDatabaseCreationScript 方法（WMI MSReportServer_ConfigurationSetting） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseCreationScript method
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cf33e467e54fda5c29d81e3437730f0ce9547cad
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098510"
---
# <a name="generatedatabasecreationscript-method-wmi-msreportserver_configurationsetting"></a>GenerateDatabaseCreationScript 方法 (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="parameters"></a>parameters  
 *Databasename*  
 包含要创建的报表服务器数据库名称的字符串。  
  
 *Lcid*  
 用于角色名称本地化的值。  
  
 *IsSharePointMode*  
 指示是以本机模式还是以 SharePoint 模式创建数据库。  
  
> [!IMPORTANT]  
>  从开始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，不支持*IsSharePointMode* = `True` ，因为在 sharepoint 模式下[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，是 sharepoint 共享服务，且不受 WMI 提供程序的控制。 您应始终将此参数设置为 `False`。  
  
 *脚本*  
 [out] 包含所生成的 SQL 脚本的字符串。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 此方法将生成一个 SQL 脚本，创建适用于当前所连接的报表服务器版本的报表服务器数据库。  
  
 在 DatabaseName  参数中提供的值必须符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库命名约定。  
  
 生成脚本时，该方法不会检查该数据库是否存在。  
  
 生成脚本时，此方法不会检查报表服务器数据库是否存在。  
  
 生成的脚本支持 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
