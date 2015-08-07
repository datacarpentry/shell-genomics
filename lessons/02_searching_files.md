


<!DOCTYPE html>
<html lang="en" class="">
  <head prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb# object: http://ogp.me/ns/object# article: http://ogp.me/ns/article# profile: http://ogp.me/ns/profile#">
    <meta charset='utf-8'>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta http-equiv="Content-Language" content="en">
    <meta name="viewport" content="width=1020">
    
    
    <title>shell-genomics/02_searching_files.md at gh-pages · mckays630/shell-genomics · GitHub</title>
    <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
    <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
    <link rel="apple-touch-icon" sizes="57x57" href="/apple-touch-icon-114.png">
    <link rel="apple-touch-icon" sizes="114x114" href="/apple-touch-icon-114.png">
    <link rel="apple-touch-icon" sizes="72x72" href="/apple-touch-icon-144.png">
    <link rel="apple-touch-icon" sizes="144x144" href="/apple-touch-icon-144.png">
    <meta property="fb:app_id" content="1401488693436528">

      <meta content="@github" name="twitter:site" /><meta content="summary" name="twitter:card" /><meta content="mckays630/shell-genomics" name="twitter:title" /><meta content="shell-genomics - Lesson for the shell for genomics" name="twitter:description" /><meta content="https://avatars0.githubusercontent.com/u/474583?v=3&amp;s=400" name="twitter:image:src" />
      <meta content="GitHub" property="og:site_name" /><meta content="object" property="og:type" /><meta content="https://avatars0.githubusercontent.com/u/474583?v=3&amp;s=400" property="og:image" /><meta content="mckays630/shell-genomics" property="og:title" /><meta content="https://github.com/mckays630/shell-genomics" property="og:url" /><meta content="shell-genomics - Lesson for the shell for genomics" property="og:description" />
      <meta name="browser-stats-url" content="https://api.github.com/_private/browser/stats">
    <meta name="browser-errors-url" content="https://api.github.com/_private/browser/errors">
    <link rel="assets" href="https://assets-cdn.github.com/">
    
    <meta name="pjax-timeout" content="1000">
    

    <meta name="msapplication-TileImage" content="/windows-tile.png">
    <meta name="msapplication-TileColor" content="#ffffff">
    <meta name="selected-link" value="repo_source" data-pjax-transient>

        <meta name="google-analytics" content="UA-3769691-2">

    <meta content="collector.githubapp.com" name="octolytics-host" /><meta content="collector-cdn.github.com" name="octolytics-script-host" /><meta content="github" name="octolytics-app-id" /><meta content="182E58F2:0A7E:121E4FD5:55C3FCE7" name="octolytics-dimension-request_id" />
    
    <meta content="Rails, view, blob#show" data-pjax-transient="true" name="analytics-event" />
    <meta class="js-ga-set" name="dimension1" content="Logged Out">
      <meta class="js-ga-set" name="dimension4" content="Current repo nav">
    <meta name="is-dotcom" content="true">
        <meta name="hostname" content="github.com">
    <meta name="user-login" content="">

      <link rel="icon" sizes="any" mask href="https://assets-cdn.github.com/pinned-octocat.svg">
      <meta name="theme-color" content="#4078c0">
      <link rel="icon" type="image/x-icon" href="https://assets-cdn.github.com/favicon.ico">

    <!-- </textarea> --><!-- '"` --><meta content="authenticity_token" name="csrf-param" />
