---
title: 查找 SQL Server 2017 Reporting Services (SSRS) 的产品密钥 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: markingmyname
ms.author: maghan
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d02280799725420f2d9df3845034fe4deb91bea2
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285515"
---
# <a name="how-to-find-the-product-key-for-sql-server-2017-reporting-services"></a>如何查找 SQL Server 2017 Reporting Services 的产品密钥

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

了解如何查找 SQL Server 2017 Reporting Services (SSRS) 产品密钥，以便在生产环境中安装服务器。

要查找产品密钥，请首先下载并运行 SQL Server 2017 的安装程序。

1. 从以下某个源下载 SQL Server 2017：

    - 批量许可服务中心
    - MSDN 订阅
    - 零售（从 Microsoft Store 下载）

1. 运行 SQL Server 2017 安装程序，复制预填充的密钥：

    ![复制 SQL Server 2017 产品密钥](media/find-reporting-services-product-key-ssrs/ssrs-ss2017-copy-product-key.png)

1. [运行 Reporting Services 安装程序](install-reporting-services.md)，并粘贴该密钥：

     ![粘贴产品密钥](media/find-reporting-services-product-key-ssrs/ssrs-ssrs2017-paste-product-key.png)

只需在首次安装 SSRS 2017 时完成此步骤。 服务更新不需要输入密钥。

## <a name="related-information"></a>相关信息

- 有关安装 SQL Server Reporting Services 本机模式的详细信息，请参阅[安装 Reporting Services 本机模式报表服务器](install-reporting-services-native-mode-report-server.md)。 
- 有关在 SharePoint 集成模式下安装 SQL Server 2016 Reporting Services（及更早版本）的详细信息，请参阅[在 SharePoint 模式下安装第一个报表服务器](install-the-first-report-server-in-sharepoint-mode.md)。

## <a name="next-steps"></a>后续步骤

- [安装 SQL Server 2017 Reporting Services](install-reporting-services.md)
- 更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
