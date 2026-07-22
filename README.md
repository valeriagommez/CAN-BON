# CAN BON
xyz

# Introduction to Hugo

## File structure
- `content` folder : necessary for Hugo to render the website. It's made up of two folders : `english` and `french`. This is where the pages' information is kept.
    - Each page has it's own folder and `_index.md` file. As it stands now, this file doesn't contain much -- just the basic information for Hugo to recognize it as a page. 
    **Example :**
    ```
    +++
    title = "About CAN BON"
    draft = true/false --> if set to true, then Hugo will not render it
    +++
    ```

- `data` folder : contains the data for each page. It is also divided in two folders: `en` and `fr`. Each page has its own YAML file (ex.: `about.yaml`), and this is where the content of the page can be edited.

- `layouts` folder : contains the layout for each page. Each page has its own folder, and the `_default` folder is used for elements that appear in every page (ex.: the footer).
    - `list.html` file : contains a list of all the elements (called _partials_) that compose a certain page. This file fetches the partials using their path, and Hugo will render them in order.
    **Example :** 
    ```
    {{ define "main" }}
        {{ partial "shared/header-pages.html" . }}
        {{ partial "our-work/introduction.html" . }}
        {{ partial "our-work/working-groups.html" . }}
        {{ partial "our-work/data-tools.html" . }}
        {{ partial "our-work/resources.html" . }}
    {{ end }}
    ```

    - `partials` folder : 

- `static` folder : 

## Creating a new page

### English and French

## How to edit a page's content 

### Markdown formatting

### YAML files

# To-do
- The `View all products >` and `View all resources >` buttons in the **Our work** page currently lead to blank pages. Eventually, these will be populated with actual content.