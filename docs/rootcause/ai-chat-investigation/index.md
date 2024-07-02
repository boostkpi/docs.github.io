---
layout: default
parent: Root-cause
title: AI-powered chat investigation
description: BoostKPI's ai-powered chat tools can help you investigate and understand your data. This page will help you understand our chat's features and how to configure a chat workspace.
---

# AI-powered chat investigation
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## AI-chat features

BoostKPI currently supports the following AI-powered chat interfaces:

- At the top of every page on [BoostKPI's dashboard](https://dashboard.boostkpi.com), the chat bubble will connect you to a chat that can help answer your questions about BoostKPI's capabilities and how to use BoostKPI's dashboard.
- Near the top right of the [dataset page](https://dashboard.booskpi.com), the "AI assistant" button opens up a chat that can be used to analyze datasets you have imported into BoostKPI along with tables from your own data warehouse.
- When you open an investigation of a specific dataset, the "AI-powered chat investigation" button on the left hand side of the page can be used to investigate the current dataset through a natural language chat interface.
- On the [alert creation page](https://dashboard.boostkpi.com/app/#/self-serve/create-alert), the "AI-powered alert creation" button brings up a chat that can help you set up new alerts.

BoostKPI's chat interfaces are currently in development and not all of the chat interfaces are enabled for all users. If you would like to enable the AI-powered chat features, please contact us at <contact@boostkpi.com>.

## Chat workspace configuration

Some of BoostKPI's chats operate on a notion of a chat workspace. A workspace consists of a collection of BoostKPI datasets, customer data warehouse tables, and custom instructions that are used to scope and guide the chat AI. To set up a workspace, select the "Workspaces" button on the right hand side of the chat interface.

1. Pick a name for your new workspace.
2. Select which external data warehouse connection you would like to use. See documentation on [supported data sources](../../data-import/data-sources/) if you need to set up a connection.
3. Select which BoostKPI datasets you want to include in this workspace.
4. Select which tables you want to include from your data warehouse.
5. Enter a set of instructions that describe the datasets and tables you have used in the workspace.

![Workspace setup](../images/workspace-setup.png)
