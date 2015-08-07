


<!DOCTYPE html>
<html lang="en" class="">
  <head prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb# object: http://ogp.me/ns/object# article: http://ogp.me/ns/article# profile: http://ogp.me/ns/profile#">
    <meta charset='utf-8'>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta http-equiv="Content-Language" content="en">
    <meta name="viewport" content="width=1020">
    
    
    <title>shell-genomics/01_the_filesystem.md at gh-pages · mckays630/shell-genomics · GitHub</title>
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

    <meta content="collector.githubapp.com" name="octolytics-host" /><meta content="collector-cdn.github.com" name="octolytics-script-host" /><meta content="github" name="octolytics-app-id" /><meta content="182E58F2:0A7E:121E3CC6:55C3FCDB" name="octolytics-dimension-request_id" />
    
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
<meta content="dsim4EZYxcpbeUfxtGPnrRAlPkmoJpN/D/9RLSrFfqGYru77bGwF5BbmXpkWQyrxrjbCMglcs1e9rK2VXS+YbA==" name="csrf-token" />
    

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
      <a class="btn" href="/login?return_to=%2Fmckays630%2Fshell-genomics%2Fblob%2Fgh-pages%2Flessons%2F01_the_filesystem.md" data-ga-click="(Logged out) Header, clicked Sign in, text:sign-in">Sign in</a>
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
    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/users/set_protocol?protocol_selector=http&amp;protocol_type=clone" class="inline-form js-clone-selector-form " data-form-nonce="53b25279ce6366b9a3227d9afadff71c4004566d" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="hhhNN5uZbRIy8R9rz9jYS6QdufvHCpEuL02JbKw28Q1lR0B/JhxwNmziWmlf17HsflhCqUwbxDPxAPdLFKPapw==" /></div><button class="btn-link js-clone-selector" data-protocol="http" type="submit">HTTPS</button></form> or <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/users/set_protocol?protocol_selector=subversion&amp;protocol_type=clone" class="inline-form js-clone-selector-form " data-form-nonce="53b25279ce6366b9a3227d9afadff71c4004566d" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="vxKkdvDgooCEPOpOwXRo95m4wHnGfVxXwKooZLRvjgl1zLVYlRh3tzMB41VMW+8MXBxBBsBcJ0XOlTaDD9ZjrA==" /></div><button class="btn-link js-clone-selector" data-protocol="subversion" type="submit">Subversion</button></form>.
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

            

<a href="/mckays630/shell-genomics/blob/f53be96dc0043f51e2f69e6312e9cfd284e78bfe/lessons/01_the_filesystem.md" class="hidden js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:0cc9daf79f2aaadab94bfbfae556d773 -->

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
               href="/mckays630/shell-genomics/blob/gh-pages/lessons/01_the_filesystem.md"
               data-name="gh-pages"
               data-skip-pjax="true"
               rel="nofollow">
              <span class="select-menu-item-icon octicon octicon-check"></span>
              <span class="select-menu-item-text css-truncate-target" title="gh-pages">
                gh-pages
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/mckays630/shell-genomics/blob/master/lessons/01_the_filesystem.md"
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
      <span class="repo-root js-repo-root"><span itemscope="" itemtype="http://data-vocabulary.org/Breadcrumb"><a href="/mckays630/shell-genomics" class="" data-branch="gh-pages" data-pjax="true" itemscope="url"><span itemprop="title">shell-genomics</span></a></span></span><span class="separator">/</span><span itemscope="" itemtype="http://data-vocabulary.org/Breadcrumb"><a href="/mckays630/shell-genomics/tree/gh-pages/lessons" class="" data-branch="gh-pages" data-pjax="true" itemscope="url"><span itemprop="title">lessons</span></a></span><span class="separator">/</span><strong class="final-path">01_the_filesystem.md</strong>
    </div>
  </div>


  <div class="commit file-history-tease">
    <div class="file-history-tease-header">
        <img alt="@mckays630" class="avatar" height="24" src="https://avatars1.githubusercontent.com/u/474583?v=3&amp;s=48" width="24" />
        <span class="author"><a href="/mckays630" rel="author">mckays630</a></span>
        <time datetime="2015-07-30T16:15:09Z" is="relative-time">Jul 30, 2015</time>
        <div class="commit-title">
            <a href="/mckays630/shell-genomics/commit/e19aedc1b0c1bfbd4e7dae99ca005eb6a9a9bbab" class="message" data-pjax="true" title="breaking out lessons">breaking out lessons</a>
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
        <a href="/mckays630/shell-genomics/raw/gh-pages/lessons/01_the_filesystem.md" class="btn btn-sm " id="raw-url">Raw</a>
          <a href="/mckays630/shell-genomics/blame/gh-pages/lessons/01_the_filesystem.md" class="btn btn-sm js-update-url-with-hash">Blame</a>
        <a href="/mckays630/shell-genomics/commits/gh-pages/lessons/01_the_filesystem.md" class="btn btn-sm " rel="nofollow">History</a>
      </div>


          <button type="button" class="octicon-btn disabled tooltipped tooltipped-n" aria-label="You must be signed in to make or propose changes">
            <span class="octicon octicon-pencil"></span>
          </button>

        <button type="button" class="octicon-btn octicon-btn-danger disabled tooltipped tooltipped-n" aria-label="You must be signed in to make or propose changes">
          <span class="octicon octicon-trashcan"></span>
        </button>
    </div>

    <div class="file-info">
        689 lines (448 sloc)
        <span class="file-info-divider"></span>
      21.49 kB
    </div>
  </div>
  
  <div id="readme" class="blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="mainContentOfPage"><table data-table-type="yaml-metadata">
  <thead>
  <tr>
  <th>layout</th>

  <th>title</th>

  <th>comments</th>

  <th>date</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div>page</div></td>

  <td><div>The Shell</div></td>

  <td><div>true</div></td>

  <td><div>2014-07-30</div></td>
  </tr>
  </tbody>
