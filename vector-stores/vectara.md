# Vectara

## Prerequisite

1. Register an account for [Vectara](https://console.vectara.com/signup)
2. Click **Create Corpus**

<figure><img src="../.gitbook/assets/vectara/1.png" alt=""><figcaption></figcaption></figure>

3. Input required fields:

* **Name**: name of the corpus to be created

<figure><img src="../.gitbook/assets/vectara/2.png" alt="" width="563"><figcaption></figcaption></figure>

4. Click **Create** and wait for the corpus to finish setting up

## Setup

1. Click on the **"Authorization"** tab in the corpus view

<figure><img src="../.gitbook/assets/vectara/3.png" alt=""><figcaption></figcaption></figure>

2. Click on the **"Create API Key"** button, choose a name for the API key and pick the **QueryService & IndexService** option

<figure><img src="../.gitbook/assets/vectara/4.png" alt="" width="375"><figcaption></figcaption></figure>

3. Click **Create** to create the API key
4. Get your **Corpus ID, API Key, and Customer ID**

<figure><img src="../.gitbook/assets/vectara/5.png" alt="" width="170"><figcaption></figcaption></figure>

5. Back to LangChain.Space canvas, drag and drop Vectara nodes. Click **Create New** from the Credentials dropdown:

<figure><img src="../.gitbook/assets/image (1).png" alt="" width="563"><figcaption></figcaption></figure>

6. Copy & Paste each details (Corpus ID, Customer ID, API Key) into below:

<figure><img src="../.gitbook/assets/image (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

7. Now you can connect any Document node under [**Document Loader**](../document-loaders.md) category to Vectara [🎉](https://emojipedia.org/party-popper/)

## Resources

* [LangChain JS Vectara Blog](https://blog.langchain.dev/langchain-vectara-better-together/)
* [5 Reasons to Use Vectara's Langchain Integration Blog Post](https://vectara.com/5-reasons-to-use-vectaras-langchain-integration/)
