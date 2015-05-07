# Developer documentation #

This documentation will help you to understand tranquilpeak-hexo-theme code.  

If you want to report a bug or ask a question, [create an issue](https://github.com/LouisBarranqueiro/tranquilpeak-hexo-theme/issues/new).

## Summary ##

- [Requirements](#requirements)
- [Installation](#installation)
- [Code structure](#code-structure)
    * [Views](#views)
    * [Assets](#assets)
         * [Stylesheets](#stylesheets)
         * [Images](#images)
         * [Javascript](#javascript)
- [Build](#build)
    * [NPM dependencies](#npm-dependencies)
    * [Bower dependencies](#bower-dependencies)
    * [Grunt tasks](#grunt-tasks)
        * [Tasks structure](#tasks-structure)
        * [Pipeline](#pipeline)
        * [Config tasks](#config-tasks)
        * [Register tasks](#register-tasks)
- [Running](#running)
 
## Requirements ##

1. **Node** : v0.10.35 or higher. Download [Node](https://nodejs.org/download/)
2. **Hexo CLI** : v0.1.4 or higher. Run ```npm install hexo-cli -g```
3. **Grunt CLI** : v0.1.13 or higher. Run ```npm install grunt-cli -g```
4. **Bower** : v1.4.1 or higher. Run ```npm install bower -g```

## Installation ##

1. Run ```git clone https://github.com/LouisBarranqueiro/tranquilpeak-hexo-theme.git```
2. Rename the folder in ```tranquilpeak``` and place it in ```themes``` folder of your Hexo blog
3. Modify the theme in ```_config.yml``` by changing ```theme``` variable  to ```tranquilpeak```
4. Complete ```theme/tranquilpeak/_config.yml``` with your informations by following directives in comments

If you want to configure the theme, please follow the [user documentation](https://github.com/LouisBarranqueiro/tranquilpeak-hexo-theme/blob/master/docs/user.md)  
  
## Code structure ##

```
tranquilpeak-hexo-theme
├── docs
│   ├── developer.md
│   └── user.md
├── layout
│   ├── _partial
│   │   ├── post
│   │   │   ├── actions.ejs
│   │   │   ├── category.ejs
│   │   │   ├── disqus.ejs
│   │   │   ├── gallery.ejs
│   │   │   ├── header.ejs
│   │   │   ├── meta.ejs
│   │   │   └── tag.ejs
│   │   ├── about.ejs
│   │   ├── archive-post.ejs
│   │   ├── archive.ejs
│   │   ├── cover.ejs
│   │   ├── footer.ejs
│   │   ├── google-analytics.ejs
│   │   ├── head.ejs
│   │   ├── header.ejs
│   │   ├── index.ejs
│   │   ├── pagination.ejs
│   │   ├── post.ejs
│   │   ├── script.ejs
│   │   └── sidebar.ejs
│   ├── all-archives.ejs
│   ├── all-categories.ejs
│   ├── all-tags.ejs
│   ├── archives.ejs
│   ├── category.ejs
│   ├── index.ejs
│   ├── layout.ejs
│   ├── page.ejs
│   ├── post.ejs
│   └── tag.ejs
├── source
│   ├── _css
│   │   ├── base
│   │   │   ├── _base.scss
│   │   ├── components
│   │   │   ├── archives.scss
│   │   │   ├── _box.scss
│   │   │   ├── _button.scss
│   │   │   ├── _category.scss
│   │   │   ├── _form.scss
│   │   │   ├── _hide.scss
│   │   │   ├── _highlight.scss
│   │   │   ├── _icon.scss
│   │   │   ├── _image-gallery.scss
│   │   │   ├── _link.scss
│   │   │   ├── _main-content.scss
│   │   │   ├── _markdown.scss
│   │   │   ├── _pagination.scss
│   │   │   ├── _post-actions.scss
│   │   │   ├── _post.scss
│   │   │   ├── _pullquote.scss
│   │   │   ├── _tag.scss
│   │   │   ├── _text.scss
│   │   │   ├── _tooltip.scss
│   │   │   └── _video.scss
│   │   ├── layout
│   │   │   ├── _about.scss
│   │   │   ├── _blog.scss
│   │   │   ├── _cover.scss
│   │   │   ├── _footer.scss
│   │   │   ├── _header.scss
│   │   │   ├── _main.scss
│   │   │   └── _sidebar.scss
│   │   ├── utils
│   │   │   ├── mixins
│   │   │   │   ├── _button.scss
│   │   │   │   ├── _category.scss
│   │   │   │   ├── _form.scss
│   │   │   │   ├── _opacity.scss
│   │   │   │   ├── _prefix.scss
│   │   │   │   └── _tag.scss
│   │   │   ├── _font.scss
│   │   │   └── _variables.scss
│   │   └── tranquilpeak.scss
│   ├── _images
│   │   └── cover.png
│   └── _js
│   │   ├── about.js
│   │   ├── archives-filter.js
│   │   ├── categories-filter.js
│   │   ├── fancybox.js.js
│   │   ├── header.js
│   │   ├── image-gallery.js
│   │   ├── post-bottom-bar.js
│   │   ├── sidebar.js
│   │   ├── smartresize.js
│   │   └── tags-filter.scss
├── tasks
│   ├── config
│   │   ├── bower.js
│   │   ├── clean.js
│   │   ├── concat.js
│   │   ├── cssmin.js
│   │   ├── replace.js
│   │   ├── sails-linker.js
│   │   ├── sass.js
│   │   ├── sync.js
│   │   ├── uglify.js
│   │   └── watch.js
│   ├── register
│   │   ├── build.js
│   │   ├── buildProd.js
│   │   ├── compileAssets.js
│   │   ├── linkAssets.js
│   │   ├── linkAssetsProd.js
│   │   ├── syncAssets.js
│   │   └── watch.js
│   └── pipeline.js
├── .bowerrc
├── Gruntfile.js
├── LICENSE
├── README.md
├── _config.yml
├── bower.json
└── package.json
```

- **docs** : Contains user and developer documentation
- **layout** : Contains all views
- **source** : Contains all assets (css, js and images)
- **tasks** : Contains all grunt tasks

### Views ###

```
├── layout
    ├── _partial
    │   ├── post
    │   │   ├── actions.ejs
    │   │   ├── category.ejs
    │   │   ├── disqus.ejs
    │   │   ├── gallery.ejs
    │   │   ├── header.ejs
    │   │   ├── meta.ejs
    │   │   └── tag.ejs
    │   ├── about.ejs
    │   ├── archive-post.ejs
    │   ├── archive.ejs
    │   ├── cover.ejs
    │   ├── footer.ejs
    │   ├── google-analytics.ejs
    │   ├── head.ejs
    │   ├── header.ejs
    │   ├── index.ejs
    │   ├── pagination.ejs
    │   ├── post.ejs
    │   ├── script.ejs
    │   └── sidebar.ejs
    ├── all-archives.ejs
    ├── all-categories.ejs
    ├── all-tags.ejs
    ├── archives.ejs
    ├── category.ejs
    ├── index.ejs
    ├── layout.ejs
    ├── page.ejs
    ├── post.ejs
    └── tag.ejs
```

- **layout** : Contails all mains views
- **layout/partial** : Contains all partial views included in main views
- **layout/partial/post** : Contains all partial views to build post

### Assets ###

#### Stylesheets ####
    
```
├── _css
    ├── base
    │   ├── _base.scss
    ├── components
    │   ├── archives.scss
    │   ├── _box.scss
    │   ├── _button.scss
    │   ├── _category.scss
    │   ├── _form.scss
    │   ├── _hide.scss
    │   ├── _highlight.scss
    │   ├── _icon.scss
    │   ├── _image-gallery.scss
    │   ├── _link.scss
    │   ├── _main-content.scss
    │   ├── _markdown.scss
    │   ├── _pagination.scss
    │   ├── _post-actions.scss
    │   ├── _post.scss
    │   ├── _pullquote.scss
    │   ├── _tag.scss
    │   ├── _text.scss
    │   ├── _tooltip.scss
    │   └── _video.scss
    ├── layout
    │   ├── _about.scss
    │   ├── _blog.scss
    │   ├── _cover.scss
    │   ├── _footer.scss
    │   ├── _header.scss
    │   ├── _main.scss
    │   └── _sidebar.scss
    ├── utils
    │   ├── mixins
    │   │   ├── _button.scss
    │   │   ├── _category.scss
    │   │   ├── _form.scss
    │   │   ├── _opacity.scss
    │   │   ├── _prefix.scss
    │   │   └── _tag.scss
    │   ├── _font.scss
    │   └── _variables.scss
    └── tranquilpeak.scss
```  
  
SCSS structure follow 7-1 pattern of [sass guidelines](http://sass-guidelin.es/#the-7-1-pattern)  
If you want more informations and to understand better this code, consult [sass guidelines](http://sass-guidelin.es/)  

#### Images #####

```
├── _images
    └── cover.png
```

- **cover.png** : Default background cover of the blog
  
Contains all images of the theme.  

#### Javascript #####

```
├── _js
    ├── about.js
    ├── archives-filter.js
    ├── categories-filter.js
    ├── fancybox.js.js
    ├── header.js
    ├── image-gallery.js
    ├── post-bottom-bar.js
    ├── sidebar.js
    ├── smartresize.js
    └── tags-filter.scss
```

- **about.js** : Fade out the blog and let drop the about card of the author and vice versa
- **archives-filter.js** : Filter posts by using their date on archives page : `/archives`
- **categories-filter.js** : Filter posts by using their categories on archives page : `/categories`
- **fancybox.js.js** : Run Fancybox plugin
- **header.js** : Hide the header when the user scrolls down, and show it when he scrolls up
- **image-gallery.js** : Resize all images of an image-gallery
- **post-bottom-bar.js** : Hide the post bottom bar when the post footer is visible by the user, and vice versa
- **sidebar.js** : Open and close the sidebar by swiping the sidebar and the blog and vice versa
- **smartresize.js** : Debouncing function from [John Hann](https://github.com/unscriptable)
- **tags-filter.scss** : Filter posts by using their tags on archives page : `/tags`  
  
Each file correspond to a feature.  
  
## Build ##

### NPM dependencies ###

To install npm dependencies, run ```npm install```  
  
NPM dependencies :  

``` json
"bower" : "^1.3.12"
"grunt" : "^0.4.5"
"grunt-bower" : "^0.18.0"
"grunt-contrib-clean" : "~0.5.0"
"grunt-contrib-concat" : "^0.5.0"
"grunt-contrib-copy" : "~0.4.1"
"grunt-contrib-cssmin" : "^0.12.0"
"grunt-contrib-sass" : "^0.8.1"
"grunt-contrib-uglify" : "^0.7.0"
"grunt-contrib-watch" : "^0.6.1"
"grunt-sails-linker" : "^0.10.1"
"grunt-sync" : "^0.2.3"
"grunt-text-replace" : "^0.4.0"
"include-all" : "^0.1.6"
"load-grunt-tasks" : "~0.2.0"
```
 
### Bower dependencies ###

To install bower dependencies, run ```bower install```  
Bower dependencies are located in ```source/_bower_components```

Bower dependencies :  

``` json
"Font-awesome" : "~4.3.0"
"jQuery" : "~2.1.3"
"Fancybox" : "~2.1.5"
```

### Grunt tasks ###

##### Tasks structure ##### 
  
```
├── tasks
    ├── config
    │   ├── bower.js
    │   ├── clean.js
    │   ├── concat.js
    │   ├── cssmin.js
    │   ├── replace.js
    │   ├── sails-linker.js
    │   ├── sass.js
    │   ├── sync.js
    │   ├── uglify.js
    │   └── watch.js
    ├── register
    │   ├── build.js
    │   ├── buildProd.js
    │   ├── compileAssets.js
    │   ├── linkAssets.js
    │   ├── linkAssetsProd.js
    │   ├── syncAssets.js
    │   └── watch.js
    └── pipeline.js
```  

- **config** : Default tasks
- **register** : Alias tasks which call mutliple default tasks
- **pipeline.js** : Files which contains a list of javascript and stylesheets files linked to the blog

#### Pipeline #####

``` javascript
// Js files to inject in `layout/_partial/script.ejs`
var tranquilpeakJsFilesToInject = [
    'jquery.js',
    'jquery.fancybox.js',
    'jquery.fancybox-thumbs.js',
    'tranquilpeak.js'
];
// Css files to inject in `layout/_partial/head.ejs`
var tranquilpeakCssFilesToInject = [
    'font-awesome.css',
    'jquery.fancybox.css',
    'jquery.fancybox-thumbs.css',
    'tranquilpeak.css'
];
```

- **tranquilpeakJsFilesToInject** :  Files injected in ```layout/_partial/script.ejs``` (developement environment)
- **tranquilpeakCssFilesToInject** :  Files injected in```layout/_partial/head.ejs``` (developement environment)

On production environment, these javascript and stylesheets files are concatenate and minify in 1 javascript file and 1 stylesheet file and linked to their respective views

#### Config tasks ####

- **bower** : Copy all needed files by types from bower dependencies  
- **clean** : Delete ```source/assets``` folder  
- **concat** : 
    * devJs : Concat all javascript files located in ```source/_js/``` into 1 file : ```source/assets/js/tranquilpeak.js```  
    * prodCss : Concat all stylesheets files located in ```source/assets/css/``` into 1 file : ```source/assets/css/style.css```  
    * prodJs : Concat all javascript listed in ```tasks/pipeline.js``` in 1 file : ```source/assets/js/script.js```  
- **cssmin** : Minify ```source/assets/cssstyle.css``` file in : ```source/assets/cssstyle.min.css```   
- **replace** : 
    * linker : Replace ```EJS_ENDTAG``` string to resolve a problem of ejs escaping with sails-linker tasks  
    * cssFancybox : Modify url of images in fancybox.css to resolve images path. Impossible to use an other plugin to do that because in the bower fancybox packages, css files and images are in the same folder and that not the case in assets folder.
- **sails-linker** : 
    * devJs : Link all javascript files listed in ```tasks/pipeline.js```  to ```layout/_partial/script.ejs```  
    * devCss : Link all stylesheets files listed in ```tasks/pipeline.js```  to ```layout/_partial/head.ejs```  
    * prodJs : Link ```source/assets/js/script.min.js``` file in ```layout/_partial/script.ejs```  
    * prodCss : Link ```source/assets/js/style.min.css``` file in ```layout/_partial/head.ejs```  
- **sass** : Compile `source/_css/tranquilpeak.scss` file in `source/assets/css/tranquilpeak.css`  
- **sync** : Synchronize images from ```source/_images``` to ```source/assets/images```  
- **uglify** : Minify ```source/assets/js/script.js``` file in ```source/assets/js/script.min.js```  
- **watch** : Watch assets from ```source/_*/**/*``` folder to detect changes and launch ```SyncAssets``` task  

#### Register tasks ####

- **build** : Synchronize bower dependencies, compile assets (css and js) and link it to views  
- **buildProd** : Synchronize bower dependencies, compile assets (css and js) with some optimization (concat and minify) and link it to views  
- **compileAssets** : Compile scss files, concat js files and syncrhonize images  
- **linkAssets** : Link all javascript and stylesheets files to views  
- **linkAssetsProd** : Link one javascript file and one stylesheet file (concatenated and minified) to views  
- **syncAssets** : Synchronize assets (css, js and images)
- **watch** : Synchronize assets (css, js and images) after changes 

When you run ```build``` or ```buildProd``` tasks, a ```source/assets``` folder will be created with all files generated in. When you will start your hexo server, only this folder will be copied in ```public``` folder

**Development environment**:    
1. For the first time, run ```grunt build``` to sync bower dependencies, compile assets and link it to views 
2. After, run ```grunt watch``` to automatically re-build the project after change on assets

**Production environment (before deploying your blog)** :  Run ```grunt buildProd``` to build the project with some optimization (concat and minify).  
Your blog will have only 1 file for javascript and 1 file for stylesheets to reduce number of HTTP requests and improve performance.

## Running ##

Run ```hexo server``` and start coding! :)