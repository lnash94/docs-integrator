---
sidebar_position: 1
sidebar_label: Knowledge Base
title: Knowledge Bases
description: Create and manage a reusable knowledge base for retrieval-augmented generation in WSO2 Cloud - Integration Platform.
keywords: [wso2 integrator, wso2 cloud, knowledge base, rag, vector store, embedding model, chunking, data source, kb service]
slug: /manage/rag-ingestion/knowledge-bases
---

import ThemedImage from '@theme/ThemedImage';
import useBaseUrl from '@docusaurus/useBaseUrl';

# Knowledge Bases

A **Knowledge Base** is a managed store of documents that your integrations and AI applications can index and query. It provides a consistent way to add content, retrieve the most relevant chunks for a query, and remove stale content, regardless of the underlying storage technology.

In WSO2 Cloud - Integration Platform, a Knowledge Base combines three pluggable parts—a **vector store**, an **embedding model**, and a **chunker**—as one reusable, managed configuration. KB data sources ingest and keep content current, while KB Services make that content available to integrations and AI agents.

For details about how a Knowledge Base behaves inside an integration, see [Knowledge Bases in Integrator AI building blocks](../../develop-and-test/integration-artifacts/ai-integrations/ai-building-blocks/knowledge-bases.md).

## Create a Knowledge Base

1. Sign in to WSO2 Cloud and select your organization.
2. In the left navigation, expand **AI Services**, and then select **Knowledge Base**.
3. Click **Add Knowledge Base**.

<ThemedImage
    alt="Knowledge Bases list with the Add Knowledge Base button"
    sources={{
        light: useBaseUrl('/img/manage/cloud/knowledge-bases/knowledge-base-list.png'),
        dark: useBaseUrl('/img/manage/cloud/knowledge-bases/knowledge-base-list.png'),
    }}
/>

4. In **Name Knowledge Base**, enter a name and an optional description. The platform derives a unique Knowledge Base key from the name.
5. In **Configure vector store**, select and configure one of the following:
   - **Pinecone**
   - **Chroma**
   - **Weaviate**
   - **PostgreSQL**
   - **WSO2 Integration Platform Managed**, when a managed PostgreSQL database is available in the organization

<ThemedImage
    alt="Configure vector store step with the supported vector store providers"
    sources={{
        light: useBaseUrl('/img/manage/cloud/knowledge-bases/configure-vector-store.png'),
        dark: useBaseUrl('/img/manage/cloud/knowledge-bases/configure-vector-store.png'),
    }}
/>

6. In **Configure embedding and chunking**:
   1. Select **OpenAI**, **Azure OpenAI**, or **Mistral AI** as the embedding provider, then enter the model and provider credentials.
   2. Select **Recursive**, **Sentence**, or **Character** as the chunking strategy.
   3. Set the maximum segment and overlap sizes.

<ThemedImage
    alt="Configure embedding and chunking step with provider, strategy, segment size, and overlap settings"
    sources={{
        light: useBaseUrl('/img/manage/cloud/knowledge-bases/configure-embedding-and-chunking.png'),
        dark: useBaseUrl('/img/manage/cloud/knowledge-bases/configure-embedding-and-chunking.png'),
    }}
/>

7. Optional: In **Add data source**, configure **Google Drive** or **Amazon S3**. Choose **One-time** to ingest after deployment, or **Scheduled** to set a recurring ingestion schedule. You can also skip this step and add a data source later.

<ThemedImage
    alt="Optional data source step with Google Drive and a recurring ingestion schedule"
    sources={{
        light: useBaseUrl('/img/manage/cloud/knowledge-bases/add-data-source.png'),
        dark: useBaseUrl('/img/manage/cloud/knowledge-bases/add-data-source.png'),
    }}
/>

8. In **Review and Create**, verify the vector store, collection or table, embedding model, chunking strategy, and Production environment.
9. Click **Create**.

<ThemedImage
    alt="Review and Create step summarizing the Knowledge Base configuration"
    sources={{
        light: useBaseUrl('/img/manage/cloud/knowledge-bases/review-and-create.png'),
        dark: useBaseUrl('/img/manage/cloud/knowledge-bases/review-and-create.png'),
    }}
/>

The platform saves the reusable Knowledge Base configuration and creates its initial KB Service. If you configured a data source, the platform also creates and deploys it. One-time data sources run after deployment; scheduled data sources run according to the configured schedule.

## Manage a Knowledge Base

Open a Knowledge Base from the **Knowledge Bases (KB)** list to manage it from the following tabs:

| Tab | What you can do |
| --- | --- |
| **Overview** | Review the vector store, collection or table, embedding provider, chunking strategy, service URL, and attached KB data sources. Run an ingestion, change its schedule, or inspect execution logs. |
| **Configurations** | Review environment-specific configuration values and edit the Knowledge Base configuration. |
| **Connect to KB** | Copy the generated service URL, create additional KB Services, and open the Developer Portal to subscribe an application and generate an API key. |
| **Retrieval** | Send a query through the generated KB Service and verify the chunks retrieved from the Knowledge Base. |

### Add and operate a data source

From the **Overview** tab, click **Add KB Data Source** to connect another source. Each data source appears with its last successful sync, schedule, deployment status, and actions. You can:

- Click **Ingest** to start an ingestion immediately.
- Add or update its recurring schedule.
- Open **Execution logs** to troubleshoot a run.
- Open the data source component or delete it from the Knowledge Base.

### Connect an application or integration

Use the **Connect to KB** tab to copy the KB Service URL. To call it from an external application, open the Developer Portal, subscribe an application to the KB Service, and generate an API key.

To use the Knowledge Base in a WSO2 Integrator project, add a **WSO2 Cloud Knowledge Base** connection and select the provisioned Knowledge Base. For connection fields and supported retrieval operations, see [Connect to an existing WSO2 Cloud Knowledge Base](../../develop-and-test/integration-artifacts/ai-integrations/ai-building-blocks/knowledge-bases.md#connect-to-an-existing-knowledge-base).

## Edit or delete a Knowledge Base

Use **Edit Knowledge Base** on the details page to change its vector store, embedding, or chunking configuration. The platform applies the shared configuration to the components that use the Knowledge Base.

You can delete a Knowledge Base from the Knowledge Base list only when no components depend on it. Remove its KB data sources and KB Services, and disconnect any other dependent components before deleting it.

## Related pages

- [Managed vector databases](./vector-databases.md)
- [RAG ingestion automation](./ingestion.md)
- [RAG retrieval](./retrieval.md)
- [RAG service](./service.md)
