---
layout: default
title: Welcome to AspireUpdate
permalink: /aspireupdate/
---

# What is AspireUpdate?

[AspireUpdate](https://github.com/aspirepress/AspireUpdate) is an open source WordPress plugin that enables WordPress sites to use an alternative repository for updates. The plugin reverts to WordPress.org repository when updates are not available in the configured AspireCloud instance.

## How to install AspireUpdate

Download and Install AspireUpdate:

[Current Build](https://github.com/aspirepress/AspireUpdate/tree/main)
[Stable Build](https://github.com/aspirepress/AspireUpdate/tree/main)
[Releases](https://github.com/aspirepress/AspireUpdate/releases)

No API Key is currently required.

## Try AspireUpdate in WP Playground

[Try out AspireUpdate WP Playground](https://playground.wordpress.net/?blueprint-url=https://raw.githubusercontent.com/aspirepress/AspireUpdate/refs/heads/playground-ready/assets/playground/blueprint.json)

[Look at WP Playground Blueprint.json](https://github.com/aspirepress/AspireUpdate/blob/playground-ready/assets/playground/blueprint.json)

## Design of Phase 1 of AspirePress

AspirePress inspiration is the Domain Name System (DNS). AspirePress has architecturally a very similar approach, except instead of domain records and zones, AspirePress serves WordPress assets.

Overall Status: Phase 1 doesn’t implement all of this design yet.

State Diagram:

[Diagram by Mermaid](https://github.blog/developer-skills/github/include-diagrams-markdown-files-mermaid/)

```mermaid
---
config:
  theme: base
---
sequenceDiagram
  participant AU as AspireUpdate on A WordPress Site
  participant AC as AspireCloud (or YourCloud)
  participant Worg as WordPress.org API
  participant AS as AspireSync
  AU -) Worg: Rewrite Mode OFF - Request asset(s)
  Worg -) AU: Return asset(s) from W.org
  Note right of Worg: This mode will eventually be deprecated.
  opt Rewrite Mode ON
    AU ->> AC: Request asset(s)
    AC ->> AU: Return asset(s)
    AC -->> Worg: Fetch asset(s)
    Worg -->> AC: Return asset(s)
    AC -->> AC: Store asset(s)
    AC ->> AU: Return asset(s)
    Worg -->> AS: Sync asset(s)
    AS ->> AC: Prime AspireCloud as necessary
  end
```

This approach has several benefits:

1. Scopes down AspireSync entirely out of the solution for now. No federation between AspireClouds for now. Initial mirror(s) start with zero plugins or themes and grow organically as demand for hosting on mirror grows. Installation is greatly reduced as you need AspireUpdate plugin at the user's end and AspireCloud service to handle update requests and delegate to .org if there is no asset to serve from configured API update endpoint.

2. Hosting companies can set this up for their default WordPress installs with default AspireClouds on their own. Let a million mirrors bloom!

3. Aspire Updater plugin is installed on a site. User can choose from a list of known AspireClouds, or it can be locked to one by host.

4. The plugin rewrites all API calls to api.aspirepress.org or to another AspireCloud powered API. AP maintains for now a set of trusted API end points which correspond to AspireCloud mirrors.

5. If AspireCloud has a response, that requested asset is available, we give the asset back to plugin.

6. If AspireCloud does not have the asset, AspireUodate then calls .org canonical repo. It fetches the asset, pushes the whole response to AspireCloud to populate the mirror with the requested asset. This is how a specific AspireCloud gets populated with new assets beyond manual population by a plugin or theme developer.

7. AspireUpdate passes the response of asset back to WordPress for handling the update install process.

8. AspireCloud receives the asset, stores it in the data store. It can later serve requests for newly acquired asset.

9. The asset that was pulled in from .org will expire after say 1 day (configurable).

10. Once the asset expires, future requests to AspireCloud tells AspireUpdate that it doesn’t have the asset, fetches it again in the similar approach as above.

11. The Process repeats as requests are made for updates. Deletgations are made to WordPress.org are made when an asset locally is not available.

## Testing AspireUpdate

### Setting up AspireUpdate

1. [Visit the WP Playground](https://playground.wordpress.net/?blueprint-url=https%3A%2F%2Fraw.githubusercontent.com%2Faspirepress%2FAspireUpdate%2Frefs%2Fheads%2Fplayground-ready%2Fassets%2Fplayground%2Fblueprint.json)to load up WordPress, with AspireUpdate latest stable version..
2. Check `Enable AspireUpdate API Rewrites`.
3. Can leave API Key blank. (not yet generated or enforced)
4. Check `Enable Debug Mode`.
5. Check `String`.
6. Click Save Changes.

### Installing a plugin

1. Navigate to Plugins -> Add New Plugin.
2. Click Install Now beside any plugin.

### Checking the log file

1. Navigate to Error Log Viewer -> Settings.
2. Check `debug-aspire-update.log`.
3. Click Save Changes.
4. Navigate to Error Log Viewer -> Log Monitor.
5. Select full file.
6. Click View.

Expected Results

✅ "Default API Found" entries should reference api.wordpress.org.
✅ "API Rerouted to" entries should reference api.aspirecloud.org.

## 👥 The AspireUpdate Contributors

[AspireUpdate Contributors](https://github.com/aspirepress/AspireUpdate/graphs/contributors)

## FAQs

Q: Why can’t I find the “Favorites” or “Features” tab when adding a new plugin or theme in AspireUpdate?
A: In the current version of AspireUpdate, the “Favorites” and “Features” tabs are unavailable due to compatibility limitations.

## 🚨Issues/Concerns

- Need Another plugin dev/tester
- A REST API dev to develop the AspireCloud
- Need a technical architect for working out the overall design going forward
- Need testers!

## 📝 Upcoming topics

- Get feedback on proposed approach from AP community

## ✅ Action items

- Continue to document a technical architecture
- Divide labour and create projects and tasks and milestones @Yosef Eliezrie

## 🔑 Key links

- Slack: See [#aspireupdate](https://app.slack.com/client/T07Q5LB7W23/C07Q88M2KQF) for discussion

### Configuration

By default the plugin is accessing the api.aspirecloud.org endpoint. There should be no other configuration required. You can turn on the debug log and reset the settings. Use the advanced=true query param in the settings screen to turn on advanced configuration settings.

## Contributing

AspirePress welcomes contributions from people like you. We encourage you to review
our [Contribution Guidelines](https://github.com/aspirepress/.github/blob/main/CONTRIBUTING.md).

## Code of Conduct

AspirePress also implements a [Code of Conduct](https://github.com/aspirepress/.github/blob/main/CODE_OF_CONDUCT.md),
adherance to which is required by all members of the project.

## Credits

AspirePress is a community project, powered by people just like you. Thank you to
our [contributors](https://github.com/aspirepress/.github/blob/main/CREDITS.md) for their generous participation in
AspirePress.
