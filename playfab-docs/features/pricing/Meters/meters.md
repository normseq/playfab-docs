---
title: Pricing Meters
author: tcrawf23
description: Describes each of the pricing meters in the new pricing model.
ms.author: tcrawf23
ms.date: 2/29/2020
ms.topic: article
ms.prod: playfab
keywords: playfab, pricing, meters
ROBOTS: NOINDEX, NOFOLLOW
ms.localizationpriority: medium
---

# Pricing Meters
PlayFab's pricing is calculated from a set of consumption-based meters. The Pricing Meters page outlines and defines the full set of PlayFab's pricing meters. For more information on PlayFab's pricing model, see [PlayFab Pricing Overview](../../pricing/pricing-overview).

> [!NOTE]
> This page does not include Add-ons like Community Sift, Snowflake, or Photon, and is subject to change as new services and capabilities are added to PlayFab


## Events
View and take action on your game's real-time data. Events are generated in two ways. Standard events can be automatically generated by PlayFab Game Services APIs and written to the event pipeline. Custom events can be created to trigger specific actions within the event pipeline.
* **PlayStream Events** - PlayStream unifies your game data into a single stream and allows you to trigger player engagement actions. In addition, it provides real time visualization of event data. PlayStream Events are metered based on the total number of PlayStream Event API calls that are processed by PlayFab.* For more information, see [PlayStream Event Model reference](../../../api-references/events/).
* **Telemetry Events** - Telemetry Events are metered based on the total number of Telemetry Event API call that are processed by PlayFab.* For more information, see [PlayStream Events - Write Telemetry Events](xref:titleid.playfabapi.com.events.playstreamevents.writetelemetryevents).

> [!NOTE] 
> The size of the event is uncompressed and only includes the payload


## Profile
There is nothing more important to the success of your games than players. Profiles help you understand and engage with players. The profile is the place that helps you understand and engage with your players. Profile includes any data stored related to the player profile, entity profile, character profile, groups, and inventory. Profile data is information that applies to an individual player, group of players, or items, and is stored as Key/Value Pairs (KVPs) by PlayFab. Profile data reads, profile data writes, and the total size of profile data are billed as part of this metered service.
* **Profile Reads** - Metered based on the total number of reads to profile data which are processed by PlayFab.* For a list of read APIs, see [Profile read APIs](profile-reads.md).
* **Profile Writes** - Metered based on the total number of writes (and deletes)  which are processed by PlayFab.* For a list of write APIs, see [Profile write APIs](profile-writes.md).
* **Profile Total Size** - Profile data size is metered based on a daily snapshot of the total volume of profile data hosted by PlayFab.


## Content & Configuration
Content & Configuration files are used to remotely manage configuration for your game. You can update game content remotely in real-time (or on a schedule), and deliver personalized news and events that keep players coming back for more. Content & Configuration files include the following items: entity files, actions, rules, scheduled tasks, matchmaking, push notifications, emails, and title news. Content & Configuration files are a set of key/value pairs that are primarily used to manage configuration for your game remotely. Content & Configuration files data reads, data writes, and storage are billed as part of this metered service.
* **Reads** - Metered based on the total number of files data reads which are processed by PlayFab.* For a list of read APIs, see [Content & Configuration read APIs](file-reads.md).
* **Writes** - Metered based on the total number of files data writes (and deletes) which are processed by PlayFab.* For a list of write APIs, see [Content & Configuration write APIs](file-writes.md).
* **Storage** - Files data size is metered based on the total volume of data hosted by PlayFab (daily snapshots).


## CloudScript
CloudScript enables you to use client code to request execution of any custom server-side functionality you can implement. It enables you to build server-side logic and functionality that scales to meet your demand, without worrying about servers or infrastructure. Both total number of CloudScript executions, and corresponding execution time, are billed as party of this metered service.
* **Execution Time** - CloudScript execution time is metered based on the per-second resource consumption across all CloudScript executions, measured in GB-s (average memory size in GBs x total execution time in milliseconds).
> [!NOTE]
> The minimum billable memory size and execution time per execution is 128MB and 1ms, respectively
* **Total Executions** - CloudScript executions include `ExecuteFunction` API calls, actions & rules, and scheduled tasks. Total executions are metered based on the total number of these CloudScript executions that are processed by PlayFab. For more information about these executions, see [Server-Side Cloud Script - Execution Function](xref:titleid.playfabapi.com.cloudscript.server-sidecloudscript.executefunction), [Actions & Rules](../../automation/actions-rules/), and [Scheduled Tasks](../../automation/scheduled-tasks/).


## Insights
Real-time analytics give you immediate insight into a game's performance and potential issues. Insights include services such as the performance of the data warehouse, long-term storage of data, custom visualization technology, managed external data sources or specialized data projects. The total combined usage of Insights products, represented by an aggregate value ("Insights Credits"), is billed as part of this metered service. Insight Credits are derived from conversion rates for usage of each Insight services.
* **Insights Credits** - The total number of Insights Credits used across all Insights products.


## Multiplayer Servers
PlayFab Multiplayer Servers deliver secure and reliable low-latency gameplay at global scale. Multiplayer Servers facilitate interoperable multiplayer infrastructure and cross-network gameplay, and allow you to operate a dynamically scaling pool of custom game servers in Azure.
* **Virtual Machine Instance Hours** - The hours of virtual machine time that your game servers use, including overhead hours generated by standby servers and virtual machine fragmentation. Price varies by datacenter, virtual machine and container selection. For more information, see [Multiplayer Servers detailed price sheet](../../multiplayer/servers/multiplayer-servers-detailed-price-sheet.md).
* **Network Egress** - The volume of data transmitted by your game servers to the Internet (in gigabytes). Network egress is billed depending on the originating datacenter. Price varies by zone.
<br>
<br>
<br>

**If the average size of [meter] exceeds 1KB per [meter], then the effective number of [meter] will be proportionally based on the average size in KBs*


## Example
To get a better understanding of how weighted meters are calculated, let's take a look at a sample title's PlayStream Events consumption for the previous month:

Event Name | Count | Size
--- | :---: | :---:
player_leveled_up | 40 | 50KB
player_bought_item | 30 | 10KB
player_statistic_changed | 20 | 30KB
player_executed_cloudscript | 10 | 20KB

By adding up the total size (110KB) and dividing by the total count (100), we get an average size of 1.1KB. Therefore, we need to multiply the total count by 1.1 to get the effective count of 110 PlayStream Events. Let's look at the same example with some adjusted numbers:

Event Name | Count | Size
--- | :---: | :---:
player_leveled_up | 40 | 40KB
player_bought_item | 30 | 10KB
player_statistic_changed | 20 | 20KB
player_executed_cloudscript | 10 | 20KB

By adding up the total size (90KB) and dividing by the total count (100), we get an average size of 0.9KB. Therefore, we don't multiply the total count by anything - we stick with 100 PlayStream Events, even though the *player_executed_cloudscript* event had an average size larger than 1KB.