# Dev-Corner

Documentation written with Mkdocs

***

### Build-process

1. You need Python (2.7.2) and the Python Package Index (1.5.2) to build the documentation. Check if your operating-system provides it already:

```
python --version 
pip --version
```

2. This Documentation uses [MkDocs](http://www.mkdocs.org/), so that the documentatio can be written in Markdown. **Cheat cheets** for Markdown can be found here: 
	* [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
	* [https://daringfireball.net/projects/markdown/](https://daringfireball.net/projects/markdown/)

3. Install MkDocs with the following command:

```
pip install mkdocs
```

4. Clone this repository to into your local-repository and build the documentation with the following command:

```
mkdocs build
```

**Attention**: If some problems occur during the build-process, you can also try to re-build the documentation with the following command:
```
mkdocs build --clean
```

5. If you want to add new pages to this documenation, create a new `.md`-Files in folder: `docs/`

6. Before building, don't forget to add your new page in the `mkdocs.yml`-file:

```
pages:
- Home: index.md
- About: about.md
- NewPage: newPage.md
```

7. Build the documenation with the command above (see: 4.). All `.md`-files will be generated into `.html`-Files in the folder `site/`.
**Hint**: For automatically building, you can use the following command, to start the built-in-MkDocs-Server:

```
mkdocs serve
```
Open a new browser-tab and go to [http://127.0.0.1:8000/](http://127.0.0.1:8000/).

For more information about MkDocs, please have a look into their documenation [http://www.mkdocs.org/](http://www.mkdocs.org/)