<meta content="IHOUjnHMDDHFsK968e7XfUevTsmTRo0/HwTqrnDOBdThyMm9gYot/Pn5XEQtdR4hkTZdr5cpDDfGevfBxu2G/A==" name="csrf-token" />
    

    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/github/index-e85c4df2f00f610f7d403b70cb6ff08a89f810737918e84973d175e3c3e31f50.css" media="all" rel="stylesheet" />
    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/github2/index-ef69b63d2441844ee240b72490c991b23eae664f050aa0236621ac6d79ede650.css" media="all" rel="stylesheet" />
    
    


    <meta http-equiv="x-pjax-version" content="70012b92e357cadd9a56e312f3a3769f">

      
  <meta name="description" content="shell-genomics - Lesson for the shell for genomics">
  <meta name="go-import" content="github.com/mckays630/shell-genomics git https://github.com/mckays630/shell-genomics.git">

  <meta content="474583" name="octolytics-dimension-user_id" /><meta content="mckays630" name="octolytics-dimension-user_login" /><meta content="39920691" name="octolytics-dimension-repository_id" /><meta content="mckays630/shell-genomics" name="octolytics-dimension-repository_nwo" /><meta content="true" name="octolytics-dimension-repository_public" /><meta content="true" name="octolytics-dimension-repository_is_fork" /><meta content="32815146" name="octolytics-dimension-repository_parent_id" /><meta content="datacarpentry/shell-genomics" name="octolytics-dimension-repository_parent_nwo" /><meta content="32815146" name="octolytics-dimension-repository_network_root_id" /><meta content="datacarpentry/shell-genomics" name="octolytics-dimension-repository_network_root_nwo" />
  <link href="https://github.com/mckays630/shell-genomics/commits/gh-pages.atom" rel="alternate" title="Recent Commits to shell-genomics:gh-pages" type="application/atom+xml">

  </head>


  <body class="logged_out  env-production  vis-public fork page-blob">
    <a href="#start-of-content" tabindex="1" class="accessibility-aid js-skip-to-content">Skip to content</a>
    <div class="wrapper">
      
      
      



        
        <div class="header header-logged-out" role="banner">
  <div class="container clearfix">

    <a class="header-logo-wordmark" href="https://github.com/" data-ga-click="(Logged out) Header, go to homepage, icon:logo-wordmark">
      <span class="mega-octicon octicon-logo-github"></span>
    </a>

    <div class="header-actions" role="navigation">
        <a class="btn btn-primary" href="/join" data-ga-click="(Logged out) Header, clicked Sign up, text:sign-up">Sign up</a>
      <a class="btn" href="/login?return_to=%2Fmckays630%2Fshell-genomics%2Fblob%2Fgh-pages%2Flessons%2F02_searching_files.md" data-ga-click="(Logged out) Header, clicked Sign in, text:sign-in">Sign in</a>
    </div>

    <div class="site-search repo-scope js-site-search" role="search">
      <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/mckays630/shell-genomics/search" class="js-site-search-form" data-global-search-url="/search" data-repo-search-url="/mckays630/shell-genomics/search" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
  <label class="js-chromeless-input-container form-control">
    <div class="scope-badge">This repository</div>
    <input type="text"
      class="js-site-search-focus js-site-search-field is-clearable chromeless-input"
      data-hotkey="s"
      name="q"
      placeholder="Search"
      aria-label="Search this repository"
      data-global-scope-placeholder="Search GitHub"
      data-repo-scope-placeholder="Search"
      tabindex="1"
      autocapitalize="off">
  </label>
</form>
    </div>

      <ul class="header-nav left" role="navigation">
          <li class="header-nav-item">
            <a class="header-nav-link" href="/explore" data-ga-click="(Logged out) Header, go to explore, text:explore">Explore</a>
          </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="/features" data-ga-click="(Logged out) Header, go to features, text:features">Features</a>
          </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="https://enterprise.github.com/" data-ga-click="(Logged out) Header, go to enterprise, text:enterprise">Enterprise</a>
          </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="/blog" data-ga-click="(Logged out) Header, go to blog, text:blog">Blog</a>
          </li>
      </ul>

  </div>
</div>



      <div id="start-of-content" class="accessibility-aid"></div>
          <div class="site" itemscope itemtype="http://schema.org/WebPage">
    <div id="js-flash-container">
      
    </div>
    <div class="pagehead repohead instapaper_ignore readability-menu ">
      <div class="container">

        <div class="clearfix">
          
<ul class="pagehead-actions">

  <li>
      <a href="/login?return_to=%2Fmckays630%2Fshell-genomics"
    class="btn btn-sm btn-with-count tooltipped tooltipped-n"
    aria-label="You must be signed in to watch a repository" rel="nofollow">
    <span class="octicon octicon-eye"></span>
    Watch
  </a>
  <a class="social-count" href="/mckays630/shell-genomics/watchers">
    1
  </a>

  </li>

  <li>
      <a href="/login?return_to=%2Fmckays630%2Fshell-genomics"
    class="btn btn-sm btn-with-count tooltipped tooltipped-n"
    aria-label="You must be signed in to star a repository" rel="nofollow">
    <span class="octicon octicon-star"></span>
    Star
  </a>

    <a class="social-count js-social-count" href="/mckays630/shell-genomics/stargazers">
      0
    </a>

  </li>

    <li>
      <a href="/login?return_to=%2Fmckays630%2Fshell-genomics"
        class="btn btn-sm btn-with-count tooltipped tooltipped-n"
        aria-label="You must be signed in to fork a repository" rel="nofollow">
        <span class="octicon octicon-repo-forked"></span>
        Fork
      </a>
      <a href="/mckays630/shell-genomics/network" class="social-count">
        7
      </a>
    </li>
