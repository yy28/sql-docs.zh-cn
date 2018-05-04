---
title: 在 Kubernetes 中配置 SQL Server 容器，以实现高可用性 |Microsoft 文档
description: 本教程演示如何部署具有 Kubernetes Azure 容器服务上的 SQL Server 高可用性解决方案。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux,mvc
ms.technology: database-engine
ms.openlocfilehash: e32e15da21bf9da2a16fc221ac8f8342d844036b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="configure-a-sql-server-container-in-kubernetes-for-high-availability"></a>在 Kubernetes 中配置 SQL Server 容器，以实现高可用性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

了解如何使用持久存储以实现高可用性 (HA) Kubernetes 中 Azure 容器服务 (AKS) 上配置的 SQL Server 实例。 解决方案提供复原能力。 如果 SQL Server 实例失败，Kubernetes 自动重新创建它在一个新的组合。 AKS 提供从 Kubernetes 节点故障中的复原。 

本教程演示如何在使用 AKS 的容器中配置高可用的 SQL Server 实例。 

> [!div class="checklist"]
> * 创建一个 SA 密码
> * 创建存储
> * 创建部署
> * 使用 SQL Server Management Studio (SSMS) 连接
> * 验证故障与恢复

## <a name="ha-solution-that-uses-kubernetes-running-in-azure-container-service"></a>HA 解决方案，它使用 Kubernetes Azure 容器服务中运行

