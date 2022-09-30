# The Seattle School IT Department - Standard Operating Procedures

Written in Markdown using `mkdocs` convention. Hosted through [GitHub Pages](https://itstaff-tss.github.io/tss-it-sop/).

[mkdocs User Guide](https://www.mkdocs.org/user-guide/)

## Installation

*Note: In Windows Command Prompt, you will have to append `py -m` to the start of all Python commands.*

- Ensure Python is installed on your machine. Install mkdocs with `pip install mkdocs`.

- Start development server: `mkdocs serve`

    - *Note: Links are hardcoded to work with GitHub Pages. They will not work as expected in a development environment.*

- Build the site: `mkdocs build`

## Revision control

- Changes are handled through Git and GitHub. The project belongs to itstaff@theseattleschool.edu.

- Updates to the docs should be committed with descriptions and pushed to the `main` branch.

## Deploying

- To automatically build, publish, and deploy your changes made in the `main` branch: `mkdocs gh-deploy`

- Built site files reside in `site/` and are ignored in the `main` branch. The `gh-pages` branch holds the site files.

- You should never have to make changes to the `gh-pages` branch, just use the CLI to deploy!