---
title: "Azure 数据湖存储连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 5acf2de3fccc2f5180358f87bd02591811c59c72
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 连接管理器
SQL Server Integration Services (SSIS) 包可以使用 Azure 数据湖存储连接管理器连接到 Azure 数据湖存储服务使用两个以下身份验证类型之一：
-   Azure AD 用户标识
-   Azure AD 服务标识 

Azure 数据湖存储连接管理器是一个组件的[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

>   [!NOTE]
> 若要确保 Azure Data Lake Store 连接管理器和使用它的组件（即 Azure Data Lake Store 源和 Azure Data Lake Store 目标）可连接到服务，请确保在 [此处](https://www.microsoft.com/download/details.aspx?id=49492)下载最新版本的 Azure 功能包。 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>配置 Azure Data Lake Store 连接管理器

1.  在**添加 SSIS 连接管理器**对话框中，选择**AzureDataLake**，然后选择**添加**。 **Azure 数据湖存储连接管理器编辑器**对话框随即打开。
  
2.  在**Azure 数据湖存储连接管理器编辑器**对话框中，在**ADLS 主机**字段中提供的 Azure 数据湖存储主机 URL。 例如：`https://test.azuredatalakestore.net`或`test.azuredatalakestore.net`。
  
3.  在**身份验证**字段中，选择要访问 Azure 数据湖存储中的数据的适当的身份验证类型。

    1.  如果你选择**Azure AD 用户标识**身份验证选项，请执行以下操作：
        1. 提供的值**用户名**和**密码**字段。 
    
        2. 若要测试连接，请选择**测试连接**。 如果你或租户管理员以前未同意允许 SSIS 要访问你的 Azure 数据湖存储数据，请选择**接受**出现提示时。 若要深入了解此同意体验，请参阅 [Integrating applications with Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application)（将应用程序与 Azure Active Directory 集成）。
    
        >   [!NOTE] 
        > 当选择**Azure AD 用户标识**不支持身份验证选项、 多因素身份验证和 Microsoft 帐户身份验证。
    
    2. 如果你选择**Azure AD 服务标识**身份验证选项，请执行以下操作：
        1. 创建 Azure Active Directory (AAD) 应用程序和服务主体来访问 Azure Data Lake 数据。
    
        2. 分配适当的权限，以便访问 Azure 数据湖资源此 AAD 应用程序。 若要深入此身份验证选项，请参阅 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)（使用门户创建可访问资源的 Active Directory 应用程序和服务主体）。
    
        3. 提供的值**客户端 Id**，**密钥**，和**租户名称**字段。
    
        4. 若要测试连接，请选择**测试连接**。  
  
6.  选择**确定**关闭**Azure 数据湖存储连接管理器编辑器**对话框。  
  
你可以看到你在“属性”  窗口中创建的连接管理器的属性。  
  
  
