# dsouzaalfred.github.io

### This repo is used to host the website [https://dsouzaalf.red/](https://dsouzaalf.red/).

### The site uses Jekyll.

### Theme
https://github.com/mmistakes/so-simple-theme

### GEM used
1. [jekyll-compose](https://github.com/jekyll/jekyll-compose)
2. [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag)
3. [jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap)
4. [jekyll-feed](https://github.com/jekyll/jekyll-feed)
5. [jekyll-paginate](https://github.com/jekyll/jekyll-paginate)

### Start Dev server
`JEKYLL_GITHUB_TOKEN=<git_token> bundle exec jekyll serve`

### Open dev server for local network
`JEKYLL_GITHUB_TOKEN=<git_token> bundle exec jekyll serve --host 0.0.0.0`

### Flow to add a new post:
1. Create a new branch:
  - `gcb “post-<post_number>-post-name”`
  - e.g.:  `gcb “post-3-react-props”`
2. In this branch create a new post
  - `bundle exec jekyll post "My New Post"`
3. Commit all changes.
4. Open a PR when you ready to publish the post.


### Checks
1. Check that post has a hero image
2. Dates and post file names are correct
3. No error on command line
