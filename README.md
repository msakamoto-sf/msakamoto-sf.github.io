# msakamoto-sf.github.io

personal blog(個人blog)

## local build

requirements:

- docker
- build docker container image: [msakamoto-sf/github-pages-jekyll-docker-image](https://github.com/msakamoto-sf/github-pages-jekyll-docker-image)

bundle install:

```
$ docker run --rm -it -u `id -u`:`id -g` -v $PWD:/src -w /src github-pages-jekyll bundle install
```

`jekyll build` (local test with [vscode Live Preview extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server) ):

```
$ docker run --rm -it -u `id -u`:`id -g` -v $PWD:/src -w /src github-pages-jekyll bundle exec jekyll build
```

`jekyll build` (same to production GitHub Pages):

```
$ docker run --rm -it -u `id -u`:`id -g` -v $PWD:/src -w /src -e JEKYLL_ENV=production github-pages-jekyll bundle exec jekyll build
```

## reference

- GitHub Pages
  - https://docs.github.com/ja/pages/getting-started-with-github-pages/what-is-github-pages
- GitHub Flavored Markdown Spec
  - https://github.github.com/gfm/
- Jekyll kramdown syntax
  - https://kramdown.gettalong.org/syntax.html
- [`[jekyll × Github Pages - Tips] 本番環境にだけ出力したいタグを設定する方法 #GithubPages - Qiita`](https://qiita.com/rhinonolike/items/7c1bb1ae85605f099f70)

## init

```
$ docker run --rm -it -u `id -u`:`id -g` -v $PWD:/src -w /src github-pages-jekyll jekyll new --skip-bundle /src/msakamoto-sf.github.io
New jekyll site installed in /src/msakamoto-sf.github.io.
Bundle install skipped.

$ cd msakamoto-sf.github.io/

$ git init

$ vi Gemfile
(...)
gem "jekyll", "~> 3.10.0"
-> comment out
#gem "jekyll", "~> 3.10.0"

(...)
# gem "github-pages", group: :jekyll_plugins
->
gem "github-pages", "~> 232", group: :jekyll_plugins

$ docker run --rm -it -u `id -u`:`id -g` -v $PWD:/src -w /src github-pages-jekyll bundle config set path 'vendor/bundle'

$ docker run --rm -it -u `id -u`:`id -g` -v $PWD:/src -w /src github-pages-jekyll bundle install
```