Kubernetes 1.6 及更高版本具有对支持[存储类](http://kubernetes.io/docs/concepts/storage/storage-classes/)，[持久卷声明](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，和[Azure 磁盘的卷类型](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)。 你可以创建和管理 SQL Server 实例以本机方式在 Kubernetes。 此文章中的示例演示如何创建[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)以实现高可用性配置类似于共享的磁盘故障转移群集实例。 在此配置中，Kubernetes 充当群集 orchestrator 的角色。 当容器中的 SQL Server 实例失败时，orchestrator 将启动另一个实例将附加到的相同的持久存储的容器。

![Kubernetes SQL Server 群集的图示](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在前面的图中，`mssql-server`是一个容器[pod](http://kubernetes.io/docs/concepts/workloads/pods/pod/)。 Kubernetes 编排群集中的资源。 A[副本集](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可确保在节点故障后自动恢复 pod。 应用程序连接到服务。 在这种情况下，服务就表示承载发生故障后将保持不变的 IP 地址的负载平衡器`mssql-server`。

在下图中，`mssql-server`容器已失败。 为 orchestrator，Kubernetes 可保证正确副本中的正常实例数设置，并将启动根据配置一个新容器。 Orchestrator 的同一节点上启动一个新的组合和`mssql-server`重新连接到相同的持久存储。 服务连接到重新创建`mssql-server`。

![Kubernetes SQL Server 群集的图示](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

在下图中，节点承载`mssql-server`容器已失败。 Orchestrator 的不同节点上启动新的 pod 和`mssql-server`重新连接到相同的持久存储。 服务连接到重新创建`mssql-server`。

![Kubernetes SQL Server 群集的图示](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>必要條件

* **Kubernetes 群集**
   - 本教程需要实现 Kubernetes 群集。 这些步骤将使用[kubectl](https://kubernetes.io/docs/user-guide/kubectl/)将群集进行管理。 

   - 请参阅[部署 Azure 容器服务 (AKS) 群集](http://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster)创建并连接到单节点 Kubernetes 群集中使用的 AKS `kubectl`。 

   >[!NOTE]
   >若要针对节点故障提供保护，实现 Kubernetes 群集需要多个节点。

* **Azure CLI 2.0.23**
   - 已对 Azure CLI 2.0.23 验证了在本教程中的说明进行操作。

## <a name="create-an-sa-password"></a>创建一个 SA 密码

在实现 Kubernetes 群集创建 SA 密码。 Kubernetes 可以管理敏感的配置信息，如密码作为[机密](http://kubernetes.io/docs/concepts/configuration/secret/)。

以下命令创建 SA 帐户的密码：

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   替换`MyC0m9l&xP@ssw0rd`使用复杂密码。

   若要在名为的 Kubernetes 中创建一个机密`mssql`保存值`MyC0m9l&xP@ssw0rd`为`SA_PASSWORD`，运行命令。


## <a name="create-storage"></a>创建存储

配置[持久卷](http://kubernetes.io/docs/concepts/storage/persistent-volumes/)和[持久卷声明](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection)Kubernetes 群集中。 完成以下步骤： 

1. 创建清单定义的存储类和持久性卷声明。  清单指定存储部署，参数，和[回收策略](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)。 Kubernetes 群集使用此清单来创建持久性存储区。 

   下面的 yaml 示例定义一个存储类和持久性卷声明。 存储类设置程序是`azure-disk`，因为此实现 Kubernetes 群集是在 Azure 中。 存储帐户类型是`Standard_LRS`。 持久卷声明名为`mssql-data`。 持久卷声明元数据包括批注连接回存储类。 

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

1. 在 Kubernetes 中创建的永久性卷声明。

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` 保存该文件的位置。

   持久的卷上自动创建为 Azure 存储帐户，并绑定到持久卷声明。 

    ![持久卷声明命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. 验证持久卷声明。

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` 是持久的卷声明的名称。

   在前面的步骤中，名为持久卷声明`mssql-data`。 若要查看有关持久性卷声明的元数据，请运行以下命令：

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   返回的元数据包括名为的值`Volume`。 此值将映射到的 blob 的名称。

   ![返回的元数据，包括卷的屏幕截图](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   卷的值匹配在下图中从 Azure 门户的 blob 的名称的一部分： 

   ![屏幕快照的 Azure 门户的 blob 名称](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. 验证持久的卷。

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` 返回有关的持久的卷的自动创建并绑定到持久卷声明的元数据。 

## <a name="create-the-deployment"></a>创建部署

在此示例中，托管 SQL Server 实例的容器被描述为实现 Kubernetes 部署对象。 部署创建一个副本集。 副本集创建 pod。 

在此步骤中，创建一个清单来描述基于 SQL Server 的容器[mssql server linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) Docker 映像。 清单引用`mssql-server`持久卷声明和`mssql`已应用于实现 Kubernetes 群集的机密。 该清单还将描述[服务](http://kubernetes.io/docs/concepts/services-networking/service/)。 将此服务的负载平衡器。 负载平衡器可确保 IP 地址恢复 SQL Server 实例之后，仍然存在。 

1. 创建清单 （YAML 文件） 来描述部署。 下面的示例描述的部署，包括基于 SQL Server 容器映像的容器。

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
           image: microsoft/mssql-server-linux
           ports:
           - containerPort: 1433
           env:
           - name: ACCEPT_EULA
             value: "Y"
           - name: SA_PASSWORD
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

   * `value: "Developer"`： 设置要运行 SQL Server Developer 版的容器。 生产数据未获授权开发人员版。 如果部署为生产环境中使用，设置适当的版本 (`Enterprise`， `Standard`，或`Express`)。 

      >[!NOTE]
      >有关详细信息，请参阅[许可证 SQL Server 如何](http://www.microsoft.com/sql-server/sql-server-2017-pricing)。

   * `persistentVolumeClaim`： 此值需要的条目`claimName:`映射到用于持久卷声明的名称。 本教程使用`mssql-data`。 

   * `name: SA_PASSWORD`： 此节中定义配置设置 SA 密码的容器映像。

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     当 Kubernetes 部署容器时，它引用名为的机密`mssql`来获取的值的密码。 

   >[!NOTE]
   >通过使用`LoadBalancer`服务类型的 SQL Server 实例是否可访问远程 （通过 internet) 在端口 1433年。

   保存该文件 (例如， **sqldeployment.yaml**)。

1. 创建部署。

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` 保存该文件的位置。

   ![部署命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   创建的部署和服务。 SQL Server 实例是在容器中，连接到持久性存储区。

   若要查看的 pod 的状态，请键入`kubectl get pod`。

   ![Get pod 命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   状态已在前面的图中，从盒`Running`。 此状态指示容器已准备。 这可能需要几分钟的时间。

   >[!NOTE]
   >创建部署后，可能需要几分钟 pod 才会显示。 延迟是因为群集拉取[mssql server linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)从 Docker hub 映像。 第一次拉取映像后，后续的部署可能更快，如果部署到已在其上缓存的映像的节点。 

1. 验证服务正在运行。 运行以下命令：

   ```azurecli
   kubectl get services 
   ```

   此命令将返回正在运行的服务以及服务的内部和外部 IP 地址。 请注意的外部 IP 地址`mssql-deployment`服务。 使用此 IP 地址连接到 SQL Server。 

   ![获取服务命令的屏幕截图](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Kubernetes 群集中的对象的状态的详细信息，请运行：

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>连接到 SQL Server 实例

如果所述配置容器，你可以使用应用程序从 Azure 虚拟网络外部进行连接。 使用`sa`为服务帐户和外部 IP 地址。 使用配置作为 Kubernetes 机密的密码。 

以下应用程序可用于连接到 SQL Server 实例。 

* [SSMS](http://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssms)

* [SSDT](http://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   若要使用连接`sqlcmd`，运行以下命令：

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   替换以下值：
      
    - `<External IP Address>` 具有的 IP 地址的`mssql-deployment`服务 
    - `MyC0m9l&xP@ssw0rd` 用您的密码

## <a name="verify-failure-and-recovery"></a>验证故障与恢复

若要验证的故障与恢复，你可以删除 pod。 请执行以下步骤操作：

1. 列出运行 SQL Server pod。

   ```azurecli
   kubectl get pods
   ```

   记下运行 SQL Server pod 的名称。

1. 删除 pod。

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` 从上一步 pod 名称返回的值。 

Kubernetes 自动重新创建 pod 恢复的 SQL Server 实例，并连接到持久性存储区。 使用`kubectl get pods`以验证部署一个新的组合。 使用`kubectl get services`以验证新的容器的 IP 地址是否相同。 

## <a name="summary"></a>“摘要”

在本教程中，您学习了如何将 SQL Server 容器部署到 Kubernetes 群集以实现高可用性。 

> [!div class="checklist"]
> * 创建一个 SA 密码
> * 创建存储
> * 创建部署
> * 使用 SQL Server Management Studio (SSMS) 进行连接
> * 验证故障与恢复

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
>[Kubernetes 简介](http://docs.microsoft.com/en-us/azure/aks/intro-kubernetes)


