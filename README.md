## GitHub Metrics: What's Possible for User Downloads? (Sep 2017)

This article was spurred by a question from [@MathCancer](https://twitter.com/MathCancer/status/913020325964771328) about obtaining download metrics from GitHub. More specifically, for academics providing open source software on GitHub, how can they track downloads? Regardless of one's opinion about the value of this metric, it would be a welcome GitHub service.

TL;DR

* GitHub seems to place more emphasis on developer/contributor metrics than user metrics

* it's possible to obtain stats about "Traffic", but it's just for the previous 14-days and it's just for clones and views and doesn't include, for example, downloaded releases.
* it's possible to upload a "binary" asset (e.g. a .zip, .tar.gz, .exe) as part of a Release and, using the [GitHub API](https://developer.github.com/v3/), obtain the number of times an asset was downloaded (over all time). However, it's not possible to have a binary asset replace  "Source code" (.zip or .tar.gz) in the Release section. 

We try to capture the UI for this in the following section and then share the email thread with GitHub Support at the end.

<hr>

## Obtaining user metrics?

![caption](/images/github-repo-Insights.jpeg "my caption")
![caption](/images/github-Insights-Graphs-Traffic.jpeg "my caption")
![caption](/images/github-releases-0-annotate.jpeg "my caption")
![caption](/images/github-new-release-0.jpeg "my caption")
![caption](/images/github-new-release-1.jpeg "my caption")
![caption](/images/github-new-release-2.jpeg "my caption")
![caption](/images/github-attach-binaries.jpeg "my caption")
![caption](/images/github-metrics8-after-download.jpeg "my caption")


```
$ curl -s https://api.github.com/repos/rheiland/cmake_learn/releases | grep download_count
        "download_count": 2,
```
<hr>

## Email thread with GitHub support
To: support@github.com

Hello,

I just created a release (v1.0) for one of my repos, then downloaded it (.tar.gz), then tried to use your API to see if it would give me the “download_count”. It does not seem to (below). Am I doing something wrong? Is there a delay in registering the download?

thanks, Randy
```
$ curl -s https://api.github.com/repos/rheiland/authpy/releases
[
 {
   "url": "https://api.github.com/repos/rheiland/authpy/releases/7913617",
   "assets_url": "https://api.github.com/repos/rheiland/authpy/releases/7913617/assets",
   ...
   "assets": [

   ],
   "tarball_url": "https://api.github.com/repos/rheiland/authpy/tarball/v1.0",
   "zipball_url": "https://api.github.com/repos/rheiland/authpy/zipball/v1.0",
   "body": ""
 }
]
```
<!------------------>
<hr>

On Thu, Sep 28, 2017 ... <support@github.com> wrote:

Hi Randy,

> why can't I see download_count?

The assets array in the <i>/releases</i> response will only include information about binary files that are attached to a release, not the source code itself. Those source code archives are stored differently than the uploaded assets (the archives are generated on demand, while the assets are actually stored somewhere), and for that reason we don't track download counts for archives currently. It might be something we add in the future, but I can't say when it might happen.

If you're interested in more general statistics, the <i>/traffic</i> endpoint might be helpful:

https://developer.github.com/v3/repos/traffic/#clones

Let me know if there's anything else I can help you with!

All the best,
xxx
<!---------------->
<hr>
xxx,

Thanks for the reply and explaining about the attached binary files to a release. So I just verified that I can indeed attach a "binary" .tar.gz, for example, and if I download that, it appears in the "download_count" in the API call. <b>So can I delete the source code archives after generating them, leaving only uploaded assets?</b>

The <i>/traffic</i> endpoint does me no good, really. A 14 day history is almost meaningless. And only "clones"? I eventually want metrics of ALL downloads associated with a repo. (And I would assume lots of academics would as well).

-Randy
<!------------------>
<hr>
Hi Randy,

> *So can I delete the source code archives after generating
> them, leaving only uploaded assets?*

Right now that's not possible, but I can see how that would be really useful in this case, so I'll pass that on to the team for consideration.

> I eventually want metrics of ALL downloads
> associated with a repo. (And I would assume lots of academics would as well).

More detailed traffic/clone/download metrics are definitely on our radar, as we know that it's something the education/research communities would really appreciate. I can't say when changes like this might be made, but I've added your request to our discussion around this issue.

Thanks,
xxx


