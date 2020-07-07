# Astart Hugo Theme
 A custom portfolio theme for Hugo

## config.toml
- `	enableEmoji = true` 

#### Social Media
```
[params]
#social media handles
	twitter = "" # omit the @
	github = ""
	email = "addressATdomainDOTcom" #obsucured  by js in social.html
	linkedin = ""
	facebook = ""
	instagram = ""
	youtube = ""
```

```
#sets url for assets folder to assertsDir + /images
	postingfolder = "images" 

# Dot colors #only works for the home page at this point
	dotColor = "#ec008c" # magenta
	# "#00aeef" # cyan
	# "#fff200" # yellow
```

#### Menu
```
# Control the navigation
	SectionPagesMenu = "main"

[[menu.main]]
	identifier = "home"
	name = "Welcome"
	title = "Welcome"
	url = "/"
	weight = 10

# Add item to secondary menu
# [[menu.secondary]]
# 		identifier = "myotherwebsite"
# 		 name = "myotherwebsite.com"
# 		title = "Myotherwebsite.com"
# 		url = "https://myotherwebsite.com"
# 		weight = 100
```

#### Allow html
```
# https://jdhao.github.io/2019/12/29/hugo_html_not_shown/
[markup]
	defaultMarkdownHandler = "goldmark"
		[markup.goldmark]
		[markup.goldmark.renderer]
			unsafe = true
```

## Frontmatter
### Custom Frontmatter Variables
Choose one when building a  new page
- Dot colours are controlled by frontmatter variables
- `dotColor: "#ec008c"`

### Frontmatter Taxonomies
Choose one when building a  new page
- categories: ["coding","graphicdesign","publishing","art","digitalmedia"]

### Menus
    menu: 
      ["main","secondary"]:
        parent: art
        weight: 100

## Shortcodes

### `youtube`
{{< youtube id="RabX4yNyd6s" width="600" class="youtube" >}}
- takes one named parameter: width="000"
- defaults to  400 x 225

### `video`
{{< video src="Extro-V2.mp4" poster="BK-ID-Poster-V2-400x225.png" width="200">}}
- links to page Bundle video
- takes 3 named parameters:src=, poster= (default image file) and width=
- width defaults to 400

### `link`
{{< link "See more here" "posts/some-title" >}}
- creates permalink shortcode relative to baseurl.
- modified from <https://github.com/jorinvo/hugo-shortcodes/blob/master/shortcodes/link.html>
- takes 2 unnamed parameters
  - First parameter is the link text "See more here"
  - Second parameter is the relative URL "posts/some-title"

### `singleimage`
{{< singleimage "\*cats\*" "This is a caption" Fill "200x200" >}}

This is a single image shortcode to display images from the Page Bundle. 
- 5 unnamed parameters
  1. name is "\*filename\*" without file ending
  2. caption
  3. Resize, Fill, or Fit
  4. Image size Resize uses "000" and Fill or Fit uses"000x000"
  5. optional external href "http://astart.ca"
- resizes linked original to "1200x800"

### `singleimagestatic`
{{< singleimagestatic "feather.jpg" "Fit 300x300" Fit "300x300" >}}

This is a single image shortcode to display images from the root `/assets/images` folder. 
- 4 unnnamed parameters
  1. name is "filename.jpg" *must have file ending!*
  2. caption
  3. Resize, Fill, or Fit
  4. Image size Resize uses "000" and Fill or Fit uses"000x000"
- resizes linked original to "1200x800"

#### `sample-figurerev`
{{< figurerev src="/feather.jpg" link="http://apple.com" Target="_blank" title="Image Title" caption="Bob, Bob, Bob!" alt="This is the alt text." height="200" width="325" class="gallery"  >}}

- based on Hugo's original `figure` short code <https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/shortcodes/figure.html>
- displays images from root `/assets/images` folder with lots of parameters available
- UNFINISHED

#### A single permanent image 
\[image alt text](/images/BK-ID-headerlogo.png)

A single image from the `/static/` folder 
- renders exactly as is
- meant for global images

### `foldergallery`
{{< foldergallery "200" >}}

An automatic gallery of photographs from the Page Bundle. 
- no way to display captions
- takes size as unnamed parameter: "400"
- resizes linked original to "1200x800"

### `foldergalleryfilter`
{{< foldergalleryfilter "200" >}}

Same as above but adds filters
- filters must be set in shortcode at this point
- Grayscale, Sepia, Gaussian Blur

### `old-foldergallerylist`
**DEPRECATED: Superceded by Using `singleimage` instead**
    <div class="clearfix"> 
    	{{< foldergallerylist "*IMG_6535*" "This is a loaf of bread" "200" >}}
    	{{< foldergallerylist "*cats*" "This is Pete and Em again" "200" >}}
    </div >

This is a gallery of images stored in the Page Bundle, but called by means of a list, which allows it to have custom sizes and captions. 
- For now it needs to have a \<div> surrounding it to clear the float.

- 4 unnnamed parameters
  1. name is "filename.jpg" *must have file ending!*
  2. caption
  3. Height Fit size
  4. optional external link "http://astart.ca"
- resizes linked original to "1200x800"

### JSON `boatlist` and `ebooklist`
Shortcodes to list json data files
- `boatlist` uses two columns
- `{{booklist "magazines"}}`  uses one parameter to name database in file
- `{{< ebooklist >}}`

## target="_blank"
- in config.toml file

#### Blackfriday
<https://code.luasoftware.com/tutorials/hugo/how-to-create-link-with-target-blanks-in-hugo-markdown/>

    [Blackfriday]
      plainIDAnchors = true
      hrefTargetBlank = true

#### Goldmark
<https://agrimprasad.com/post/hugo-goldmark-markdown/>

The Markdown renderer has changed in the latest Hugo v0.62.0 from Blackfriday to Goldmark which should allow Hugo markdown to be more compatible with other markdown flavours, such as that of GitHub.

In order to open links in new tab with the Goldmark markdown renderer, create a file at `layouts/_default/_markup/render-link.html` with the following content:

`<a href="{{ .Destination | safeURL }}"{{ with .Title}} title="{{ . }}"{{ end }}{{ if strings.HasPrefix .Destination "http" }} target="_blank"{{ end }}>{{ .Text }}</a>
`

## Enable html in markdown
<https://jdhao.github.io/2019/12/29/hugo_html_not_shown/>
#### Goldmark
    [markup]
    	defaultMarkdownHandler = "goldmark"
    		[markup.goldmark]
    		[markup.goldmark.renderer]
    			unsafe = true
    			
#### Blackfriday

    [markup]
      defaultMarkdownHandler = "blackfriday"

## Emojis
`	enableEmoji = true` to config.toml
<https://www.webfx.com/tools/emoji-cheat-sheet/>

Must be above Optional Parameters section
- :smile:
- :frowning_face_:
- :heart:

Use `{{ emojify :smile: :heart: :frowning_face_: }}` in templates

## Fancybox
Image links for the above shortcodes use Fancybox3 as a lightbox <http://fancyapps.com/fancybox/3/>


## Data
- Use in layouts folder (templates)
- place datafile in /data/ 
- json, YAML, toml

`{{range .Site.Data.filename}}`  
	`{{.Name}} — ${{.Price}}`<br>  
`{{end}}`

