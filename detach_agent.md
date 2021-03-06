---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: LogDNA, IBM, Log Analysis, logging, detach config agent

subcollection: LogDNA

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Detaching a LogDNA agent from an instance
{: #detach_agent}

Detach a LogDNA agent from a logging instance to stop collecting logs.
{:shortdesc}

## Detaching a LogDNA agent from a Kubernetes cluster
{: #detach_agent_kube}

To stop your Kubernetes cluster from sending logs to your {{site.data.keyword.la_full_notm}} instance, you must remove the LogDNA agent from your cluster. 

To stop your Kubernetes cluster from forwarding logs to your LogDNA instance, complete the following steps from the command line:

1. Open a terminal. Then, [log in to the {{site.data.keyword.cloud_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}, and follow the prompts.

    Select the account where you provisioned the {{site.data.keyword.la_full_notm}} instance.

2. Set up the cluster environment. Run the following commands:

    First, get the command to set the environment variable and download the Kubernetes configuration files.

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

    When the download of the configuration files is finished, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable.

    Then, copy and paste the command that is displayed in your terminal to set the `KUBECONFIG` environment variable.

3. Remove the secret from your Kubernetes cluster. The Kubernetes secret contains the LogDNA ingestion key. Run the following command:

    ```
    kubectl delete secret logdna-agent-key
    ```
    {: codeblock}

4. Remove the LogDNA agent on every worker(node) of your Kubernetes cluster. The LogDNA agent is responsible for collecting and forwarding your logs. Run the following command:

    ```
    kubectl delete daemonset logdna-agent
    ```
    {: codeblock}

5. Verify that the LogDNA agent is deleted successfully. Run the following command:

    ```
    kubectl get pods
    ```
    {: codeblock}

    You should not see any LogDNA pods.