</ul>

          <h1 itemscope itemtype="http://data-vocabulary.org/Breadcrumb" class="entry-title public ">
            <span class="mega-octicon octicon-repo-forked"></span>
            <span class="author"><a href="/mckays630" class="url fn" itemprop="url" rel="author"><span itemprop="title">mckays630</span></a></span><!--
         --><span class="path-divider">/</span><!--
         --><strong><a href="/mckays630/shell-genomics" data-pjax="#js-repo-pjax-container">shell-genomics</a></strong>

            <span class="page-context-loader">
              <img alt="" height="16" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-32.gif" width="16" />
            </span>

              <span class="fork-flag">
                <span class="text">forked from <a href="/datacarpentry/shell-genomics">datacarpentry/shell-genomics</a></span>
              </span>
          </h1>
        </div>

      </div>
    </div>

      <div class="container">
        <div class="repository-with-sidebar repo-container new-discussion-timeline ">
          <div class="repository-sidebar clearfix">
              

<nav class="sunken-menu repo-nav js-repo-nav js-sidenav-container-pjax js-octicon-loaders"
     role="navigation"
     data-pjax="#js-repo-pjax-container"
     data-issue-count-url="/mckays630/shell-genomics/issues/counts">
  <ul class="sunken-menu-group">
    <li class="tooltipped tooltipped-w" aria-label="Code">
      <a href="/mckays630/shell-genomics" aria-label="Code" aria-selected="true" class="js-selected-navigation-item selected sunken-menu-item" data-hotkey="g c" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches /mckays630/shell-genomics">
        <span class="octicon octicon-code"></span> <span class="full-word">Code</span>
        <img alt="" class="mini-loader" height="16" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-32.gif" width="16" />
</a>    </li>


    <li class="tooltipped tooltipped-w" aria-label="Pull requests">
      <a href="/mckays630/shell-genomics/pulls" aria-label="Pull requests" class="js-selected-navigation-item sunken-menu-item" data-hotkey="g p" data-selected-links="repo_pulls /mckays630/shell-genomics/pulls">
          <span class="octicon octicon-git-pull-request"></span> <span class="full-word">Pull requests</span>
          <span class="js-pull-replace-counter"></span>
          <img alt="" class="mini-loader" height="16" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-32.gif" width="16" />
</a>    </li>

  </ul>
  <div class="sunken-menu-separator"></div>
  <ul class="sunken-menu-group">

    <li class="tooltipped tooltipped-w" aria-label="Pulse">
      <a href="/mckays630/shell-genomics/pulse" aria-label="Pulse" class="js-selected-navigation-item sunken-menu-item" data-selected-links="pulse /mckays630/shell-genomics/pulse">
        <span class="octicon octicon-pulse"></span> <span class="full-word">Pulse</span>
        <img alt="" class="mini-loader" height="16" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-32.gif" width="16" />
</a>    </li>

    <li class="tooltipped tooltipped-w" aria-label="Graphs">
      <a href="/mckays630/shell-genomics/graphs" aria-label="Graphs" class="js-selected-navigation-item sunken-menu-item" data-selected-links="repo_graphs repo_contributors /mckays630/shell-genomics/graphs">
        <span class="octicon octicon-graph"></span> <span class="full-word">Graphs</span>
        <img alt="" class="mini-loader" height="16" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-32.gif" width="16" />
</a>    </li>
  </ul>


</nav>

                <div class="only-with-full-nav">
                    
<div class="js-clone-url clone-url open"
  data-protocol-type="http">
  <h3><span class="text-emphasized">HTTPS</span> clone URL</h3>
  <div class="input-group js-zeroclipboard-container">
    <input type="text" class="input-mini input-monospace js-url-field js-zeroclipboard-target"
           value="https://github.com/mckays630/shell-genomics.git" readonly="readonly" aria-label="HTTPS clone URL">
    <span class="input-group-button">
      <button aria-label="Copy to clipboard" class="js-zeroclipboard btn btn-sm zeroclipboard-button tooltipped tooltipped-s" data-copied-hint="Copied!" type="button"><span class="octicon octicon-clippy"></span></button>
    </span>
  </div>
</div>

  
<div class="js-clone-url clone-url "
  data-protocol-type="subversion">
  <h3><span class="text-emphasized">Subversion</span> checkout URL</h3>
  <div class="input-group js-zeroclipboard-container">
    <input type="text" class="input-mini input-monospace js-url-field js-zeroclipboard-target"
           value="https://github.com/mckays630/shell-genomics" readonly="readonly" aria-label="Subversion checkout URL">
    <span class="input-group-button">
      <button aria-label="Copy to clipboard" class="js-zeroclipboard btn btn-sm zeroclipboard-button tooltipped tooltipped-s" data-copied-hint="Copied!" type="button"><span class="octicon octicon-clippy"></span></button>
    </span>
  </div>
