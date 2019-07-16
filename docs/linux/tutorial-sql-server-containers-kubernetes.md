---
title: 部署 SQL Server 容器在 Kubernetes 中使用 Azure Kubernetes 服务 (AKS)
description: 本教程演示如何部署 SQL Server 高可用性解决方案与 Azure Kubernetes 服务上的 Kubernetes。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: mvc
ms.technology: linux
ms.openlocfilehash: 2ae299553c700de7f22976917fa8556f93dbe61b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032049"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>部署 SQL Server 容器在 Kubernetes 中使用 Azure Kubernetes 服务 (AKS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

了解如何使用持久性存储区以实现高可用性 (HA) 在 Kubernetes 中 Azure Kubernetes 服务 (AKS) 上配置 SQL Server 实例。 该解决方案提供复原能力。 如果 SQL Server 实例失败，Kubernetes 会自动重新创建该新 pod 中。 Kubernetes 还提供了针对节点故障的复原能力。

本教程演示如何在 AKS 上的容器中配置高度可用的 SQL Server 实例。 此外可以创建[Always On 可用性组的 SQL Server 容器](sql-server-ag-kubernetes.md)。 若要比较两个不同的 Kubernetes 解决方案，请参阅[SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)。

> [!div class="checklist"]
> * 创建的 SA 密码
> * 创建存储
> * 创建部署
> * 使用 SQL Server Management Studio (SSMS) 连接
> * 验证故障与恢复

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>在 Azure Kubernetes 服务中运行的 Kubernetes 上的 HA 解决方案

