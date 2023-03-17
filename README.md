# markdown-resume

A tool that uses [pandoc](https://pandoc.org/MANUAL.html#pandocs-markdown) to generate a good looking CV in .pdf and .html formats from a vanilla markdown file.

Supports working with multiple markdown files at the same time (if, for example you need them in multiple languages), and doesn't depend on jekyll nor latex.

Absolutely no dependencies if you use GitHub CI to build the resulting files!. Just put your resume markdown file under `src/`, commit and push. You'll find a zip file with the output files in the [CI workflow summary page](https://github.com/actions/upload-artifact#where-does-the-upload-go).

## CV file structure

You can use [`src/sample.md`](src/sample.md) for reference. Most of it should be self-explanatory. Other than that:

- The `title` variable from the frontmatter gets set as the first `h1` in the content
- The `style` variable in the front matter chooses the style to use (from the [`styles/`](styles/) directory)
- Some markdown elements might have a special function in a given style (like the `h4` used for time periods in the default style). Again, consult the samples to see how it fits together.

## Running locally

You'll need to install `pandoc` and `wkhtmltopdf`. Afterwards just run `make`!

on Linux:

```bash
sudo apt install pandoc lmodern wkhtmltopdf
make
open output/sample.pdf
```

To have the output files automagically regenerated when you edit the source files:

```bash
sudo apt install pandoc lmodern wkhtmltopdf inotify-tools
make watch
```

The latter is Linux only, to use the same workflow on Mac, use the Docker workflow.

## Running with Docker

If you have docker installed, you can run

```bash
make docker
```

While the docker container is running, the `src/` and the `output/` directories are mounted to it and pdfs will be re-generated whenever the markdown files are edited.

## Credit

- Markdown and css structure based on a Eliseo Papa's [markdown-cv](https://github.com/elipapa/markdown-cv) jekyll workflow
- Default theme based on [Kamil Wójcicki](https://www.isca-speech.org/iscamember/resumes/10211_12071110395691cd.pdf)'s LaTex template I've been using for about 15 years
- The trick for fetching front matter variables in bash from [u/cr0sh](https://www.reddit.com/r/pandoc/comments/f6oxm5/convert_yaml_frontmatter_to_bash_variables/?utm_source=share&utm_medium=web2x&context=3)

# Development

## Contributing

Contributions welcome! Especially new styles and tweaks to the default style.

## Creating a new style

Create a directory under `styles/` - the name of the directory will be the style name.
Any css files put in the directory will be included, in alphabetical order, in a resume compiled with that style.

## Comming soon

- multiple styles
- styles consisting of multiple .css files
- FontAwesome icons in the default style

## TODO

- [x] list out prereqs for the script to work locally
- [x] dockerfile for local compilation
- [x] CI with tests, compilation and output download
- [x] working style selection
- [x] multiple css files in a style (for vendored stuff)
- [ ] fontAwesome icons in the default styles
- [x] default style tweaks (link colors?)
- [ ] add sample output files to the repo and gitignore. Add a make task for them
- [x] credit the projects that inspired this one
- [ ] add pdf metadata using exiftool?
