---
title: 使用数字证书对包进行签名 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- digital signatures [Integration Services]
- signing packages [Integration Services]
- signatures [Integration Services]
ms.assetid: 182b115e-0fe2-4717-8dff-183f9eb6e397
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 31da686dbf25922205ea4d1b03ecaa3758457573
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055618"
---
# <a name="sign-a-package-by-using-a-digital-certificate"></a>使用数字证书对包签名
  本主题介绍如何使用数字证书对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包进行签名。 可以使用数字签名以及其他设置来防止加载和运行无效的包。  
  
 必须先执行下列任务才能对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包进行签名：  
  
-   创建或获取私钥以便与证书关联，并将此私钥存储在本地计算机上。  
  
-   以代码签名为目的从可信证书颁发机构获取证书。 可以使用下列方法之一来获取或创建证书：  
  
    -   从颁发证书的公共商业证书颁发机构获取证书。  
  
    -   从允许组织在内部颁发证书的证书服务器获取证书。 必须将用于对证书进行签名的根证书添加到 **“受信任的根证书颁发机构”** 存储区中。 若要添加根证书，可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理控制台 (MMC) 的证书管理单元。 有关详细信息，请参阅 MSDN 库中的主题“[Certificate Services](https://go.microsoft.com/fwlink/?LinkId=100755)（证书服务）”。  
  
    -   创建自己的证书（仅用于测试目的）。 证书创建工具 (Makecert.exe) 会生成仅用于测试目的的 X.509 证书。 有关详细信息，请参阅 MSDN Library 中的主题“[证书创建工具 (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)”。  
  
     有关证书的详细信息，请参阅证书管理单元的联机帮助。 有关如何对数字资产进行签名的详细信息，请参阅 MSDN 库中的主题“[Signing and Checking Code with Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)（使用 Authenticode 签名和检查代码）”。  
  
-   确保已为代码签名启用证书。 若要确定证书是否是为代码签名而启用的，请在“证书”管理单元中检查证书的属性。  
  
-   将证书存储在个人存储区中。  
  
 完成上述任务后，即可使用下列过程对包进行签名。  
  
### <a name="to-sign-a-package"></a>签署包  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要签名的包所在的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器的 **“SSIS”** 菜单上，单击 **“数字签名”**。  
  
4.  在 **“数字签名”** 对话框中，单击 **“签名”**。  
  
5.  在 **“选择证书”** 对话框中，选择一个证书。  
  
6.  也可单击“查看证书”**** 来查看证书信息。  
  
7.  单击 **“确定”** 关闭 **“选项证书”** 对话框。  
  
8.  单击 **“确定”** 关闭 **“数字签名”** 对话框。  
  
9. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
     虽然已对包进行了签名，您现在必须配置 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，以便在加载该包之前检查或验证数字签名。 有关详细信息，请参阅 [使用数字签名标识包的源](security/identify-the-source-of-packages-with-digital-signatures.md)。  
  
## <a name="see-also"></a>另请参阅  
 [安全性概述 (Integration Services)](security/security-overview-integration-services.md)  
  
  
