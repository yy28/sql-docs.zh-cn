---
title: 导入 SCOM 管理包的分析平台系统 |Microsoft Docs
description: 按照以下步骤导入 System Center Operations Manager (SCOM) 管理包 Analytics Platform System (APS)。 监视 SCOM 中的并行数据仓库所需的管理包。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c4280fb257147f3c401badc6eaec18929f6d69b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149692"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>导入 SCOM 管理包中的分析平台系统
按照以下步骤导入 System Center Operations Manager (SCOM) 管理包 Analytics Platform System (APS)。 监视 SCOM 中的并行数据仓库所需的管理包。 
  
## <a name="BeforeBegin"></a>开始之前  
**先决条件**  
  
System Center Operations Manager 2007 R2 必须安装并正在运行。  
  
必须安装管理包。 请参阅[安装的 SCOM 管理包&#40;分析平台系统&#41;](install-the-scom-management-packs.md)。  
  
## <a name="Step1"></a>步骤 1:导入 SQL Server 设备基础管理包  
  
1.  登录到该帐户是 Operations Manager 2007 管理组的 Operations Manager 管理员角色的成员的计算机上。  
  
2.  在操作控制台中，单击**管理**。  
  
3.  右键单击**管理包**节点，并单击**导入管理包**。  
  
    ![单击导入管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  在管理包列表中，选择你想要导入，请单击管理包**选择**，然后单击**添加**。  
  
    ![管理包列表](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  搜索**装置**以及然后向下钻取到 SQL Server 设备库，然后单击**添加**的两种选择。  
  
    ![SQL Server 工具库](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  后两个管理包已在所选窗格的底部，然后单击**确定**。  
  
    ![选择这两个管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  单击 **“安装”**。  
  
    ![单击安装](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完成后，单击**关闭**。  
  
    ![完成后，单击关闭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Microsoft SQL Server 2008 R2 并行数据仓库设备导入监视包  
  
1.  右键单击**管理包**节点，并单击**导入管理包**。  
  
2.  选择**从磁盘中的添加**...  
  
    ![右键单击管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  转到解压缩 SQL Server PDW 管理包的位置并选择"所选管理包导入"部分中的三个管理包。 可以通过选择第一个中，单击 shift 键，并选择最后一个执行此操作。 它们全部选中后，单击**打开**。  
  
    ![选择管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  单击 **“安装”**。  
  
    ![单击安装](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  单击 **“关闭”**。  
  
    ![单击关闭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>下一步  
现在，导入管理包之后，继续下一步：[配置 SCOM 以监视 Analytics Platform System&#40;分析平台系统&#41;](configure-scom-to-monitor-analytics-platform-system.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
