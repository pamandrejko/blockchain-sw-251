---

copyright:
  years: 2018, 2021
lastupdated: "2021-01-07"

keywords: IBM Blockchain Platform console, deploy, resource requirements, storage, parameters, multicloud

subcollection: blockchain-sw-251

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Deploying {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1
{: #deploy-k8}

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="/docs/blockchain-sw?topic=blockchain-sw-deploy-k8">2.1.2</a>,
    <a href="/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-k8">2.1.3</a>,
    <a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-deploy-k8">2.5</a>
    </p>
</div>


You can use the following instructions to deploy the {{site.data.keyword.blockchainfull}} Platform 2.5.1 on any x86_64 Kubernetes cluster running at v1.16 - v1.19 or on s390x on OpenShift Container Platform running LinuxONE. The {{site.data.keyword.blockchainfull_notm}} Platform uses a [Kubernetes Operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/){: external} to install the {{site.data.keyword.blockchainfull_notm}} Platform console on your cluster and manage the deployment and your blockchain nodes. When the {{site.data.keyword.blockchainfull_notm}} Platform console is running on your cluster, you can use the console to create blockchain nodes and operate a multicloud blockchain network.
{:shortdesc}

## Resources required
{: #deploy-k8-resources-required}

Ensure that your Kubernetes cluster has sufficient resources for the {{site.data.keyword.blockchainfull_notm}} Platform console and for the blockchain nodes that you create. The amount of resources that are required can vary depending on your infrastructure, network design, and performance requirements. To help you deploy a cluster of the appropriate size, the default CPU, memory, and storage requirements for each component type are provided in this table. Your actual resource allocations are visible in your blockchain console when you deploy a node and can be adjusted at deployment time or after deployment according to your business needs.

The resources for the CA, peer, and ordering nodes need to be multiplied by the number of these nodes that you require. The operator and console resources are per blockchain deployment. For example, if you deployed development, staging, and test networks in a single cluster, you need to have enough resources for three instances of the operator and console, one for each blockchain deployment. On the other hand, the webhook resources are per Kubernetes cluster, only one instance is required, regardless of the number of blockchain networks in the cluster.

| **Component** (all containers) | CPU**  | Memory (GB) | Storage (GB) |
|--------------------------------|---------------|-----------------------|------------------------|
| **Peer (Hyperledger Fabric v1.4)**                       | 1.1           | 2.8                   | 200 (includes 100GB for peer and 100GB for state database)|
| **Peer (Hyperledger Fabric v2.x)**                       | 0.7           | 2.0                   | 200 (includes 100GB for peer and 100GB for state database)|
| **CA**                         | 0.1           | 0.2                   | 20                     |
| **Ordering node**              | 0.35          | 0.7                   | 100                    |
| **Operator**                   | 0.1           | 0.2                   | 0                      |
| **Console**                    | 1.2           | 2.4                   | 10                     |
| **Webhook**                    | 0.1           | 0.2                   | 0                      |
{: caption="Table 1. Default resource allocations" caption-side="bottom"}
** These values can vary slightly. Actual VPC allocations are visible in the blockchain console when a node is deployed.

Note that when smart contracts are installed on peers that run a Fabric v2.x image, the smart contract is launched in its own pod instead of a separate container on the peer, which accounts for the smaller amount of resources required on the peer.

## Browsers
{: #deploy-k8-browsers}
The {{site.data.keyword.blockchainfull_notm}} Platform console has been successfully tested on the following browsers:

- Chrome Version 85.0.4183.121 (Official Build) (64-bit)
- Safari Version 13.0.3 (15608.3.10.1.4)

## Storage
{: #deploy-k8-storage}

In addition to a small amount of storage (10 GB) required by the {{site.data.keyword.blockchainfull_notm}} console, persistent storage is required for each CA, peer, and ordering node that you deploy. Because blockchain components do not use the Kubernetes node local storage, network-attached remote storage is required so that blockchain nodes can fail over to a different Kubernetes worker node in the event of a node outage.  And because you cannot change your storage type after deploying peer, CA, or ordering nodes, you need to decide the type of persistent storage that you want to use _before_ you deploy any blockchain nodes.

The {{site.data.keyword.blockchainfull_notm}} Platform console uses dynamic provisioning to allocate storage for each blockchain node that you deploy by using a pre-defined storage class. You can choose your persistent storage from the available Kubernetes storage options.

If the storage includes support for the `volumeBindingMode: WaitForFirstCustomer` setting, you should configure it to delay volume binding until the pod is scheduled. Read more in the [Kubernetes Storage Classes documentation](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode){: external}.
{: tip}

Before you deploy the {{site.data.keyword.blockchainfull_notm}} Platform, you must create a storage class with enough backing storage for the {{site.data.keyword.blockchainfull_notm}} console and the nodes that you create. You can set this storage class to use the default storage class of your Kubernetes cluster or create a new class that is used by the {{site.data.keyword.blockchainfull_notm}} Platform console. If you are using a multizone cluster in {{site.data.keyword.cloud_notm}} and you change the default storage class definition, then you must configure the default storage class for each zone.  
After you create the storage class, run the following command to set the storage class of the multizone region to be the default storage class:
```
kubectl patch storageclass
```
{: codeblock}

If you prefer not to choose a persistent storage option, the default storage class of your namespace or OpenShift project is used. `Host-local` volume storage is not supported.
{: note}

### Considerations when choosing your persistent storage
{: ibp-storage-considerations}

| **Consideration** | **Recommendations** |
|---------------|------|
| **Type** | Fabric supports three types of storage for your nodes: File, Block, and Portworx.  All three types support snapshots, which are important for backups and disaster recovery. Portworx is also useful when you have multiple zones in your cluster. Object storage is not supported by Fabric but can be used for backups. |
| **Performance**| When you choose your storage, you need to factor in the read/write speed (IOPS/GB). {{site.data.keyword.blockchainfull_notm}} Platform suggests at least 2 IOPS/GB for a development or test environment and 4 IOPS/GB for production networks. Your results may vary depending on your use case and how your client application is written. |
| **Scalability **| When a node runs out of storage, it ceases to operate. Even if Kubernetes attempts to redeploy the node elsewhere, when the storage is full, the node cannot operate. Because the ledger is immutable and can only grow over time, expandable storage is nice to have for blockchain networks whenever available. At some point, you will run out of storage on your peers and ordering nodes and expandable storage helps to avoid this situation. If the storage is not expandable, when a peer or ordering runs out of storage, you need to provision a new node with a larger storage capacity and then delete the old one. When the new node is deployed, it must replicate the ledger, which can take time depending on the depth of the block history. |
| **Monitoring** | It's critical to monitor the storage consumption by your nodes. Consider the scenario where you deploy five ordering nodes, all with the same amount of storage. They are all replicating the same ledgers so they will all run out of storage at approximately the same time and you will lose consensus, causing the network to stop functioning. Therefore, you might want to consider varying the storage across the nodes and monitoring it as the ledger grows to avoid this situation. Before storage is exhausted on a node, you can expand it or provision a new node. |
| **Encryption** | Fabric does not require storage to be encrypted but it is a best practice for Security. You need to decide whether encryption is important for your business. If you have the option of encrypting the persistent volume, there may be some performance implications with encryption to consider.  |
| **High Availability (HA)** | There should be redundancy in the storage to avoid a single point of failure. |
| **Multi-zone capable storage** | {{site.data.keyword.cloud_notm}} includes the ability to create a single Kubernetes cluster across multiple data centers or "zones". Portworx offers multi-zone capable storage that can be used to potentially reduce the number of peers required. Consider a scenario where you build two zones with two peers for redundancy, one zone can go down and you still have two peers up in another zone. With multi-zone capable storage, you could instead have two zones with one peer each. If one zone goes down, the peer comes up in the other zone with its storage intact, reducing the overall redundant peer requirements. |

## Filesystem permissions
{: #deploy-k8-fs-perm}

{{site.data.keyword.blockchainfull_notm}} Platform uses Kubernetes [init containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: externnal} to set the correct filesystem permissions for the mounted volumes. The init containers run as the root user. The volumes are mounted on the init container which then changes the owner of the mounted folder to be the non-root user of the container that will use it. Learn  more about [how to give non-root users write permission on the volume mount path](/docs/containers?topic=containers-cs_troubleshoot_storage#nonroot){: external}.

## Get your entitlement key
{: #deploy-k8-entitlement-key}

When you purchase the {{site.data.keyword.blockchainfull_notm}} Platform from PPA, you receive an entitlement key for the software is associated with your MyIBM account. You need to access and save this key to deploy the platform.

1. Log in to [MyIBM Container Software Library](https://myibm.ibm.com/products-services/containerlibrary){: external} with the IBMid and password that are associated with the entitled software.

2. In the Entitlement keys section, select **Copy key** to copy the entitlement key to the clipboard. Save this value for use later during deployment.

## Before you begin
{: #deploy-k8-prerequisites}

1. The {{site.data.keyword.blockchainfull_notm}} Platform can be installed only on the [Supported Platforms](/docs/blockchain-sw-251?topic=blockchain-sw-251-console-ocp-about#console-ocp-about-prerequisites){: external}.

2. You cannot deploy an {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x and 2.5.x instance to the same cluster. If you need to run both instances of the product, then they must be running in separate clusters.

3. You need to install and connect to your cluster by using the [kubectl CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl){: external} to deploy the platform.

4. If you are not running the platform on Red Hat OpenShift Container Platform or Red Hat Open Kubernetes Distribution then you need to set up the NGINX Ingress controller and it needs to be running in [SSL passthrough mode](https://kubernetes.github.io/ingress-nginx/user-guide/tls/#ssl-passthrough){: external}. For more information, see [Considerations when using Kubernetes distributions](#console-deploy-k8-considerations).

5. If you have a Hardware Security Module (HSM) that you plan to use to generate and store the private key for your CA, peer, or ordering nodes, you need to create an HSM client image and push it to your container registry. Follow instructions in the [advanced deployment](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-adv-deployment#ibp-console-adv-deployment-hsm-build-docker) topic to build the image.

**Looking for a way to script the deployment of the service?** Check out the [Ansible playbooks](/docs/blockchain-sw-251?topic=blockchain-sw-251-ansible), a powerful tool for scripting the deployment of components in your blockchain network. If you prefer a manual installation, proceed to the next section.

## Log in to your cluster
{: #deploy-k8-login}

Before you can complete the next steps, you need to log in to your cluster by using the kubectl CLI. Follow the instructions for logging in to your cluster.

## Create the `ibpinfra` namespace for the webhook
{: #deploy-k8-ibpinfra}

Because the platform has updated the internal apiversion from `v1alpha1` in previous versions to `v1beta1` in 2.5.1, a Kubernetes conversion webhook is required to update the CA, peer, operator, and console to the new API version. This webhook will continue to be used in the future, so new deployments of the platform are required to deploy it as well.  The webhook is deployed to its own namespace, referred to as  `ibpinfra` throughout these instructions.

After you log in to your cluster, you can create the new `ibpinfra` namespace for the Kubernetes conversion webhook using the kubectl CLI. The new namespace needs to be created by a cluster administrator.

Run the following command to create the namespace.
```
kubectl create namespace ibpinfra
```
{:codeblock}

## Create a secret for your entitlement key
{: #deploy-k8-secret-ibpinfra}

After you purchase the {{site.data.keyword.blockchainfull_notm}} Platform, you can access the [My IBM dashboard](https://myibm.ibm.com/dashboard/){: external} to obtain your entitlement key for the offering. You need to store the entitlement key on your cluster by creating a [Kubernetes Secret](https://kubernetes.io/docs/concepts/configuration/secret/){: external}. Kubernetes secrets are used to securely store the key on your cluster and pass it to the operator and the console deployments.

Run the following command to create the secret and add it to your `ibpinfra` namespace or project:
```
kubectl create secret docker-registry docker-key-secret --docker-server=cp.icr.io --docker-username=cp --docker-password=<KEY> --docker-email=<EMAIL> -n ibpinfra
```
{:codeblock}
- Replace `<KEY>` with your entitlement key.
- Replace `<EMAIL>` with your email address.

The name of the secret that you are creating is `docker-key-secret`. It is required by the webhook that you will deploy later. You can only use the key once per deployment. You can refresh the key before you attempt another deployment and use that value here.
{: note}

## Deploy the webhook and custom resource definitions (CRDS) to your Kubernetes cluster
{: #deploy-k8s-webhook-crd}

Before you can upgrade an existing 2.1.x network to 2.5.1, or deploy a new instance of the platform to your Kubernetes cluster, you need to create the conversion webhook by completing the steps in this section. The webhook is deployed to its own namespace or project, referred to `ibpinfra` throughout these instructions.

The first three steps are for deployment of the webhook. The last step is for the custom resource definitions for the CA, peer, orderer, and console components that the {{site.data.keyword.blockchainfull_notm}} Platform requires. You only have to deploy the webhook and custom resource definitions **once per cluster**. If you have already deployed this webhook and custom resource definitions to your cluster, you can skip these four steps below.
{: important}

### 1. Configure role-based access control (RBAC) for the webhook
{: #webhook-rbac}

First, copy the following text to a file on your local system and save the file as `rbac.yaml`. This step allows the webhook to read and create a TLS secret in its own project.

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: webhook
  namespace: ibpinfra
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: webhook
rules:
- apiGroups:
  - "*"
  resources:
  - secrets
  verbs:
  - "*"
---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: ibpinfra
subjects:
- kind: ServiceAccount
  name: webhook
  namespace: ibpinfra
roleRef:
  kind: Role
  name: webhook
  apiGroup: rbac.authorization.k8s.io
```
{: codeblock}

Run the following command to add the file to your cluster definition:
```
kubectl apply -f rbac.yaml -n ibpinfra
```
{:codeblock}

When the command completes successfully, you should see something similar to:
```
serviceaccount/webhook created
role.rbac.authorization.k8s.io/webhook created
rolebinding.rbac.authorization.k8s.io/ibpinfra created
```
### 2. (OpenShift cluster only) Apply the Security Context Constraint
{: #webhook-scc}

The {{site.data.keyword.blockchainfull_notm}} Platform requires specific security and access policies to be added to the `ibpinfra` project. Copy the security context constraint object below and save it to your local system as `ibpinfra-scc.yaml`.

```yaml
allowHostDirVolumePlugin: false
allowHostIPC: false
allowHostNetwork: false
allowHostPID: false
allowHostPorts: false
allowPrivilegeEscalation: true
allowPrivilegedContainer: true
allowedCapabilities:
- NET_BIND_SERVICE
- CHOWN
- DAC_OVERRIDE
- SETGID
- SETUID
- FOWNER
apiVersion: security.openshift.io/v1
defaultAddCapabilities: []
fsGroup:
  type: RunAsAny
groups:
- system:serviceaccounts:ibpinfra
kind: SecurityContextConstraints
metadata:
  name: ibpinfra
readOnlyRootFilesystem: false
requiredDropCapabilities: []
runAsUser:
  type: RunAsAny
seLinuxContext:
  type: RunAsAny
supplementalGroups:
  type: RunAsAny
volumes:
- "*"
```
{:codeblock}

After you save the file, run the following commands to add the file to your cluster and add the policy to your project.

```
oc apply -f ibpinfra-scc.yaml -n ibpinfra
oc adm policy add-scc-to-user ibpinfra system:serviceaccounts:ibpinfra
```
{:codeblock}

If the commands are successful, you can see a response that is similar to the following example:
```
securitycontextconstraints.security.openshift.io/ibpinfra created
clusterrole.rbac.authorization.k8s.io/system:openshift:scc:ibpinfra added: "system:serviceaccounts:ibpinfra"
```

### 3. Deploy the webhook
{: #webhook-deploy}

In order to deploy the webhook, you need to create two `.yaml` files and apply them to your Kubernetes cluster.

#### deployment.yaml
{: #webhook-deployment-yaml}

Copy the following text to a file on your local system and save the file as `deployment.yaml`. If you are deploying on OpenShift Container Platform on LinuxONE, you need to replace `amd64` with `s390x`.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: "ibp-webhook"
  labels:
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp-webhook"
spec:
  replicas: 1
  selector:
    matchLabels:
      app.kubernetes.io/instance: "ibp-webhook"
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      labels:
        helm.sh/chart: "ibm-ibp"
        app.kubernetes.io/name: "ibp"
        app.kubernetes.io/instance: "ibp-webhook"
      annotations:
        productName: "IBM Blockchain Platform"
        productID: "54283fa24f1a4e8589964e6e92626ec4"
        productVersion: "2.5.1"
    spec:
      serviceAccountName: webhook
      imagePullSecrets:
        - name: docker-key-secret
      hostIPC: false
      hostNetwork: false
      hostPID: false
      securityContext:
        runAsNonRoot: true
        runAsUser: 1000
        fsGroup: 2000
      containers:
        - name: "ibp-webhook"
          image: "cp.icr.io/cp/ibp-crdwebhook:2.5.1-20210112-amd64"
          imagePullPolicy: Always
          securityContext:
            privileged: false
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
            runAsNonRoot: true
            runAsUser: 1000
            capabilities:
              drop:
              - ALL
              add:
              - NET_BIND_SERVICE
          env:
            - name: "LICENSE"
              value: "accept"
            - name: NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: server
              containerPort: 3000
          livenessProbe:
            httpGet:
              path: /healthz
              port: server
              scheme: HTTPS
            initialDelaySeconds: 30
            timeoutSeconds: 5
            failureThreshold: 6
          readinessProbe:
            httpGet:
              path: /healthz
              port: server
              scheme: HTTPS
            initialDelaySeconds: 26
            timeoutSeconds: 5
            periodSeconds: 5
          resources:
            requests:
              cpu: 0.1
              memory: "100Mi"
```
{: codeblock}

Run the following command to add the file to your cluster definition:
```
kubectl apply -n ibpinfra -f deployment.yaml
```
{: codeblock}

When the command completes successfully, you should see something similar to:
```
deployment.apps/ibp-webhook created
```

#### service.yaml
{: #webhook-service-yaml}

Second, copy the following text to a file on your local system and save the file as `service.yaml`.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: "ibp-webhook"
  labels:
    type: "webhook"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp-webhook"
    helm.sh/chart: "ibm-ibp"
spec:
  type: ClusterIP
  ports:
    - name: server
      port: 443
      targetPort: server
      protocol: TCP
  selector:
    app.kubernetes.io/instance: "ibp-webhook"
```
{: codeblock}

Run the following command to add the file to your cluster definition:
```
kubectl apply -n ibpinfra -f service.yaml
```
{: codeblock}

When the command completes successfully, you should see something similar to:
```
service/ibp-webhook created
```

### 4. Extract the certificate and create the custom resource definitions

1. Extract the webhook TLS certificate from the `ibpinfra` namespace by running the following command:

  ```
  TLS_CERT=$(kubectl get secret/webhook-tls-cert -n ibpinfra -o jsonpath={'.data.cert\.pem'})
  ```
  {: codeblock}
2. When you deploy the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 you need to apply the following four CRDs for the CA, peer, orderer, and console. If you are upgrading to 2.5.1, before you can update the operator, you need to update the CRDs to include a new `v1beta1` section as well as the webhook TLS certificate that you just stored in the `TLS_CERT` environment variable. In either case, run the following four commands to apply or update each CRD.

Run this command to update the CA CRD:  

```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  labels:
    app.kubernetes.io/instance: ibpca
    app.kubernetes.io/managed-by: ibp-operator
    app.kubernetes.io/name: ibp
    helm.sh/chart: ibm-ibp
    release: operator
  name: ibpcas.ibp.com
spec:
  preserveUnknownFields: false
  conversion:
    strategy: Webhook
    webhookClientConfig:
      service:
        namespace: ibpinfra
        name: ibp-webhook
        path: /crdconvert
      caBundle: "${TLS_CERT}"
  validation:
    openAPIV3Schema:
      x-kubernetes-preserve-unknown-fields: true
  group: ibp.com
  names:
    kind: IBPCA
    listKind: IBPCAList
    plural: ibpcas
    singular: ibpca
  scope: Namespaced
  subresources:
    status: {}
  version: v1beta1
  versions:
  - name: v1beta1
    served: true
    storage: true
  - name: v1alpha2
    served: true
    storage: false
  - name: v210
    served: false
    storage: false
  - name: v212
    served: false
    storage: false
  - name: v1alpha1
    served: true
    storage: false
EOF
```
{: codeblock}

Depending on whether you are creating or updating the CRD, when successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibpcas.ibp.com created
```
or
```
customresourcedefinition.apiextensions.k8s.io/ibpcas.ibp.com configured
```

Run this command to update the peer CRD:  

```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: ibppeers.ibp.com
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibpca"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  preserveUnknownFields: false
  conversion:
    strategy: Webhook
    webhookClientConfig:
      service:
        namespace: ibpinfra
        name: ibp-webhook
        path: /crdconvert
      caBundle: "${TLS_CERT}"
  validation:
    openAPIV3Schema:
      x-kubernetes-preserve-unknown-fields: true
  group: ibp.com
  names:
    kind: IBPPeer
    listKind: IBPPeerList
    plural: ibppeers
    singular: ibppeer
  scope: Namespaced
  subresources:
    status: {}
  version: v1beta1
  versions:
  - name: v1beta1
    served: true
    storage: true
  - name: v1alpha2
    served: true
    storage: false
  - name: v1alpha1
    served: true
    storage: false
EOF
```
{: codeblock}
When successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibppeers.ibp.com created
```
or
```
customresourcedefinition.apiextensions.k8s.io/ibppeers.ibp.com configured
```

Run this command to update the console CRD:   

```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: ibpconsoles.ibp.com
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibpca"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  preserveUnknownFields: false
  conversion:
    strategy: Webhook
    webhookClientConfig:
      service:
        namespace: ibpinfra
        name: ibp-webhook
        path: /crdconvert
      caBundle: "${TLS_CERT}"
  validation:
    openAPIV3Schema:
      x-kubernetes-preserve-unknown-fields: true
  group: ibp.com
  names:
    kind: IBPConsole
    listKind: IBPConsoleList
    plural: ibpconsoles
    singular: ibpconsole
  scope: Namespaced
  subresources:
    status: {}
  version: v1beta1
  versions:
  - name: v1beta1
    served: true
    storage: true
  - name: v1alpha2
    served: true
    storage: false
  - name: v1alpha1
    served: true
    storage: false
EOF
```
{: codeblock}

When successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibpconsoles.ibp.com created
```
or
```
customresourcedefinition.apiextensions.k8s.io/ibpconsoles.ibp.com configured
```

Run this command to update the orderer CRD:  

```yaml
cat <<EOF | kubectl apply  -f -
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: ibporderers.ibp.com
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibpca"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  preserveUnknownFields: false
  conversion:
    strategy: Webhook
    webhookClientConfig:
      service:
        namespace: ibpinfra
        name: ibp-webhook
        path: /crdconvert
      caBundle: "${TLS_CERT}"
  validation:
    openAPIV3Schema:
      x-kubernetes-preserve-unknown-fields: true
  group: ibp.com
  names:
    kind: IBPOrderer
    listKind: IBPOrdererList
    plural: ibporderers
    singular: ibporderer
  scope: Namespaced
  subresources:
    status: {}
  version: v1beta1
  versions:
  - name: v1beta1
    served: true
    storage: true
  - name: v1alpha2
    served: true
    storage: false
  - name: v1alpha1
    served: true
    storage: false
EOF
```
{: codeblock}

When successful, you should see:
```
customresourcedefinition.apiextensions.k8s.io/ibporderers.ibp.com created
```
or
```
customresourcedefinition.apiextensions.k8s.io/ibporderers.ibp.com configured
```

## Create a new namespace for your {{site.data.keyword.blockchainfull_notm}} Platform deployment
{: #deploy-k8-namespace}

Next, you need to create a second project for your deployment of {{site.data.keyword.blockchainfull_notm}} Platform. You can create a namespace by using the kubectl CLI. The namespace needs to be created by a cluster administrator.

If you are using the CLI, create a new namespace by running the following command:
```
kubectl create namespace <NAMESPACE>
```
{:codeblock}

Replace `<NAMESPACE>` with the name that you want to use for your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

It is required that you create a namespace for each blockchain network that you deploy with the {{site.data.keyword.blockchainfull_notm}} Platform. For example, if you plan to create different networks for development, staging, and production, then you need to create a unique namespace for each environment. Using a separate namespace provides each network with separate resources and allows you to set unique access policies for each network. You need to follow these deployment instructions to deploy a separate operator and console for each namespace.
{: important}

You can also use the CLI to find the available storage classes for your namespace. If you created a new storage class for your deployment, that storage class must be visible in the output in the following command:
```
kubectl get storageclasses
```
{:codeblock}

If you are not using the default storage class, additional configuration is required. See [Storage](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-k8#deploy-k8-storage) for the considerations.

## Create a secret for your entitlement key
{: #deploy-k8-docker-registry-secret}

You've already created a secret for the entitlement key in the `ibpinfra` namespace or project, now you need to create one in your {{site.data.keyword.blockchainfull_notm}} Platform namespace or project. After you purchase the {{site.data.keyword.blockchainfull_notm}} Platform, you can access the [My IBM dashboard](https://myibm.ibm.com/dashboard/){: external} to obtain your entitlement key for the offering. You need to store the entitlement key on your cluster by creating a [Kubernetes Secret](https://kubernetes.io/docs/concepts/configuration/secret/){: external}. Kubernetes secrets are used to securely store the key on your cluster and pass it to the operator and the console deployments.

Run the following command to create the secret and add it to your namespace or project:
```
kubectl create secret docker-registry docker-key-secret --docker-server=cp.icr.io --docker-username=cp --docker-password=<KEY> --docker-email=<EMAIL> -n <NAMESPACE>
```
{:codeblock}
- Replace `<KEY>` with your entitlement key.
- Replace `<EMAIL>` with your email address.
- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace or OpenShift project.

The name of the secret that you are creating is `docker-key-secret`. This value is used by the operator to deploy the offering in future steps. If you change the name of any of secrets that you create, you need to change the corresponding name in future steps.
{: note}

## Add security and access policies
{: #deploy-k8-scc}

The {{site.data.keyword.blockchainfull_notm}} Platform requires specific security and access policies to be added to your namespace. The contents of a set of `.yaml` files are provided here for you to copy and edit to define the security policies. You must save these files to your local system and then add them your namespace by using the kubectl CLI. These steps need to be completed by a cluster administrator. Also, be aware that the peer `init` and `dind` containers that get deployed are required to run in privileged mode.

### Apply the Pod Security Policy
{: #deploy-k8-apply-psp}

Copy the PodSecurityPolicy object below and save it to your local system as `ibp-psp.yaml`.

If you are running **Kubernetes v1.16 or higher**, you will need to change the line `apiVersion: extensions/v1beta1` in the following PodSecurityPolicy object to `apiVersion: policy/v1beta1`.
{: important}

```yaml
apiVersion: extensions/v1beta1
kind: PodSecurityPolicy
metadata:
  name: ibm-blockchain-platform-psp
spec:
  hostIPC: false
  hostNetwork: false
  hostPID: false
  privileged: true
  allowPrivilegeEscalation: true
  readOnlyRootFilesystem: false
  seLinux:
    rule: RunAsAny
  supplementalGroups:
    rule: RunAsAny
  runAsUser:
    rule: RunAsAny
  fsGroup:
    rule: RunAsAny
  requiredDropCapabilities:
  - ALL
  allowedCapabilities:
  - NET_BIND_SERVICE
  - CHOWN
  - DAC_OVERRIDE
  - SETGID
  - SETUID
  - FOWNER
  volumes:
  - '*'
```
{:codeblock}

After you save and edit the file, run the following command to add the file to your cluster and add the policy to your namespace.
```
kubectl apply -f ibp-psp.yaml -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

### Apply the ClusterRole
{: #deploy-k8-clusterrole}

Copy the following text to a file on your local system and save the file as `ibp-clusterrole.yaml`. This file defines the required ClusterRole for the PodSecurityPolicy. Edit the file and replace `<NAMESPACE>` with the name of your namespace.
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: <NAMESPACE>
rules:
- apiGroups:
  - extensions
  resourceNames:
  - ibm-blockchain-platform-psp
  resources:
  - podsecuritypolicies
  verbs:
  - use
- apiGroups:
  - "*"
  resources:
  - pods
  - pod/logs
  - services
  - endpoints
  - persistentvolumeclaims
  - persistentvolumes
  - events
  - configmaps
  - secrets
  - ingresses
  - roles
  - rolebindings
  - serviceaccounts
  - nodes
  - jobs
  verbs:
  - '*'
- apiGroups:
  - ""
  resources:
  - namespaces
  - nodes
  verbs:
  - 'get'
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - customresourcedefinitions
  verbs:
  - get
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - persistentvolumeclaims
  - persistentvolumes
  verbs:
  - '*'
- apiGroups:
  - ibp.com
  resources:
  - '*'
  - ibpservices
  - ibpcas
  - ibppeers
  - ibpfabproxies
  - ibporderers
  verbs:
  - '*'
- apiGroups:
  - ibp.com
  resources:
  - '*'
  verbs:
  - '*'
- apiGroups:
  - apps
  resources:
  - deployments
  - daemonsets
  - replicasets
  - statefulsets
  verbs:
  - '*'
```
{:codeblock}

After you save and edit the file, run the following commands.
```
kubectl apply -f ibp-clusterrole.yaml -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.


### Apply the ClusterRoleBinding
{: #deploy-k8-clusterrolebinding}

Copy the following text to a file on your local system and save the file as `ibp-clusterrolebinding.yaml`. This file defines the ClusterRoleBinding. Edit the file and replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

```yaml
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: <NAMESPACE>
subjects:
- kind: ServiceAccount
  name: default
  namespace: <NAMESPACE>
roleRef:
  kind: ClusterRole
  name: <NAMESPACE>
  apiGroup: rbac.authorization.k8s.io
```
{:codeblock}

After you save and edit the file, run the following commands.
```
kubectl apply -f ibp-clusterrolebinding.yaml -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

### Create the role binding
{: #deploy-k8-rolebinding}

After applying the policies, you must grant your service account the required level of permissions to deploy your console. Run the following command with the name of your target namespace:
```
kubectl -n <NAMESPACE> create rolebinding ibp-operator-rolebinding --clusterrole=<NAMESPACE> --group=system:serviceaccounts:<NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

## Deploy the {{site.data.keyword.blockchainfull_notm}} Platform operator
{: #deploy-k8-operator}

The {{site.data.keyword.blockchainfull_notm}} Platform uses an operator to install the {{site.data.keyword.blockchainfull_notm}} Platform console. You can deploy the operator on your cluster by adding a custom resource to your namespace by using the kubectl CLI. The custom resource pulls the operator image from the Docker registry and starts it on your cluster.  

Copy the following text to a file on your local system and save the file as `ibp-operator.yaml`.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ibp-operator
  labels:
    release: "operator"
    helm.sh/chart: "ibm-ibp"
    app.kubernetes.io/name: "ibp"
    app.kubernetes.io/instance: "ibp"
    app.kubernetes.io/managed-by: "ibp-operator"
spec:
  replicas: 1
  strategy:
    type: "Recreate"
  selector:
    matchLabels:
      name: ibp-operator
  template:
    metadata:
      labels:
        name: ibp-operator
        release: "operator"
        helm.sh/chart: "ibm-ibp"
        app.kubernetes.io/name: "ibp"
        app.kubernetes.io/instance: "ibp"
        app.kubernetes.io/managed-by: "ibp-operator"  
      annotations:
        productName: "IBM Blockchain Platform"
        productID: "54283fa24f1a4e8589964e6e92626ec4"
        productVersion: "2.5.1"
        productChargedContainers: ""
        productMetric: "VIRTUAL_PROCESSOR_CORE"
    spec:
      hostIPC: false
      hostNetwork: false
      hostPID: false
      serviceAccountName: default
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: beta.kubernetes.io/arch
                operator: In
                values:
                - amd64
      securityContext:
        runAsNonRoot: true
        runAsUser: 1001
        fsGroup: 2000
      imagePullSecrets:
        - name: docker-key-secret
      containers:
        - name: ibp-operator
          image: cp.icr.io/cp/ibp-operator:2.5.1-20210112-amd64
          command:
          - ibp-operator
          imagePullPolicy: Always
          securityContext:
            privileged: false
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: false
            runAsNonRoot: false
            runAsUser: 1001
            capabilities:
              drop:
              - ALL
              add:
              - CHOWN
              - FOWNER
          livenessProbe:
            tcpSocket:
              port: 8383
            initialDelaySeconds: 10
            timeoutSeconds: 5
            failureThreshold: 5
          readinessProbe:
            tcpSocket:
              port: 8383
            initialDelaySeconds: 10
            timeoutSeconds: 5
            periodSeconds: 5
          env:
            - name: WATCH_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: OPERATOR_NAME
              value: "ibp-operator"
            - name: CLUSTERTYPE
              value: K8S
          resources:
            requests:
              cpu: 100m
              memory: 200Mi
            limits:
              cpu: 100m
              memory: 200Mi
```
{:codeblock}

- If you changed the name of the Docker key secret, then you need to edit the field of `name: docker-key-secret`.

Then, use the kubectl CLI to add the custom resource to your namespace.

```
kubectl apply -f ibp-operator.yaml -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

You can confirm that the operator deployed by running the command `kubectl get deployment -n <NAMESPACE>`. If your operator deployment is successful, then you can see the following tables with four ones displayed. The operator takes about a minute to deploy.
```
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1     1            1           1m
```

## Deploy the {{site.data.keyword.blockchainfull_notm}} Platform console
{: #deploy-k8-console}

When the operator is running on your namespace, you can apply a custom resource to start the {{site.data.keyword.blockchainfull_notm}} Platform console on your cluster. You can then access the console from your browser. Note that you can deploy only one console per namespace.

Save the custom resource definition below as `ibp-console.yaml` on your local system.

```yaml
apiVersion: ibp.com/v1beta1
kind: IBPConsole
metadata:
  name: ibpconsole
spec:
  arch:
  - amd64
  license:
    accept: true
  serviceAccountName: default
  email: "<EMAIL>"
  password: "<PASSWORD>"
  registryURL: cp.icr.io/cp
  imagePullSecrets:
    - docker-key-secret
  networkinfo:
    domain: <DOMAIN>
  storage:
    console:
      class: default
      size: 10Gi
```
{:codeblock}

You need to specify the external endpoint information of the console in the `ibp-console.yaml` file:
- Replace `<DOMAIN>` with the name of your cluster domain. You need to make sure that this domain is pointed to the load balancer of your cluster.  

You also need to provide the user name and password that is used to access the console for the first time:
- Replace `<EMAIL>` with the email address of the console administrator.
- Replace `<PASSWORD>` with the password of your choice. This password also becomes the default password of the console until it is changed.

You may need to make additional edits to the file depending on your choices in the deployment process:
- If you changed the name of your Docker key secret, change corresponding value of the `imagePullSecrets:` field.
- If you created a new storage class for your network, provide the storage class that you created to the `class:` field.

Because you can only run the following command once, you should review the [Advanced deployment options](#console-deploy-k8-advanced) in case any of the options are relevant to your configuration, before you install the console.  For example, if you are deploying your console on a multizone cluster, you need to configure that before you run the following step to install the console.
{: important}

After you update the file, you can use the CLI to install the console.
```
kubectl apply -f ibp-console.yaml -n <NAMESPACE>
```
{:codeblock}

Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace. Before you install the console, you might want to review the advanced deployment options in the next section. The console can take a few minutes to deploy.

### Advanced deployment options
{: #console-deploy-k8-advanced}

Before you deploy the console, you can edit the `ibp-console.yaml` file to allocate more resources to your console or use zones for high availability in a multizone cluster. To take advantage of these deployment options, you can use the console resource definition with the `resources:` and `clusterdata:` sections added:

```yaml
apiVersion: ibp.com/v1beta1
kind: IBPConsole
metadata:
  name: ibpconsole
spec:
  arch:
  - amd64
  license:
    accept: true
  serviceAccountName: default
  proxyIP:
  email: "<EMAIL>"
  password: "<PASSWORD>"
  registryURL: cp.icr.io/cp
  imagePullSecrets:
    - docker-key-secret
  networkinfo:
      domain: <DOMAIN>
  storage:
    console:
      class: default
      size: 10Gi
  clusterdata:
    zones:
  resources:
    console:
      requests:
        cpu: 500m
        memory: 1000Mi
      limits:
        cpu: 500m
        memory: 1000Mi
    configtxlator:
      limits:
        cpu: 25m
        memory: 50Mi
      requests:
        cpu: 25m
        memory: 50Mi
    couchdb:
      limits:
        cpu: 500m
        memory: 1000Mi
      requests:
        cpu: 500m
        memory: 1000Mi
    deployer:
      limits:
        cpu: 100m
        memory: 200Mi
      requests:
        cpu: 100m
        memory: 200Mi
```
{:codeblock}

- You can use the `resources:` section to allocate more resources to your console. The values in the example file are the default values allocated to each container. Allocating more resources to your console allows you to operate a larger number of nodes or channels. You can allocate more resources to a currently running console by editing the resource file and applying it to your cluster. The console will restart and return to its previous state, allowing you to operate all of your exiting nodes and channels.
  ```
  kubectl apply -f ibp-console.yaml -n <NAMESPACE>
  ```
  {:codeblock}
  Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.


- If you plan to use the console with a multizone Kubernetes cluster, you need to add the zones to the `clusterdata.zones:` section of the file. When zones are provided to the deployment, you can select the zone that a node is deployed to using the console or the APIs. As an example, if you are deploying to a cluster across the zones of dal10, dal12, and dal13, you would add the zones to the file by using the format below.
  ```yaml
  clusterdata:
    zones:
      - dal10
      - dal12
      - dal13
  ```
  {:codeblock}

  When you finish editing the file, apply it to your cluster.
  ```
  kubectl apply -f ibp-console.yaml -n <NAMESPACE>
  ```
  {:codeblock}
  Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.


Unlike the resource allocation, you cannot add zones to a running network. If you have already deployed a console and used it to create nodes on your cluster, you will lose your previous work. After the console restarts, you need to deploy new nodes.
{: Important}

### Use your own TLS Certificates (Optional)
{: #deploy-k8-tls}

The {{site.data.keyword.blockchainfull_notm}} Platform console uses TLS certificates to secure the communication between the console and your blockchain nodes and between the console and your browser. You have the option of creating your own TLS certificates and providing them to the console by using a Kubernetes secret. If you skip this step, the console creates its own self-signed TLS certificates during deployment.

This step needs to be performed before the console is deployed.
{: important}

You can use a Certificate Authority or tool to create the TLS certificates for the console. The TLS certificate needs to include the hostname of the console and the proxy in the subject name or the alternative domain names. The console and proxy hostname are in the following format:

**Console hostname:** ``<NAMESPACE>-ibpconsole-console.<DOMAIN>``  
**Proxy hostname:** ``<NAMESPACE>-ibpconsole-proxy.<DOMAIN>``

- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.
- Replace `<DOMAIN>` with the name of your cluster domain.

Navigate to the TLS certificates that you plan to use on your local system. Name the TLS certificate `tlscert.pem` and the corresponding private key `tlskey.pem`. Run the following command to create the Kubernetes secret and add it to your Kubernetes namespace. The TLS certificate and key need to be in PEM format.
```
kubectl create secret generic console-tls-secret --from-file=tls.crt=./tlscert.pem --from-file=tls.key=./tlskey.pem -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

After you create the secret, add the `tlsSecretName` field to the `spec:` section of `ibp-console.yaml` with one indent added, at the same level as the `resources:` and `clusterdata:` sections of the advanced deployment options. You must provide the name of the TLS secret that you created to the field. The following example deploys a console with the TLS certificate and key stored in a secret named `"console-tls-secret"`:

```yaml
apiVersion: ibp.com/v1beta1
kind: IBPConsole
metadata:
  name: ibpconsole
spec:
  arch:
  - amd64
  license:
    accept: true
  serviceAccountName: default
  email: "<EMAIL>"
  password: "<PASSWORD>"
  registryURL: cp.icr.io/cp
  imagePullSecrets:
    - docker-key-secret
  networkinfo:
        domain: <DOMAIN>
        consolePort: <CONSOLE_PORT>
        proxyPort: <PROXY_PORT>
  storage:
    console:
      class: default
      size: 10Gi
  tlsSecretName: "console-tls-secret"
  clusterdata:
    zones:
      - dal10
      - dal12
      - dal13
```
{:codeblock}

When you finish editing the file, you can apply it to your cluster in order to secure communications with your own TLS certificates:
```
kubectl apply -f ibp-console.yaml -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.

### Verifying the console installation
{: #deploy-k8-verify}

You can confirm that the operator deployed by running the command `kubectl get deployment -n <NAMESPACE>`. If your console deployment is successful, you can see `ibpconsole` added to the deployment table, with four ones displayed. The console takes a few minutes to deploy. You might need to click refresh and wait for the table to be updated.
```
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1     1            1           10m
ibpconsole     1/1     1            1           4m
```

The console consists of four containers that are deployed inside a single pod:
- `optools`: The console UI.
- `deployer`: A tool that allows your console to communicate with your deployments.
- `configtxlator`: A tool used by the console to read and create channel updates.
- `couchdb`: An instance of CouchDB that stores the data from your console, including your authorization information.

If there is an issue with your deployment, you can view the logs from one of the containers inside the pod. First, run the following command to get the name of the console pod:
```
kubectl get pods -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.


Then, use the following command to get the logs from one of the four containers listed above:
```
kubectl logs -f <pod_name> <container_name> -n <NAMESPACE>
```
{:codeblock}
Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.


As an example, a command to get the logs from the UI container would look like the following example:
```
kubectl logs -f ibpconsole-55cf9db6cc-856nz optools -n blockchain-project
```
{:codeblock}


## Log in to the console
{: #deploy-k8-log-in}

You can use your browser to access the console by using the console URL:
```
https://<NAMESPACE>-ibpconsole-console.<DOMAIN>:443
```

- Replace `<NAMESPACE>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment namespace.
- Replace `<DOMAIN>` with the name of your cluster domain. You passed this value to the `DOMAIN:` field of the `ibp-console.yaml` file.

Your console URL looks similar to the following example:
```
https://blockchain-project-ibpconsole-console.xyz.abc.com:443
```

If you navigate to the console URL in your browser, you can see the console login screen:
- For the **User ID**, use the value you provided for the `email:` field in the `ibp-console.yaml` file.
- For the **Password**, use the value you encoded for the `password:` field in the `ibp-console.yaml` file. This password becomes the default password for the console that all new users use to log in to the console. After you log in for the first time, you will be asked to provide a new password that you can use to log in to the console.

Ensure that you are not using the ESR version of Firefox. If you are, switch to another browser such as Chrome and log in.
{: important}

The administrator who provisions the console can grant access to other users and restrict the actions they can perform. For more information, see [Managing users from the console](/docs/blockchain-sw-251?topic=blockchain-sw-251-console-icp-manage#console-icp-manage-users).

## Next steps
{: #console-deploy-k8-next-steps}

When you access your console, you can view the **nodes** tab of your console UI. You can use this screen to deploy components on the cluster where you deployed the console. See the [Build a network tutorial](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-build-network#ibp-console-build-network) to get started with the console. You can also use this tab to operate nodes that are created on other clouds. For more information, see [Importing nodes](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-import-nodes#ibp-console-import-nodes).

To learn how to manage the users that can access the console, view the logs of your console and your blockchain components, see [Administering your console](/docs/blockchain-sw-251?topic=blockchain-sw-251-console-icp-manage#console-icp-manage).  

Ready to automate the entire deployment process? Check out the [Ansible Playbook](/docs/blockchain-sw-251?topic=blockchain-sw-251-ansible-install-ibp) that can be used to complete all of the steps  in this topic for you.

## Considerations when using Kubernetes distributions
{: #console-deploy-k8-considerations}

Before you attempt to install the {{site.data.keyword.blockchainfull_notm}} Platform on Azure Kubernetes Service, Amazon Web Services, Rancher, Amazon Elastic Kubernetes Service, or Google Kubernetes Engine, you should perform the following steps. Refer to your Kubernetes distribution documentation for more details.

1. Ensure that a load balancer with a public IP is configured in front of the Kubernetes cluster.
2. Create a DNS entry for the IP address of the load balancer.
3. Create a wild card host entry in DNS for the load balancer. This entry is a `DNS A` record with a wild card host.

    For example, if the DNS entry for the load balancer is `test.example.com`, the DNS entry would be:
    ```
    *.test.example.com
    ```

    that ultimately resolves to
    ```
    test.example.com
    ```

    When this host entry is configured, the following examples should all resolve to test.example.com:
    ```
    console.test.example.com
    peer.test.example.com
    ```

    You can use `nslookup` to verify that DNS is configured correctly:

    ```
    $ nslookup console.test.example.com
    ```

4. The DNS entry for the load balancer should then be used as the **Domain name** during the installation of IBM Blockchain Platform.

5. The NGINX ingress controller must be used. See the [ingress controller installation guide](https://github.com/kubernetes/ingress-nginx/blob/master/docs/deploy/index.md){: external} that can be used for most Kubernetes distributions.

6. Use the following instructions to edit the NGINX ingress controller deployment to enable ssl-passthrough or refer to the [Kubernetes instructions](https://kubernetes.github.io/ingress-nginx/user-guide/tls/#ssl-passthrough).

    This example might not be exact for your installation. The key is to ensure the last line that enables `ssl-passthrough` is present.

    ```
    /nginx-ingress-controller
    --configmap=$(POD_NAMESPACE)/nginx-configuration
    --tcp-services-configmap=$(POD_NAMESPACE)/tcp-services
    --udp-services-configmap=$(POD_NAMESPACE)/udp-services
    --publish-service=$(POD_NAMESPACE)/ingress-nginx
    --annotations-prefix=nginx.ingress.kubernetes.io
    --enable-ssl-passthrough=true
    ```
    {: codeblock}

7. Verify that all pods are running before you attempt to [install](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-k8#deploy-k8-login) the {{site.data.keyword.blockchainfull_notm}} Platform.

You can now [resume your installation](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-k8#deploy-k8-login).

