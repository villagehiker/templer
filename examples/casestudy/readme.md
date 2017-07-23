# Templer Case Study for Real-World Website

This case study describes the conversion of a 10-year-old hand-coded website to the Templer static-site generator. The website belongs to [Village Hiker Publishing Company](http://villagehiker.com).

![Homepage layout of villagehiker.com showing desktop three-column layout](media/villagehiker-homepage.jpg)

The converted website uses a simple design employing only HTML and CSS. It contains no javascript. The layout consists of header, footer and three columns. The three columns are:

* Left column for article text and images on content pages, and article links on index.html pages.
* Middle column for internal and external links to related content.
* Right column for affiliate advertising.

The left column receives its text and images from HTML and Markdown content files. While Templer supports Textile markup, the site does not use it. Templer merges content files into the pages while building the website. The middle and right columns receive their content from include files added during the build. The include files are designed to be page specific, but are currently specific to a section such as `travel` or `research-writing`.

The site is responsive to desktop, tablet and smart phone browsers in a simple way. The middle and right columns move below the left column when the viewport is narrow. Images keep their percentage widths regardless of viewport width. Because the images are moderate in bandwidth usage, the site does not use responsive images. 

The case study shows the flexibility of Templer. Templer provides fewer features than some others static-site generators—such as Jekyll or Hugo—but is much much much much much much easier to use, especially if are building a site with a structured design. Templer requires no knowledge of Perl, the development language of Templer. In contrast, the Jekyll and Hugo static-site generators assume come knowledge of Ruby and Go, respectively.

Templer builds a 370-plus page website in 10-12 seconds on a 2.9 GHz Intel Core i5 MacBook Pro. Rebuilds take 6 seconds. Copying images to the output folders accounts for the  longer first-time builds. 

Village Hiker chose Templer after evaluating Jekyll, Hugo and several other static-site generators. The simplicity, ease-of-use, speed and stability of Templer helped make the decision easy. For site developers needing more features, Templer is extensible through plug-ins. Templer appears to be bug free. 

## Assumptions

This case study assumes basic-skills familiarity with HTML and CSS, plus the [Templer readme file](https://github.com/skx/templer/blob/master/README.md). It assumes a high-level understanding of the Templer configuration file, the include files, the template layout file and the content files, plus concepts such as looping and variable usage.

To help gain that knowledge, in summary:

* The Configuration file manages the overall settings of the website. The configuration file includes global variables, such as organization name and paths to folders.
* Template layout files use HTML to define the appearance of the website. A website design can use one or more template files. The Village Hiker site uses one.
* Include files contain information Templer can include on multiple pages. Changing information in an include file changes that information wherever Templer includes the file. Village Hiker uses these files for setting featured articles, external links and advertising content on individual pages.
* Content files contain articles to display as webpages. These can be written in HTML, Markdown or Textile. Village uses mostly HTML input files. 
* Variables define changeable content used in the template layout and the content pages. Village Hiker uses variables to build its index pages and to define include files to use for each content page. It also uses variables for page-specific information, such as the page title and page description, plus the metadata requested by social media sites.

## About the Case Study

The author of this case study is the owner and developer of the Village Hiker website. 

###  Old Site, New Site 

The original site contained 550-plus pages. The website consisted of text files and formatted with CSS, CCS2 and CSS3. It used no javascript.

While most pages of the website looked similar to the user, the pages suffered from inconsistent HTML and CSS. Some pages used HTML 4, others used XHTML. More recent ones used HTML 5. Many of the pages used customized CSS to force the HTML into adaptive and responsive behaviors. The complexity of the site made updating it difficult and extremely time consuming.

The new website contains 370-plus pages, with the removal of individual pages for single photos accounting for almost all of the page reduction. The site uses a single template file. Formatting comes from a single common file off the root folder, plus custom css files in subfolders with displayable content. Subfolders go a maximum of four levels. The site is responsive to viewports on desktop, tablet and smartphone browsers. 

### Case Study Elements

The case study describes:

* templer configuration file
* include files
* a single template layout
* page-specific content input files written in HTML and markdown formats
* images

It briefly highlights the conversion process.

### Software Versions

The Templer installation uses version 1.2 running on Perl version 5.16.0. Perl was installed on MacOS Sierra using PerlBrew, to avoid using the system Perl. The development environment is Coda 2 and the MacOS Terminal application.

### Website Status

The Templer-created site went online July 28, 2017. It receives updates multiple times each week. Updates including adding content pages, fixing errors in current pages and changing content of include files. Such an schedule would very difficult without using a static-site generator.

## Website Design

The new website uses a structured design. The design provides consistency for users and supports the use of Templer.

### Website Purpose

The website serves as the business card and web presence for Village Hiker Publishing Company. The company provides writing, editing and publishing services. It specializes in content development. Village Hiker is not a vanity publisher. 

The website provides original-research content—including documentary-quality photos—on a variety of subjects to illustrate the capabilities of the company. The site contains affiliate advertising, plus a small number of Google ads, all separated from the articles.

### Website Sections

In addition to the root homepage level, the website contains five primary sections, each contained in a subfolder off the root:

* About
* Photos
* Research-Writing
* Travel
* Store

The About, Research-Writing and Travel sections contain subfolders. Some of these subfolders contain their own subfolders. For example, the Research-Writing folder contains subfolders on topics such as books, nature and writing skills. And the Travel folder includes subfolders such as Japan, Vietnam and USA. 

The root level contains a css folder, a media folder and an index.html file. Each subfolder with text files for creating displayable content also contains a css folder, media older and index.html file.

### Text-File Naming 

File naming conventions provide for easily changing the featured articles presented on the index.html pages. The top-level homepage lists a subset of articles from each section and subsection. These subsets change at least monthly and sometimes as often as weekly. The subsections also list article subsets on their index.html pages. Each index.html page at the lowest levels of a folder tree contain a list of all articles in its folder. 

Consider travel as an example. The website homepage lists at least one article from each travel subsection—such as Japan, Taiwan and USA—plus a link to the travel section. In turn, the travel section index.html file lists a few articles from each country, plus links to the country sections. In the bottom level subfolders, the index.html pages for each country section—such as Vietnam and Travel Gear—list all articles in those sections. 

The naming pattern is `description-of-content-vh-tt-nn.wgn`, where:

* `description-of-content` supplies some indication of the file content.
* `-vh` identifies the file as belonging to the Village Hiker website.
* `-tt` identifies the type of content, such as as -ts for travel story or -jn for journal notes. This is optional.
* `-nn` provides a number used to glob files for listing in the index.html files. Each content folder contains a maximum of seven files with names ending in a specific number. A maximum of five may be better. The globing function of Templer also allows selecting files by using  complete basenames and extensions.
* `wgn` is the file extension for input files. This is a default suggested by the Templer configure file.

An example file name is `chasing-the-vermilion-torii-wakayama-japan-vh-ts-00.wgn`, a travel story about Japan.

The website uses file globs to select the files to include in each index.html file. The naming convention supports file globing.

For example, the glob `taiwang: file_glob( travel-taiwan/*jn*.wgn)` includes all Taiwan journal (-jn) files in the index.

And the glob `vietnamg: file_glob( travel-vietnam/*01.wgn)` includes all Vietnam travel files with names ending in 01.

### Banner Images Via CSS

Each section uses it own page banner image. The banner to use is identified in the section-specific css file. The design of the website includes a variable to define page-specific banner images, but this is not currently implemented. 

The current implementation uses fixed-named, section-specific css files. Every section folder includes a css folder containing the locally-customized css file. The template layout file points to a css file named `custom.css` within a folder named css: `<link rel="stylesheet" href="css/customize.css">`

### Index Page

While the website is small, containing less than 400 pages, it is 10 years old and has some following. The new site design caused the renaming of almost all URLs. To help people find lost webpages, the 404 page points to the site index page. The site index page contains links and descriptions for all index.html pages and most original content pages. It links only the index.html page of two historical documents published on the website.

## Templer Components 

This sections describes the use of Templer files in the site.

### Configuration File

The file `templer.cfg` contains website options. The website uses most of the defaults supplied with Templer. The most obvious exception includes setting many navigation path variables, each pointing to a specific folder. The path variables support the creation of menu links, plus internal links between content files. Examples of path variables include:

* `travelpath = path_to(travel)`
* `photospath = path_to(photos)`
* `writingpath = path_to(research-writing)`

The text to the left of the equal sign is a variable name.

Using a path variable as part of an HTML link creates a correct relative href path from the source page to the destination page. For example, this href link uses the `travelpath` variable for the travel folder: `<a href="<!-- tmpl_var name='travelpath' -->/">Travel</a>`. Templer renders the link correctly from:

* the root folder as: `<a href="travel/">Travel</a>`
* a subfolder of the root folder as: `<a href="../travel/">Travel</a>`
* a subfolder of the subfolder as: `<a href="../../travel/">Travel</a>`

This makes trivial the creation of menus from a single template layout as the paths alway render correctly, regardless of the folder depth within the website. The same path  functions work for links between internal content pages.

Global variables go at the end of `templer.cfg` file.They go after the line saying `# Anything below this is a global variable, accessible by name in your templates.`

### Template Layout File

All of the HTML for page design goes into the Template Layout File. The default template layout file is `default.layout`.  A template file is a regular HTML file. It contains at least one variable for inserting page content. Optionally, the template can include variables for inserting other items such as page-specific content or include files. Conditional statements can include or exclude content.

The Village Hiker site uses one page template. It works for both index.html pages and website content pages. The template uses both global and page-specific variables to make each page unique. It also contains conditional statements. This is the heart of the Village Hiker website design. After building the website, several pages are validated at the W3 website. Any errors are corrected in the template file. After rebuilding the site, the validation test are run again.    



### Include Files

### Page Files

#### Index Pages

#### Content Pages
