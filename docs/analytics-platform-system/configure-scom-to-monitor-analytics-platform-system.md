---
title: 配置 SCOM 以监视 Analytics Platform System |Microsoft Docs
description: 按照以下步骤来为分析平台系统配置 System Center Operations Manager (SCOM) 管理包。 监视 SCOM 中的分析平台系统所需的管理包。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2dae92263d7be76490a51ea7027f79ab5fcd6118
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509696"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>配置 System Center Operations Manager (SCOM) 以监视 Analytics Platform System
按照以下步骤来为分析平台系统配置 System Center Operations Manager (SCOM) 管理包。 监视 SCOM 中的分析平台系统所需的管理包。  
  
## <a name="BeforeBegin"></a>开始之前  
**先决条件**  
  
System Center Operations Manager 2007 R2 必须安装并正在运行。  
  
必须安装和配置管理包。 请参阅[安装的 SCOM 管理包&#40;分析平台系统&#41;](install-the-scom-management-packs.md)并[导入 SCOM 管理包为 PDW&#40;分析平台系统&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
## <a name="ConfigureRunAsProfile"></a>在 System Center 配置运行方式配置文件  
若要配置 System Center，您必须执行以下步骤：  
  
-   创建运行方式帐户用于**APS 观察程序**域用户并将其映射到**APS 观察程序的 Microsoft 帐户。**  
  
-   创建运行方式帐户用于**monitoring_user** APS 用户并将其映射到**Microsoft APS 操作帐户**。  
  
下面是如何执行任务的详细的说明：  
  
1.  创建**APS 观察程序**与运行方式帐户**Windows**账户类型**APS 观察程序**域用户。  
  
    1.  导航到**Administration**窗格中，右键单击**运行方式配置** -> **帐户**，然后选择**创建运行方式帐户...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  **创建运行方式帐户向导**对话框将打开。 上**简介**页上，单击**下一步**。  
  
    3.  上**常规属性**页上，选择**Windows**从**运行方式帐户类型**和"AP 观察程序"指定为**显示名称**。  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  上**凭据**页上， ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  上**分发安全**页上，选择**安全级别较低**然后单击**创建**按钮即可完成。  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  如果您决定使用**更安全**选项，则必须手动指定凭据将分发到计算机。 为此，请在创建运行方式帐户后，右键单击它并选择**属性**。  
  
        2.  导航到**分发**选项卡和**添加**所需的计算机。  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  设置**APS 观察程序的 Microsoft 帐户**配置文件以使用**APS 观察程序**运行方式帐户。  
  
    1.  导航到**Administration** -> **运行方式配置** -> **配置文件**。  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  右键单击**APS 观察程序的 Microsoft 帐户**从该列表，然后选择**属性**。  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  **运行方式配置文件向导**对话框将打开。 跳过**简介**通过单击页面**下一步**。  
  
    4.  上**常规属性**页上，单击**下一步**。  
  
    5.  上**运行方式帐户**页上，单击**添加...** 按钮，然后选择以前创建**APS 观察程序**运行方式帐户。  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  单击**保存**完成分配配置文件。  
  
3.  等到发现完成 APS 设备。  
  
    1.  导航到**监视**窗格，然后打开**SQL Server 设备** -> **Microsoft Analytics Platform System**  ->  **设备**状态视图。  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  等待，直到该设备将显示在列表中。 设备的名称应为等于 1 在注册表中指定。 发现完成后，你应看到列出，但不是受监视的所有设备。 若要启用监视，请执行后续步骤。  
  
    > [!NOTE]  
    > 在等待初始设备发现完成时，可以并行完成后续步骤。  
  
4.  创建查询 AP 的运行状况数据检索到的另一个新运行方式帐户。  
  
    1.  开始创建新的运行方式帐户，在步骤 1 中所述。  
  
    2.  上**常规属性**页上，选择**基本身份验证**帐户类型。  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  上**凭据**页上，提供有效凭据访问 APS 运行状况状态 Dmv。  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  配置**Microsoft APS 操作帐户**新创建的运行方式帐户用于 APS 实例配置文件。  
  
    1.  导航到**Microsoft APS 操作帐户**属性在步骤 2 中所述。  
  
    2.  上**运行方式帐户**页上，单击**添加...** 和 
    3.  选择新创建的运行方式帐户。  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>下一步  
现在，已配置的管理包，已准备好开始监视该设备。 有关详细信息，请参阅[监视使用 System Center Operations Manager 通过设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
