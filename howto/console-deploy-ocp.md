---

copyright:
  years: 2018, 2021
lastupdated: "2021-01-07"

keywords: OpenShift, IBM Blockchain Platform console, deploy, resource requirements, storage, parameters, multicloud

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


# Deploy {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 manually
{: #deploy-ocp}

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="/docs/blockchain-sw?topic=blockchain-sw-deploy-ocp">2.1.2</a>,
    <a href="/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-ocp">2.1.3</a>,
    <a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-deploy-ocp">2.5</a>
    </p>
</div>

You can use the following instructions to deploy the {{site.data.keyword.blockchainfull}} Platform 2.5.1 onto a Kubernetes cluster that is running on OpenShift Container Platform. The {{site.data.keyword.blockchainfull_notm}} Platform uses a [Kubernetes Operator](https://www.openshift.com/learn/topics/operators){: external} to install the {{site.data.keyword.blockchainfull_notm}} Platform console on your cluster and manage the deployment and your blockchain nodes. After the {{site.data.keyword.blockchainfull_notm}} Platform console is running on your cluster, you can use the console to create blockchain nodes and operate a multicloud blockchain network.
{:shortdesc}

## Get your entitlement key
{: #deploy-ocp-entitlement-key}

When you purchase the {{site.data.keyword.blockchainfull_notm}} Platform from PPA, you receive an entitlement key for the software is associated with your MyIBM account. You need to access and save this key to deploy the platform.

1. Log in to [MyIBM Container Software Library](https://myibm.ibm.com/products-services/containerlibrary){: external} with the IBMid and password that are associated with the entitled software.

2. In the Entitlement keys section, select **Copy key** to copy the entitlement key to the clipboard. Save this value for use later during deployment.

## Before you begin
{: #deploy-ocp-prerequisites}

1. See [Supported platforms](/docs/blockchain-sw-251?topic=blockchain-sw-251-console-ocp-about#console-ocp-about-prerequisites) for a list of supported versions.

2. You cannot deploy an {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x and 2.5.x instance to the same cluster. If you need to run both instances of the product, then they must be running in separate clusters.

3. You need to install and connect to your cluster by using the [OpenShift Container Platform CLI](https://docs.openshift.com/container-platform/4.5/cli_reference/openshift_cli/getting-started-cli.html){: external} to deploy the platform. If you are using an OpenShift cluster that was deployed with the {{site.data.keyword.IBM_notm}} Kubernetes Service, use these instructions to [Install the OpenShift Origin CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc).

4. If you have a Hardware Security Module (HSM) that you plan to use to generate and store the private key for your CA, peer, or ordering nodes, you need to create an HSM client image and push it to your container registry. Follow instructions in the [advanced deployment](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-adv-deployment#ibp-console-adv-deployment-hsm-build-docker) topic to build the image.

**Looking for a way to script the deployment of the service?** Check out the [Ansible playbooks](/docs/blockchain-sw-251?topic=blockchain-sw-251-ansible), a powerful tool for scripting the deployment of components in your blockchain network. If you prefer a manual installation, proceed to the next section.

## Log in to your OpenShift cluster
{: #deploy-ocp-login}

Before you can complete the next steps, you need to log in to your cluster by using the OpenShift CLI. You can log in to your cluster by using the OpenShift web console.

1. Open the OpenShift web console. If you are using the {{site.data.keyword.IBM_notm}} Kubernetes Service, you can go to your cluster by using the [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/kubernetes/clusters){: external}. In the upper right corner of the cluster overview page, click **OpenShift web console**.

2. From the web console, click the dropdown menu in the upper right corner and then click **Copy Login Command**. Paste the copied command in your terminal window.

The command looks similar to the following example:
```
oc login https://c100-e.us-south.containers.cloud.ibm.com:31394 --token=<TOKEN>
```
If the command is successful, you can see the list of pods in your cluster in your terminal by running the following command:
```
oc get pods
```
{:codeblock}

If this is not a new cluster, you can see the pods that are running in your default namespace:
```
docker-registry-7d8875c7c5-5fv5j    1/1       Running   0          7d
docker-registry-7d8875c7c5-x8dfq    1/1       Running   0          7d
registry-console-6c74fc45f9-nl5nw   1/1       Running   0          7d
router-6cc88df47c-hqjmk             1/1       Running   0          7d
router-6cc88df47c-mwzbq             1/1       Running   0          7d
```

When you connect to your cluster by using the OpenShift CLI, you also connect by using the `kubectl` CLI. You can find the same pods by running the equivalent `kubectl` command:
```
kubectl get pods
```
{:codeblock}

## Create the `ibpinfra` project for the webhook
{: #deploy-ocp-ibpinfra}

Because the platform has updated the internal apiversion from `v1alpha1` in previous versions to `v1beta1` in 2.5.1, a Kubernetes conversion webhook is required to update the CA, peer, operator, and console to the new API version. This webhook will continue to be used in the future, so new deployments of the platform are required to deploy it as well.  The webhook is deployed to its own project, referred to as  `ibpinfra` throughout these instructions. **Webhooks are supported in Kubernetes v1.15 and higher. If your cluster is running Kubernetes v1.14 or lower, you need to upgrade it now to take advantage of this release of the {{site.data.keyword.blockchainfull_notm}} Platform.**

After you log in to your cluster, you can create the new `ibpinfra` project for the Kubernetes conversion webhook using the kubectl CLI. The new project needs to be created by a cluster administrator.  

Run the following command to create the project:   
```
oc new-project ibpinfra
```
{:codeblock}

When you create a new project, a new namespace is created with the same name as your project. You can verify that the existence of the new namespace by using the `oc get namespace` command:
```
$ oc get namespace
NAME                                STATUS    AGE
ibpinfra                            Active    2m
```

## Create a secret for your entitlement key
{: #deploy-ocp-secret-ibpinfra}

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

## Deploy the webhook and custom resource definitions (CRDs) to your OpenShift cluster
{: #deploy-ocp-webhook-crd}

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

## Create a new project for your {{site.data.keyword.blockchainfull_notm}} Platform deployment
{: #deploy-ocp-project}

Next, you need to create a second project for your deployment of {{site.data.keyword.blockchainfull_notm}} Platform. You can create a new project by using the OpenShift web console or OpenShift CLI. The new project needs to be created by a cluster administrator.

If you are using the CLI, create a new project by the following command:
```
oc new-project <PROJECT_NAME>
```
{:codeblock}

Replace `<PROJECT_NAME>` with the name that you want to use for your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

It is required that you create a new OpenShift project for each blockchain network that you deploy with the {{site.data.keyword.blockchainfull_notm}} Platform. For example, if you plan to create different networks for development, staging, and production, then you need to create a unique project for each environment. Each project creates a new Kubernetes namespace. Using a separate namespace provides each network with separate resources and allows you to set unique access policies for each network. You need to follow these deployment instructions to deploy a separate operator and console for each project.
{: important}

When you create a new project, a new namespace is created with the same name as your project. You can verify that the existence of the new namespace by using the `oc get namespace` command:
```
$ oc get namespace
NAME                                STATUS    AGE
blockchain-project                  Active    2m
```

You can also use the CLI to find the available storage classes for your namespace. If you created a new storage class for your deployment, that storage class must be visible in the output in the following command:
```
kubectl get storageclasses
```
{:codeblock}

If you are not using the default storage class, additional configuration is required. See [Storage](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-ocp-getting-started#deploy-ocp-storage) for the considerations.

## Create a secret for your entitlement key
{: #deploy-ocp-docker-registry-secret}

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
{: #deploy-ocp-scc}

The {{site.data.keyword.blockchainfull_notm}} Platform requires specific security and access policies to be added to your project. The contents of a set of `.yaml` files are provided here for you to copy and edit to define the security policies for your project. You must save these files to your local system and then add them your project by using the OpenShift CLI. These steps need to be completed by a cluster administrator. Also, be aware that the peer `init` and `dind` containers that get deployed are required to run in privileged mode.

### Apply the Security Context Constraint

Copy the security context constraint object below and save it to your local system as `ibp-scc.yaml`. Edit the file and replace `<PROJECT_NAME>` with the name of your project.

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
- system:serviceaccounts:<PROJECT_NAME>
kind: SecurityContextConstraints
metadata:
  name: <PROJECT_NAME>
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

After you save and edit the file, run the following commands to add the file to your cluster and add the policy to your project.
```
oc apply -f ibp-scc.yaml -n <PROJECT_NAME>
oc adm policy add-scc-to-user <PROJECT_NAME> system:serviceaccounts:<PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name that you want to use for your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

If the command is successful, you can see a response that is similar to the following example:
```
securitycontextconstraints.security.openshift.io/blockchain-project created
scc "blockchain-project" added to: ["system:serviceaccounts:blockchain-project"]
```

### Apply the ClusterRole

Copy the following text to a file on your local system and save the file as `ibp-clusterrole.yaml`. This file defines the required ClusterRole for the PodSecurityPolicy. Edit the file and replace `<PROJECT_NAME>` with the name of your project.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: <PROJECT_NAME>
rules:
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - persistentvolumeclaims
  - persistentvolumes
  verbs:
  - '*'
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - customresourcedefinitions
  verbs:
  - 'get'
- apiGroups:
  - "*"
  resources:
  - pods
  - pods/log
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
  - routes
  - routes/custom-host
  verbs:
  - '*'
- apiGroups:
  - ""
  resources:
  - namespaces
  - nodes
  verbs:
  - get
- apiGroups:
  - apps
  resources:
  - deployments
  - daemonsets
  - replicasets
  - statefulsets
  verbs:
  - '*'
- apiGroups:
  - monitoring.coreos.com
  resources:
  - servicemonitors
  verbs:
  - get
  - create
- apiGroups:
  - apps
  resourceNames:
  - ibp-operator
  resources:
  - deployments/finalizers
  verbs:
  - update
- apiGroups:
  - ibp.com
  resources:
  - '*'
  verbs:
  - '*'
- apiGroups:
  - config.openshift.io
  resources:
  - '*'
  verbs:
  - '*'
```
{:codeblock}

After you save and edit the file, run the following commands.
```
oc apply -f ibp-clusterrole.yaml -n <PROJECT_NAME>
oc adm policy add-scc-to-group <PROJECT_NAME> system:serviceaccounts:<PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

If successful, you can see a response that is similar to the following example:
```
clusterrole.rbac.authorization.k8s.io/blockchain-project created
scc "blockchain-project" added to groups: ["system:serviceaccounts:blockchain-project"]
```

### Apply the ClusterRoleBinding

Copy the following text to a file on your local system and save the file as `ibp-clusterrolebinding.yaml`. This file defines the ClusterRoleBinding. Edit the file and replace `<PROJECT_NAME>` with the name of your project.

```yaml
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: <PROJECT_NAME>
subjects:
- kind: ServiceAccount
  name: default
  namespace: <PROJECT_NAME>
roleRef:
  kind: ClusterRole
  name: <PROJECT_NAME>
  apiGroup: rbac.authorization.k8s.io
```
{:codeblock}

After you save and edit the file, run the following commands:
```
oc apply -f ibp-clusterrolebinding.yaml -n <PROJECT_NAME>
oc adm policy add-cluster-role-to-user <PROJECT_NAME> system:serviceaccounts:<PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

If successful, you can see a response that is similar to the following example:
```
clusterrolebinding.rbac.authorization.k8s.io/blockchain-project created
cluster role "blockchain-project" added: "system:serviceaccounts:blockchain-project"
```

## Deploy the {{site.data.keyword.blockchainfull_notm}} Platform operator
{: #deploy-ocp-operator}

The {{site.data.keyword.blockchainfull_notm}} Platform uses an operator to install the {{site.data.keyword.blockchainfull_notm}} Platform console. You can deploy the operator on your cluster by adding a custom resource to your project by using the OpenShift CLI. The custom resource pulls the operator image from the Docker registry and starts it on your cluster.   

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
              value: OPENSHIFT
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
- If you are using OpenShift Container Platform on LinuxONE, you need to make the following additional customizations:
   1. In the `spec.affinity` section, change `amd64` to `s390x`.
   2. In the `spec.containers` section, replace `amd64` in the operator `images` tag with `s390x`.

Then, use the `kubectl` CLI to add the custom resource to your project.

```
kubectl apply -f ibp-operator.yaml -n <PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

You can confirm that the operator deployed by running the command `kubectl get deployment -n <PROJECT_NAME>`. If your operator deployment is successful, then you can see the following tables with four ones displayed. The operator takes about a minute to deploy.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           46s
```

## Deploy the {{site.data.keyword.blockchainfull_notm}} Platform console
{: #deploy-ocp-console}

When the operator is running on your namespace, you can apply a custom resource to start the {{site.data.keyword.blockchainfull_notm}} Platform console on your cluster. You can then access the console from your browser. Note that you can deploy only one console per OpenShift project.

Save the custom resource definition below as `ibp-console.yaml` on your local system. If you changed the name of the entitlement key secret, then you need to edit the field of `name: docker-key-secret`.

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
- Replace `<DOMAIN>` with the name of your cluster domain. You can find this value by using the OpenShift web console. Examine the URL for that page. It will be similar to `console.xyz.abc.com/k8s/cluster/dashboards`. The value of the domain then would be `xyz.abc.com`, after removing `console` and `/k8s/cluster/dashboards`.

You need to provide the user name and password that is used to access the console for the first time:
- Replace `<EMAIL>` with the email address of the console administrator.
- Replace `<PASSWORD>` with the password of your choice. This password also becomes the default password of the console until it is changed.

You also need to make additional edits to the file depending on your choices in the deployment process:
- If you changed the name of your Docker key secret, change corresponding value of the `imagePullSecrets:` field.
- If you created a new storage class for your network, provide the storage class that you created to the `class:` field.

If you are deploying on OpenShift Container Platform on LinuxONE, you need to replace:
```yaml
arch:
- amd64
```
in the `spec:` section with:
```yaml
arch:
- s390x
```

If you are running OpenShift on Azure, you also need to change the storage class from `default` to `azure-standard`, unless you created your own storage class.
{: tip}

Because you can only run the following command once, you should review the [Advanced deployment options](#console-deploy-ocp-advanced) in case any of the options are relevant to your configuration, before you install the console.  For example, if you are deploying your console on a multizone cluster, you need to configure that before you run the following step to install the console.
{: important}

After you update the file, you can use the CLI to install the console.
```
kubectl apply -f ibp-console.yaml -n <PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project. The console can take a few minutes to deploy.

### Advanced deployment options
{: #console-deploy-ocp-advanced}

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
  kubectl apply -f ibp-console.yaml -n <PROJECT_NAME>
  ```
  {:codeblock}
  Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

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
  kubectl apply -f ibp-console.yaml -n <PROJECT_NAME>
  ```
  {:codeblock}
  Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

Unlike the resource allocation, you cannot add zones to a running network. If you have already deployed a console and used it to create nodes on your cluster, you will lose your previous work. After the console restarts, you need to deploy new nodes.
{: Important}

### Use your own TLS Certificates (Optional)
{: #console-deploy-ocp-use-your-own-tls-certificates-optional}

The {{site.data.keyword.blockchainfull_notm}} Platform console uses TLS certificates to secure the communication between the console and your blockchain nodes and between the console and your browser. You have the option of creating your own TLS certificates and providing them to the console by using a Kubernetes secret. If you skip this step, the console creates its own self-signed TLS certificates during deployment.

This step needs to be performed before the console is deployed.
{: important}

You can use a Certificate Authority or tool to create the TLS certificates for the console. The TLS certificate needs to include the hostname of the console and the proxy in the subject name or the alternative domain names. The console and proxy hostname are in the following format:

**Console hostname:** ``<PROJECT_NAME>-ibpconsole-console.<DOMAIN>``  
**Proxy hostname:** ``<PROJECT_NAME>-ibpconsole-proxy.<DOMAIN>``  

- Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.
- - Replace `<DOMAIN>` with the name of your cluster domain. You can find this value by using the OpenShift web console. Examine the URL for that page. It will be similar to `console.xyz.abc.com/k8s/cluster/dashboards`. The value of the domain then would be `xyz.abc.com`, after removing `console` and `/k8s/cluster/dashboards`.

Navigate to the TLS certificates that you plan to use on your local system. Name the TLS certificate `tlscert.pem` and the corresponding private key `tlskey.pem`. Run the following command to create the Kubernetes secret and add it to your OpenShift project. The TLS certificate and key need to be in PEM format.
```
kubectl create secret generic console-tls-secret --from-file=tls.crt=./tlscert.pem --from-file=tls.key=./tlskey.pem -n <PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

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
kubectl apply -f ibp-console.yaml -n <PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

### Verifying the console installation

You can confirm that the operator deployed by running the command `kubectl get deployment -n <PROJECT_NAME>`. If your console deployment is successful, you can see `ibpconsole` added to the deployment table, with four ones displayed. The console takes a few minutes to deploy. You might need to click refresh and wait for the table to be updated.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           10m
ibpconsole     1/1       1            1           4m
```

The console consists of four containers that are deployed inside a single pod:
- `optools`: The console UI.
- `deployer`: A tool that allows your console to communicate with your deployments.
- `configtxlator`: A tool used by the console to read and create channel updates.
- `couchdb`: An instance of CouchDB that stores the data from your console, including your authorization information.

If there is an issue with your deployment, you can view the logs from one of the containers inside the pod. First, run the following command to get the name of the console pod:
```
kubectl get pods -n <PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

Then, use the following command to get the logs from one of the four containers listed above:
```
kubectl logs -f <pod_name> <container_name> -n <PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

As an example, a command to get the logs from the UI container would look like the following example:
```
kubectl logs -f ibpconsole-55cf9db6cc-856nz optools -n blockchain-project
```
{:codeblock}

## Log in to the console
{: #deploy-ocp-log-in}

You can use your browser to access the console by browsing to the console URL:

```
https://<PROJECT_NAME>-ibpconsole-console.<DOMAIN>
```
{: codeblock}

- Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.
- Replace `<DOMAIN>` with the name of your cluster domain. You passed this value to the `DOMAIN:` field of the `ibp-console.yaml` file.

Your console URL looks similar to the following example:

```
https://blockchain-project-ibpconsole-console.xyz.abc.com
```
{: codeblock}

You can also find your console URL by logging in to your OpenShift cluster and running the following command:
```
oc get routes -n <PROJECT_NAME>
```
{:codeblock}
Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.

In the output of the command, you can see the URLs for the proxy and the console. You need to add `https://` to the beginning console URL to access the console. You do not need to add a port to the URL.

In your browser, you can see the console login screen:
- For the **User ID**, use the value you provided for the `email:` field in the `ibp-console.yaml` file.
- For the **Password**, use the value you encoded for the `password:` field in the `ibp-console.yaml` file. This password becomes the default password for the console that all new users use to log in to the console. After you log in for the first time, you will be asked to provide a new password that you can use to log in to the console.

Ensure that you are not using the ESR version of Firefox. If you are, switch to another browser such as Chrome and log in.
{: important}

The administrator who provisions the console can grant access to other users and restrict the actions they can perform. For more information, see [Managing users from the console](/docs/blockchain-sw-251?topic=blockchain-sw-251-console-icp-manage#console-icp-manage-users).

## Next steps
{: #console-deploy-ocp-next-steps}

When you access your console, you can view the **nodes** tab of your console UI. You can use this screen to deploy components on the cluster where you deployed the console. See the [Build a network tutorial](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-build-network#ibp-console-build-network) to get started with the console. You can also use this tab to operate nodes that are created on other clouds. For more information, see [Importing nodes](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-import-nodes#ibp-console-import-nodes).

To learn how to manage the users that can access the console, view the logs of your console and your blockchain components, see [Administering your console](/docs/blockchain-sw-251?topic=blockchain-sw-251-console-icp-manage#console-icp-manage).  

Ready to automate the entire deployment process? Check out the [Ansible Playbook](/docs/blockchain-sw-251?topic=blockchain-sw-251-ansible-install-ibp) that can be used to complete all of the steps  in this topic for you.
