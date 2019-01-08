---
title: 通过设置注册表值实现签名策略 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing policies [Integration Services]
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8daa6582f18d9c5279e7539dd9c3740d90e36d2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353199"
---
# <a name="implement-a-signing-policy-by-setting-a-registry-value"></a>通过设置注册表值实现签名策略
  使用可选的注册表值可以管理组织用于加载签名包和未签名包的策略。 如果使用此注册表值，则必须在将运行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包以及将强制实施该策略的每台计算机上创建此注册表值。 设置该注册表值后， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将在加载包之前检查或验证签名。  
  
 本主题中的此过程将介绍如何将可选的 `BlockedSignatureStates` DWORD 值添加到 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS 注册表项中。 `BlockedSignatureStates` 中的数据值决定当包具有不可信签名、具有无效签名或未签名时是否阻止该包。 对于用来进行包签名的签名的状态，`BlockedSignatureStates` 注册表值使用下列定义：  
  
-   “有效签名”  是一个可以成功读取的签名。  
  
-   “无效签名”是一个解密的校验和（由私钥加密的包代码的单向哈希）与在加载 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的过程中计算的解密校验和不相符的签名。  
  
-   “可信签名”  是一个使用由受信任的根证书颁发机构签名的数字证书创建的签名。 该设置不要求签名者出现在可信发布服务器的用户列表中。  
  
-   “不可信签名  ”是一个不能验证为由受信任的根证书颁发机构颁发的签名，或不是最新版本的签名。  
  
 下表列出了 DWORD 数据的有效值及其相关策略。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0|无管理限制。|  
|1|阻止无效签名。<br /><br /> 该设置不阻止未签名的包。|  
|2|阻止无效签名和不可信签名。<br /><br /> 该设置不阻止未签名的包，但会阻止自我生成的签名。|  
|3|阻止无效签名、不可信签名以及未签名的包<br /><br /> 该设置也阻止自我生成的签名。|  
  
> [!NOTE]  
>  `BlockedSignatureStates` 的建议设置为 3。 该设置提供针对未签名包或者无效或不可信签名的最强保护功能。 不过，建议的设置并非适用于所有情况。 有关如何进行数字资产签名的详细信息，请参阅 MSDN Library 中的主题“[Introduction to Code Signing](https://go.microsoft.com/fwlink/?LinkId=51414)（代码签名简介）”。  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>实现包的签名策略  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。  
  
2.  在运行对话框中，键入`Regedit`，然后单击**确定**。  
  
3.  找到注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS。  
  
4.  右键单击“MSDTS”，指向“新建”，然后单击“DWORD 值”。  
  
5.  将新值的名称更新为 `BlockedSignatureStates`。  
  
6.  右键单击`BlockedSignatureStates`然后单击**修改**。  
  
7.  在 **“编辑 DWORD 值”** 对话框中，键入值 0、1、2 或 3。  
  
8.  单击“确定” 。  
  
9. 在 **“文件”** 菜单中，单击 **“退出”**。  
  
## <a name="see-also"></a>请参阅  
 [安全性概述 (Integration Services)](security/security-overview-integration-services.md)   
 [使用数字签名标识包的源](security/identify-the-source-of-packages-with-digital-signatures.md)  
  
  
