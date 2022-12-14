# alfred quicklinks workflow
Workflow to quickly show links from Goodlinks. Oh yeah. it also supports simply fuzzy search.

## Rationale
My work requires me to save a lot of link to internal company resources. I need to access them quite often - few times per day. Previously I kept such links in either Obsidian or save as bookmark in Safari. The thing is, my work is project oriented. In other words, I work on different projects and switch between them few times per day. After some time my safari bookmarks has becomed a mess. Keeping links in Obsidian was a really good option, but this require me to switch to another document while I'm working on other one. So I decided to keep all project related links in GoodLinks and develop this workflow.


## How it works
It basically loads all links from GoodLinks application with specific (configured) tag using some apple scripting (jxa) and with caching.


## Commands
 * **jl** - searchs for links. First load could take a time. After first run by default results will be cached.
 * **jl-settag** - loads all tags from GoodLinks and allows to select one to use as quicklinks.
 * **jl-resetcache** - as it says, resets cache. This could be useful if cache TTL is long (which is recommended).

## Settings

To set default tag use `jl-settag` command within the Alfred.

The following settings are also available thru Alfred workflow configuration:
 * **cache_ttl** - value in minutes. Set it to some big value such as 7 days (10080)  in order not to wait links loading too often (Goodlinks quite slow even with small amount of links)
 * **log_level** - predefined list of values: error, info, debug. By default set to "error". Set to "debug* so script will be more verbous. You don't need to change this settings unless you want to develop a new features for this workflow or fix a bug.
 * **fuzzy_matcher** - allows to select fuzzy matching algorhytm for links search. Possible values are: simple - simply matches symbols; fuzzy - tries to guess strings similarity; sublime like - as it says, tries to mimic sublime strings matching.
 * **simple_matcher_weight** - weight for simple matcher. The more weight - the more strings has to be similar in order to be shown in Alfred results. Value between 0.1 and 1. Default is 0.5.
 * **fuzzy_matcher_weight** - weight for fuzzy matcher. The more weight - the more strings has to be similar in order to be shown in Alfred results. Value between 0.1 and 1. Default is 0.5.
 * **reset_cache_after_add** - indicates that cache has to be invalidated immediately after new link is added. Existence of this variable in workflow context is treat as true.
 * **rebuild_cache_after_add**  - indicates that after link is added and cache is invalidated, workflow will trigger new cache building. Existence of this variable in workflow context is treat as true. Also note that Goodlinks has it's own cache and after addition of a new link does not immediately updates its own cache. In order to get fresh results there is small delay in script (currently 5 seconds).