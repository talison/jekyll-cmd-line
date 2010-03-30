### Description ###

`jekyll-cmd-line` is a Python script that makes it easier to create posts and drafts for a [Jekyll-powered](http://github.com/mojombo/jekyll) site, particularly when you maintain multiple sites.

### Requirements ###

`jekyll-cmd-line` has been tested with Python 2.6.

It requires the [PyYAML library](http://pyyaml.org/).


### Configuration File ###

To use `jekyll-cmd-line` you must create a simple YAML config file that is either passed explicitly to the script, or saved with the name `.jekyll` in your `HOME` directory.

The config file includes the following parameters:

* `default_site`: The name of the default site for multi-site configs. (optional)
* `editor`: The path to the editor you want to edit posts or drafts in (optional). If this is not present, the value of the `EDITOR` environment variable is used.
* `sites`: A list of sites and their configuration attributes.

Each site in the `sites` list has the following attributes:

* `name`: The name of the site. (required)
* `location`: The directory of the site. (required)
* `layout`: The layout that should be specified in the [YAML Front Matter](http://wiki.github.com/mojombo/jekyll/yaml-front-matter) for new posts and drafts in this site. (optional, defaults to 'none')
* `extension`: The file extension to use when creating post and draft files. (optional)

For a full example, see [sample.jekyll](http://github.com/talison/jekyll-cmd-line/blob/master/sample.jekyll).

### Usage ###

These examples assume you have a `.jekyll` file in your `HOME` directory with contents of [sample.jekyll](http://github.com/talison/jekyll-cmd-line/blob/master/sample.jekyll).

__Print usage__

    jekyll-cmd-line --help

__Create a new draft in your default site__

    jekyll-cmd-line -d "My Next Great Blog Post"


__Create a new draft in a non-default site__

    jekyll-cmd-line -s journal -d "Deep Thoughts"


__Create a draft, pass in a different config__

    jekyll-cmd-line -d "A Post Somewhere Else" -c alternate.jekyll

__Create a post from an existing draft__

When you create a new post in a given site, `jekyll-cmd-line` will first check to see if a matching draft exists. The match is based on filename patterns.

If a match is found, you'll be prompted if want to convert the existing draft to a post. For example:

    jekyll-cmd-line -s journal -p "deep"

This command will find the "Deep Thoughts" draft and prompt:

    Found matching drafts. Select a draft or hit ENTER to create a new post.

    1: deep-thoughts.markdown

    Draft number (or ENTER for new post):

At this point, you can choose to convert draft 1 to a post by entering 1 and hitting ENTER. This will move `deep-thoughts.markdown` from the drafts directory to the posts directory and rename it with today's date.

If a matching draft was found, but you just want to create a new post, hit ENTER. The draft will stay put and a new post is created.

__Create a post__

    jekyll-cmd-line -p "A Brand New Post"

### Tips ###

Bash aliases are helpful. I use the following:

* `alias jd="jekyll-cmd-line -d"`
* `alias jp="jekyll-cmd-line -p"`
