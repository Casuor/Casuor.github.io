---
title: JsDeliver-usages
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/kawayi0.jpg
date: 2019-4-25
---
## GitHub CDN
We recommend using npm for projects that support it for better UX - npm packages are searchable on our website, and package pages show additional useful information, such as description and link to homepage.
We use a permanent S3 storage to ensure all files remain available even if GitHub goes down, or a repository or a release is deleted by its author. Files are fetched directly from GitHub only the first time, or when S3 goes down.
Load any GitHub release, commit, or branch:

https://cdn.jsdelivr.net/gh/user/repo@version/file
Load an exact version of a file:

https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/dist/jquery.min.js
https://cdn.jsdelivr.net/gh/jquery/jquery@32b00373b3f42e5cdcb709df53f3b08b7184a944/dist/jquery.min.js
Use a version range instead of an exact version:

https://cdn.jsdelivr.net/gh/jquery/jquery@3.2/dist/jquery.min.js
https://cdn.jsdelivr.net/gh/jquery/jquery@3/dist/jquery.min.js
If you use this feature and a file you requested is not available in the newest release, the link will keep working thanks to our version-fallback feature. We'll continue to serve the file from older release instead of failing with a 404 error.
Omit the version completely or use "latest" to load the latest one (not recommended for production usage):

https://cdn.jsdelivr.net/gh/jquery/jquery@latest/dist/jquery.min.js
https://cdn.jsdelivr.net/gh/jquery/jquery/dist/jquery.min.js
Requesting the latest version (as opposed to "latest major" or "latest minor") is dangerous because major versions usually come with breaking changes. Only do this if you really know what you are doing.
Add ".min" to any JS/CSS file to get a minified version - if one doesn't exist, we'll generate it for you. All generated files come with source maps and can be easily used during development:

https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/src/core.min.js
Minifying a large file can take several seconds. However, we store all generated files in our permanent storage, so this delay only applies to the first few requests.
Get a directory listing:

https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/
https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/dist/
Combine multiple files
Our combine endpoint allows you to load several files from npm and GitHub endpoints in one request:

https://cdn.jsdelivr.net/combine/url1,url2,url3
All features that work for individual files (version ranges, minification, etc.) work here as well. All combined files come with source maps and can be easily used during development.

https://cdn.jsdelivr.net/combine/gh/jquery/jquery@3.2/dist/jquery.min.js,gh/twbs/bootstrap@3.3/dist/js/bootstrap.min.js
https://cdn.jsdelivr.net/combine/npm/bootstrap@3.3/dist/css/bootstrap.min.css,npm/bootstrap@3.3/dist/css/bootstrap-theme.min.css
Combining large/many files can take several seconds. However, we store all generated files in our permanent storage, so this delay only applies to the first few requests.
## Problem
Package size exceeded the configured limit of 50 MB