</div>



  <div class="clone-options">You can clone with
    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/users/set_protocol?protocol_selector=http&amp;protocol_type=clone" class="inline-form js-clone-selector-form " data-form-nonce="074ebea10877b64b202577660aaafbe323553331" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="GYXbzZpsYfOvkFR4AY4ANY+SjhZuLiEEgUMncTPZU0qjCtQ7KTzVaEqYwnbWYHCAiCA5d6aetC8FZSlsQk6xbQ==" /></div><button class="btn-link js-clone-selector" data-protocol="http" type="submit">HTTPS</button></form> or <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/users/set_protocol?protocol_selector=subversion&amp;protocol_type=clone" class="inline-form js-clone-selector-form " data-form-nonce="074ebea10877b64b202577660aaafbe323553331" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="V5xh/SqHTaCxje7qG4Cyw7iUpefMGiNoY3NfqyQIVolpeR+hPQdX5fwxIEWYppgyBUn6xJTNsKyUEEdfUD5ncQ==" /></div><button class="btn-link js-clone-selector" data-protocol="subversion" type="submit">Subversion</button></form>.
    <a href="https://help.github.com/articles/which-remote-url-should-i-use" class="help tooltipped tooltipped-n" aria-label="Get help on which URL is right for you.">
      <span class="octicon octicon-question"></span>
    </a>
  </div>

                  <a href="/mckays630/shell-genomics/archive/gh-pages.zip"
                     class="btn btn-sm sidebar-button"
                     aria-label="Download the contents of mckays630/shell-genomics as a zip file"
                     title="Download the contents of mckays630/shell-genomics as a zip file"
                     rel="nofollow">
                    <span class="octicon octicon-cloud-download"></span>
                    Download ZIP
                  </a>
                </div>
          </div>
          <div id="js-repo-pjax-container" class="repository-content context-loader-container" data-pjax-container>

            

<a href="/mckays630/shell-genomics/blob/f53be96dc0043f51e2f69e6312e9cfd284e78bfe/lessons/02_searching_files.md" class="hidden js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:dca5c5e730b789df069458e517ea1cf0 -->

  <div class="file-navigation js-zeroclipboard-container">
    
<div class="select-menu js-menu-container js-select-menu left">
  <span class="btn btn-sm select-menu-button js-menu-target css-truncate" data-hotkey="w"
    data-ref="gh-pages"
    title="gh-pages"
    role="button" aria-label="Switch branches or tags" tabindex="0" aria-haspopup="true">
    <i>Branch:</i>
    <span class="js-select-button css-truncate-target">gh-pages</span>
  </span>

  <div class="select-menu-modal-holder js-menu-content js-navigation-container" data-pjax aria-hidden="true">

    <div class="select-menu-modal">
      <div class="select-menu-header">
        <span class="select-menu-title">Switch branches/tags</span>
        <span class="octicon octicon-x js-menu-close" role="button" aria-label="Close"></span>
      </div>

      <div class="select-menu-filters">
        <div class="select-menu-text-filter">
          <input type="text" aria-label="Filter branches/tags" id="context-commitish-filter-field" class="js-filterable-field js-navigation-enable" placeholder="Filter branches/tags">
        </div>
        <div class="select-menu-tabs">
          <ul>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="branches" data-filter-placeholder="Filter branches/tags" class="js-select-menu-tab" role="tab">Branches</a>
            </li>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="tags" data-filter-placeholder="Find a tag…" class="js-select-menu-tab" role="tab">Tags</a>
            </li>
          </ul>
        </div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="branches" role="menu">

        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


            <a class="select-menu-item js-navigation-item js-navigation-open selected"
               href="/mckays630/shell-genomics/blob/gh-pages/lessons/02_searching_files.md"
               data-name="gh-pages"
               data-skip-pjax="true"
               rel="nofollow">
              <span class="select-menu-item-icon octicon octicon-check"></span>
              <span class="select-menu-item-text css-truncate-target" title="gh-pages">
                gh-pages
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/mckays630/shell-genomics/blob/master/lessons/02_searching_files.md"
               data-name="master"
               data-skip-pjax="true"
               rel="nofollow">
              <span class="select-menu-item-icon octicon octicon-check"></span>
              <span class="select-menu-item-text css-truncate-target" title="master">
                master
              </span>
            </a>
        </div>

          <div class="select-menu-no-results">Nothing to show</div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="tags">
        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


        </div>

        <div class="select-menu-no-results">Nothing to show</div>
      </div>

    </div>
  </div>