Kubernetes 版本 1.6 和更高版本已支持[存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)，[永久性卷声明](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，并[Azure 磁盘的卷类型](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)。 您可以创建和管理 SQL Server 实例以本机方式在 Kubernetes 中。 此文章中的示例演示如何创建[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)来实现类似于共享的磁盘故障转移群集实例的高可用性配置。 在此配置中，Kubernetes 充当群集协调器的角色。 当在容器中的 SQL Server 实例失败时，业务流程协调程序会引导将附加到相同的持久性存储的容器的另一个实例。

![Kubernetes SQL Server 群集的关系图](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上图中，`mssql-server`是中的容器[pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/)。 Kubernetes 会协调群集中的资源。 一个[副本集](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可确保在节点发生故障后自动恢复 pod。 应用程序连接到服务。 在这种情况下，该服务表示承载的发生故障后保持不变的 IP 地址的负载均衡器`mssql-server`。

在下图中，`mssql-server`容器已失败。 作为业务流程协调程序，Kubernetes 可保证正确的副本中的正常实例数设置，并启动根据配置的新容器。 业务流程协调程序在同一节点上启动新 pod 和`mssql-server`重新连接到相同的持久存储。 该服务连接到重新创建`mssql-server`。

![Kubernetes SQL Server 群集的关系图](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

在下图中，节点承载`mssql-server`容器已失败。 业务流程协调程序的不同节点上启动新的 pod 和`mssql-server`重新连接到相同的持久存储。 该服务连接到重新创建`mssql-server`。

![Kubernetes SQL Server 群集的关系图](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>先决条件

* **Kubernetes 群集**
   - 本教程需要 Kubernetes 群集。 这些步骤会用[kubectl](https://kubernetes.io/docs/user-guide/kubectl/)群集进行管理。 

   - 请参阅[部署 Azure 容器服务 (AKS) 群集](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster)若要创建并连接到与 AKS 中的单节点 Kubernetes 群集`kubectl`。 

   >[!NOTE]
   >若要针对节点故障提供保护，Kubernetes 群集需要多个节点。

* **Azure CLI 2.0.23**
   - 针对 Azure CLI 2.0.23 验证了在本教程中的说明进行操作。

## <a name="create-an-sa-password"></a>创建的 SA 密码

在 Kubernetes 群集中创建的 SA 密码。 Kubernetes 可以管理敏感配置信息，如密码作为[机密](https://kubernetes.io/docs/concepts/configuration/secret/)。

以下命令创建 SA 帐户的密码：

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   替换为`MyC0m9l&xP@ssw0rd`使用复杂密码。

   若要在名为 Kubernetes 中创建的机密`mssql`保留值`MyC0m9l&xP@ssw0rd`为`SA_PASSWORD`，运行命令。


## <a name="create-storage"></a>创建存储

配置[永久性卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)并[永久性卷声明](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection)的 Kubernetes 群集中。 完成以下步骤： 

1. 创建清单来定义的存储类和永久性卷声明。  该清单指定存储预配程序，参数，并[回收策略](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)。 Kubernetes 群集使用此清单创建的永久性存储。 

   下面的 yaml 示例定义一个存储类和永久性卷声明。 存储类预配程序是`azure-disk`，因为此 Kubernetes 群集是在 Azure 中。 存储帐户类型是`Standard_LRS`。 永久性卷声明名为`mssql-data`。 永久性卷声明元数据包括批注连接回存储类。 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   保存该文件 (例如， **pvc.yaml**)。

1. 在 Kubernetes 中创建永久性卷声明。

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` 是保存该文件的位置。

   永久性卷自动作为 Azure 存储帐户，创建并绑定到永久性卷声明。 

    ![永久性卷声明命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 验证永久性卷声明。

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` 是永久性卷声明的名称。

   在前面步骤中，名为永久性卷声明`mssql-data`。 若要查看有关永久性卷声明的元数据，请运行以下命令：

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   返回的元数据包括名为的值`Volume`。 此值映射到的 blob 的名称。

   ![返回的元数据，包括卷的屏幕截图](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   卷的值匹配以下映像从 Azure 门户中的 blob 的名称的部分： 

   ![屏幕截图显示 Azure 门户的 blob 名称](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 验证永久性卷。

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` 返回有关已自动创建并绑定到永久性卷声明的永久性卷的元数据。 

## <a name="create-the-deployment"></a>创建部署

在此示例中，托管 SQL Server 实例的容器被描述为 Kubernetes 部署对象。 部署创建的副本集。 副本集创建 pod。 

在此步骤中，创建一个清单来描述基于 SQL Server 容器[mssql server linux](https://hub.docker.com/_/microsoft-mssql-server) Docker 映像。 清单的引用`mssql-server`永久性卷声明和`mssql`已应用于 Kubernetes 群集的机密。 清单还描述[服务](https://kubernetes.io/docs/concepts/services-networking/service/)。 此服务是负载均衡器。 负载均衡器可确保 IP 地址后恢复 SQL Server 实例仍存在。 

1. 创建清单 （YAML 文件） 来描述部署。 下面的示例介绍了部署，包括基于 SQL Server 容器映像的容器。

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server:2017-latest
           ports:
           - containerPort: 1433
           env:
           - name: MSSQL_PID
             value: "Developer"
           - name: ACCEPT_EULA
             value: "Y"
           - name: MSSQL_SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   将上面的代码复制到新文件，名为`sqldeployment.yaml`。 更新以下值： 

   * MSSQL_PID `value: "Developer"`:设置要运行的 SQL Server Developer edition 的容器。 开发人员版未获得许可的生产数据。 如果部署适用于生产环境中使用，请设置相应的版本 (`Enterprise`， `Standard`，或`Express`)。 

      >[!NOTE]
      >有关详细信息，请参阅[授权的 SQL Server 如何](https://www.microsoft.com/sql-server/sql-server-2017-pricing)。

   * `persistentVolumeClaim`：此值需要为一个条目`claimName:`，它映射到的永久性卷声明使用的名称。 本教程使用`mssql-data`。 

   * `name: SA_PASSWORD`：将容器映像设置 SA 密码配置为在本部分中定义。

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     在 Kubernetes 部署容器，它引用名为的机密`mssql`要获取其值的密码。 

   >[!NOTE]
   >通过使用`LoadBalancer`服务类型的 SQL Server 实例是否可访问远程 （通过 internet) 在端口 1433年。

   保存该文件 (例如， **sqldeployment.yaml**)。

1. 创建部署。

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` 是保存该文件的位置。

   ![部署命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   创建的部署和服务。 SQL Server 实例是在连接到持久性存储区的容器中。

   若要查看 pod 的状态，请键入`kubectl get pod`。

   ![Get pod 命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   在上图中，pod 的状态为`Running`。 此状态指示容器已准备。 这可能需要几分钟的时间。

   >[!NOTE]
   >创建部署后，它可能需要几分钟之后是可见的 pod。 延迟是因为群集中拉取[mssql server linux](https://hub.docker.com/_/microsoft-mssql-server)从 Docker hub 映像。 第一次拉取映像后，后续部署可能更快，如果部署到已有图像缓存在其上的节点。 

1. 验证服务正在运行。 运行下面的命令：

   ```azurecli
   kubectl get services 
   ```

   此命令将返回正在运行的服务，以及服务的内部和外部 IP 地址。 请注意的外部 IP 地址`mssql-deployment`服务。 使用此 IP 地址连接到 SQL Server。 

   ![获取服务命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Kubernetes 群集中的对象的状态的详细信息，请运行：

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>连接到 SQL Server 实例

如果所述配置容器，你可以使用从 Azure 虚拟网络外部的应用程序进行连接。 使用`sa`帐户和外部 IP 地址为服务。 使用 Kubernetes 机密作为配置的密码。 

可以使用以下应用程序连接到 SQL Server 实例。 

* [SSMS](https://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   若要使用连接`sqlcmd`，运行以下命令：

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   替换为以下值：
      
    - `<External IP Address>` 使用的 IP 地址`mssql-deployment`服务 
    - `MyC0m9l&xP@ssw0rd` 用您的密码

## <a name="verify-failure-and-recovery"></a>验证故障与恢复

若要验证的故障与恢复，可以删除 pod。 执行以下步骤操作：

1. 列出运行 SQL Server 的 pod。

   ```azurecli
   kubectl get pods
   ```

   记下运行 SQL Server pod 的名称。

1. 删除 pod。

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` 上一步骤中的 pod 名称返回的值。 

Kubernetes 会自动重新创建 pod 中恢复的 SQL Server 实例，并连接到持久性存储。 使用`kubectl get pods`以验证部署新的 pod。 使用`kubectl get services`以验证新的容器的 IP 地址是否相同。 

## <a name="summary"></a>总结

在本教程中，您学习了如何将 SQL Server 容器部署到 Kubernetes 群集以实现高可用性。 

> [!div class="checklist"]
> * 创建的 SA 密码
> * 创建存储
> * 创建部署
> * 使用 SQL Server Management Studio (SSMS) 连接
> * 验证故障与恢复

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
>[Kubernetes 简介](https://docs.microsoft.com/azure/aks/intro-kubernetes)


