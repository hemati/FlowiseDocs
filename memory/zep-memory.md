# Zep Memory

[Zep](https://github.com/getzep/zep) is long-term memory store for LLM applications. It stores, summarizes, embeds, indexes, and enriches LLM app / chatbot histories, and exposes them via simple, low-latency APIs.

It is suitable when you are using LangFlux as API, and want the AI to remember conversations between different users. You can achieve that using **sessionId**.

## Deploy Zep

You can easily deploy Zep to cloud services like [Render](https://render.com/), [Flyio](https://fly.io/). If you prefer to test it locally, you can also spin up a docker container by following their [quick guide](https://github.com/getzep/zep#quick-start).

In this example, we are going to deploy to Render.

1. Head over to [Zep Repo](https://github.com/getzep/zep#quick-start) and click **Deploy to Render**
2. This will bring you to Render's Blueprint page and simply click **Create New Resources**

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

3. When the deployment is done, you should see 3 applications created on your dashboard

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

4. Simply click the first one called **zep** and copy the deployed URL

<figure><img src="../.gitbook/assets/image (38) (1).png" alt=""><figcaption></figcaption></figure>

## Guide to Deploy Zep to Digital Ocean (via Docker)

1. Clone the Repo
```bash
git clone https://github.com/getzep/zep.git
cd zep
nano .env

```

2. Add IN your OpenAI API Key in.ENV

```bash
ZEP_OPENAI_API_KEY=

```

```bash
docker-compose up -d --build
```

3. Allow firewall access to port 8000

```bash
sudo ufw allow from any to any port 8000 proto tcp
ufw status numbered
```

If using Digital ocean separate firewall from dashboard, make sure port 8000 is added there too

## Use in LangFlux UI

1. Back to LangFlux application, simply create a new canvas or use one of the template from marketplace. In this example, we are going to use **Simple Conversational Chain**

<figure><img src="../.gitbook/assets/Untitled (3) (1).png" alt=""><figcaption></figcaption></figure>

2. Replace **Buffer Memory** with **Zep Memory**. Then replace the **Base URL** with the Zep URL you have copied above

<figure><img src="../.gitbook/assets/Untitled (5).png" alt=""><figcaption></figcaption></figure>

3. Save the chatflow and test it out to see if conversations are remembered.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

4. Now try clearing the chat history, and see if it still remember the previous conversations

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

By default, the first chat message id will be used as **sessionId** for Zep Memory, allowing AI to remember the conversations.

When chat history is cleared, all chat messages will be deleted. When user ask a new question, a new chat message is being saved with a new id. The id of that first new chat message will then be used as the new **sessionId**. As you can see from picture above, it does not remember user's name after the chat history is cleared.

## Use in LangFlux API

To use as API, especially when multiple users are interacting with the flow, you can use **sessionId** to differentiate conversations between each user.

<figure><img src="../.gitbook/assets/Untitled (1) (1).png" alt=""><figcaption></figcaption></figure>

For instance, in your front-end application, you can dynamically generate a **sessionId** using a combination of **userid** and **timestamp**. When user clear the chats from your front-end application, you can generate a new **sessionId** with the same **userid** and <mark style="color:red;">**new**</mark> **timestamp**. This will begins a new chat session with no previous conversations memory.

Example of a POST call:

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

## Zep Authentication

Zep allows you to secure your instance using JWT authentication. We'll be using the `zepcli` command line utility [here](https://github.com/getzep/zepcli/releases).

#### 1. Generate a secret and the JWT token <a href="#1-generate-a-secret-and-the-jwt-token" id="1-generate-a-secret-and-the-jwt-token"></a>

After downloaded the ZepCLI:

On Linux or MacOS

```
./zepcli -i
```

On Windows

```
zepcli.exe -i
```

You will first get your SECRET Token:

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Then you will get JWT Token:

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Configure Auth environment variables <a href="#2-configure-auth-environment-variables" id="2-configure-auth-environment-variables"></a>

Set the following environment variables in your Zep server environment:

```
ZEP_AUTH_REQUIRED=true
ZEP_AUTH_SECRET=<the secret you generated above>
```

#### 3. Configure Credential on LangFlux <a href="#2-configure-auth-environment-variables" id="2-configure-auth-environment-variables"></a>

Add a new credential for Zep, and put in the JWT Token in the API Key field:

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

#### 4. Use the created credential on Zep node <a href="#2-configure-auth-environment-variables" id="2-configure-auth-environment-variables"></a>

In the Zep node Connect Credential, select the credential you have just created. And that's it!

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
