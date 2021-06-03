Most tests have been running in LUCI for multiple flutter repositories, including [post-submit framework](https://flutter-dashboard.appspot.com/#/build), [pre-submit frameowrk](https://ci.chromium.org/p/flutter/g/framework-try/builders), etc. This page uses framework as an example, and talks about what to do when a LUCI build failure happens.

## Infra Failure
An infra failure shows up as a purple box in the dashboards:

* Framework post-submit build dashboard: [[/images/luci_post_submit_infra_failure.png|luci_post_submit_infra_failure]]
* Framework pre-submit build console: [[/images/luci_pre_submit_infra_failure.png|luci_pre_submit_infra_failure]]

### Overview of an infra failure build
An example build: [Linux color_filter_and_fade_perf__e2e_summary](https://ci.chromium.org/ui/p/flutter/builders/prod/Linux%20color_filter_and_fade_perf__e2e_summary/1563/overview)

<img src="https://raw.githubusercontent.com/wiki/flutter/flutter/images/luci_infra_failure_overview.png" align="center" height="450" width="800"/>

*  (i) Link to the historical build list of this builder
*  (ii) A quick glimpse of the infra failure 
*  (iii) The step list of this builder, defined by the recipe on the right
*  (iv) The real failed step causing the build failure 
*  (v) Check `stdout` for detailed log
### What to do
1. Check if the infra failure has happened on earlier builds by clicking (i)
2. Check if issue already exists in the [infra bug pool](https://github.com/flutter/flutter/issues?q=is%3Aopen+is%3Aissue+label%3A%22team%3A+infra%22)
3. If not, file [an infra bug](https://github.com/flutter/flutter/issues/new?assignees=&labels=team%3A+infra&template=6_infrastructure.md&title=)
4. If this is a blocking failure, please add Projects [`Infra Ticket Queue`](https://github.com/flutter/flutter/wiki/Infra-Ticket-Queue). The infra gardener will scan through the queue frequently.
5. If you want to get an immediate help, please ask in the discord `hackers-infra` channel
6. If this is an infra flake, and a retry is needed
   *  For pre-submit test, click `Re-run` in the [check run page](https://github.com/flutter/flutter/pull/83894/checks?check_run_id=2738146673): [[/images/luci_pre_submit_rerun.png|luci_pre_submit_rerun]]
   *  For post-submit test, login to [framework build dashboard](https://flutter-dashboard.appspot.com/#/build), click the task box, and click `RERUN`: [[/images/luci_post_submit_rerun.png|luci_post_submit_rerun]]

### Difference of Engine from framework repo
