---

copyright:
  years: 2019, 2021
lastupdated: "2021-01-12"

keywords: OpenShift, IBM Blockchain Platform console, deploy, resource requirements, storage, parameters

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


# Upgrading your console and components
{: #upgrade-ocp}

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="/docs/blockchain-sw?topic=blockchain-sw-upgrade-ocp">2.1.2</a>,
    <a href="/docs/blockchain-sw-213?topic=blockchain-sw-213-upgrade-ocp">2.1.3</a>,
    <a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-upgrade-ocp">2.5</a>
    </p>
</div>


You can upgrade the {{site.data.keyword.blockchainfull}} Platform without disrupting a running network. Because the platform is deployed by using a Kubernetes operator, you can pull the latest {{site.data.keyword.blockchainfull_notm}} Platform images from the {{site.data.keyword.IBM_notm}} Entitlement registry without having to reinstall the platform. You can use these instructions to upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1.
{:shortdesc}

## {{site.data.keyword.blockchainfull_notm}} Platform overview
{: #upgrade-ocp-platform-overview}

Use these instructions to upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from versions 2.5, 2.1.3, 2.1.2, 2.1.1, and 2.1.0. The table provides an overview of the current and past releases.

| Version | Release date | Image tags | New features |
|----|----|----|----|
| [{{site.data.keyword.blockchainfull_notm}} Platform 2.5.1](/docs/blockchain-sw-251?topic=blockchain-sw-251-release-notes-saas-20#12-08-2020) | 12 Jan 2021| **Console and tools** <ul><li>2.5.1-20210112-amd64</li> <li>2.5.1-20201208-amd64</li> <li>2.5.1-20201119-amd64</li> <li>2.5.1-20201030-amd64</li></ul> **Fabric nodes** <ul><li>1.4.9-20210112-amd64</li><li>1.4.9-20201208-amd64</li> <li>1.4.9-20201119-amd64</li> <li>1.4.9-20201030-amd64</li><li>2.2.1-20210112-amd64</li><li>2.2.1-20201208-amd64</li><li>2.2.1-20201119-amd64</li><li>2.2.1-20201030-amd64</li></ul> **CouchDB** <ul> <li>2.3.1-20210112-amd64</li> <li>2.3.1-20201208-amd64</li>  <li>2.3.1-20201119-amd64</li><li>2.3.1-20201030-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.9 and 2.2.1</ul> **Improvements to the Console UI** <ul><li>Support for Fabric v2.x Lifecycle.</li><li>Upgrade CA, peer, and ordering nodes from Fabric v1.4 to Fabric v2.x.</li><li>Certificate renewal enhancements added to the console.</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform 2.5](/docs/blockchain-sw-25?topic=blockchain-sw-25-release-notes-saas-20#08-25-2020){: external} | 9 Sept 2020| **Console and tools** <ul><li>2.5.0-20200825-amd64</li><li>2.5.0-20200714-amd64</li><li>2.5.0-20200618-amd64</li></ul> **Fabric nodes** <ul><li>1.4.7-20200825-amd64</li><li>1.4.7-20200714-amd64</li><li>1.4.7-20200618-amd64</li><li>2.1.1-202000825-amd64</li><li>2.1.1-20200714-amd64</li><li>2.1.1-20200618-amd64</li></ul> **CouchDB** <ul><li>2.3.1-20200825-amd64</li><li>2.3.1-20200714-amd64</li><li>2.3.1-20200618-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.7 and 2.1.1</ul> **Improvements to the Console UI** <ul><li>Ability to select Fabric version when you deploy a new peer or ordering node.</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform v2.1.3](/docs/blockchain-sw-213?topic=blockchain-sw-213-whats-new#whats-new-03-24-2020){: external} | 24 March 2020| **Console and tools** <ul><li>2.1.3-20200520-amd64</li><li>2.1.3-20200416-amd64</li><li>2.1.3-20200324-amd64</li></ul> **Fabric nodes** <ul><li>1.4.6-20200520-amd64</li><li>1.4.6-20200416-amd64</li><li>1.4.6-20200324-amd64</li></ul> **CouchDB** <ul><li>2.3.1-20200520-amd64</li><li>2.3.1-20200416-amd64</li><li>2.3.1-20200324-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.6</ul> **Additional platforms** <ul><li>Platform can be deployed on the OpenShift Container Platform 4.2 on LinuxONE (s390x)</ul> **Improvements to the Console UI** <ul><li>Hardware Security Module (HSM) support for node identities</li><li>Ability to override CA, peer, and ordering node configuration</li><li>Ability to add and remove Raft ordering nodes</li><li>Java smart contract instantiation</li><li>Updated create channel and create organization panels</ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform v2.1.2](/docs/blockchain-sw?topic=blockchain-sw-whats-new#whats-new-12-17-2019){: external} | 17 December 2019 | **Console and tools** <ul><li>2.1.2-20191217-amd64</li><li>2.1.2-20200213-amd64</li></ul> **Fabric nodes** <ul><li>1.4.4-20191217-amd64</li><li>1.4.4-20200213-amd64</li></ul> **CouchDB** <ul><li>2.3.1-20191217-amd64</li><li>2.3.1-20200213-amd64</li></ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.4</ul> **Additional platforms** <ul><li>Platform can be deployed on the OpenShift Container Platform 4.1 and 4.2</ul> **Improvements to the Console UI** <ul><li>Simplified component creation flows</li><li>Zone selection for ordering nodes</li><li>Add peer to a channel from Channels tab</li><li>Anchor peer during join</li><li>Export/Import all</ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform v2.1.1]( /docs/blockchain-sw?topic=blockchain-sw-whats-new#whats-new-11-08-2019){: external}| 8 November 2019 | **Console and tools** <ul><li>2.1.1-20191108-amd64</ul> **Fabric nodes** <ul><li>1.4.3-20191108-amd64</ul> **CouchDB** <ul><li>2.3.1-20191108-amd64</ul> | **Additional platforms** <ul><li>Platform can be deployed on Kubernetes v1.14 - v1.16</li><li>Platform can be deployed on {{site.data.keyword.cloud_notm}} Private 3.2.1</li></ul> |
| [{{site.data.keyword.blockchainfull_notm}} Platform v2.1.0](/docs/blockchain-sw?topic=blockchain-sw-whats-new#whats-new-9-24-2019){: external} | 24 September 2019 | **Console and tools** <ul><li>2.1.0-20190918-amd64</ul> **Fabric nodes** <ul><li>1.4.3-20190918-amd64</ul> **CouchDB** <ul><li>2.3.1-20190918-amd64</ul> | **Fabric Version Upgrade** <ul><li>Fabric version 1.4.3</ul> **Additional platforms** <ul><li>Platform can be deployed on the OpenShift Container Platform 3.11</ul> |
{: caption="Table 1. {{site.data.keyword.blockchainfull_notm}} Platform versions" caption-side="bottom"}



## Before you begin
{: #upgrade-ocp-before}

The upgrade process that you follow depends on the version of the platform that you are upgrading from, v2.1.x or v2.5.
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from v2.5](#upgrade-ocp-steps-251)
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from v2.1.x](#upgrade-ocp-steps-21x)  

Or, if you are upgrading from behind a firewall
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from v2.5](#upgrade-ocp-steps-251)
- [Upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from v2.1.x](#upgrade-ocp-firewall)

After you upgrade the {{site.data.keyword.blockchainfull_notm}} Platform operator, the operator will automatically upgrade the console that is deployed on your OpenShift project. You can then use the upgraded console to upgrade your blockchain nodes.

You can continue to submit transactions to your network while you are upgrading your network. However, you cannot use the console to deploy new nodes, deploy smart contracts, or create new channels during the upgrade process.

Updating the Operator triggers a restart of all components managed by this installation of the {{site.data.keyword.blockchainfull_notm}} Platform including Fabric nodes. To avoid disruption of service, a multiregion setup is recommended.
{: note}

It is a best practice to upgrade your SDK to the latest version as part of a general upgrade of your network. While the SDK will always be compatible with equivalent releases of Fabric and lower, it might be necessary to upgrade to the latest SDK to leverage the latest Fabric features. Also, after upgrading, it's possible your client application may experience errors. Consult the your Fabric SDK documentation for information about how to upgrade.
{: tip}

## Platform limitations
{: #upgrade-ocp-platform}

If your {{site.data.keyword.blockchainfull_notm}} Platform is running on OpenShift Container Platform 3.11, you cannot upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 unless you first upgrade your OpenShift cluster from 3.11 to 4.5. For more information, see [Planning your migrationn](https://docs.openshift.com/container-platform/4.5/migration/migrating_3_4/planning-migration-3-to-4.html).


## Upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from 2.5
{: #upgrade-ocp-steps-251}

When you upgrade to {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from 2.5  you need to update the webhook, the custom resource definitions (CRDs), the ClusterRole, and the operator using the following steps. **These same steps can be followed even if your deployment is behind a firewall.**

1. [Update webhook image.](#upgrade-ocp-steps-251-webhook)
2. [Update the CRDs.](#upgrade-ocp-steps-251-crds)
3. [Update the ClusterRole.](#upgrade-ocp-steps-251-clusterrole)
4. [Update the operator.](#upgrade-ocp-steps-251-operator)
5. [Use your console to upgrade your running blockchain nodes.](#upgrade-ocp-nodes)
6. [Update MSPs in consortium to add organization-level endorsement policy.](#upgrade-ocp-update-consortium)

You need to repeat steps 3-5 for each network that that runs on a separate project. If you experience any problems, see the instructions for [rolling back an upgrade](#upgrade-ocp-rollback). If you deployed your network behind a firewall, without access to the external internet, see the separate set of instructions for [Upgrading the {{site.data.keyword.blockchainfull_notm}} Platform behind a firewall](#upgrade-ocp-firewall).

### Step one: Update the webhook image
{: #upgrade-ocp-steps-251-webhook}

Log in to your cluster and run the following command to update the webhook image in the `ibpinfra` namespace or project:

```
kubectl set image deploy/ibp-webhook -n ibpinfra ibp-webhook="cp.icr.io/cp/ibp-crdwebhook:2.5.1-20210112-amd64"
```
{: codeblock}

If you are running the platform on LinuxONE, replace `-amd64` with `-s390x`.

### Step two: Update the CRDs
{: #upgrade-ocp-steps-251-crds}

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

### Step three: Update the ClusterRole
{: #upgrade-ocp-steps-251-clusterrole}

You need to update the ClusterRole that is applied to your project. Copy the following text to a file on your local system and save the file as `ibp-clusterrole.yaml`. Edit the file and replace `<PROJECT_NAME>` with the name of your project.

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

After you edit and save the file, run the following commands. Replace `<PROJECT_NAME>` with the name of your project.
```
oc apply -f ibp-clusterrole.yaml
oc adm policy add-scc-to-group <PROJECT_NAME> system:serviceaccounts:<PROJECT_NAME>
```
{:codeblock}

### Step four: Upgrade the {{site.data.keyword.blockchainfull_notm}} operator
{: #upgrade-ocp-steps-251-operator}

Before updating the operator image, you need to stop the ibpconsole by running the following command. Replace <PROJECT_NAME> with the name of your project:
```
kubectl patch ibpconsole ibpconsole -n <PROJECT_NAME> -p='[{"op": "replace", "path":"/spec/replicas", "value":0}]' --type=json
```
{: codeblock}

Wait a few minutes for the console to stop.

While the console is stopped you are unable to deploy or manage your blockchain components.
{: note}

Run the following command to upgrade the operator. Replace <PROJECT_NAME> with the name of your project:

```
kubectl set image deploy/ibp-operator -n <PROJECT_NAME> ibp-operator="cp.icr.io/cp/ibp-operator:2.5.1-20210112-amd64"
```
{: codeblock}

After applying the new image to the operator deployment, the operator will restart and pull the latest image. The upgrade takes about a minute. While the upgrade is taking place, you can still access your console UI. However, you cannot use the console to deploy smart contracts, or use the console or the APIs to create or remove a node.

Run the command `kubectl get deployment ibp-operator -o yaml` command to confirm that the command updated the operator spec.

You can check that the upgrade is complete by running `kubectl get deployment`. If the upgrade is successful, then you can see the following tables with four ones displayed for your operator and your console.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           1m
ibpconsole     1/1       1            1           4m
```

After the operator restarts, you can now restart the console by running the following command:

```
kubectl patch ibpconsole ibpconsole -n <PROJECT_NAME> -p='[{"op": "replace", "path":"/spec/replicas", "value":1}]' --type=json
```
{: codeblock}

### Step six: Upgrade your nodes

You can now follow the [steps](#upgrade-ocp-nodes) to upgrade your blockchain nodes. Be aware that after the nodes are upgraded, there is no way to roll back the upgrade from 2.5.1 to 2.5. After you upgrade to 2.5.1, you can take advantage of the new Fabric v2.x Lifecycle deployment process for your  smart contracts. But to avoid your peers crashing, you need to ensure that you upgrade your peers before you upgrade your channels. Learn more about considerations when [Upgrading to a new version of Fabric](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-govern-components#ibp-console-govern-components-upgrade).

After you upgrade your nodes, you can [update the MSPs in your consortium to add organization-level endorsement policies](#upgrade-ocp-update-consortium).

### Step seven: Update MSPs in consortium to add organization-level endorsement policy
{: #upgrade-ocp-update-consortium}

To use the 2.x smart contract lifecycle, an organization must have an endorsement policy defined. If any organization in the consortium (the list of organizations maintained by the ordering service that are allowed to create channels) do not have an endorsement policy defined, a warning message will appear on the **Details** page of the ordering service with a list of organization MSPs that must be updated.

The best practice to add this endorsement policy to the MSP is to delete the MSP from the system channel and then re-add the MSP. The console detects the fact that the MSP does not contain the endorsment policy and automatically adds it. Note that this action can only be completed by an ordering service administrator. You do not need to delete and re-add the MSPs in the configuration of any application channels that have already been created. For these MSPs, the endorsement policy is added as part of the process of deploying the smart contract.

## Upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from 2.1.x
{: #upgrade-ocp-steps-21x}

To upgrade your network, you need to [retrieve your entitlement key](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-ocp#deploy-ocp-entitlement-key) from the My {{site.data.keyword.IBM_notm}} Dashboard, and you should have already [created a Kubernetes secret](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-ocp#deploy-ocp-docker-registry-secret) to store the key on your OpenShift project. If the Entitlement key secret was removed from your cluster, or if your key is expired, then you need to download another key and create a new secret.  

You can upgrade an {{site.data.keyword.blockchainfull_notm}} Platform network by using the following steps:

1. [Create the `ibpinfra` project for the webhook](#deploy-ocp-ibpinfra)
2. [Create a secret for your entitlement key](#deploy-ocp-secret-ibpinfra)
3. [Deploy the webhook and custom resource definitions to your OpenShift cluster](#webhook)
4. [Update the ClusterRole](#upgrade-ocp-clusterrole)
5. [Upgrade the {{site.data.keyword.blockchainfull_notm}} Platform operator](#upgrade-ocp-operator)
6. [Use your console to upgrade your running blockchain nodes](#upgrade-ocp-nodes)
7. [Update MSPs in consortium to add organization-level endorsement policy](#upgrade-ocp-update-nodes-consortium)

You need to complete steps 4-6 for each network that that runs on a separate project. If you experience any problems, see the instructions for [rolling back an upgrade](#upgrade-ocp-rollback). If you deployed your network behind a firewall, without access to the external internet, see the separate set of instructions for [Upgrading the {{site.data.keyword.blockchainfull_notm}} Platform behind a firewall](#upgrade-ocp-firewall).

Occasionally, a five node ordering service that was deployed using v2.1.2 will be deleted by the Kubernetes garbage collector because it considers the nodes a resource that needs to be cleaned up. This process is both random and unrecoverable --- if the ordering service is deleted, all of the channels hosted on it are permanently lost. To prevent this, the `ownerReferences` field in the configuration of each ordering node must be removed **before upgrading to 2.5.1**. For the steps about how to pull the configuration file, remove `ordererReferences`, and apply the change, see [Known issues](/docs/blockchain-sw?topic=blockchain-sw-sw-known-issues#sw-known-issues-ordering-service-delete) in the v2.1.2 documentation.
{:important}

### Step one: Create the `ibpinfra` project for the webhook
{: #deploy-ocp-ibpinfra}

Because the platform has updated the internal apiversion from `v1alpha1` in previous versions to `v1beta1` in 2.5.1, a Kubernetes conversion webhook is required to update the CA, peer, operator, and console to the new API version. This webhook will continue to be used in the future, so new deployments of the platform are required to deploy it as well.  The webhook is deployed to its own project, referred to as  `ibpinfra` throughout these instructions.

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
### Step two: Create a secret for your entitlement key
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

### Step three: Deploy the webhook and custom resource definitions to your OpenShift cluster
{: #webhook}
Before you can upgrade an existing 2.1.x network to 2.5.1, or deploy a new instance of the platform to your Kubernetes cluster, you need to create the conversion webhook by completing the steps in this section. The webhook is deployed to its own namespace or project, referred to `ibpinfra` throughout these instructions.

The first three steps are for deployment of the webhook. The last step is for creation of the custom resource definitions for the CA, peer, orderer and console components that the {{site.data.keyword.blockchainfull_notm}} Platform requires. You only have to deploy the webhook and custom resource definitions **once per cluster**. If you have already deployed this webhook and custom resource definitions to your cluster, you can skip these four steps below.
{: important}

#### 1. Configure role-based access control (RBAC) for the webhook
{: #upgrade-webhook-rbac}

Copy the following text to a file on your local system and save the file as `rbac.yaml`. This step allows the webhook to read and create a TLS secret in its own project.

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
#### 2.(OpenShift cluster only) Apply the Security Context Constraint
{: #upgrade-webhook-scc}

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
scc "ibpinfra" added to: ["system:serviceaccounts:ibpinfra"]
```

#### 3. Deploy the webhook
{: #upgrade-webhook-deploy}

In order to deploy the webhook, you need to create two `.yaml` files and apply them to your Kubernetes cluster.

##### deployment.yaml
{: #upgrade-webhook-deployment-yaml}

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

Run the following command to add the configuration to your cluster definition:
```
kubectl apply -n ibpinfra -f deployment.yaml
```
{: codeblock}

When the command completes successfully you should see something similar to:
```
deployment.apps/ibp-webhook created
```

##### service.yaml
{: #upgrade-webhook-service-yaml}

Secondly, copy the following text to a file on your local system and save the file as `service.yaml`.
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

Run the following command to add the configuration to your cluster definition:
```
kubectl apply -n ibpinfra -f service.yaml
```
{: codeblock}

When the command completes successfully you should see something similar to:
```
service/ibp-webhook created
```

#### 4. Extract the certificate and create the custom resource definitions
{: #upgrade-webhook-extract-cert}

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

### Step four: Update the ClusterRole
{: #upgrade-ocp-clusterrole}

You need to update the ClusterRole that is applied to your project. Copy the following text to a file on your local system and save the file as `ibp-clusterrole.yaml`. Edit the file and replace `<PROJECT_NAME>` with the name of your project.

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

After you save and edit the file, run the following commands. Replace `<PROJECT_NAME>` with your project.
```
oc apply -f ibp-clusterrole.yaml
oc adm policy add-scc-to-group <PROJECT_NAME> system:serviceaccounts:<PROJECT_NAME>
```
{:codeblock}


### Step five: Upgrade the {{site.data.keyword.blockchainfull_notm}} operator
{: #upgrade-ocp-operator}

You can upgrade the {{site.data.keyword.blockchainfull_notm}} operator by fetching the operator deployment spec from your OpenShift project. When the operator upgrade is complete, the operator will upgrade your console and download the latest images for your blockchain nodes.

Log in to your cluster by using the OpenShift CLI. Because each {{site.data.keyword.blockchainfull_notm}} network runs in a different project, you must switch to each OpenShift project and upgrade each network separately. Go to the OpenShift project of the network that you want to upgrade. Replace `<PROJECT_NAME>` with the name of your project.
```
oc project <PROJECT_NAME>
```
{:codeblock}

When you are operating from your project, run the following command to download the operator deployment spec to your local file system:
```
kubectl get deployment ibp-operator -o yaml > operator.yaml
```
{:codeblock}

Open `operator.yaml` in a text editor and save a new copy of the file as `operator-upgrade.yaml`. Open `operator-upgrade.yaml` in a text editor. You need to update the `image:` field with the updated version of the operator image. You can find the name and tag of the latest operator image below:
```yaml
cp.icr.io/cp/ibp-operator:2.5.1-20210112-amd64
```
{:codeblock}

If you are upgrading from v2.1.0 or v2.1.1, then you also need to edit the `env:` section of the file. Find the following lines in `operator-upgrade.yaml`:
```yaml
- name: ISOPENSHIFT
  value: "true"
```
{:codeblock}

Replace this section with the following lines at the same indentation:
```yaml
- name: CLUSTERTYPE
  value: OPENSHIFT
```
{:codeblock}

When you are finished editing the file, the `env:` section would look similar to the following:
```yaml
env:
- name: WATCH_NAMESPACE
  valueFrom:
    fieldRef:
      apiVersion: v1
      fieldPath: metadata.namespace
- name: POD_NAME
  valueFrom:
    fieldRef:
      apiVersion: v1
      fieldPath: metadata.name
- name: OPERATOR_NAME
  value: ibp-operator
- name: CLUSTERTYPE
  value: OPENSHIFT
```
{:codeblock}

Save the file on your local system. You can then issue the following command upgrade your operator:
```
kubectl apply -f operator-upgrade.yaml
```
{:codeblock}

You can use the `kubectl get deployment ibp-operator -o yaml` command to confirm that the command updated the operator spec.

After you apply the `operator-upgrade.yaml` operator spec to your OpenShift project, the operator will restart and pull the latest image. The upgrade takes about a minute. While the upgrade is taking place, you can still access your console UI. However, you cannot use the console to deploy smart contracts, or use the console or the APIs to create or remove a node.

You can check that the upgrade is complete by running `kubectl get deployment`. If the upgrade is successful, then you can see the following tables with four ones displayed for your operator and your console.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           1m
ibpconsole     1/1       1            1           4m
```

If you experience a problem while you are upgrading the operator, go to this [troubleshooting topic](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-v2-troubleshooting#ibp-v2-troubleshooting-deployment-cr) for a list of commonly encountered problems. You can run the command to apply the original operator file, `kubectl apply -f operator.yaml` to restore your original operator deployment.

### Step six: Upgrade your nodes

After you upgrade your console, you can use the console to upgrade the nodes of your blockchain network. For more information, see [Upgrade your blockchain nodes](#upgrade-ocp-nodes).

After you upgrade your nodes, make sure to [update your organization-level endorsement policies](#upgrade-ocp-update-consortium).

### Step seven: Update MSPs in consortium to add organization-level endorsement policy
{: #upgrade-ocp-update-nodes-consortium}

To use the 2.x smart contract lifecycle, an organization must have an endorsement policy defined. If any organization in the consortium (the list of organizations maintained by the ordering service that are allowed to create channels) do not have an endorsement policy defined, a warning message will appear on the **Details** page of the ordering service with a list of organization MSPs that must be updated.

The best practice to add this endorsement policy to the MSP is to delete the MSP from the system channel and then re-add the MSP. The console detects the fact that the MSP does not contain the endorsment policy and automatically adds it. Note that this action can only be completed by an ordering service administrator. You do not need to delete and re-add the MSPs in the configuration of any application channels that have already been created. For these MSPs, the endorsement policy is added as part of the process of deploying the smart contract.

## Upgrade to the {{site.data.keyword.blockchainfull_notm}} Platform 2.5.1 from 2.1.x from behind a firewall
{: #upgrade-ocp-firewall}

If you deployed the {{site.data.keyword.blockchainfull_notm}} Platform behind a firewall, without access to the external internet, you can upgrade your network by using the following steps:

1. [Pull the latest {{site.data.keyword.blockchainfull_notm}} Platform images](#upgrade-ocp-images-firewall)
2. [Create the `ibpinfra` project for the webhook](#deploy-ocp-ibpinfra-fw)
3. [Create a secret for your entitlement key](#deploy-ocp-secret-ibpinfra-fw)
4. [Deploy the webhook and custom resource definitions to your OpenShift cluster](#webhook-fw)
5. [Update the ClusterRole](#upgrade-ocp-clusterrole-firewall)
6. [Upgrade the {{site.data.keyword.blockchainfull_notm}} Platform operator](#upgrade-ocp-operator-firewall)
7. [Use your console to upgrade your running blockchain nodes](#upgrade-ocp-nodes-firewall)
8. [Update MSPs in consortium to add organization-level endorsement policy](#upgrade-ocp-nodes-firewall-update-consortium)

You can continue to submit transactions to your network while you are upgrading your network. However, you cannot use the console to deploy new nodes, deploy smart contracts, or create new channels during the upgrade process.

### Before you begin
{: #upgrade-ocp-begin-firewall}

To upgrade your network, you need to [retrieve your entitlement key](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-ocp-firewall#deploy-ocp-entitlement-key-firewall) from the My {{site.data.keyword.IBM_notm}} Dashboard, and [create a Kubernetes secret](/docs/blockchain-sw-251?topic=blockchain-sw-251-deploy-ocp#deploy-ocp-docker-registry-secret) to store the key on your OpenShift project. If the Entitlement key secret was removed from your cluster, or if your key is expired, then you need to download another key and create a new secret.

### Step one: Pull the latest {{site.data.keyword.blockchainfull_notm}} Platform images
{: #upgrade-ocp-images-firewall}

To upgrade your network, download the latest set of {{site.data.keyword.blockchainfull_notm}} Platform images and push them to a container registry that you can access from behind your firewall.

The platform recommends that you use the `skopeo` utility to download and copy your images to your local container registry. [skopeo](https://www.redhat.com/en/blog/skopeo-10-released){: external} is a tool for moving container images between different types of container storages. In order to download the platform images and copy them to your container registry behind a firewall, you first need to [install skopeo](https://github.com/containers/skopeo/blob/master/install.md){: external}.

Before attempting these instructions, you need to have your IBM Blockchain Platform entitlement key and container registry user id and password available. After you purchase the {{site.data.keyword.blockchainfull_notm}} Platform, you can access the [My IBM dashboard](https://myibm.ibm.com/dashboard/){: external} to obtain your entitlement key for the offering. You can then use this key to access the {{site.data.keyword.blockchainfull_notm}} Platform images.

Run the following set of commands to download the images and push them to your registry.  

Replace
- `<ENTITLEMENT_KEY>` with your entitlement key.
- `<LOCAL_REGISTRY_USER>` with the userid with access to your container registry.
- `<LOCAL_REGISTRY_PASSWORD>` with the password to your container registry.
- `amd64` - with `s390x` if you are installing on LinuxONE.

The following commands only work with a Docker container registry. Depending on the level of permissions required for the target location for the images, you might need to prefix each command with `sudo`.
{: note}

```
skopeo copy docker://cp.icr.io/cp/ibp-operator:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-operator:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-init:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-init:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-console:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-console:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-grpcweb:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-grpcweb:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-deployer:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-deployer:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-fluentd:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-fluentd:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-couchdb:2.3.1-20210112 docker://<LOCAL_REGISTRY>/ibp-couchdb:2.3.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-couchdb:3.1.0-20210112 docker://<LOCAL_REGISTRY>/ibp-couchdb:3.1.0-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-peer:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-peer:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-orderer:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-orderer:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-ca:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-ca:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-dind:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-dind:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-utilities:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-utilities:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-peer:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-peer:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-orderer:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-orderer:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-chaincode-launcher:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-chaincode-launcher:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-utilities:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-utilities:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-ccenv:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-ccenv:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-goenv:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-goenv:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-nodeenv:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-nodeenv:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-javaenv:2.2.1-20210112 docker://<LOCAL_REGISTRY>/ibp-javaenv:2.2.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-crdwebhook:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-crdwebhook:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-ccenv:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-ccenv:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-goenv:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-goenv:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-nodeenv:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-nodeenv:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-javaenv:1.4.9-20210112 docker://<LOCAL_REGISTRY>/ibp-javaenv:1.4.9-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
skopeo copy docker://cp.icr.io/cp/ibp-enroller:2.5.1-20210112 docker://<LOCAL_REGISTRY>/ibp-enroller:2.5.1-20210112 -q --src-creds cp:<ENTITLEMENT_KEY> --dest-creds <LOCAL_REGISTRY_USER>:<LOCAL_REGISTRY_PASSWORD> --all
```
{: codeblock}

After you complete these steps, you can use the following instructions to deploy the {{site.data.keyword.blockchainfull_notm}} Platform with the images in your registry.

### Step two: Create the `ibpinfra` project for the webhook
{: #deploy-ocp-ibpinfra-fw}

Because the platform has updated the internal apiversion from `v1alpha1` in previous versions to `v1beta1` in 2.5.1, a Kubernetes conversion webhook is required to update the CA, peer, operator, and console to the new API version. This webhook will continue to be used in the future, so new deployments of the platform are required to deploy it as well.  The webhook is deployed to its own project, referred to as  `ibpinfra` throughout these instructions.

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
### Step three: Create a secret for your entitlement key
{: #deploy-ocp-secret-ibpinfra-fw}

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

### Step four: Deploy the webhook and custom resource definitions to your OpenShift cluster
{: #webhook-fw}

Before you can upgrade an existing 2.1.x network to 2.5.1, or deploy a new instance of the platform to your Kubernetes cluster, you need to create the conversion webhook by completing the steps in this section. The webhook is deployed to its own namespace or project, referred to `ibpinfra` throughout these instructions.

The first three steps are for deployment of the webhook. The last step is for creation of the custom resource definitions for the CA, peer, orderer and console components that the {{site.data.keyword.blockchainfull_notm}} Platform requires. You only have to deploy the webhook and custom resource definitions **once per cluster**. If you have already deployed this webhook and custom resource definitions to your cluster, you can skip these four steps below.
{: important}

#### 1. Configure role-based access control (RBAC) for the webhook
{: #upgrade-webhook-rbac}

Copy the following text to a file on your local system and save the file as `rbac.yaml`. This step allows the webhook to read and create a TLS secret in its own project.

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
#### 2.(OpenShift cluster only) Apply the Security Context Constraint
{: #upgrade-webhook-scc}

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
scc "ibpinfra" added to: ["system:serviceaccounts:ibpinfra"]
```

#### 3. Deploy the webhook
{: #upgrade-webhook-deploy}

In order to deploy the webhook, you need to create two `.yaml` files and apply them to your Kubernetes cluster.

##### deployment.yaml
{: #upgrade-webhook-deployment-yaml}

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

Run the following command to add the configuration to your cluster definition:
```
kubectl apply -n ibpinfra -f deployment.yaml
```
{: codeblock}

When the command completes successfully you should see something similar to:
```
deployment.apps/ibp-webhook created
```

##### service.yaml
{: #upgrade-webhook-service-yaml}

Secondly, copy the following text to a file on your local system and save the file as `service.yaml`.
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

Run the following command to add the configuration to your cluster definition:
```
kubectl apply -n ibpinfra -f service.yaml
```
{: codeblock}

When the command completes successfully you should see something similar to:
```
service/ibp-webhook created
```

#### 4. Extract the certificate and create the custom resource definitions
{: #upgrade-webhook-extract-cert}

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

### Step five: Update the ClusterRole
{: #upgrade-ocp-clusterrole-firewall}

You need to update the ClusterRole that is applied to your project. Copy the following text to a file on your local system and save the file as `ibp-clusterrole.yaml`. Edit the file and replace `<PROJECT_NAME>` with the name of your project.

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

After you save and edit the file, run the following commands. Replace `<PROJECT_NAME>` with the name of your {{site.data.keyword.blockchainfull_notm}} Platform deployment project.
```
oc apply -f ibp-clusterrole.yaml -n <PROJECT_NAME>
oc adm policy add-scc-to-group <PROJECT_NAME> system:serviceaccounts:<PROJECT_NAME>
```

### Step six: Upgrade the {{site.data.keyword.blockchainfull_notm}} operator
{: #upgrade-ocp-operator-firewall}

You can upgrade the {{site.data.keyword.blockchainfull_notm}} operator by fetching the operator deployment spec from your OpenShift project. You can then update the spec with the latest operator image that you pushed to your local registry. When the operator upgrade is complete, the operator will download the images that you pushed to your local registry and upgrade your console.

Log in to your cluster by using the OpenShift CLI. Because each {{site.data.keyword.blockchainfull_notm}} network runs in a different project, you must switch to each OpenShift project and upgrade each network separately. Go to the OpenShift project of the network that you want to upgrade. Replace `<PROJECT_NAME>` with the name of your project.
```
oc project <PROJECT_NAME>
```
{:codeblock}

When you are operating from your project, run the following command to download the operator deployment spec to your local file system:
```
kubectl get deployment ibp-operator -o yaml > operator.yaml
```
{:codeblock}

Open `operator.yaml` in a text editor and save a new copy of the file as `operator-upgrade.yaml`. Open `operator-upgrade.yaml` a text editor. You need to update the `image:` field with the updated version of the operator image:
```
<LOCAL_REGISTRY>/ibp-operator:2.5.1-20210112-amd64
```
{:codeblock}

If you are upgrading from v2.1.0 or v2.1.1, then you also need to edit the `env:` section of the file. Find the following lines in `operator-upgrade.yaml`:
```
- name: ISOPENSHIFT
  value: "true"
```
{:codeblock}

Replace the values above with the following lines at the same indentation:
```
- name: CLUSTERTYPE
  value: OPENSHIFT
```

When you are finished editing the file, the `env:` section would look similar to the following:
```
env:
- name: WATCH_NAMESPACE
  valueFrom:
    fieldRef:
      apiVersion: v1
      fieldPath: metadata.namespace
- name: POD_NAME
  valueFrom:
    fieldRef:
      apiVersion: v1
      fieldPath: metadata.name
- name: OPERATOR_NAME
  value: ibp-operator
- name: CLUSTERTYPE
  value: OPENSHIFT
```
{:codeblock}

Save the file on your local system. You can then issue the following command upgrade your operator:
```
kubectl apply -f operator-upgrade.yaml
```
{:codeblock}

You can use the `kubectl get deployment ibp-operator -o yaml` command to confirm that the command updated the operator spec.

After you apply the `operator-upgrade.yaml` operator spec to your OpenShift project, the operator will restart and pull the latest image. The upgrade takes about a minute. While the upgrade is taking place, you can still access your console UI. However, you cannot use the console to deploy smart contracts, or use the console or the APIs to create or remove a node.

You can check that the upgrade is complete by running `kubectl get deployment`. If the upgrade is successful, then you can see the following tables with four ones displayed for your operator and your console.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           1m
ibpconsole     1/1       1            1           4m
```

If you experience a problem while you are upgrading the operator, go to this [troubleshooting topic](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-v2-troubleshooting#ibp-v2-troubleshooting-deployment-cr) for a list of commonly encountered problems.

If your console experiences an image pull error, you may need to update the console deployment spec with the local registry that you used to download the images.
```
NAME                          READY     STATUS              RESTARTS   AGE
ibp-operator-b9446759-6tmls   1/1       Running             0          1m
ibpconsole-57ff4bcbb7-79dhn   0/4       Init:ErrImagePull   0          1m
```
This can happen if you have changed your regsitry URL between deployments. Run the following command to download the CR spec of the console:
```
kubectl get ibpconsole ibpconsole -o yaml > console.yaml
```
{:codeblock}

Then add the URL of your local registry to the `spec:` section of `console.yaml`. Replace `<LOCAL_REGISTRY>` with the URL of your local registry:
```
spec:
  registryURL: <LOCAL_REGISTRY>
```
{:codeblock}

Save the updated file as `console-upgrade.yaml` on your local system. You can then issue the following command upgrade your console:
```
kubectl apply -f console-upgrade.yaml
```
{:codeblock}

### Step seven: Upgrade your blockchain nodes
{: #upgrade-ocp-nodes-firewall}

After you upgrade your console, you can use the console UI to upgrade the nodes of your blockchain network. For more information, see [Upgrade your blockchain nodes](#upgrade-ocp-nodes).

### Step eight: Update MSPs in consortium to add organization-level endorsement policy
{: #upgrade-ocp-nodes-firewall-update-consortium}

To use the 2.x smart contract lifecycle, an organization must have an endorsement policy defined. If any organization in the consortium (the list of organizations maintained by the ordering service that are allowed to create channels) do not have an endorsement policy defined, a warning message will appear on the **Details** page of the ordering service with a list of organization MSPs that must be updated.

The best practice to add this endorsement policy to the MSP is to delete the MSP from the system channel and then re-add the MSP. The console detects the fact that the MSP does not contain the endorsment policy and automatically adds it. Note that this action can only be completed by an ordering service administrator. You do not need to delete and re-add the MSPs in the configuration of any application channels that have already been created. For these MSPs, the endorsement policy is added as part of the process of deploying the smart contract.

## Upgrade your blockchain nodes
{: #upgrade-ocp-nodes}

After you upgrade your console, you can use the console UI to upgrade the nodes of your blockchain network. Browse to the console UI and open the nodes overview tab. You can find the **Upgrade available** text on a node tile if there is an update available for the component. You can install this upgrade whenever you are ready. These upgrades are optional, but they are recommended. You cannot upgrade nodes that were imported into the console.

Apply upgrades to nodes one at a time. Your nodes are unavailable to process requests or transactions while the patch is being applied. Therefore, to avoid any disruption of service, you need to ensure that another node of the same type is available to process requests whenever possible. Installing upgrades on a node takes about a minute to complete and when it is complete, the node is ready to process requests.
{:important}

To upgrade a node, open the node tile and click the **Upgrade available** button. You cannot upgrade nodes that you imported to the console. Learn more about considerations when [Upgrading to a new version of Fabric](/docs/blockchain-sw-251?topic=blockchain-sw-251-ibp-console-govern-components#ibp-console-govern-components-upgrade).

## Roll back an upgrade
{: #upgrade-ocp-rollback}

When you upgrade your operator, the operator saves the secrets, deployment spec, and network information of your console before attempting to upgrade the console. If your upgrade fails for any reason, the {{site.data.keyword.IBM_notm}} Support can roll back your upgrade and restore your previous deployment by using the information on your cluster. If you need to roll back your upgrade, you can submit a support case from the [mysupport](https://www.ibm.com/support/pages/node/1072956){: external} page.

You can roll back an upgrade after you use the console to operate your network. However, after you use the console to upgrade your blockchain nodes, you can no longer roll back your console to a previous version of the platform.
