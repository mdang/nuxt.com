---
title: AWS Amplify
description: 'Deploy your Nuxt Application to AWS Amplify infrastructure.'
componentImg: Amplify
logoIcon: 'i-logos-aws-amplify'
category: Hosting
website: 'https://aws.amazon.com/amplify/?trk=bed847b4-6e9f-4e09-ba09-0d4680a0447b&sc_channel=el'
---

## Setup

Before you start, make sure you have AWS credentials for your AWS account, [Node.js](https://nodejs.org/en/download) 22.12 or later, and the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) version 2.35.0 or later.

::tabs

:::tabs-item{label="With an AI agent"}

1. Install the Amplify skill, then restart your agent:

   ```bash [Terminal]
   aws agent-toolkit add-skill --skill-name aws-amplify
   ```

   The command is part of the AWS CLI and installs the skill for every supported agent it detects on your machine. To install it for one agent only, add `--agent kiro` or `--agent claude-code`.

2. In your Nuxt project folder, ask your agent:

   ```text
   Deploy my Nuxt app to Amplify and give me the preview URL.
   ```

   The agent installs the Amplify CLI if needed, sets up the Nuxt adapter, creates the app and deploys it to the `preview` environment.

:::

:::tabs-item{label="Manual"}

1. Install the Amplify CLI:

   ```bash [Terminal]
   npm install -g @omega/cli
   ```

2. Install the Amplify Nuxt adapter:

   ::::code-group{sync="pm"}

   ```bash [npm]
   npm install -D @aws-amplifygen3/adapter-nuxt
   ```

   ```bash [yarn]
   yarn add -D @aws-amplifygen3/adapter-nuxt
   ```

   ```bash [pnpm]
   pnpm add -D @aws-amplifygen3/adapter-nuxt
   ```

   ```bash [bun]
   bun add -D @aws-amplifygen3/adapter-nuxt
   ```

   ::::

3. Set the adapter's Nitro preset in your Nuxt config:

   ```ts [nuxt.config.ts]
   export default defineNuxtConfig({
     nitro: {
       preset: '@aws-amplifygen3/adapter-nuxt/nitro.config'
     }
   })
   ```

4. Create the Amplify app. Replace `my-app` with the name of your app:

   ```bash [Terminal]
   aws amplifygen3 create --name my-app
   ```

   This creates the app in your AWS account and writes an `amplify.jsonc` file with your build settings. Commit `amplify.jsonc` to your repository.

5. Deploy to the `preview` environment:

   ```bash [Terminal]
   aws amplifygen3 deploy
   ```

   When the deploy finishes, it prints your preview URL.

6. When your app works in preview, deploy to `production`:

   ```bash [Terminal]
   aws amplifygen3 deploy --env production
   ```

:::

::

::note
**Static sites**: if you use `nuxt generate`, turn on link crawling so the adapter prerenders every page. Without it, only the `200.html` and `404.html` fallback pages are generated.

```ts [nuxt.config.ts]
export default defineNuxtConfig({
  nitro: {
    preset: '@aws-amplifygen3/adapter-nuxt/nitro.config',
    prerender: {
      crawlLinks: true,
      routes: ['/']
    }
  }
})
```
::

## Learn more

::read-more{to="https://integ.www.docs.aws.a2z.com/amplify/latest/userguide/getting-started.html" target="_blank"}
Head over to the **AWS Amplify documentation** to learn more about deploying with Amplify.
::

::read-more{to="https://integ.www.docs.aws.a2z.com/amplify/latest/userguide/deploy-with-ai-agents.html" target="_blank"}
Learn how to **deploy with AI coding agents** using the Amplify skill.
::