</div>

    <div class="btn-group right">
      <a href="/mckays630/shell-genomics/find/gh-pages"
            class="js-show-file-finder btn btn-sm empty-icon tooltipped tooltipped-nw"
            data-pjax
            data-hotkey="t"
            aria-label="Quickly jump between files">
        <span class="octicon octicon-list-unordered"></span>
      </a>
      <button aria-label="Copy file path to clipboard" class="js-zeroclipboard btn btn-sm zeroclipboard-button tooltipped tooltipped-s" data-copied-hint="Copied!" type="button"><span class="octicon octicon-clippy"></span></button>
    </div>

    <div class="breadcrumb js-zeroclipboard-target">
      <span class="repo-root js-repo-root"><span itemscope="" itemtype="http://data-vocabulary.org/Breadcrumb"><a href="/mckays630/shell-genomics" class="" data-branch="gh-pages" data-pjax="true" itemscope="url"><span itemprop="title">shell-genomics</span></a></span></span><span class="separator">/</span><span itemscope="" itemtype="http://data-vocabulary.org/Breadcrumb"><a href="/mckays630/shell-genomics/tree/gh-pages/lessons" class="" data-branch="gh-pages" data-pjax="true" itemscope="url"><span itemprop="title">lessons</span></a></span><span class="separator">/</span><strong class="final-path">02_searching_files.md</strong>
    </div>
  </div>


  <div class="commit file-history-tease">
    <div class="file-history-tease-header">
        <img alt="@mckays630" class="avatar" height="24" src="https://avatars1.githubusercontent.com/u/474583?v=3&amp;s=48" width="24" />
        <span class="author"><a href="/mckays630" rel="author">mckays630</a></span>
        <time datetime="2015-07-31T20:26:30Z" is="relative-time">Jul 31, 2015</time>
        <div class="commit-title">
            <a href="/mckays630/shell-genomics/commit/f53be96dc0043f51e2f69e6312e9cfd284e78bfe" class="message" data-pjax="true" title="fixed mistake about fastq record">fixed mistake about fastq record</a>
        </div>
    </div>

    <div class="participation">
      <p class="quickstat">
        <a href="#blob_contributors_box" rel="facebox">
          <strong>1</strong>
           contributor
        </a>
      </p>
      
    </div>
    <div id="blob_contributors_box" style="display:none">
      <h2 class="facebox-header">Users who have contributed to this file</h2>
      <ul class="facebox-user-list">
          <li class="facebox-user-list-item">
            <img alt="@mckays630" height="24" src="https://avatars1.githubusercontent.com/u/474583?v=3&amp;s=48" width="24" />
            <a href="/mckays630">mckays630</a>
          </li>
      </ul>
    </div>
  </div>

<div class="file">
  <div class="file-header">
    <div class="file-actions">

      <div class="btn-group">
        <a href="/mckays630/shell-genomics/raw/gh-pages/lessons/02_searching_files.md" class="btn btn-sm " id="raw-url">Raw</a>
          <a href="/mckays630/shell-genomics/blame/gh-pages/lessons/02_searching_files.md" class="btn btn-sm js-update-url-with-hash">Blame</a>
        <a href="/mckays630/shell-genomics/commits/gh-pages/lessons/02_searching_files.md" class="btn btn-sm " rel="nofollow">History</a>
      </div>


          <button type="button" class="octicon-btn disabled tooltipped tooltipped-n" aria-label="You must be signed in to make or propose changes">
            <span class="octicon octicon-pencil"></span>
          </button>

        <button type="button" class="octicon-btn octicon-btn-danger disabled tooltipped tooltipped-n" aria-label="You must be signed in to make or propose changes">
          <span class="octicon octicon-trashcan"></span>
        </button>
    </div>

    <div class="file-info">
        237 lines (157 sloc)
        <span class="file-info-divider"></span>
      8.222 kB
    </div>
  </div>
  
  <div id="readme" class="blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="mainContentOfPage"><h2></h2>

<p>layout: page
title: "The Shell"
comments: true</p>

<h2><a id="user-content-date-2015-07-30" class="anchor" href="#date-2015-07-30" aria-hidden="true"><span class="octicon octicon-link"></span></a>date: 2015-07-30</h2>

<h1><a id="user-content-the-shell" class="anchor" href="#the-shell" aria-hidden="true"><span class="octicon octicon-link"></span></a>The Shell</h1>

