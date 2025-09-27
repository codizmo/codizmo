# Howto publish content on GitHub Pages

## Starting with GitHub Pages
1. Get a GitHub account if you don't have one yet
1. Login to your account and create a new repository
1. Add a new file to it (clicking the + button at the top right). Name it index.html if you plan to use HTML to create your page or index.md if you want to use markdown for your page to keep things simple
1. On the top bar click «Settings» then «Pages» on the left menu panel which will appear
2. Under «Build and deployment» choose «Deploy from branch» Below that choose the branch and the directory from which the website shoud be served
3. Instead of using <username>.github.io which is the default servername at whoich your page will be shown you may set your own servername in the «Custom domain» section. Follow the instructions given there.
4. Once you have created one or more pages click the «Visit site» button at the top of the page to see your new website.
5. Unlike most other services github.io allows the integration of pages in iFrames which is extremly helpful to get the documentation of a parameter in the Online OpenSCAD renderer shown as an overlay instead on a separate webpage
   
## Multiple pages
It is possible to provide multiple pages in a GitHub Pages repository, but there are some important details about how it works:

**Markdown files:** When you create multiple Markdown files (.md) in your repository, GitHub Pages will automatically convert them to HTML. However, the URL structure depends on how GitHub Pages processes these files:
- README.md becomes the index page at username.github.io/repository-name/
- Other Markdown files like HOWTO.md would be accessible at username.github.io/repository-name/HOWTO.html (note the .html extension in the URL)

**HTML files:** If you create HTML files directly, they work more straightforwardly:
- index.html serves as the homepage
- howto.html would be accessible at username.github.io/repository-name/howto.html
- You can omit the .html in the URL (username.github.io/repository-name/howto) and it will still work

> Please note that after making changes (to .md files in particular) it will usually take a few minutes before they are published on GitHub Pages
