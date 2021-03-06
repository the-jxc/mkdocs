# Configuration

Guide to all available configuration settings.

---

## Introduction

Project settings are always configured by using a YAML configuration file in the project directory named `mkdocs.yml`.

As a miniumum this configuration file must contain the `site_name` setting.  All other settings are optional.

## Project information

#### site_name

This is a **required setting**, and should be a string that is used as the main title for the project documentation.  For example:

    site_name: Mashmallow Generator

When rendering the theme this setting will be passed as the `site_name` context variable.

#### site_url

Quo ex ceteros theophrastus, mel eius repudiandae an, has autem legendos ut. Eu quo moderatius interpretaris, pro ad homero tractatos cotidieque. His errem dictas instructior ad, tation causae ceteros ex eum. Nam falli dicunt te, mea et unum contentiones, ius noluisse rationibus cotidieque ei.

**default**: `null`

#### repo_url

When set, provides a link to your GitHub or Bitbucket repository on each page.

    repo_url: https://github.com/example/repository/

**default**: `null`

#### site_description

Eam no quis bonorum legendos. Eos prodesset cotidieque in, atqui saperet eos te. Sit eruditi fastidii detraxit cu, sed elit voluptatum in. Vel esse possim accumsan et, eam et amet nihil putent. Mei putent impetus no, iuvaret labores duo an.

**default**: `null`

#### site_author

Sit eruditi fastidii detraxit cu, sed elit voluptatum in. Vel esse possim accumsan et, eam et amet nihil putent.

**default**: `null`

#### site_favicon

Sit eruditi fastidii detraxit cu, sed elit voluptatum in. Vel esse possim accumsan et, eam et amet nihil putent.

**default**: `null`

## Documentation layout

#### pages

This is setting is used to determine the set of pages that should be built for the documentation.

The setting should be a list.  Each row in the list represents information about a single page as a list of strings.  The first string represents the path of the documentation source file, and should be relative to the `docs_dir` setting.  Remaining strings represent the title of the page in the site navigation.

Here's a simple example that would cause the build stage to create three pages:

    pages:
    - ['index.md', 'Introduction']
    - ['user-guide.md', 'User Guide']
    - ['about.md', 'About']

Assuming the `docs_dir` setting was left with the default value of `docs`, the source files for this site's build process would be `docs/index.md`, `docs/user-guide.md` and `docs/about.md`.

If you have a lot of project documentation you might choose to use headings to break up your site navigation by category.  You can do so by including an extra string in the page configuration for any pages that require a navigation heading, like so: 

    pages:
    - ['index.md', 'Introduction']
    - ['user-guide/creating.md', 'User Guide', 'Creating a new Mashmallow project']
    - ['user-guide/api.md', 'User Guide', 'Mashmallow API guide']
    - ['user-guide/configuration.md', 'User Guide', 'Configuring Mashmallow']
    - ['about/license.md', 'About', 'License']

## Build directories

#### theme

Sets the theme of your documentation site, for a list of available themes visit
[styling your docs](styling-your-docs.md).

**default**: `'mkdocs'`

#### theme_dir

Lets you set a directory to a custom theme.  This can either be a relative directory, in which case it is resolved relative to the directory containing you configuration file, or it can be an absolute directory path.

For example, given this example project layout:

    mkdocs.yml
    docs/
        index.md
        about.md
    custom_theme/
        base.html
        ...

You would include the following setting to use the custom theme directory:

    theme_dir: 'custom_theme'

If used, then this setting overrides any `theme` configuration value.

**default**: `null`

#### docs_dir

Lets you set the directory containing the documentation source markdown files.  This can either be a relative directory, in which case it is resolved relative to the directory containing you configuration file, or it can be an absolute directory path.

**default**: `'docs'`

#### site_dir

Lets you set the directory where the output HTML and other files are created.  This can either be a relative directory, in which case it is resolved relative to the directory containing you configuration file, or it can be an absolute directory path.

**default**: `'site'`

---

**Note**: If you are using source code control you will normally want to ensure that your *build output* files are not commited into the repository, and only keep the *source* files under version control.  For example, if using `git` you might add the following line to your `.gitignore` file:

    site/

If you're using another source code control you'll want to check its documentation on how to ignore specific directories.

---

<!--
## Extra build steps

#### include_search