<p>Author: Sheldon McKay</p>

<p>Adapted from the lesson by Tracy Teal.
Original contributors:
Paul Wilson, Milad Fatenejad, Sasha Wood and Radhika Khetani for Software Carpentry (<a href="http://software-carpentry.org/">http://software-carpentry.org/</a>)</p>

<h2><a id="user-content-searching-files" class="anchor" href="#searching-files" aria-hidden="true"><span class="octicon octicon-link"></span></a>Searching files</h2>

<p>We showed a little how to search within a file using <code>less</code>. We can also
search within files without even opening them, using <code>grep</code>. Grep is a command-line
utility for searching plain-text data sets for lines matching a string or regular expression.
Let's give it a try!</p>

<p>Suppose we want to see how many reads in our file have really bad, with 10 consecutive Ns<br>
Let's search for the string NNNNNNNNNN in file </p>

<pre><code> grep NNNNNNNNNN SRR098026.fastq
</code></pre>

<p>We get back a lot of lines.  What is we want to see the whole fastq record for each of these read.
We can use the '-B' argument for grep to return the matched line plus one before (-B 1) and two
lines after (-A 2). Since each record is four lines and the last second is the sequence, this should
give the whole record.</p>

<pre><code>grep -B1 -A2 NNNNNNNNNN SRR098026.fastq
</code></pre>

<p>for example:</p>

<pre><code>@SRR098026.177 HWUSI-EAS1599_1:2:1:1:2025 length=35
CNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
+SRR098026.177 HWUSI-EAS1599_1:2:1:1:2025 length=35
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
</code></pre>

<hr>

<p><strong>Exercise</strong></p>

<p>1) Search for the sequence GNATNACCACTTCC in SRR098026.fastq.
In addition to finding the sequence, have your search also return
the name of the sequence.</p>

<p>2) Search for that sequence in both fastq files.</p>

<hr>

<h2><a id="user-content-redirection" class="anchor" href="#redirection" aria-hidden="true"><span class="octicon octicon-link"></span></a>Redirection</h2>

<p>We're excited we have all these sequences that we care about that we
just got from the FASTQ files. That is a really important motif
that is going to help us answer our important question. But all those
sequences just went whizzing by with grep. How can we capture them?</p>

<p>We can do that with something called "redirection". The idea is that
we're redirecting the output to the terminal (all the stuff that went
whizzing by) to something else. In this case, we want to print it
to a file, so that we can look at it later.</p>

<p>The redirection command for putting something in a file is <code>&gt;</code></p>

<p>Let's try it out and put all the sequences that contain 'TTATCCGGATTTATTGGGTTTAAAGGGT'
from all the files in to another file called 'good-data.txt'</p>

<pre><code>grep -B3 NNNNNNNNNN SRR098026.fastq &gt; bad_reads.txt
</code></pre>

<p>The prompt should sit there a little bit, and then it should look like nothing
happened. But type <code>ls</code>. You should have a new file called good-data.txt. Take
a look at it and see if it has what you think it should.</p>

<p>If we use '&gt;&gt;', it will append to rather tha overwrite a file.  This can be useful for
saving more than one search, for example:</p>

<pre><code>grep -B3 NNNNNNNNNN SRR098026.fastq &gt; bad_reads.txt
grep -B3 NNNNNNNNNN SRR097977.fastq &gt;&gt; bad_reads.txt
</code></pre>

<p>There's one more useful redirection command that we're going to show, and that's
called the pipe command, and it is <code>|</code>. It's probably not a key on
your keyboard you use very much. What <code>|</code> does is take the output that
scrolling by on the terminal and then can run it through another command.
When it was all whizzing by before, we wished we could just slow it down and
look at it, like we can with <code>less</code>. Well it turns out that we can! We pipe
the <code>grep</code> command through <code>less</code></p>

<pre><code>grep -B3 NNNNNNNNNN SRR098026.fastq | less
</code></pre>

<p>Now we can use the arrows to scroll up and down and use <code>q</code> to get out.</p>

<p>We can also do something tricky and use the command <code>wc</code>. <code>wc</code> stands for
<code>word count</code>. It counts the number of lines or characters. So, we can use
it to count the number of lines we're getting back from our <code>grep</code> command.
And that will magically tell us how many sequences we're finding. We're</p>

<pre><code>grep -B3 NNNNNNNNNN SRR098026.fastq | wc
</code></pre>

<p>That tells us the number of lines, words and characters in the file. If we
just want the number of lines, we can use the <code>-l</code> flag for <code>lines</code>.</p>

