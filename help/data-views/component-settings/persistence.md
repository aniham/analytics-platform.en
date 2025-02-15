---
title: Persistence component settings
description: Determine how or whether dimension values persist from one event to the next.
exl-id: b8b234c6-a7d9-40e9-8380-1db09610b941
solution: Customer Journey Analytics
---

# [!UICONTROL Persistence] component settings

[!UICONTROL Persistence] is the ability for a given dimension value to relate to a metric beyond the event it is set on. It uses a combination of allocation and expiration.

* **Allocation** lets you determine which value is kept when more than one dimension item can persist at a time in a single column.
* **Expiration** lets you determine how long a dimension item persists beyond the event it is set on.

[!UICONTROL Persistence] is available only on dimensions, and is retroactive to the data it is applied to. It is an immediate data transformation that happens before filtering or other analysis operations are applied.

![Persistence](../assets/persistence.png)

| Setting | Description |
| --- | --- |
| [!UICONTROL Set persistence] | Enable persistence for the dimension. If persistence is not enabled, the dimension only relates to metrics that exist in the same event. This setting is disabled by default. |
| [!UICONTROL Allocation] | Lets you specify the allocation model used on a dimension for persistence. Options are: [!UICONTROL Most recent], [!UICONTROL Original], [!UICONTROL Instance], [!UICONTROL All]. As of October 28, 2021, a lookback window of up to 90 days will be added to the [!UICONTROL Allocation] setting. |
| [!UICONTROL Expiration] | Lets you specify the persistence window for a dimension. Options are: [!UICONTROL Session] (default), [!UICONTROL Person], [!UICONTROL Custom Time], [!UICONTROL Metric]. You might need to be able to expire the dimension on a purchase (such as internal search terms or other merchandising use cases). The maximum expiration time you can set is 90 days. If you select an allocation of [!UICONTROL All], only [!UICONTROL Session] or [!UICONTROL Person] expiration is available. |

## [!UICONTROL Allocation] settings

Details around the available allocation settings.

* **[!UICONTROL Most Recent]**: persists the most recent (by timestamp) value present in the dimension. Any subsequent values that occur within the dimension's expiration period replaces the previously persisting value. If "Treat 'No Value' as a value" is enabled on this dimension under [No value options](no-value-options.md), empty values overwrite previously persisted values. For example, consider the following table with [!UICONTROL Most recent] allocation and [!UICONTROL Session] expiration:

  | Dimension | Hit 1 | Hit 2 | Hit 3 | Hit 4 | Hit 5 |
  | --- | --- | --- | --- | --- | --- |
  | Dataset values |  | C | B |  | A |
  | Most recent allocation |  | C | B | B | A |

* **[!UICONTROL Original]**: Persists the original value by timestamp present within the dimension for the duration of the expiration period. If this dimension has a value, it is not overwritten when a different value is seen on a subsequent event. For example, consider the following table with [!UICONTROL Original] allocation and [!UICONTROL Session] expiration:

  | Dimension | Hit 1 | Hit 2 | Hit 3 | Hit 4 | Hit 5 |
  | --- | --- | --- | --- | --- | --- |
  | Dataset values |  | C | B |  | A |
  | Original allocation |  | C | C | C | C |

* **[!UICONTROL All]**: Acts similarly to the [!UICONTROL Participation] attribution model for metrics. Persists all values equally so each get full credit for the metric in reporting. For example, consider the following table with [!UICONTROL All] allocation and [!UICONTROL Session] expiration:

  | Dimension | Hit 1 | Hit 2 | Hit 3 | Hit 4 | Hit 5 |
  | --- | --- | --- | --- | --- | --- |
  | Dataset values | A | B | C |  | A |
  | All allocation | A | A,B | A,B,C | A,B,C | A,B,C |

## [!UICONTROL Expiration] settings

Details around the available expiration settings.

* **Session**: Expires after a given session. Default expiration window.
* **Person**: Expires at the end of the reporting window.
* **Time**: You can set the dimension value to expire after a specified time period (up to 90 days). This expiration option is only available for Original and Most Recent allocation models. When using time-based expiration, values previous to the start of your reporting window (up to 90 days) are considered.
* **Metric**: When this metric is seen in a hit, immediately expire the persisted value in the dimension. You can use any metric as the expiration end for this dimension. This expiration option is only available for Original and Most Recent allocation settings.
