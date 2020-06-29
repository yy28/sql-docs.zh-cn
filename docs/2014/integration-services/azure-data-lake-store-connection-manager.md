---
title: Azure Data Lake Store 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSCM.F1
- SQL11.DTS.DESIGNER.AFPADLSCM.F1
ms.assetid: 7f1323f9-9dc3-4378-9c70-bbc65bfeabfd
author: yualan
ms.author: chugu
ms.openlocfilehash: 89278c4d6a099214a75f3c7898558f1f1ce4fd0c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439424"
---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 连接管理器
  **Azure Data Lake Store 连接管理器** 启用了 SSIS 包，该包通过以下两种身份验证类型连接到 Azure Data Lake Store 服务：Azure AD 用户标识和 Azure AD 服务标识。  

## <a name="configure-the-azure-data-lake-store-connection-manager"></a>配置 Azure Data Lake Store 连接管理器 
  
1.  在“添加 SSIS 连接管理器” **** 对话框中，选择“AzureDataLake” ****，然后单击“添加” ****。   
  
2.  在“Azure Data Lake Store 连接管理器编辑器”对话框的“ADLS 主机” **** 字段中，键入 Azure Data Lake Store 主机 URL。 例如： https： \/ /test.azuredatalakestore.net 或 test.azuredatalakestore.net。
  
3.  选择相应的身份验证类型来访问 Azure Data Lake Store 数据。

    1.  如果选择“Azure AD 用户标识” **** 身份验证选项，请执行以下操作：

        1. 为“用户名” **** 和“密码” **** 字段指定值。 
    
        2. 单击“测试连接” **** 以测试连接。 如果你和你的租户管理员先前不同意 SSIS 访问 Azure Data Lake Store 数据，则需在弹出对话框中单击“接受” **** 按钮，允许 SSIS 访问 Azure Data Lake Store 数据。 若要深入了解此同意体验，请参阅 [Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad)（将应用程序与 Azure Active Directory 集成）。
    
        > [!NOTE] 
        > “Azure AD 用户标识”身份验证选项不支持多重身份验证和 Microsoft 帐户。
    
    2.  如果选择“Azure AD 服务标识” **** 身份验证选项，请执行以下操作：
        1. 创建 AAD 应用程序和服务主体，使其可访问 Azure Data Lake 资源。
    
        2. 为此 AAD 应用程序分配相应权限，以便访问 Azure Data Lake 资源。 若要深入此身份验证选项，请参阅 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)（使用门户创建可访问资源的 Active Directory 应用程序和服务主体）。
    
        3. 为“客户端 ID” ****、“密钥” **** 和“租户名” **** 字段指定值。
    
        4. 单击“测试连接” **** 以测试连接。  
  
4.  单击“确定”  关闭对话框。  
  
    你可以看到你在“属性” **** 窗口中创建的连接管理器的属性。  
  
  