<pre><code>grep -B3 NNNNNNNNNN SRR098026.fastq | wc -l
</code></pre>

<p>Redirecting is not super intuitive, but it's really powerful for stringing
together these different commands, so you can do whatever you need to do.</p>

<p>The philosophy behind these command line programs is that none of them
really do anything all that impressive. BUT when you start chaining
them together, you can do some really powerful things really
efficiently. If you want to be proficient at using the shell, you must
learn to become proficient with the pipe and redirection operators:
<code>|</code>, <code>&gt;</code>, <code>&gt;&gt;</code>.</p>

<p>Finally, let's use the new tools in our kit and a few new ones to example our SRA metadata file.</p>

<pre><code>cd 
cd dc_sample_data/
</code></pre>

<p>Let's ask a few questions about the data</p>

<p>1) How many of the read libraries are paired end?</p>

<p>First, what are the column headers?</p>

<pre><code>head -n 1 SraRunTable.txt
BioSample_s InsertSize_l    LibraryLayout_s Library_Name_s  LoadDate_s  MBases_l    MBytes_l    ReleaseDate_s Run_s SRA_Sample_s Sample_Name_s Assay_Type_s AssemblyName_s BioProject_s Center_Name_s Consent_s Organism_Platform_s SRA_Study_s g1k_analysis_group_s g1k_pop_code_s source_s strain_s
</code></pre>

<p>That's only the first line but it is a lot to take in.  'cut' is a program that will extract columns in tab-delimited
files.  It is a very good command to know.  Lets look at just the first four columns in the header using the '|' readirect
and 'cut'</p>

<pre><code>head -n 1 SraRunTable.txt | cut -f1-4
BioSample_s InsertSize_l      LibraryLayout_s   Library_Name_s    
</code></pre>

<p>'-f1-4' means to cut the first four fields (columns).  The LibraryLayout_s column looks promising.  Let's look at some data for just that column.</p>

<pre><code>cut -f3 SraRunTable.txt | head -n 10
LibraryLayout_s
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
PAIRED
</code></pre>

<p>We can see that there are (at least) two categories, SINGLE and PAIRED.  We want to search all entries in this column
for just PAIRED and count the number of hits.</p>

<pre><code>cut -f3 SraRunTable.txt | grep PAIRED | wc -l
2
</code></pre>

<p>2) How many of each class of library layout are there?</p>

<p>We can use some new tools 'sort' and 'uniq' to extract more information.  For example, cut the third column, remove the
header and sort the values.  The '-v' option for greap means return all lines that DO NOT match.</p>

<pre><code>cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort
</code></pre>

<p>This returns a sorted list (too long to show here) of PAIRED and SINGLE values.  Now we can use 'uniq' with the '-c' flag to
count the different categories.</p>

<pre><code>cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort | uniq -c
  2 PAIRED
 35 SINGLE 
</code></pre>

<p>3) Sort the metadata file by PAIRED/SINGLE and save to a new file
   We can use if '-k' option for sort to specify which column to sort on.  Note that this does something
   similar to cut's '-f'.</p>

<pre><code>sort -k3 SraRunTable.txt &gt; SraRunTable_sorted_by_layout.txt
</code></pre>

<p>4) Extract only paired end records into a new file
   Do we know PAIRED only occurs in column 4?  WE know there are only two in the file, so let's check.</p>

<pre><code>grep PAIRED SraRunTable.txt | wc -l
2
</code></pre>

<p>OK, we are good to go.</p>

<pre><code>grep PAIRED SraRunTable.txt &gt; SraRunTable_only_paired_end.txt
</code></pre>

<hr>

<p><strong>Final Exercise</strong></p>

<p>1) How many sample load dates are there?</p>

<p>2) How many samples were loaded on each date</p>

<p>3) Filter subsets into new files bases on load date</p>

<hr>

<h2><a id="user-content-where-can-i-learn-more-about-the-shell" class="anchor" href="#where-can-i-learn-more-about-the-shell" aria-hidden="true"><span class="octicon octicon-link"></span></a>Where can I learn more about the shell?</h2>

<ul>
<li>Software Carpentry tutorial - <a href="http://software-carpentry.org/v4/shell/index.html">The Unix shell</a></li>
<li>The shell handout - <a href="http://files.fosswire.com/2007/08/fwunixref.pdf">Command Reference</a></li>
<li><a href="http://explainshell.com">explainshell.com</a></li>
<li><a href="http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html">http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html</a></li>
<li>man bash</li>
<li>Google - if you don't know how to do something, try Googling it. Other people
have probably had the same question.</li>
<li>Learn by doing. There's no real other way to learn this than by trying it
out.  Write your next paper in nano (really emacs or vi), open pdfs from
the command line, automate something you don't really need to automate.</li>
</ul>