</table>

<h1><a id="user-content-the-shell" class="anchor" href="#the-shell" aria-hidden="true"><span class="octicon octicon-link"></span></a>The Shell</h1>

<p>Author: Sheldon McKay  </p>

<p>Adapted from the lesson by Tracy Teal.
Original contributors:
Paul Wilson, Milad Fatenejad, Sasha Wood and Radhika Khetani for Software Carpentry (<a href="http://software-carpentry.org/">http://software-carpentry.org/</a>)</p>

<h2><a id="user-content-learning-objectives" class="anchor" href="#learning-objectives" aria-hidden="true"><span class="octicon octicon-link"></span></a>Learning Objectives</h2>

<ul>
<li>What is the shell?</li>
<li>How do you access it?</li>
<li>How do you use it?

<ul>
<li>Getting around the Unix file system</li>
<li>looking at files</li>
<li>manipulating files</li>
<li>automating tasks</li>
</ul></li>
<li>What is it good for?</li>
<li>Where are resources where I can learn more? (because the shell is awesome)</li>
</ul>

<h2><a id="user-content-what-is-the-shell" class="anchor" href="#what-is-the-shell" aria-hidden="true"><span class="octicon octicon-link"></span></a>What is the shell?</h2>

<p>The <em>shell</em> is a program that presents a command line interface
which allows you to control your computer using commands entered
with a keyboard instead of controlling graphical user interfaces
(GUIs) with a mouse/keyboard combination.</p>

<p>There are many reasons to learn about the shell.</p>

<ul>
<li>For most bioinformatics tools, you have to use the shell. There is no
graphical interface. If you want to work in metagenomics or genomics you're
going to need to use the shell.</li>
<li>The shell gives you <em>power</em>. The command line gives you the power to do your work more efficiently and
more quickly.  When you need to do things tens to hundreds of times,
knowing how to use the shell is transformative.</li>
<li>To use remote computers or cloud computing, you need to use the shell.</li>
</ul>

<p><a href="/mckays630/shell-genomics/blob/gh-pages/img/gvng.jpg" target="_blank"><img src="/mckays630/shell-genomics/raw/gh-pages/img/gvng.jpg" alt="Automation" style="max-width:100%;"></a></p>

<p>Unix is user-friendly. It's just very selective about who its friends are.</p>

<p>Today we're going to go through how to access Unix/Linux and some of the basic
shell commands.</p>

<h2><a id="user-content-information-on-the-shell" class="anchor" href="#information-on-the-shell" aria-hidden="true"><span class="octicon octicon-link"></span></a>Information on the shell</h2>

<p>shell cheat sheets:<br></p>

<ul>
<li><a href="http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/">http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/</a></li>
<li><a href="https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md">https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md</a></li>
</ul>

<p>Explain shell - a web site where you can see what the different components of
a shell command are doing.  </p>

<ul>
<li><a href="http://explainshell.com">http://explainshell.com</a></li>
<li><a href="http://www.commandlinefu.com">http://www.commandlinefu.com</a></li>
</ul>

<h2><a id="user-content-how-to-access-the-shell" class="anchor" href="#how-to-access-the-shell" aria-hidden="true"><span class="octicon octicon-link"></span></a>How to access the shell</h2>

<p>The shell is already available on Mac and Linux. For Windows, you'll
have to download a separate program.</p>

<h2><a id="user-content-mac" class="anchor" href="#mac" aria-hidden="true"><span class="octicon octicon-link"></span></a>Mac</h2>

<p>On Mac the shell is available through Terminal<br>
Applications -&gt; Utilities -&gt; Terminal<br>
Go ahead and drag the Terminal application to your Dock for easy access.</p>

<h2><a id="user-content-windows" class="anchor" href="#windows" aria-hidden="true"><span class="octicon octicon-link"></span></a>Windows</h2>

<p>For Windows, we're going to be using gitbash.<br>
Download and install <a href="http://msysgit.github.io">gitbash</a>;
Open up the program.</p>

<h2><a id="user-content-linux--" class="anchor" href="#linux--" aria-hidden="true"><span class="octicon octicon-link"></span></a>Linux  </h2>

<p>You should be set.</p>

<h2><a id="user-content-starting-with-the-shell" class="anchor" href="#starting-with-the-shell" aria-hidden="true"><span class="octicon octicon-link"></span></a>Starting with the shell</h2>

<p>We will spend most of our time learning about the basics of the shell
by manipulating some experimental data.</p>

<p>Now we're going to download the data for the tutorial. For this you'll need
internet access, because you're going to get it off the web.  </p>

<p>We're going to be working with data on our remote server.</p>

<p>After loggin on, let's check out the example data.</p>

<p>Let's go into the sample data  directory</p>

<pre><code>  cd dc_sample data
</code></pre>

<p>'cd' stands for 'change directory'</p>

<p>Let's see what is in here. Type
      ls</p>

<p>You will see
    sra_metadata  untrimmed_fastq</p>

<p>ls stands for 'list' and it lists the contents of a directory.</p>

<p>There are two items listed.  What are they? We can use a command line argumant with 'ls' to get more information.</p>

<pre><code>  ls -F
  sra_metadata/  untrimmed_fastq/
</code></pre>

<p>Anything with a "/" after it is a directory.<br>
Things with a "*" after them are programs.<br>
It there are nodecorations, it's a file.</p>

<p>You can also use the command</p>

<pre><code>ls -l
drwxr-x--- 2 dcuser sudo 4096 Jul 30 11:37 sra_metadata
drwxr-xr-x 2 dcuser sudo 4096 Jul 30 11:38 untrimmed_fastq
</code></pre>

<p>to see whether items in a directory are files or directories. <code>ls -l</code> gives a lot more
information too.</p>

<p>Let's go into the untrimmed_fastq directory and see what is in there.</p>

<pre><code>cd untrimmed_fastq
ls -F
SRR097977.fastq  SRR098026.fastq
</code></pre>

<p>There are two items in this directory with no trailing slash, so they are files.</p>

<h2><a id="user-content-arguments" class="anchor" href="#arguments" aria-hidden="true"><span class="octicon octicon-link"></span></a>Arguments</h2>

<p>Most programs take additional arguments that control their exact
behavior. For example, <code>-F</code> and <code>-l</code> are arguments to <code>ls</code>.  The <code>ls</code>
program, like many programs, take a lot of arguments. Another useful one is '-a',
which show everything, including hidden files.  How do we
know what the options are to particular commands?</p>

<p>Most commonly used shell programs have a manual. You can access the
manual using the <code>man</code> program. Try entering:</p>

<pre><code>man ls
</code></pre>

<p>This will open the manual page for <code>ls</code>. Use the space key to go
forward and b to go backwards. When you are done reading, just hit <code>q</code>
to quit.</p>

<p>Programs that are run from the shell can get extremely complicated. To
see an example, open up the manual page for the <code>find</code> program.
No one can possibly learn all of
these arguments, of course. So you will probably find yourself
referring back to the manual page frequently.</p>

<h2><a id="user-content-the-unix-directory-file-structure-aka-where-am-i" class="anchor" href="#the-unix-directory-file-structure-aka-where-am-i" aria-hidden="true"><span class="octicon octicon-link"></span></a>The Unix directory file structure (a.k.a. where am I?)</h2>

<p>As you've already just seen, you can move around in different directories
or folders at the command line. Why would you want to do this, rather
than just navigating around the normal way.</p>

<p>When you're working with bioinformatics programs, you're working with
your data and it's key to be able to have that data in the right place
and make sure the program has access to the data. Many of the problems
people run in to with command line bioinformatics programs is not having the
data in the place the program expects it to be.</p>

<h2><a id="user-content-moving-around-the-file-system" class="anchor" href="#moving-around-the-file-system" aria-hidden="true"><span class="octicon octicon-link"></span></a>Moving around the file system</h2>

<p>Let's practice moving around a bit.</p>

<p>We're going to work in that <code>dc_sample_data</code> directory.</p>

<p>First we did something like go to the folder of our username. Then we opened
'dc_sample_data' then 'data'</p>

<p>Let's draw out how that went.</p>

<p>Now let's draw some of the other files and folders we could have clicked on.</p>

<p>This is called a hierarchical file system structure, like an upside down tree
with root (/) at the base that looks like this.</p>

<p><a href="/mckays630/shell-genomics/blob/gh-pages/img/Slide1.jpg" target="_blank"><img src="/mckays630/shell-genomics/raw/gh-pages/img/Slide1.jpg" alt="Unix" style="max-width:100%;"></a></p>

<p>That (/) at the base is often also called the 'top' level.</p>

<p>When you are working at your computer or log in to a remote computer,
you are on one of the branches of that tree, your home directory (/home/dcuser)</p>

<p>Now let's go do that same navigation at the command line.</p>

<p>Type</p>

<pre><code> cd
</code></pre>

<p>This puts you in your home directory. This folder here.</p>

<p>Now using <code>cd</code> and <code>ls</code>, go in to the 'dc_sample_data' directory and list its contents.</p>

<p>Let's also check to see where we are. Sometimes when we're wandering around
in the file system, it's easy to lose track of where we are and get lost.</p>

<p>If you want to know what directory you're currently in, type</p>

<pre><code> pwd
</code></pre>

<p>This stands for 'print working directory'. The directory you're currently working in.</p>

<p>What if we want to move back up and out of the 'data' directory? Can we just
type <code>cd dc_sample_data</code>? Try it and see what happens.</p>

<p>To go 'back up a level' we need to use <code>..</code></p>

<p>Type</p>

<pre><code> cd ..
</code></pre>

<p>Now do <code>ls</code> and <code>pwd</code>. See now that we went back up in to the 'dc_sample_data'
directory. <code>..</code> means go back up a level.</p>

<hr>

<p><strong>Exercise</strong></p>

<p>Now we're going to try a hunt.  Find a hidden directory in dc_sample_data list its contents
and file the text file in there.  What is the name of the file?</p>

<p>Hint: hidden files and folders in unix start with '.', for example .my_hidden_directory</p>

<hr>

<h2><a id="user-content-examining-the-contents-of-other-directories" class="anchor" href="#examining-the-contents-of-other-directories" aria-hidden="true"><span class="octicon octicon-link"></span></a>Examining the contents of other directories</h2>

<p>By default, the <code>ls</code> commands lists the contents of the working
directory (i.e. the directory you are in). You can always find the
directory you are in using the <code>pwd</code> command. However, you can also
give <code>ls</code> the names of other directories to view. Navigate to the
home directory if you are not already there.</p>

<p>Type:</p>

<pre><code>cd
</code></pre>

<p>Then enter the command:</p>

<pre><code>ls dc_sample_data
</code></pre>

<p>This will list the contents of the <code>dc_sample_data</code> directory without
you having to navigate there.</p>

<p>The <code>cd</code> command works in a similar way. Try entering:</p>

<pre><code>cd
cd dc_sample_data/untrimmed_fastq
</code></pre>

<p>and you will jump directly to <code>untrimmed_fastq</code> without having to go through
the intermediate directory.</p>

<hr>

<p><strong>Exercise</strong></p>

<p>List the 'SRR097977.fastq' file from your home directory without changing directories</p>

<hr>

<h3><a id="user-content-shortcut-tab-completion" class="anchor" href="#shortcut-tab-completion" aria-hidden="true"><span class="octicon octicon-link"></span></a>Shortcut: Tab Completion</h3>

<p>Navigate to the home directory. Typing out directory names can waste a
lot of time. When you start typing out the name of a directory, then
hit the tab key, the shell will try to fill in the rest of the
directory name. For example, type <code>cd</code> to get back to your home directy, then enter:</p>

<pre><code>cd dc_&lt;tab&gt;
</code></pre>

<p>The shell will fill in the rest of the directory name for
<code>dc_sample_data</code>. Now go to dc_sample_data/untrimmed_fastq</p>

<pre><code>ls SR&lt;tab&gt;&lt;tab&gt;
</code></pre>

<p>When you hit the first tab, nothing happens. The reason is that there
are multiple directories in the home directory which start with
<code>SR</code>. Thus, the shell does not know which one to fill in. When you hit
tab again, the shell will list the possible choices.</p>

<p>Tab completion can also fill in the names of programs. For example,
enter <code>e&lt;tab&gt;&lt;tab&gt;</code>. You will see the name of every program that
starts with an <code>e</code>. One of those is <code>echo</code>. If you enter <code>ec&lt;tab&gt;</code> you
will see that tab completion works.</p>

<h2><a id="user-content-full-vs-relative-paths" class="anchor" href="#full-vs-relative-paths" aria-hidden="true"><span class="octicon octicon-link"></span></a>Full vs. Relative Paths</h2>

<p>The <code>cd</code> command takes an argument which is the directory
name. Directories can be specified using either a <em>relative</em> path or a
full <em>path</em>. The directories on the computer are arranged into a
hierarchy. The full path tells you where a directory is in that
hierarchy. Navigate to the home directory. Now, enter the <code>pwd</code>
command and you should see:</p>

<pre><code>/home/dcuser
</code></pre>

<p>which is the full name of your home directory. This tells you that you
are in a directory called <code>dcuser</code>, which sits inside a directory called
<code>home</code> which sits inside the very top directory in the hierarchy. The
very top of the hierarchy is a directory called <code>/</code> which is usually
referred to as the <em>root directory</em>. So, to summarize: <code>dcuser</code> is a
directory in <code>home</code> which is a directory in <code>/</code>.</p>

<p>Now enter the following command:</p>

<pre><code>cd /home/dcuser/dc_sample_data/.hidden
</code></pre>

<p>This jumps to <code>.hidden</code>. Now go back to the home directory (cd). We saw
earlier that the command:</p>

<pre><code>cd dc_sample_data/.hidden
</code></pre>

<p>had the same effect - it took us to the <code>hidden</code> directory. But,
instead of specifying the full path
(<code>/home/dcuser/dc_sample_data/data</code>), we specified a <em>relative path</em>. In
other words, we specified the path relative to our current
directory. A full path always starts with a <code>/</code>. A relative path does
not.</p>

<p>A relative path is like getting directions
from someone on the street. They tell you to "go right at the Stop sign, and
then turn left on Main Street". That works great if you're standing there
together, but not so well if you're trying to tell someone how to get there
from another country. A full path is like GPS coordinates.
It tells you exactly where something
is no matter where you are right now.</p>

<p>You can usually use either a full path or a relative path
depending on what is most convenient. If we are in the home directory,
it is more convenient to just enter the relative path since it
involves less typing.</p>

<p>Over time, it will become easier for you to keep a mental note of the
structure of the directories that you are using and how to quickly
navigate amongst them.</p>

<hr>

<p><strong>Exercise</strong></p>

<p>Now, list the contents of the /bin directory. Do you see anything
familiar in there? 
How can you tell these are programs rather than plain files?</p>

<hr>

<h2><a id="user-content-saving-time-with-shortcuts-wild-cards-and-tab-completion" class="anchor" href="#saving-time-with-shortcuts-wild-cards-and-tab-completion" aria-hidden="true"><span class="octicon octicon-link"></span></a>Saving time with shortcuts, wild cards, and tab completion</h2>

<h3><a id="user-content-shortcuts" class="anchor" href="#shortcuts" aria-hidden="true"><span class="octicon octicon-link"></span></a>Shortcuts</h3>

<p>There are some shortcuts which you should know about. Dealing with the
home directory is very common. So, in the shell the tilde character,
""~"", is a shortcut for your home directory. Navigate to the <code>dc_sample_data</code>
directory:</p>

<pre><code>cd
cd dc_sample_data
</code></pre>

<p>Then enter the command:</p>

<pre><code>ls ~
</code></pre>

<p>This prints the contents of your home directory, without you having to
type the full path. The shortcut <code>..</code> always refers to the directory
above your current directory. Thus:</p>

<pre><code>ls ..
</code></pre>

<p>prints the contents of the <code>/home/dcuser/dc_sample_data</code>. You can chain
these together, so:</p>

<pre><code>ls ../../
</code></pre>

<p>prints the contents of <code>/home/dcuser</code> which is your home
directory. Finally, the special directory <code>.</code> always refers to your
current directory. So, <code>ls</code>, <code>ls .</code>, and <code>ls ././././.</code> all do the
same thing, they print the contents of the current directory. This may
seem like a useless shortcut right now, but we'll see when it is
needed in a little while.</p>

<p>To summarize, while you are in the <code>shell</code> directory, the commands
<code>ls ~</code>, <code>ls ~/.</code>, <code>ls ../../</code>, and <code>ls /home/dcuser</code> all do exactly the
same thing. These shortcuts are not necessary, they are provided for
your convenience.</p>

<h3><a id="user-content-our-data-set-fastq-files" class="anchor" href="#our-data-set-fastq-files" aria-hidden="true"><span class="octicon octicon-link"></span></a>Our data set: FASTQ files</h3>

<p>We did an experiment and want to look at sequencing results.
We want to be able to look at these files and do some things with them.</p>

<h3><a id="user-content-wild-cards" class="anchor" href="#wild-cards" aria-hidden="true"><span class="octicon octicon-link"></span></a>Wild cards</h3>

<p>Navigate to the <code>~/dc_sample_data/data/untrimmed_fastq</code> directory. This
directory contains our FASTQ files.</p>

<p>The <code>*</code> character is a shortcut for "everything". Thus, if
you enter <code>ls *</code>, you will see all of the contents of a given
directory. Now try this command:</p>

<pre><code>ls *fastq
</code></pre>

<p>This lists every file that ends with a <code>fastq</code>. This command:</p>

<pre><code>ls /usr/bin/*.sh
</code></pre>

<p>Lists every file in <code>/usr/bin</code> that ends in the characters <code>.sh</code>.</p>

<pre><code>ls *977.fastq
</code></pre>

<p>lists only the file that ends with '977.fastq'</p>

<p>So how does this actually work? Well...when the shell (bash) sees a
word that contains the <code>*</code> character, it automatically looks for filenames
that match the given pattern. </p>

<p>We can use the command 'echo' to see wilcards are they are intepreted by the shell.</p>

<p>echo *.fastq
   SRR097977.fastq SRR098026.fastq</p>

<p>The '*' is expanded to include any file that ends with '.fastq'</p>

<hr>

<p><strong>Exercise</strong></p>

<p>Do each of the following using a single <code>ls</code> command without
navigating to a different directory.</p>

<ol>
<li> List all of the files in <code>/bin</code> that start with the letter 'c</li>
<li> List all of the files in <code>/bin</code> that contain the letter 'a'</li>
<li> List all of the files in <code>/bin</code> that end with the letter 'o'</li>
</ol>

<p>BONUS: List all of the files in '/bin' that contain the letter 'a' or 'c'</p>

<hr>

<h2><a id="user-content-command-history" class="anchor" href="#command-history" aria-hidden="true"><span class="octicon octicon-link"></span></a>Command History</h2>

<p>You can easily access previous commands.  Hit the up arrow.
Hit it again.  You can step backwards through your command history.
The down arrow takes your forwards in the command history.</p>

<p>^-C will cancel the command you are writing, and give you a fresh prompt.</p>

<p>^-R will do a reverse-search through your command history.  This
is very useful.</p>

<p>You can also review your recent commands with the <code>history</code> command.  Just enter:</p>

<pre><code>history
</code></pre>

<p>to see a numbered list of recent commands, including this just issues
<code>history</code> command.  You can reuse one of these commands directly by
referring to the number of that command.</p>

<p>If your history looked like this:</p>

<pre><code>259  ls *
260  ls /usr/bin/*.sh
261  ls *R1*fastq
</code></pre>

<p>then you could repeat command #260 by simply entering:</p>

<pre><code>!260
</code></pre>

<p>(that's an exclamation mark).  You will be glad you learned this when you try to re-run very complicated commands.</p>

<hr>

<p><strong>Exercise</strong></p>

<ol>
<li>Find the line number in your history for the last exercise (listing
files in /bin) and reissue that command.</li>
</ol>

<hr>

<h2><a id="user-content-examining-files" class="anchor" href="#examining-files" aria-hidden="true"><span class="octicon octicon-link"></span></a>Examining Files</h2>

<p>We now know how to switch directories, run programs, and look at the
contents of directories, but how do we look at the contents of files?</p>

<p>The easiest way to examine a file is to just print out all of the
contents using the program <code>cat</code>. Enter the following command:</p>

<pre><code>cat SRR098026.fastq
</code></pre>

<p>This prints out the all the contents of the the <code>SRR098026.fastq</code> to the screen.</p>

<hr>

<p><strong>Exercises</strong></p>

<ol>
<li><p>Print out the contents of the <code>~/dc_sample_data/untrimmed_fastq/SRR097977.fastq</code>
file. What does this file contain?</p></li>
<li><p>From your home directory, without changing directories,
use one short command to print the contents of all of the files in
the <code>/home/dcuser/dc_sample_data/untrimmed_fastq</code> directory.</p></li>
</ol>

<hr>

<pre><code>cd ~/dc_sample_data/untrimmed_fastq
</code></pre>

<p><code>cat</code> is a terrific program, but when the file is really big, it can
be annoying to use. The program, <code>less</code>, is useful for this
case. Enter the following command:</p>

<pre><code>less SRR098026.fastq
</code></pre>

<p><code>less</code> opens the file, and lets you navigate through it. The commands
are identical to the <code>man</code> program.</p>

<p><strong>Some commands in <code>less</code></strong></p>

<table><thead>
<tr>
<th>key</th>
<th>action</th>
</tr>
</thead><tbody>
<tr>
<td>"space"</td>
<td>to go forward</td>
</tr>
<tr>
<td>"b"</td>
<td>to go backwarsd</td>
</tr>
<tr>
<td>"g"</td>
<td>to go to the beginning</td>
</tr>
<tr>
<td>"G"</td>
<td>to go to the end</td>
</tr>
<tr>
<td>"q"</td>
<td>to quit</td>
</tr>
</tbody></table>

<p><code>less</code> also gives you a way of searching through files. Just hit the
"/" key to begin a search. Enter the name of the word you would like
to search for and hit enter. It will jump to the next location where
that word is found. Try searching the <code>dictionary.txt</code> file for the
word "cat". If you hit "/" then "enter", <code>less</code> will just repeat
the previous search. <code>less</code> searches from the current location and
works its way forward. If you are at the end of the file and search
for the word "cat", <code>less</code> will not find it. You need to go to the
beginning of the file and search.</p>

<p>For instance, let's search for the sequence <code>GTGCGGGCAATTAACAGGGGTTCAC</code> in our file.
You can see that we go right to that sequence and can see
what it looks like.</p>

<p>Remember, the <code>man</code> program actually uses <code>less</code> internally and
therefore uses the same commands, so you can search documentation
using "/" as well!</p>

<p>There's another way that we can look at files, and in this case, just
look at part of them. This can be particularly useful if we just want
to see the beginning or end of the file, or see how it's formatted.</p>

<p>The commands are <code>head</code> and <code>tail</code> and they just let you look at
the beginning and end of a file respectively.</p>

<p>head SRR098026.fastq
tail SRR098026.fastq</p>

<p>The <code>-n</code> option to either of these commands can be used to print the
first or last <code>n</code> lines of a file. To print the first/last line of the
file use:</p>

<p>head -n 1 SRR098026.fastq
tail -n 1 SRR098026.fastq</p>

<h2><a id="user-content-creating-moving-copying-and-removing" class="anchor" href="#creating-moving-copying-and-removing" aria-hidden="true"><span class="octicon octicon-link"></span></a>Creating, moving, copying, and removing</h2>

<p>Now we can move around in the file structure, look at files, search files,
redirect. But what if we want to do normal things like copy files or move
them around or get rid of them. Sure we could do most of these things
without the command line, but what fun would that be?! Besides it's often
faster to do it at the command line, or you'll be on a remote server
like Amazon where you won't have another option.</p>

<p>Our raw data in this case is fastq files.  We don't want to change the original files,
so let's make a copy to work with.</p>

<p>Lets copy the file using the <code>cp</code> command. The <code>cp</code>
command backs up the file. Navigate to the <code>data</code> directory and enter:</p>

<pre><code>cp SRR098026.fastq SRR098026-copy.fastq
ls -F
SRR097977.fastq  SRR098026-copy.fastq  SRR098026.fastq 
</code></pre>

<p>Now SRR098026-copy.fastq has been created as a copy of SRR098026.fastq</p>

<p>Let's make a <code>backup</code> directory where we can put this file.</p>

<p>The <code>mkdir</code> command is used to make a directory. Just enter <code>mkdir</code>
followed by a space, then the directory name.</p>

<pre><code>mkdir backup
</code></pre>

<p>We can now move our backed up file in to this directory. We can
move files around using the command <code>mv</code>. Enter this command:</p>

<pre><code>mv *-copy.fastq backup
ls -al backup
total 52
drwxrwxr-x 2 dcuser dcuser  4096 Jul 30 15:31 .
drwxr-xr-x 3 dcuser dcuser  4096 Jul 30 15:31 ..
-rw-r--r-- 1 dcuser dcuser 43421 Jul 30 15:28 SRR098026-copy.fastq
</code></pre>

<p>The <code>mv</code> command is also how you rename files. Since this file is so
important, let's rename it:</p>

<pre><code>cd backup
mv SRR098026-copy.fastq SRR098026-copy.fastq_DO_NOT_TOUCH!
ls 
SRR098026-copy.fastq_DO_NOT_TOUCH!

Finally, we decided this was silly and want to start over.

rm backup/SRR*
</code></pre>

<p>The <code>rm</code> file permanently removes the file. Be careful with this command. It doesn't
just nicely put the files in the Trash. They're really gone.</p>

<hr>

<p><strong>Exercise</strong></p>

<p>Do the following:</p>

<ol>
<li> Create a backup of your fastq files</li>
<li> Create a backup directory </li>
<li> Copr your backup files there</li>
</ol>

<hr>

<p>By default, <code>rm</code>, will NOT delete directories. You can tell <code>rm</code> to
delete a directory using the <code>-r</code> option. Let's delete that <code>new</code> directory
we just made. Enter the following command:</p>

<pre><code>rm -r backup
</code></pre>

<h2><a id="user-content-writing-files" class="anchor" href="#writing-files" aria-hidden="true"><span class="octicon octicon-link"></span></a>Writing files</h2>

<p>We've been able to do a lot of work with files that already exist, but what
if we want to write our own files. Obviously, we're not going to type in
a FASTA file, but you'll see as we go through other tutorials, there are
a lot of reasons we'll want to write a file, or edit an existing file.</p>

<p>To write in files, we're going to use the program <code>nano</code>. We're going to create
a file that contains the favorite grep command so you can remember it for later. We'll name this file
'awesome.sh'.</p>

<pre><code>nano awesome.sh
</code></pre>

<p>Now you have something that looks like</p>

<p><a href="/mckays630/shell-genomics/blob/gh-pages/img/nano1.png" target="_blank"><img src="/mckays630/shell-genomics/raw/gh-pages/img/nano1.png" alt="nano1.png" style="max-width:100%;"></a></p>

<p>Type in your command, so it looks like</p>

<p><a href="/mckays630/shell-genomics/blob/gh-pages/img/nano2.png" target="_blank"><img src="/mckays630/shell-genomics/raw/gh-pages/img/nano2.png" alt="nano2.png" style="max-width:100%;"></a></p>

<p>Now we want to save the file and exit. At the bottom of nano, you see the "^X Exit". That
means that we use Ctrl-X to exit. Type <code>Ctrl-X</code>. It will ask if you want to save it. Type <code>y</code> for yes.
Then it asks if you want that file name. Hit 'Enter'.</p>

<p>Now you've written a file. You can take a look at it with less or cat, or open it up again and edit it.</p>

<hr>

<p><strong>Exercise</strong></p>

<p>Open 'awesome.sh' and add "echo AWESOME!" after the grep command and save the file.</p>

<p>We're going to come back and use this file in just a bit.</p>

<hr>
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
      <li>&copy; 2015 <span title="0.04296s from github-fe129-cp1-prd.iad.github.net">GitHub</span>, Inc.</li>
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

