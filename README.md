# public analytics

I track [web analytics](https://en.wikipedia.org/wiki/Web_analytics) on a number of websites I manage (mostly related to [nimib](https://github.com/pietroppeter/nimib))
and also for some website related to [Nim](https://nim-lang.org) ecosystem (website, scinim, ...).
I like to use for this [plausible analytics](https://plausible.io) which is very easy to use, privacy friendly (compliant with GDPR without needing cookies),
and I also like how Uku and Marko are [building a sustainable open source business](https://plausible.io/blog/open-source-saas).

A feature I like a lot of plausible is the fact that you can make the analytics dashboard **public** 👀 so everybody can actually see the statistics on the site I am tracking.
I feel this is particularly apt for open source projects. I am not aware of other websites having this approach, if you do please let me know.

Here below are all the sites for which I have set up public analytics:

| # | 🌍 site | 📈 analytics | 💻 repository |
|---|---|---|---|
|1.|[nim-lang.org](https://nim-lang.org)|[plausible.io/nim-lang.org](https://plausible.io/nim-lang.org)|[github.com/nim-lang/website](https://github.com/nim-lang/website)|
|2.|[conf.nim-lang.org](https://conf.nim-lang.org)|[plausible.io/conf.nim-lang.org](https://plausible.io/conf.nim-lang.org)|[github.com/nim-lang/conf.nim-lang.org](https://github.com/nim-lang/conf.nim-lang.org)|
|3.|[scinim.github.io/getting-started](https://scinim.github.io/getting-started)|[plausible.io/scinim.github.io%2Fgetting-started](https://plausible.io/scinim.github.io%2Fgetting-started)|[github.com/scinim/getting-started](https://github.com/scinim/getting-started)|
|4.|[pietroppeter.github.io/nimib](https://pietroppeter.github.io/nimib)|[plausible.io/pietroppeter.github.io%2Fnimib](https://plausible.io/pietroppeter.github.io%2Fnimib)|[github.com/pietroppeter/nimib](https://github.com/pietroppeter/nimib)|
|5.|[pietroppeter.github.io/nimibook](https://pietroppeter.github.io/nimibook)|[plausible.io/pietroppeter.github.io%2Fnimibook](https://plausible.io/pietroppeter.github.io%2Fnimibook)|[github.com/pietroppeter/nimibook](https://github.com/pietroppeter/nimibook)|
|6.|[pietroppeter.github.io/nblog](https://pietroppeter.github.io/nblog)|[plausible.io/pietroppeter.github.io%2Fnblog](https://plausible.io/pietroppeter.github.io%2Fnblog)|[github.com/pietroppeter/nblog](https://github.com/pietroppeter/nblog)|
|7.|[pietroppeter.github.io/adventofnim](https://pietroppeter.github.io/adventofnim)|[plausible.io/pietroppeter.github.io%2Fadventofnim](https://plausible.io/pietroppeter.github.io%2Fadventofnim)|[github.com/pietroppeter/adventofnim](https://github.com/pietroppeter/adventofnim)|
|8.|[pietroppeter.github.io/p5nim](https://pietroppeter.github.io/p5nim)|[plausible.io/pietroppeter.github.io%2Fp5nim](https://plausible.io/pietroppeter.github.io%2Fp5nim)|[github.com/pietroppeter/p5nim](https://github.com/pietroppeter/p5nim)|
|9.|[pietroppeter.github.io/wordle-it](https://pietroppeter.github.io/wordle-it)|[plausible.io/pietroppeter.github.io%2Fwordle-it](https://plausible.io/pietroppeter.github.io%2Fwordle-it)|[github.com/pietroppeter/wordle-it](https://github.com/pietroppeter/wordle-it)|
|10.|[par-le.github.io/gioco](https://par-le.github.io/gioco)|[plausible.io/par-le.github.io](https://plausible.io/par-le.github.io)|[github.com/par-le/gioco](https://github.com/par-le/gioco)|

note that on `wordle-it` website statistics are tracked randomly once every N pageviews (N currently 40).

## update table above

Use the following nim script (and update it):

```nim
import std / [strformat, strutils]

# used to update 
let data = [
  ("nim-lang.org", "", "github.com/nim-lang/website"),  # default plausible
  ("conf.nim-lang.org", "", "github.com/nim-lang/conf.nim-lang.org"),
  ("scinim.github.io/getting-started", "", ""), # default github pages
  ("pietroppeter.github.io/nimib", "", ""),
  ("pietroppeter.github.io/nimibook", "", ""),
  ("pietroppeter.github.io/nblog", "", ""),
  ("pietroppeter.github.io/adventofnim", "", ""),
  ("pietroppeter.github.io/p5nim", "", ""),
  ("pietroppeter.github.io/wordle-it", "", ""),
  # not sure why I need this special case for plausible url (maybe some plausible misconfiguration):
  ("par-le.github.io/gioco", "plausible.io/par-le.github.io", ""),
]

var result = """
| # | 🌍 site | 📈 analytics | 💻 repository |
|---|---|---|---|
"""
for i, row in data:
  let
    site = row[0]
    plausible = if row[1].len > 0: row[1] else: "plausible.io/" & site.replace("/", "%2F")
    repo = if row[2].len > 0: row[2] else: "github.com/" & site.replace(".github.io", "")
  result.add &"|{i+1}.|[{site}](https://{site})|[{plausible}](https://{plausible})|[{repo}](https://{repo})|\n"
echo result
```

## opting out

You can opt out with standard ad-blocking or with a simple command in browser console, see https://plausible.io/docs/excluding-localstorage
