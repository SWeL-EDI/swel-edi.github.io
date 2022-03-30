# swel-edi.github.io
This repository contains the files for the Semantic Web Lab, Edinburgh website. 

## Contribute
Feel free to propose changes to the website! This can be done by opening an [issue](https://github.com/SWeL-EDI/swel-edi.github.io/issues) or by forking this repository and making a pull request. The content of this website is built using a combination of Markdown and HTML.

## Theme

The pages are styled using the remote theme [Petridish](https://github.com/peterdesmet/petridish).

## Logo 

Logos were designed by Ruben Kruiper.

Logo files are in the assets directory.

Colours:
- Grey: #46505c
- Blue: #2e9bdd

## Deployment
The website is deployed on [GitHub](https://github.com/) using [Jekyll](https://jekyllrb.com/).

The automated deployment is done using the [jekyll-action-ts](https://github.com/limjh16/jekyll-action-ts) workflow.

### Previewing your changes on your own fork

Since the website uses [GitHub pages](https://pages.github.com/) for its deployment, it is possible to create live previews to inspect your changes. Go to your fork -> settings tab -> pages and select the branch you are working on to activate GitHub pages. GitHub will do the rest and will tell you at which url the website will be served.

### Deploying the website locally

It is possible to preview the website locally to preview changes. You need a Ruby installation in order to do so. Ruby version 2.7.* works out of the box well with Jekyll, more recent versions will need `bundle add webrick` to make it work. If you already have the correct Ruby installed on your machine, then the following files will allow you to get started by installing the relevant dependencies:

- Install Jekyll and Dependencies: ```gem install jekyll bundler ``` and ```gem install jekyll-sitemap jekyll-sitemap jekyll-gist jekyll-redirect-from```
- Clone the repository: ```git clone https://github.com/SWeL-EDI/swel-edi.github.io.git```
- Run the website: ```bundle exec jekyll serve```

If you need more help with installing Jekyll, then see their [installation instructions](https://jekyllrb.com/docs/installation/) for full details.