Mea et graeci persecuti, sit possit neglegentur ex. Nam modus maluisset id. Praesent laboramus expetendis an vis. Mea scripta eleifend et. Ex zril quidam facilis nec, eu inani errem expetendis eum. Falli electram periculis te ius, sed nihil saperet cu. Possit quodsi cu sea, usu ei saperet lobortis adolescens.

#### include_404

Lorem ipsum dolor sit amet, ex usu velit harum dignissim. Graeco saperet tibique ea mea. Mel vocent veritus assentior ne, ponderum dissentiunt nec eu. No civibus commune duo, nec in mollis regione eruditi, nec feugiat accumsan interesset te. Natum accusam legendos sea no, te eam libris tamquam, ius fabulas vocibus rationibus ad. Eum ex sonet nostrum argumentum, mel persius cotidieque repudiandae in, cum legendos patrioque in.

#### include_sitemap

Consul percipitur usu an, no dico facer inermis cum. Eum ea mentitum accommodare. An sea periculis euripidis, dicant minimum patrioque at vis. Justo atomorum abhorreant vel in. Eos agam intellegam disputando at, zril consul nostrud ut eum.
-->

## Preview controls

#### url_format

This setting controls the format of the URLs (and filenames for a static "build").  The options for `url_format` 
are `directory` (default), `index` or `file`.  This parameter replaces the old `use_directory_urls` flag.

The behavior for `url_format` = `directory` is the default and matches the old `use_directory_urls` = True.
This generates clean URLS, although it has the problem that a static build does not generate links that work 
when browsing off a file.

Also, this format breaks relative links to images and other media files which are stored within the `.md` document 
tree.  E.g. if `system.md` contains an image `<img src="a.jpg">` where `a.jpg` is in the same directory as `system.md`, 
then this image will not display with `url_format` = `directory` either in static `build` or dynamic `serve` modes,
inside the `system.md` you must now refer to the image as `<img src="../a.jpg">`, due to the trailing `/` which is
added to the navigation link.

If you wish to preserve relative image links after processing, you may want to consider `url_format` = `file`.

Source file  | Generated HTML       | Navigation Links
------------ | -------------------- | ------------------------
index.md     | index.html           | /
api-guide.md | api-guide/index.html | /api-guide/
about.md     | about/index.html     | /about/
dir/file.md  | dir/file/index.html  | /dir/file/

The behavior for `url_format` = `index` matches what the old `use_directory_urls` = False claimed to do.
This generates a static build which does work when browsing from a file system.  However it still breaks 
relative links to images and other media files which are stored within the `.md` document tree.

Source file  | Generated HTML       | Navigation Links
------------ | -------------------- | ------------------------
index.md     | index.html           | /index.html
api-guide.md | api-guide/index.html | /api-guide/index.html
about.md     | about/index.html     | /about/index.html
dir/file.md  | dir/file/index.html  | /dir/file/index.html

The behavior for `url_format` = `file` simply translates the `.md` suffix into `.html`. 
This generates a static build which does work when browsing from a file system, and preserves
relative links to images and other media files which are stored within the `.md` document tree.

Source file  | Generated HTML       | Navigation Links
------------ | -------------------- | ------------------------
index.md     | index.html           | /index.html
api-guide.md | api-guide.html       | /api-guide.html
about.md     | about.html           | /about.html
dir/file.md  | dir/file.html        | /dir/file.html

**default**: `directory`

#### dev_addr

Determines the address used when running `mkdocs serve`.  Setting this allows you to use another port, or allows you to make the service accessible over your local network by using the `0.0.0.0` address.

As with all settings, you can set this from the command line, which can be usful, for example:

    mkdocs serve --dev-addr=0.0.0.0:80  # Run on port 80, accessible over the local network.

**default**: `'127.0.0.1:8000'`

<!--
## Other configuration

Vel at magna falli fierent. Clita putant nam no, cu per eros possit omnium, dicit pertinacia consetetur at has. Nam quis delenit cu, at vix consul expetendis, mucius mediocrem reprimique te mel. Ex vim quem oratio cotidieque, periculis iracundia at his, his omnium consulatu ei.

No sale minim definiebas vis. An quem utinam eam, est et consul patrioque maiestatis. Vel id decore periculis eloquentiam. Eu vim graeco causae, nec ut dicta graecis delicatissimi. Ne quod etiam salutandi vix, est stet veritus ne. Modus corrumpit usu ea, pri et dicam dignissim, quo ea sumo essent interesset.
-->