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

    **Example : **
    ```
    introduction: 
        title: "About CAN BON"
        subtitle: "Nature is undergoing a major transformation due to <span style='color:var(--red)'>**climate change**</span>."
        text: |
            Biodiversity loss is accelerating and with it the many economic and cultural benefits we derive from healthy ecosystems...
    ```
    **Note :** As seen above, you can format the content of each page using Markdown or HTML tags.

    These YAML files are structured in key-value pairs (`key: value`), delimited by indentations. For example, if you want to refer to the subtitle, it would be under `introduction.subtitle`. 
    
    For simplicity, I have categorized each YAML file in different "sections", corresponding to each **partial** under the `partials/page/` folder. The above example is a snippet of the `about.yaml` page, and it contains the text that will be fetched by the HTML file located under `partials/about/introduction.html`. You don't necessarily need to keep the same formatting, but it makes it simpler when you're creating a new page.

- `layouts` folder : contains the layout for each page. Each page has its own folder, and the `_default` folder is used for elements that appear in every page (ex.: the footer).
    - `list.html` file : contains a list of all the elements (called **partials**) that compose a certain page. This file fetches the partials using their path, and Hugo will render them in order.
    
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

    - `partials` folder : contains the HTML files detailing how we want the content to be rendered. Partials fetch content from the YAML files in the `data` folder. In general, each HTML file should have the following lines at the very start : 
    ```
    {{ $lang := .Site.Language.Name }}
    {{ $d := index hugo.Data $lang "name of the YAML file corresponding to this page" "name of the key corresponding to this partial" }}
    ...
    ```
    This makes it easier to "plug-in" the content from the YAML data file into this HTML file. This can be done using the following syntax : 
    ```
    <div>
        ...
        <h1>{{ $d.title | markdownify}}</h1>
        ...
    </div>
    ```
    You can customize the partials however you want using CSS!

- `static` folder : contains the main CSS file (under the `css/` folder), and all the images used in the website (under `images/`).

## Creating a new page
1. To create a new page, you must create folders under `content/english` and `content/french`, as well as two `_index.md` files (an example can be seen above). The file set up should look like : 
    ```
    ├── content/
    │   ├── english/
    │   │   ├── ...
    │   │   ├── new/
    │   │   │   ├── _index.md
    │   ├── french/
    │   │   ├── ...
    │   │   ├── new/
    │   │   │   ├── _index.md
    ```
2. Similarly, you will need to create two YAML files under the data folder : 
    ```
        ├── data/
        │   ├── en/
        │   │   ├── ...
        │   │   ├── new.yaml
        │   ├── fr/
        │   │   ├── ...
        │   │   ├── new.yaml
    ```
    This is where the text component will live, it's also where you can modify it later on.

3. Create a new folder under `layouts` : 
    ```
        ├── layouts/
        │   ├── ...
        │   ├── new/
        │   │   ├── list.html
    ```
    Also, the `list.html` file should look like this : 
    ```
    {{ define "main" }}
        {{ partial "shared/header-pages.html" . }}  --> crucial to render the header in this new page
        {{ partial "new/partial-1.html" . }}        --> all other partials used in this page. You will create the partials in the next step.
        ...
    {{ end }}
    ```

4. Finally, you will need to create the partials! You can create various HTML pages under the `partials` folder, depending on how you want the page to look like.
    ```
        ├── partials/
        │   ├── ...
        │   ├── new/
        │   │   ├── partial-1.html
        │   │   ├── partial-2.html
        │   │   ├── ...
    ```
    
## Editing a page
To edit the content of a page, you really only need to modify its YAML file.

# To-do
- The `View all products >` and `View all resources >` buttons in the **Our work** page currently lead to blank pages. Eventually, these will be populated with actual content.