<h2><a id="user-content-bonus" class="anchor" href="#bonus" aria-hidden="true"><span class="octicon octicon-link"></span></a>Bonus:</h2>

<p><strong>backtick, xargs</strong>: Example find all files with certain text</p>

<p><strong>alias</strong> -&gt; rm -i</p>

<p><strong>variables</strong> -&gt; use a path example</p>

<p><strong>.bashrc</strong></p>

<p><strong>du</strong></p>

<p><strong>ln</strong></p>

<p><strong>ssh and scp</strong></p>

<p><strong>Regular Expressions</strong></p>

<p><strong>Permissions</strong></p>

<p><strong>Chaining commands together</strong></p>
</article>
  </div>

</div>

<a href="#jump-to-line" rel="facebox[.linejump]" data-hotkey="l" style="display:none">Jump to Line</a>
<div id="jump-to-line" style="display:none">
  <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="" class="js-jump-to-line-form" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <input class="linejump-input js-jump-to-line-field" type="text" placeholder="Jump to line&hellip;" aria-label="Jump to line" autofocus>
    <button type="submit" class="btn">Go</button>
</form></div>

          </div>
        </div>
        <div class="modal-backdrop"></div>
      </div>
  </div>


    </div><!-- /.wrapper -->

      <div class="container">
  <div class="site-footer" role="contentinfo">
    <ul class="site-footer-links right">
        <li><a href="https://status.github.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
      <li><a href="https://developer.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li><a href="https://training.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
      <li><a href="https://shop.github.com" data-ga-click="Footer, go to shop, text:shop">Shop</a></li>
        <li><a href="https://github.com/blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a href="https://github.com/about" data-ga-click="Footer, go to about, text:about">About</a></li>
        <li><a href="https://help.github.com" data-ga-click="Footer, go to help, text:help">Help</a></li>

    </ul>

    <a href="https://github.com" aria-label="Homepage">
      <span class="mega-octicon octicon-mark-github" title="GitHub"></span>
</a>
    <ul class="site-footer-links">
      <li>&copy; 2015 <span title="0.03948s from github-fe131-cp1-prd.iad.github.net">GitHub</span>, Inc.</li>
        <li><a href="https://github.com/site/terms" data-ga-click="Footer, go to terms, text:terms">Terms</a></li>
        <li><a href="https://github.com/site/privacy" data-ga-click="Footer, go to privacy, text:privacy">Privacy</a></li>
        <li><a href="https://github.com/security" data-ga-click="Footer, go to security, text:security">Security</a></li>
        <li><a href="https://github.com/contact" data-ga-click="Footer, go to contact, text:contact">Contact</a></li>
    </ul>
  </div>
</div>


    <div class="fullscreen-overlay js-fullscreen-overlay" id="fullscreen_overlay">
  <div class="fullscreen-container js-suggester-container">
    <div class="textarea-wrap">
      <textarea name="fullscreen-contents" id="fullscreen-contents" class="fullscreen-contents js-fullscreen-contents" placeholder="" aria-label=""></textarea>
      <div class="suggester-container">
        <div class="suggester fullscreen-suggester js-suggester js-navigation-container"></div>
      </div>
    </div>
  </div>
  <div class="fullscreen-sidebar">
    <a href="#" class="exit-fullscreen js-exit-fullscreen tooltipped tooltipped-w" aria-label="Exit Zen Mode">
      <span class="mega-octicon octicon-screen-normal"></span>
    </a>
    <a href="#" class="theme-switcher js-theme-switcher tooltipped tooltipped-w"
      aria-label="Switch themes">
      <span class="octicon octicon-color-mode"></span>
    </a>
  </div>
</div>



    
    
    

    <div id="ajax-error-message" class="flash flash-error">
      <span class="octicon octicon-alert"></span>
      <a href="#" class="octicon octicon-x flash-close js-ajax-error-dismiss" aria-label="Dismiss error"></a>
      Something went wrong with that request. Please try again.
    </div>


      <script crossorigin="anonymous" src="https://assets-cdn.github.com/assets/frameworks-a5550e0bb066809cdc63a2cb60405556f966a5493a91004512f8df5d524376aa.js"></script>
      <script async="async" crossorigin="anonymous" src="https://assets-cdn.github.com/assets/github/index-37dcf3694f94f84a19aa47b4cf8c7deea0666a4085b0e90f6e4212da65c4a8fb.js"></script>
      
      
  </body>
</html>

