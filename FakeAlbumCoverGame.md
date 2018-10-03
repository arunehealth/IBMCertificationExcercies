
 <div class="alert alert-block alert-info" style="margin-top: 20px">
 <a href="http://cocl.us/NotebooksPython101"><img src = "https://ibm.box.com/shared/static/yfe6h4az47ktg2mm9h05wby2n7e8kei3.png" width = 750, align = "center"></a>

<a href="https://www.bigdatauniversity.com"><img src = "https://ibm.box.com/shared/static/ugcqz6ohbvff804xp84y4kqnvvk3bq1g.png" width = 300, align = "center"></a>

<h1 align=center><font size = 5> Make Fake Album Cover Game</font></h1>

## Table of Contents
Our goal is to create randomly generated album covers with:

<div class="alert alert-block alert-info" style="margin-top: 20px">
<ol>

<li><a href="#ref1">Learn how to use the function display_cover</a></li>
<li><a href="#ref2">Loading a random page from Wikipedia</a></li>
<li><a href="#ref3">Extracting the Title of the Article</a></li>
<li><a href="#ref4"> Displaying the Album Cover</a></li>


</ol>
<br>
<p></p>
Estimated Time Needed: <strong>60 min</strong>
</div>

<hr>


Inspiration: [Fake Album Covers](https://fakealbumcovers.com/)

#### Import libraries 



```python
from IPython.display import Image as IPythonImage
from PIL import Image
from PIL import ImageFont
from PIL import ImageDraw
```

#### Helper function to superimpose text on image 



```python
def display_cover(top,bottom ):
    """This fucntoin
    """
    import requests
    
    name='album_art_raw.png'
    # Now let's make get an album cover.
    # https://picsum.photos/ is a free service that offers random images.
    # Let's get a random image:
    album_art_raw = requests.get('https://picsum.photos/500/500/?random')
    # and save it as 'album_art_raw.png'
    with open(name,'wb') as album_art_raw_file:
       album_art_raw_file.write(album_art_raw.content)
    # Now that we have our raw image, let's open it 
    # and write our band and album name on it
    img = Image.open("album_art_raw.png")
    draw = ImageDraw.Draw(img)

    # We'll choose a font for our band and album title, 
    # run "% ls /usr/share/fonts/truetype/dejavu" in a cell to see what else is available,
    # or download your own .ttf fonts!
    band_name_font = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf", 25) #25pt font
    album_name_font = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf", 20) # 20pt font

    # the x,y coordinates for where our album name and band name text will start
    # counted from the top left of the picture (in pixels)
    band_x, band_y = 50, 50
    album_x, album_y = 50, 400

    # Our text should be visible on any image. A good way
    # of accomplishing that is to use white text with a 
    # black border. We'll use the technique shown here to draw the border:
    # https://mail.python.org/pipermail/image-sig/2009-May/005681.html
    outline_color ="black"

    draw.text((band_x-1, band_y-1), top, font=band_name_font, fill=outline_color)
    draw.text((band_x+1, band_y-1), top, font=band_name_font, fill=outline_color)
    draw.text((band_x-1, band_y+1), top, font=band_name_font, fill=outline_color)
    draw.text((band_x+1, band_y+1), top, font=band_name_font, fill=outline_color)

    draw.text((album_x-1, album_y-1), bottom , font=album_name_font, fill=outline_color)
    draw.text((album_x+1, album_y-1), bottom , font=album_name_font, fill=outline_color)
    draw.text((album_x-1, album_y+1), bottom , font=album_name_font, fill=outline_color)
    draw.text((album_x+1, album_y+1), bottom , font=album_name_font, fill=outline_color)

    draw.text((band_x,band_y),top,(255,255,255),font=band_name_font)
    draw.text((album_x, album_y),bottom,(255,255,255),font=album_name_font)

    return img
```

## 1) Learn how to use the function display_cover <a id='ref1'></a>

 The function **display_cover**  selects a random image from https://picsum.photos/  and will help us superimpose two strings over the image. The parameter **top** is the string we would like to superimpose on the top of an image.  The parameter bottom is the string we would like to display on the bottom of the image.  The function does not return the image but returns an object of type  Image from the Pillow library; the object represents a PIL image. 


```python
img=display_cover(top='Python',bottom='Data Science')
```

To save the image, we use the method **save** . The argument is the file  name of the image  we would like to save in this case 'sample-out.png'


```python
img.save('sample-out.png')
```

Finely we use **IPythonImage** to read the image file and display the results.



```python
IPythonImage(filename='sample-out.png')
```




![png](output_14_0.png)



**Question 1)** Use the **display_cover** function to display the image with the name Python on the top and Data Science on the bottom. Save the image as **'sample-out.png'**.

## Part 2: Loading a random page from Wikipedia  <a id='ref2'></a>

 In this project, we will use the request library, we used it in the function **display_cover**, but you should import the library in the next cell.


```python
import requests
```

 The following is the URL to the  page 

**Question 2)** Get Wikipedia page is converted to a string


```python
wikipedia_link='https://en.wikipedia.org/wiki/Special:Random'
response = requests.get('https://en.wikipedia.org/wiki/Special:Random')
print (response)
```

    <Response [200]>



```python
print (response.text)
print(type(response.text))
```

    <!DOCTYPE html>
    <html class="client-nojs" lang="en" dir="ltr">
    <head>
    <meta charset="UTF-8"/>
    <title>Witches Abroad - Wikipedia</title>
    <script>document.documentElement.className = document.documentElement.className.replace( /(^|\s)client-nojs(\s|$)/, "$1client-js$2" );</script>
    <script>(window.RLQ=window.RLQ||[]).push(function(){mw.config.set({"wgCanonicalNamespace":"","wgCanonicalSpecialPageName":false,"wgNamespaceNumber":0,"wgPageName":"Witches_Abroad","wgTitle":"Witches Abroad","wgCurRevisionId":848046218,"wgRevisionId":848046218,"wgArticleId":610417,"wgIsArticle":true,"wgIsRedirect":false,"wgAction":"view","wgUserName":null,"wgUserGroups":["*"],"wgCategories":["Pages to import images to Wikidata","1991 British novels","Discworld books","1991 fantasy novels"],"wgBreakFrames":false,"wgPageContentLanguage":"en","wgPageContentModel":"wikitext","wgSeparatorTransformTable":["",""],"wgDigitTransformTable":["",""],"wgDefaultDateFormat":"dmy","wgMonthNames":["","January","February","March","April","May","June","July","August","September","October","November","December"],"wgMonthNamesShort":["","Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"],"wgRelevantPageName":"Witches_Abroad","wgRelevantArticleId":610417,"wgRequestId":"W7TQqwrAIEMAAGmhwj4AAAAG","wgCSPNonce":false,"wgIsProbablyEditable":true,"wgRelevantPageIsProbablyEditable":true,"wgRestrictionEdit":[],"wgRestrictionMove":[],"wgFlaggedRevsParams":{"tags":{}},"wgStableRevisionId":null,"wgCategoryTreePageCategoryOptions":"{\"mode\":0,\"hideprefix\":20,\"showcount\":true,\"namespaces\":false}","wgWikiEditorEnabledModules":[],"wgBetaFeaturesFeatures":[],"wgMediaViewerOnClick":true,"wgMediaViewerEnabledByDefault":true,"wgPopupsShouldSendModuleToUser":true,"wgPopupsConflictsWithNavPopupGadget":false,"wgVisualEditor":{"pageLanguageCode":"en","pageLanguageDir":"ltr","pageVariantFallbacks":"en","usePageImages":true,"usePageDescriptions":true},"wgMFExpandAllSectionsUserOption":true,"wgMFEnableFontChanger":true,"wgMFDisplayWikibaseDescriptions":{"search":true,"nearby":true,"watchlist":true,"tagline":false},"wgRelatedArticles":null,"wgRelatedArticlesUseCirrusSearch":true,"wgRelatedArticlesOnlyUseCirrusSearch":false,"wgULSCurrentAutonym":"English","wgNoticeProject":"wikipedia","wgCentralNoticeCookiesToDelete":[],"wgCentralNoticeCategoriesUsingLegacy":["Fundraising","fundraising"],"wgWikibaseItemId":"Q1994566","wgScoreNoteLanguages":{"arabic":"العربية","catalan":"català","deutsch":"Deutsch","english":"English","espanol":"español","italiano":"italiano","nederlands":"Nederlands","norsk":"norsk","portugues":"português","suomi":"suomi","svenska":"svenska","vlaams":"West-Vlams"},"wgScoreDefaultNoteLanguage":"nederlands","wgCentralAuthMobileDomain":false,"wgCodeMirrorEnabled":true,"wgVisualEditorToolbarScrollOffset":0,"wgVisualEditorUnsupportedEditParams":["undo","undoafter","veswitched"],"wgEditSubmitButtonLabelPublish":true});mw.loader.state({"ext.gadget.charinsert-styles":"ready","ext.globalCssJs.user.styles":"ready","ext.globalCssJs.site.styles":"ready","site.styles":"ready","noscript":"ready","user.styles":"ready","ext.globalCssJs.user":"ready","ext.globalCssJs.site":"ready","user":"ready","user.options":"ready","user.tokens":"loading","ext.cite.styles":"ready","mediawiki.legacy.shared":"ready","mediawiki.legacy.commonPrint":"ready","mediawiki.toc.styles":"ready","wikibase.client.init":"ready","ext.visualEditor.desktopArticleTarget.noscript":"ready","ext.uls.interlanguage":"ready","ext.wikimediaBadges":"ready","ext.3d.styles":"ready","mediawiki.skinning.interface":"ready","skins.vector.styles":"ready"});mw.loader.implement("user.tokens@0tffind",function($,jQuery,require,module){/*@nomin*/mw.user.tokens.set({"editToken":"+\\","patrolToken":"+\\","watchToken":"+\\","csrfToken":"+\\"});
    });RLPAGEMODULES=["ext.cite.a11y","site","mediawiki.page.startup","mediawiki.user","mediawiki.page.ready","mediawiki.toc","mediawiki.searchSuggest","ext.gadget.teahouse","ext.gadget.ReferenceTooltips","ext.gadget.watchlist-notice","ext.gadget.DRN-wizard","ext.gadget.charinsert","ext.gadget.refToolbar","ext.gadget.extra-toolbar-buttons","ext.gadget.switcher","ext.centralauth.centralautologin","mmv.head","mmv.bootstrap.autostart","ext.popups","ext.visualEditor.desktopArticleTarget.init","ext.visualEditor.targetLoader","ext.eventLogging.subscriber","ext.wikimediaEvents","ext.navigationTiming","ext.uls.eventlogger","ext.uls.init","ext.uls.compactlinks","ext.uls.interface","ext.3d","ext.centralNotice.geoIP","ext.centralNotice.startUp","skins.vector.js"];mw.loader.load(RLPAGEMODULES);});</script>
    <link rel="stylesheet" href="/w/load.php?debug=false&amp;lang=en&amp;modules=ext.3d.styles%7Cext.cite.styles%7Cext.uls.interlanguage%7Cext.visualEditor.desktopArticleTarget.noscript%7Cext.wikimediaBadges%7Cmediawiki.legacy.commonPrint%2Cshared%7Cmediawiki.skinning.interface%7Cmediawiki.toc.styles%7Cskins.vector.styles%7Cwikibase.client.init&amp;only=styles&amp;skin=vector"/>
    <script async="" src="/w/load.php?debug=false&amp;lang=en&amp;modules=startup&amp;only=scripts&amp;skin=vector"></script>
    <meta name="ResourceLoaderDynamicStyles" content=""/>
    <link rel="stylesheet" href="/w/load.php?debug=false&amp;lang=en&amp;modules=ext.gadget.charinsert-styles&amp;only=styles&amp;skin=vector"/>
    <link rel="stylesheet" href="/w/load.php?debug=false&amp;lang=en&amp;modules=site.styles&amp;only=styles&amp;skin=vector"/>
    <meta name="generator" content="MediaWiki 1.32.0-wmf.23"/>
    <meta name="referrer" content="origin"/>
    <meta name="referrer" content="origin-when-crossorigin"/>
    <meta name="referrer" content="origin-when-cross-origin"/>
    <meta property="og:image" content="https://upload.wikimedia.org/wikipedia/en/7/71/Witches-abroad-cover.jpg"/>
    <link rel="alternate" href="android-app://org.wikipedia/http/en.m.wikipedia.org/wiki/Witches_Abroad"/>
    <link rel="alternate" type="application/x-wiki" title="Edit this page" href="/w/index.php?title=Witches_Abroad&amp;action=edit"/>
    <link rel="edit" title="Edit this page" href="/w/index.php?title=Witches_Abroad&amp;action=edit"/>
    <link rel="apple-touch-icon" href="/static/apple-touch/wikipedia.png"/>
    <link rel="shortcut icon" href="/static/favicon/wikipedia.ico"/>
    <link rel="search" type="application/opensearchdescription+xml" href="/w/opensearch_desc.php" title="Wikipedia (en)"/>
    <link rel="EditURI" type="application/rsd+xml" href="//en.wikipedia.org/w/api.php?action=rsd"/>
    <link rel="license" href="//creativecommons.org/licenses/by-sa/3.0/"/>
    <link rel="canonical" href="https://en.wikipedia.org/wiki/Witches_Abroad"/>
    <link rel="dns-prefetch" href="//login.wikimedia.org"/>
    <link rel="dns-prefetch" href="//meta.wikimedia.org" />
    <!--[if lt IE 9]><script src="/w/load.php?debug=false&amp;lang=en&amp;modules=html5shiv&amp;only=scripts&amp;skin=vector&amp;sync=1"></script><![endif]-->
    </head>
    <body class="mediawiki ltr sitedir-ltr mw-hide-empty-elt ns-0 ns-subject page-Witches_Abroad rootpage-Witches_Abroad skin-vector action-view">		<div id="mw-page-base" class="noprint"></div>
    		<div id="mw-head-base" class="noprint"></div>
    		<div id="content" class="mw-body" role="main">
    			<a id="top"></a>
    			<div id="siteNotice" class="mw-body-content"><!-- CentralNotice --></div><div class="mw-indicators mw-body-content">
    </div>
    <h1 id="firstHeading" class="firstHeading" lang="en"><i>Witches Abroad</i></h1>			<div id="bodyContent" class="mw-body-content">
    				<div id="siteSub" class="noprint">From Wikipedia, the free encyclopedia</div>				<div id="contentSub"></div>
    				<div id="jump-to-nav"></div>				<a class="mw-jump-link" href="#mw-head">Jump to navigation</a>
    				<a class="mw-jump-link" href="#p-search">Jump to search</a>
    				<div id="mw-content-text" lang="en" dir="ltr" class="mw-content-ltr"><div class="mw-parser-output"><table class="infobox vcard" style="width:22em"><caption style="font-style:italic;padding-bottom:0.2em;">Witches Abroad <span class="Z3988" title="ctx_ver=Z39.88-2004&amp;rft_val_fmt=info%3Aofi%2Ffmt%3Akev%3Amtx%3Abook&amp;rft.genre=book&amp;rft.btitle=Witches+Abroad&amp;rft.author=%5B%5BTerry+Pratchett%5D%5D&amp;rft.date=1991&amp;rft.pub=%5B%5BVictor+Gollancz%5D%5D&amp;rft.series=%27%27%5B%5BDiscworld%5D%5D%27%27%3Cbr+%2F%3E12th+novel+%E2%80%93+3rd+witches+story"></span></caption><tbody><tr><td colspan="2" style="text-align:center">
    <a href="/wiki/File:Witches-abroad-cover.jpg" class="image"><img alt="Witches-abroad-cover.jpg" src="//upload.wikimedia.org/wikipedia/en/7/71/Witches-abroad-cover.jpg" width="204" height="300" data-file-width="204" data-file-height="300" /></a></td></tr><tr><th scope="row">Author</th><td>
    <a href="/wiki/Terry_Pratchett" title="Terry Pratchett">Terry Pratchett</a></td></tr><tr><th scope="row">Language</th><td>
    English</td></tr><tr><th scope="row">Series</th><td>
    <i><a href="/wiki/Discworld" title="Discworld">Discworld</a></i><br />12th novel – 3rd witches story</td></tr><tr><th scope="row">Subject</th><td>
    <p><a href="/wiki/Fairy_tale" title="Fairy tale">Fairy tales</a>, <a href="/wiki/Haitian_Vodou" title="Haitian Vodou">voodoo</a> and <a href="/wiki/Tourism" title="Tourism">tourism</a>
    </p>
    <dl><dt>Characters</dt>
    <dd><a href="/wiki/Granny_Weatherwax" title="Granny Weatherwax">Granny Weatherwax</a>, <a href="/wiki/Nanny_Ogg" title="Nanny Ogg">Nanny Ogg</a>, <a href="/wiki/Magrat_Garlick" class="mw-redirect" title="Magrat Garlick">Magrat Garlick</a></dd>
    <dt>Locations</dt>
    <dd><a href="/wiki/Genua_(Discworld)" class="mw-redirect" title="Genua (Discworld)">Genua</a>, <a href="/w/index.php?title=The_Road_From_Lancre_to_Genua&amp;action=edit&amp;redlink=1" class="new" title="The Road From Lancre to Genua (page does not exist)">The Road From Lancre to Genua</a></dd></dl>
    </td></tr><tr><th scope="row">Genre</th><td>
    <a href="/wiki/Fantasy" title="Fantasy">Fantasy</a></td></tr><tr><th scope="row">Publisher</th><td>
    <a href="/wiki/Victor_Gollancz" title="Victor Gollancz">Victor Gollancz</a></td></tr><tr><th scope="row"><div style="padding:0.1em 0;line-height:1.2em;">Publication date</div></th><td>
    1991</td></tr><tr><th scope="row"><a href="/wiki/International_Standard_Book_Number" title="International Standard Book Number">ISBN</a></th><td>
    <style data-mw-deduplicate="TemplateStyles:r861714446">.mw-parser-output cite.citation{font-style:inherit}.mw-parser-output q{quotes:"\"""\"""'""'"}.mw-parser-output code.cs1-code{color:inherit;background:inherit;border:inherit;padding:inherit}.mw-parser-output .cs1-lock-free a{background:url("//upload.wikimedia.org/wikipedia/commons/thumb/6/65/Lock-green.svg/9px-Lock-green.svg.png")no-repeat;background-position:right .1em center}.mw-parser-output .cs1-lock-limited a,.mw-parser-output .cs1-lock-registration a{background:url("//upload.wikimedia.org/wikipedia/commons/thumb/d/d6/Lock-gray-alt-2.svg/9px-Lock-gray-alt-2.svg.png")no-repeat;background-position:right .1em center}.mw-parser-output .cs1-lock-subscription a{background:url("//upload.wikimedia.org/wikipedia/commons/thumb/a/aa/Lock-red-alt-2.svg/9px-Lock-red-alt-2.svg.png")no-repeat;background-position:right .1em center}.mw-parser-output .cs1-subscription,.mw-parser-output .cs1-registration{color:#555}.mw-parser-output .cs1-subscription span,.mw-parser-output .cs1-registration span{border-bottom:1px dotted;cursor:help}.mw-parser-output .cs1-hidden-error{display:none;font-size:100%}.mw-parser-output .cs1-visible-error{font-size:100%}.mw-parser-output .cs1-subscription,.mw-parser-output .cs1-registration,.mw-parser-output .cs1-format{font-size:95%}.mw-parser-output .cs1-kern-left,.mw-parser-output .cs1-kern-wl-left{padding-left:0.2em}.mw-parser-output .cs1-kern-right,.mw-parser-output .cs1-kern-wl-right{padding-right:0.2em}</style><a href="/wiki/Special:BookSources/0-575-04980-4" title="Special:BookSources/0-575-04980-4">0-575-04980-4</a></td></tr></tbody></table>
    <p><i><b>Witches Abroad</b></i> is the twelfth <i><a href="/wiki/Discworld" title="Discworld">Discworld</a></i> novel by <a href="/wiki/Terry_Pratchett" title="Terry Pratchett">Terry Pratchett</a>, originally published in 1991.<sup id="cite_ref-1" class="reference"><a href="#cite_note-1">&#91;1&#93;</a></sup>
    </p>
    <div id="toc" class="toc"><input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none" /><div class="toctitle" lang="en" dir="ltr"><h2>Contents</h2><span class="toctogglespan"><label class="toctogglelabel" for="toctogglecheckbox"></label></span></div>
    <ul>
    <li class="toclevel-1 tocsection-1"><a href="#Plot"><span class="tocnumber">1</span> <span class="toctext">Plot</span></a></li>
    <li class="toclevel-1 tocsection-2"><a href="#Themes"><span class="tocnumber">2</span> <span class="toctext">Themes</span></a></li>
    <li class="toclevel-1 tocsection-3"><a href="#See_also"><span class="tocnumber">3</span> <span class="toctext">See also</span></a></li>
    <li class="toclevel-1 tocsection-4"><a href="#References"><span class="tocnumber">4</span> <span class="toctext">References</span></a></li>
    <li class="toclevel-1 tocsection-5"><a href="#External_links"><span class="tocnumber">5</span> <span class="toctext">External links</span></a></li>
    </ul>
    </div>
    
    <h2><span class="mw-headline" id="Plot">Plot</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=Witches_Abroad&amp;action=edit&amp;section=1" title="Edit section: Plot">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <p>Following the death of the witch Desiderata Hollow, <a href="/wiki/Magrat_Garlick" class="mw-redirect" title="Magrat Garlick">Magrat Garlick</a> is sent her magic wand, for Desiderata was not only a witch, but also a <a href="/wiki/Fairy_godmother" title="Fairy godmother">fairy godmother</a>. Having given the wand to Magrat, she effectively makes Magrat the new fairy godmother to a young woman called Emberella, who lives across the Disc in <a href="/wiki/Genua_(Discworld)" class="mw-redirect" title="Genua (Discworld)">Genua</a>. Sadly, Desiderata does not give Magrat any instruction on the use of the wand, so pretty much anything that Magrat points it at becomes a pumpkin. This leaves several animals around Magrat's cottage now as pumpkins, one of which still thinks it is a stoat. Desiderata had promised Emberella previously that she will not marry the Duke, who's really a prince/frog, and now it is up to Magrat and her companions (<a href="/wiki/Granny_Weatherwax" title="Granny Weatherwax">Granny Weatherwax</a> and <a href="/wiki/Nanny_Ogg" title="Nanny Ogg">Nanny Ogg</a>) to ensure that Emberella does not marry the Duke, despite the desires of another Witch in Genua called Lily, Desiderata's counterpart. She used the power of her own reflection to capture Genua.
    </p><p>The journey to Genua takes some time and involves numerous mis-adventures, such as an encounter with a village terrorised by a <a href="/wiki/Vampire" title="Vampire">Vampire</a>—<a href="/wiki/Flora_and_fauna_of_the_Discworld#Greebo" title="Flora and fauna of the Discworld">Greebo</a> catches it in bat form and eats it—an incident where they encounter a <a href="/wiki/Running_of_the_Bulls" class="mw-redirect" title="Running of the Bulls">Running of the Bulls</a>-like event, a house falling on Nanny's head which she survives thanks to her hat with the willow reinforcement. Upon arrival in Genua, Magrat goes to meet Emberella, whilst the two older witches meet Erzulie Gogol, a voodoo witch and her zombie servant, Baron Saturday (who was also her late lover). It is at this time that Magrat finds out that Emberella has two fairy godmothers, Magrat and Lilith. It was Lilith who had manipulated many of the various stories that the Witches had traveled through and who was now manipulating Genua itself, wrapping the city around her version of the Cinderella story. Lilith has had people arrested for crimes against stories, including the arrest of a toymaker for not being jolly, not whistling and not telling the children stories. At this point it is revealed that Lilith is actually Lily, Granny Weatherwax's older sister.
    </p><p>Using hypnosis, Granny convinces Magrat to attend a Masked Ball in place of Emberella. Greebo is transformed into human form to aid the witches. Emberella's dress fits, but the glass slippers do not. After enjoying themselves for a while at the ball, the witches are discovered and are cast into a dungeon.
    </p><p>At that point, Emberella, Mrs. Gogol and Baron Saturday arrive at the Ball, having broken the witches out of their prison. A high concentration of Magic causes the Duke to revert to his frog form, and he is trampled by Baron Saturday causing Lilith to flee. Granny starts to follow, but Mrs. Gogol tries to stop her using a voodoo doll, wanting to kill Lilith. Granny uses Mrs Gogol's own belief in the power of the voodoo doll to make the voodoo doll burst into flames when Granny thrusts her own arm into a flaming <a href="/wiki/Torch" title="Torch">torch</a>. Granny Weatherwax then pursues Lilith.  Emberella is informed that, as the daughter of the late <a href="/wiki/Baron_Samedi" title="Baron Samedi">Baron Saturday</a> (who was the late <a href="/wiki/Duke" title="Duke">Duke</a> in Genua), she is now <a href="/wiki/Duchess" class="mw-redirect" title="Duchess">Duchess</a> of Genua. Her first command is to end the Ball (she dislikes them) and attend the Mardi Gras parade, a form of binge drinking carnival.
    </p><p>Granny manages to defeat Lilith by trapping her in a mirror, and the three Witches return home. Granny shows Magrat how to use the wand to do magic, that it takes more than wishing. Magrat throws the wand into a river, to be lost forever. Then the Witches go home, the long way, and <a href="/wiki/Seeing_the_elephant" title="Seeing the elephant">see the elephant</a>.
    </p>
    <h2><span class="mw-headline" id="Themes">Themes</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=Witches_Abroad&amp;action=edit&amp;section=2" title="Edit section: Themes">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <ul><li>Fairy tales</li>
    <li>Fairy godmothers</li>
    <li>Cinderella</li>
    <li>New Orleans</li>
    <li>Carnival / Mardi Gras</li>
    <li>Swamps</li>
    <li>Voodoo</li></ul>
    <h2><span class="mw-headline" id="See_also">See also</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=Witches_Abroad&amp;action=edit&amp;section=3" title="Edit section: See also">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <ul><li><a href="/wiki/The_Frog_Princess" title="The Frog Princess">The Frog Princess</a></li></ul>
    <h2><span class="mw-headline" id="References">References</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=Witches_Abroad&amp;action=edit&amp;section=4" title="Edit section: References">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <div class="reflist" style="list-style-type: decimal;">
    <div class="mw-references-wrap"><ol class="references">
    <li id="cite_note-1"><span class="mw-cite-backlink"><b><a href="#cite_ref-1">^</a></b></span> <span class="reference-text">Fantastic Fiction <a rel="nofollow" class="external text" href="http://www.fantasticfiction.co.uk/p/terry-pratchett/witches-abroad.htm">Witches Abroad (Discworld, book 12) Terry Pratchett</a> Retrieved 2009-05-9</span>
    </li>
    </ol></div></div>
    <h2><span class="mw-headline" id="External_links">External links</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=Witches_Abroad&amp;action=edit&amp;section=5" title="Edit section: External links">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <table role="presentation" class="mbox-small plainlinks sistersitebox" style="background-color:#f9f9f9;border:1px solid #aaa;color:#000">
    <tbody><tr>
    <td class="mbox-image"><img alt="" src="//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikiquote-logo.svg/34px-Wikiquote-logo.svg.png" width="34" height="40" class="noviewer" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikiquote-logo.svg/51px-Wikiquote-logo.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikiquote-logo.svg/68px-Wikiquote-logo.svg.png 2x" data-file-width="300" data-file-height="355" /></td>
    <td class="mbox-text plainlist">Wikiquote has quotations related to: <i><b><a href="https://en.wikiquote.org/wiki/Discworld#Witches_Abroad" class="extiw" title="q:Discworld">Witches Abroad</a></b></i></td></tr></tbody></table>
    <ul><li><a rel="nofollow" class="external text" href="http://www.isfdb.org/cgi-bin/title.cgi?827"><i>Witches Abroad</i></a> title listing at the <a href="/wiki/Internet_Speculative_Fiction_Database" title="Internet Speculative Fiction Database">Internet Speculative Fiction Database</a></li>
    <li><a rel="nofollow" class="external text" href="http://www.lspace.org/books/apf/witches-abroad.html">Annotations for <i>Witches Abroad</i></a></li>
    <li><a rel="nofollow" class="external text" href="http://www.lspace.org/books/pqf/witches-abroad.html">Quotes from <i>Witches Abroad</i></a></li>
    <li><a rel="nofollow" class="external text" href="http://www.lspace.org/books/synopses/witches-abroad.html">Synopsis for <i>Witches Abroad</i></a></li></ul>
    <table class="wikitable succession-box" style="margin:0.5em auto; font-size:95%;clear:both;">
    
    <tbody><tr>
    <th colspan="3" style="border-top: 5px solid #cccccc;"><a href="/wiki/Discworld_reading_order" class="mw-redirect" title="Discworld reading order">Reading order guide</a>
    </th></tr>
    
    <tr style="text-align:center;">
    <td style="width:30%;" rowspan="1">Preceded&#160;by<br /><span style="font-weight: bold"><a href="/wiki/Reaper_Man" title="Reaper Man">Reaper Man</a></span>
    </td>
    <td style="width: 40%; text-align: center;" rowspan="1"><b> 12th <a href="/wiki/Discworld#Novels" title="Discworld">Discworld Novel</a></b>
    </td>
    <td style="width: 30%; text-align: center;" rowspan="1">Succeeded&#160;by<br /><span style="font-weight: bold"><a href="/wiki/Small_Gods" title="Small Gods">Small Gods</a></span>
    </td></tr>
    
    
    <tr style="text-align:center;">
    <td style="width:30%;" rowspan="1">Preceded&#160;by<br /><span style="font-weight: bold"><a href="/wiki/Wyrd_Sisters" title="Wyrd Sisters">Wyrd Sisters</a></span>
    </td>
    <td style="width: 40%; text-align: center;" rowspan="1"><b> 3rd <a href="/wiki/Discworld_reading_order#The_Witches_Series" class="mw-redirect" title="Discworld reading order">Witches Story</a></b><br />Published in 1991
    </td>
    <td style="width: 30%; text-align: center;" rowspan="1">Succeeded&#160;by<br /><span style="font-weight: bold"><a href="/wiki/Lords_and_Ladies_(novel)" title="Lords and Ladies (novel)">Lords and Ladies</a></span>
    </td></tr>
    </tbody></table>
    <div role="navigation" class="navbox" aria-labelledby="Terry_Pratchett&amp;#039;s_Discworld" style="padding:3px"><table class="nowraplinks hlist collapsible autocollapse navbox-inner" style="border-spacing:0;background:transparent;color:inherit"><tbody><tr><th scope="col" class="navbox-title" colspan="2"><div class="plainlinks hlist navbar mini"><ul><li class="nv-view"><a href="/wiki/Template:Discworld" title="Template:Discworld"><abbr title="View this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">v</abbr></a></li><li class="nv-talk"><a href="/wiki/Template_talk:Discworld" title="Template talk:Discworld"><abbr title="Discuss this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">t</abbr></a></li><li class="nv-edit"><a class="external text" href="//en.wikipedia.org/w/index.php?title=Template:Discworld&amp;action=edit"><abbr title="Edit this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">e</abbr></a></li></ul></div><div id="Terry_Pratchett&amp;#039;s_Discworld" style="font-size:114%;margin:0 4em"><span class="vcard"><span class="fn"><a href="/wiki/Terry_Pratchett" title="Terry Pratchett">Terry Pratchett</a></span></span>'s <i><a href="/wiki/Discworld" title="Discworld">Discworld</a></i></div></th></tr><tr><th scope="row" class="navbox-group" style="width:1%">Novels</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px;font-style:italic;"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/The_Colour_of_Magic" title="The Colour of Magic">The Colour of Magic</a></li>
    <li><a href="/wiki/The_Light_Fantastic" title="The Light Fantastic">The Light Fantastic</a></li>
    <li><a href="/wiki/Equal_Rites" title="Equal Rites">Equal Rites</a></li>
    <li><a href="/wiki/Mort" title="Mort">Mort</a></li>
    <li><a href="/wiki/Sourcery" title="Sourcery">Sourcery</a></li>
    <li><a href="/wiki/Wyrd_Sisters" title="Wyrd Sisters">Wyrd Sisters</a></li>
    <li><a href="/wiki/Pyramids_(novel)" title="Pyramids (novel)">Pyramids</a></li>
    <li><a href="/wiki/Guards!_Guards!" title="Guards! Guards!">Guards! Guards!</a></li>
    <li><a href="/wiki/Eric_(novel)" title="Eric (novel)">Eric</a></li>
    <li><a href="/wiki/Moving_Pictures_(novel)" title="Moving Pictures (novel)">Moving Pictures</a></li>
    <li><a href="/wiki/Reaper_Man" title="Reaper Man">Reaper Man</a></li>
    <li><a class="mw-selflink selflink">Witches Abroad</a></li>
    <li><a href="/wiki/Small_Gods" title="Small Gods">Small Gods</a></li>
    <li><a href="/wiki/Lords_and_Ladies_(novel)" title="Lords and Ladies (novel)">Lords and Ladies</a></li>
    <li><a href="/wiki/Men_at_Arms" title="Men at Arms">Men at Arms</a></li>
    <li><a href="/wiki/Soul_Music_(novel)" title="Soul Music (novel)">Soul Music</a></li>
    <li><a href="/wiki/Interesting_Times" title="Interesting Times">Interesting Times</a></li>
    <li><a href="/wiki/Maskerade" title="Maskerade">Maskerade</a></li>
    <li><a href="/wiki/Feet_of_Clay_(novel)" title="Feet of Clay (novel)">Feet of Clay</a></li>
    <li><a href="/wiki/Hogfather" title="Hogfather">Hogfather</a></li>
    <li><a href="/wiki/Jingo_(novel)" title="Jingo (novel)">Jingo</a></li>
    <li><a href="/wiki/The_Last_Continent" title="The Last Continent">The Last Continent</a></li>
    <li><a href="/wiki/Carpe_Jugulum" title="Carpe Jugulum">Carpe Jugulum</a></li>
    <li><a href="/wiki/The_Fifth_Elephant" title="The Fifth Elephant">The Fifth Elephant</a></li>
    <li><a href="/wiki/The_Truth_(novel)" title="The Truth (novel)">The Truth</a></li>
    <li><a href="/wiki/Thief_of_Time" title="Thief of Time">Thief of Time</a></li>
    <li><a href="/wiki/The_Last_Hero" title="The Last Hero">The Last Hero</a></li>
    <li><a href="/wiki/The_Amazing_Maurice_and_his_Educated_Rodents" class="mw-redirect" title="The Amazing Maurice and his Educated Rodents">The Amazing Maurice and his Educated Rodents</a></li>
    <li><a href="/wiki/Night_Watch_(Discworld)" title="Night Watch (Discworld)">Night Watch</a></li>
    <li><a href="/wiki/The_Wee_Free_Men" title="The Wee Free Men">The Wee Free Men</a></li>
    <li><a href="/wiki/Monstrous_Regiment_(novel)" title="Monstrous Regiment (novel)">Monstrous Regiment</a></li>
    <li><a href="/wiki/A_Hat_Full_of_Sky" title="A Hat Full of Sky">A Hat Full of Sky</a></li>
    <li><a href="/wiki/Going_Postal" title="Going Postal">Going Postal</a></li>
    <li><a href="/wiki/Thud!" title="Thud!">Thud!</a></li>
    <li><a href="/wiki/Wintersmith" title="Wintersmith">Wintersmith</a></li>
    <li><a href="/wiki/Making_Money" title="Making Money">Making Money</a></li>
    <li><a href="/wiki/Unseen_Academicals" title="Unseen Academicals">Unseen Academicals</a></li>
    <li><a href="/wiki/I_Shall_Wear_Midnight" title="I Shall Wear Midnight">I Shall Wear Midnight</a></li>
    <li><a href="/wiki/Snuff_(Pratchett_novel)" title="Snuff (Pratchett novel)">Snuff</a></li>
    <li><a href="/wiki/Raising_Steam" title="Raising Steam">Raising Steam</a></li>
    <li><a href="/wiki/The_Shepherd%27s_Crown" title="The Shepherd&#39;s Crown">The Shepherd's Crown</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Short stories</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li>"<a href="/wiki/Troll_Bridge" title="Troll Bridge">Troll Bridge</a>"</li>
    <li>"<a href="/wiki/Theatre_of_Cruelty_(Discworld)" title="Theatre of Cruelty (Discworld)">Theatre of Cruelty</a>"</li>
    <li>"<a href="/wiki/The_Sea_and_Little_Fishes" title="The Sea and Little Fishes">The Sea and Little Fishes</a>"</li>
    <li>"<a href="/wiki/Death_and_What_Comes_Next" title="Death and What Comes Next">Death and What Comes Next</a>"</li>
    <li>"<a href="/wiki/A_Collegiate_Casting-Out_of_Devilish_Devices" title="A Collegiate Casting-Out of Devilish Devices">A Collegiate Casting-Out of Devilish Devices</a>"</li>
    <li><a href="/wiki/A_Blink_of_the_Screen" title="A Blink of the Screen"><i>A Blink of the Screen</i> <span style="font-size:85%;">(anthology)</span></a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Other books</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px;font-style:italic;"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/The_Discworld_Companion" title="The Discworld Companion">The Discworld Companion</a></li>
    <li><a href="/wiki/The_Science_of_Discworld" title="The Science of Discworld">The Science of Discworld</a></li>
    <li><a href="/wiki/The_Science_of_Discworld_II:_The_Globe" title="The Science of Discworld II: The Globe">The Science of Discworld II: The Globe</a></li>
    <li><a href="/wiki/The_Science_of_Discworld_III:_Darwin%27s_Watch" title="The Science of Discworld III: Darwin&#39;s Watch">The Science of Discworld III: Darwin's Watch</a></li>
    <li><a href="/wiki/The_Science_of_Discworld_IV:_Judgement_Day" title="The Science of Discworld IV: Judgement Day">The Science of Discworld IV: Judgement Day</a></li>
    <li><a href="/wiki/The_Pratchett_Portfolio" title="The Pratchett Portfolio">The Pratchett Portfolio</a></li>
    <li><a href="/wiki/The_Art_of_Discworld" title="The Art of Discworld">The Art of Discworld</a></li>
    <li><a href="/wiki/The_Unseen_University_Challenge" title="The Unseen University Challenge">The Unseen University Challenge</a></li>
    <li><a href="/wiki/The_Unseen_University_Challenge#Sequel" title="The Unseen University Challenge">The Wyrdest Link</a></li>
    <li><a href="/wiki/The_Streets_of_Ankh-Morpork" title="The Streets of Ankh-Morpork">The Streets of Ankh-Morpork</a></li>
    <li><a href="/wiki/The_Discworld_Mapp" title="The Discworld Mapp">The Discworld Mapp</a></li>
    <li><a href="/wiki/A_Tourist_Guide_to_Lancre" title="A Tourist Guide to Lancre">A Tourist Guide to Lancre</a></li>
    <li><a href="/wiki/Death%27s_Domain" title="Death&#39;s Domain">Death's Domain</a></li>
    <li><a href="/wiki/Nanny_Ogg%27s_Cookbook" title="Nanny Ogg&#39;s Cookbook">Nanny Ogg's Cookbook</a></li>
    <li><a href="/wiki/The_Discworld_Almanak" title="The Discworld Almanak">The Discworld Almanak</a></li>
    <li><a href="/wiki/Where%27s_My_Cow%3F" title="Where&#39;s My Cow?">Where's My Cow?</a></li>
    <li><a href="/wiki/The_Unseen_University_Cut_Out_Book" title="The Unseen University Cut Out Book">The Unseen University Cut Out Book</a></li>
    <li><a href="/wiki/Discworld_Diary" title="Discworld Diary">The Discworld Diaries</a></li>
    <li><a href="/wiki/Once_More*_with_Footnotes" title="Once More* with Footnotes">Once More* with Footnotes</a></li>
    <li><a href="/wiki/Wit_and_Wisdom_of_Discworld" class="mw-redirect" title="Wit and Wisdom of Discworld">The Wit and Wisdom of Discworld</a></li>
    <li><a href="/wiki/The_Folklore_of_Discworld" class="mw-redirect" title="The Folklore of Discworld">The Folklore of Discworld</a></li>
    <li><a href="/wiki/The_World_of_Poo" title="The World of Poo">The World of Poo</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Games</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px;font-style:italic;"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/The_Colour_of_Magic_(video_game)" title="The Colour of Magic (video game)">The Colour of Magic</a></li>
    <li><a href="/wiki/Discworld_MUD" title="Discworld MUD">Discworld MUD</a></li>
    <li><a href="/wiki/Discworld_(video_game)" title="Discworld (video game)">Discworld</a></li>
    <li><a href="/wiki/Discworld_II:_Missing_Presumed...!%3F" title="Discworld II: Missing Presumed...!?">Discworld II</a></li>
    <li><a href="/wiki/GURPS_Discworld" title="GURPS Discworld">GURPS Discworld</a></li>
    <li><a href="/wiki/Discworld_Noir" title="Discworld Noir">Discworld Noir</a></li>
    <li><a href="/wiki/Discworld:_Ankh-Morpork" title="Discworld: Ankh-Morpork">Discworld: Ankh-Morpork</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Films and TV series</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px;font-style:italic;"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Welcome_to_the_Discworld" title="Welcome to the Discworld">Welcome to the Discworld</a></li>
    <li><a href="/wiki/Soul_Music_(TV_series)" title="Soul Music (TV series)">Soul Music</a></li>
    <li><a href="/wiki/Wyrd_Sisters_(TV_series)" title="Wyrd Sisters (TV series)">Wyrd Sisters</a></li>
    <li><a href="/wiki/Terry_Pratchett%27s_Hogfather" title="Terry Pratchett&#39;s Hogfather">Hogfather</a></li>
    <li><a href="/wiki/Terry_Pratchett%27s_The_Colour_of_Magic" title="Terry Pratchett&#39;s The Colour of Magic">The Colour of Magic</a></li>
    <li><a href="/wiki/Terry_Pratchett%27s_Going_Postal" title="Terry Pratchett&#39;s Going Postal">Going Postal</a></li>
    <li><a href="/wiki/The_Watch_(TV_series)" title="The Watch (TV series)">The Watch</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%"><a href="/wiki/Discworld_characters" title="Discworld characters">Characters</a></th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Tiffany_Aching" title="Tiffany Aching">Tiffany Aching</a></li>
    <li><a href="/wiki/Death_(Discworld)" title="Death (Discworld)">Death</a></li>
    <li><a href="/wiki/Hex_(Discworld)" title="Hex (Discworld)">Hex</a></li>
    <li><a href="/wiki/Moist_von_Lipwig" title="Moist von Lipwig">Moist von Lipwig</a></li>
    <li><a href="/wiki/Nanny_Ogg" title="Nanny Ogg">Nanny Ogg</a></li>
    <li><a href="/wiki/Rincewind" title="Rincewind">Rincewind</a></li>
    <li><a href="/wiki/Susan_Sto_Helit" title="Susan Sto Helit">Susan Sto Helit</a></li>
    <li><a href="/wiki/Lord_Vetinari" title="Lord Vetinari">Lord Vetinari</a></li>
    <li><a href="/wiki/Sam_Vimes" title="Sam Vimes">Sam Vimes</a></li>
    <li><a href="/wiki/Granny_Weatherwax" title="Granny Weatherwax">Granny Weatherwax</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Races and creatures</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Dwarfs_(Discworld)" title="Dwarfs (Discworld)">Dwarfs</a></li>
    <li><a href="/wiki/Elves_(Discworld)" title="Elves (Discworld)">Elves</a></li>
    <li><a href="/wiki/Discworld_gods" title="Discworld gods">Gods</a></li>
    <li><a href="/wiki/Golems_(Discworld)" title="Golems (Discworld)">Golems</a></li>
    <li><a href="/wiki/Nac_Mac_Feegle" title="Nac Mac Feegle">Nac Mac Feegle</a></li>
    <li><a href="/wiki/Troll_(Discworld)" title="Troll (Discworld)">Trolls</a></li>
    <li><a href="/wiki/Igor_(Discworld)" title="Igor (Discworld)">Igors</a></li>
    <li><a href="/wiki/Flora_and_fauna_of_the_Discworld" title="Flora and fauna of the Discworld">Flora and fauna of the Discworld</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Locations</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Discworld_(world)" title="Discworld (world)">Discworld</a></li>
    <li><a href="/wiki/Ankh-Morpork" title="Ankh-Morpork">Ankh-Morpork</a></li>
    <li><a href="/wiki/List_of_dimensions_of_the_Discworld" title="List of dimensions of the Discworld">Other dimensions</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Organisations</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Ankh-Morpork_Assassins%27_Guild" title="Ankh-Morpork Assassins&#39; Guild">Assassins' Guild</a></li>
    <li><a href="/wiki/Guilds_of_Ankh-Morpork" title="Guilds of Ankh-Morpork">Other Guilds</a></li>
    <li><a href="/wiki/Ankh-Morpork_City_Watch" title="Ankh-Morpork City Watch">City Watch</a></li>
    <li><a href="/wiki/History_Monks" title="History Monks">History Monks</a></li>
    <li><a href="/wiki/Unseen_University" title="Unseen University">Unseen University</a></li>
    <li><a href="/wiki/Witches_(Discworld)" title="Witches (Discworld)">The Witches</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Other</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Technology_of_the_Discworld" title="Technology of the Discworld">Technology of the Discworld</a></li>
    <li><a href="/wiki/Religions_of_the_Discworld" title="Religions of the Discworld">Religions of the Discworld</a></li>
    <li><a href="/wiki/Games_of_the_Discworld" title="Games of the Discworld">Games of the Discworld</a></li>
    <li><a href="/wiki/Lie-to-children" title="Lie-to-children">Lie-to-children</a></li></ul>
    </div></td></tr><tr><td class="navbox-abovebelow" colspan="2"><div>
    <ul><li><img alt="Wikipedia book" src="//upload.wikimedia.org/wikipedia/commons/thumb/8/89/Symbol_book_class2.svg/16px-Symbol_book_class2.svg.png" title="Wikipedia book" width="16" height="16" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/8/89/Symbol_book_class2.svg/23px-Symbol_book_class2.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/8/89/Symbol_book_class2.svg/31px-Symbol_book_class2.svg.png 2x" data-file-width="180" data-file-height="185" /> <a href="/wiki/Book:Discworld" title="Book:Discworld">Book</a></li>
    <li><img alt="Portal" src="//upload.wikimedia.org/wikipedia/en/thumb/f/fd/Portal-puzzle.svg/16px-Portal-puzzle.svg.png" title="Portal" width="16" height="14" srcset="//upload.wikimedia.org/wikipedia/en/thumb/f/fd/Portal-puzzle.svg/24px-Portal-puzzle.svg.png 1.5x, //upload.wikimedia.org/wikipedia/en/thumb/f/fd/Portal-puzzle.svg/32px-Portal-puzzle.svg.png 2x" data-file-width="32" data-file-height="28" /> <a href="/wiki/Portal:Discworld" title="Portal:Discworld">Portal</a></li></ul>
    </div></td></tr></tbody></table></div>
    <div role="navigation" class="navbox" aria-labelledby="Works_by_Terry_Pratchett" style="padding:3px"><table class="nowraplinks hlist collapsible autocollapse navbox-inner" style="border-spacing:0;background:transparent;color:inherit"><tbody><tr><th scope="col" class="navbox-title" colspan="2"><div class="plainlinks hlist navbar mini"><ul><li class="nv-view"><a href="/wiki/Template:Terry_Pratchett" title="Template:Terry Pratchett"><abbr title="View this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">v</abbr></a></li><li class="nv-talk"><a href="/wiki/Template_talk:Terry_Pratchett" title="Template talk:Terry Pratchett"><abbr title="Discuss this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">t</abbr></a></li><li class="nv-edit"><a class="external text" href="//en.wikipedia.org/w/index.php?title=Template:Terry_Pratchett&amp;action=edit"><abbr title="Edit this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">e</abbr></a></li></ul></div><div id="Works_by_Terry_Pratchett" style="font-size:114%;margin:0 4em">Works by <a href="/wiki/Terry_Pratchett" title="Terry Pratchett">Terry Pratchett</a></div></th></tr><tr><th scope="row" class="navbox-group" style="width:1%"><i><a href="/wiki/Discworld" title="Discworld">Discworld</a></i></th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em"></div><table class="nowraplinks navbox-subgroup" style="border-spacing:0"><tbody><tr><th scope="row" class="navbox-group" style="width:1%">Novels</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/The_Colour_of_Magic" title="The Colour of Magic">The Colour of Magic</a></i></li>
    <li><i><a href="/wiki/The_Light_Fantastic" title="The Light Fantastic">The Light Fantastic</a></i></li>
    <li><i><a href="/wiki/Equal_Rites" title="Equal Rites">Equal Rites</a></i></li>
    <li><i><a href="/wiki/Mort" title="Mort">Mort</a></i></li>
    <li><i><a href="/wiki/Sourcery" title="Sourcery">Sourcery</a></i></li>
    <li><i><a href="/wiki/Wyrd_Sisters" title="Wyrd Sisters">Wyrd Sisters</a></i></li>
    <li><i><a href="/wiki/Pyramids_(novel)" title="Pyramids (novel)">Pyramids</a></i></li>
    <li><i><a href="/wiki/Guards!_Guards!" title="Guards! Guards!">Guards! Guards!</a></i></li>
    <li><i><a href="/wiki/Eric_(novel)" title="Eric (novel)">Eric</a></i></li>
    <li><i><a href="/wiki/Moving_Pictures_(novel)" title="Moving Pictures (novel)">Moving Pictures</a></i></li>
    <li><i><a href="/wiki/Reaper_Man" title="Reaper Man">Reaper Man</a></i></li>
    <li><i><a class="mw-selflink selflink">Witches Abroad</a></i></li>
    <li><i><a href="/wiki/Small_Gods" title="Small Gods">Small Gods</a></i></li>
    <li><i><a href="/wiki/Lords_and_Ladies_(novel)" title="Lords and Ladies (novel)">Lords and Ladies</a></i></li>
    <li><i><a href="/wiki/Men_at_Arms" title="Men at Arms">Men at Arms</a></i></li>
    <li><i><a href="/wiki/Soul_Music_(novel)" title="Soul Music (novel)">Soul Music</a></i></li>
    <li><i><a href="/wiki/Interesting_Times" title="Interesting Times">Interesting Times</a></i></li>
    <li><i><a href="/wiki/Maskerade" title="Maskerade">Maskerade</a></i></li>
    <li><i><a href="/wiki/Feet_of_Clay_(novel)" title="Feet of Clay (novel)">Feet of Clay</a></i></li>
    <li><i><a href="/wiki/Hogfather" title="Hogfather">Hogfather</a></i></li>
    <li><i><a href="/wiki/Jingo_(novel)" title="Jingo (novel)">Jingo</a></i></li>
    <li><i><a href="/wiki/The_Last_Continent" title="The Last Continent">The Last Continent</a></i></li>
    <li><i><a href="/wiki/Carpe_Jugulum" title="Carpe Jugulum">Carpe Jugulum</a></i></li>
    <li><i><a href="/wiki/The_Fifth_Elephant" title="The Fifth Elephant">The Fifth Elephant</a></i></li>
    <li><i><a href="/wiki/The_Truth_(novel)" title="The Truth (novel)">The Truth</a></i></li>
    <li><i><a href="/wiki/Thief_of_Time" title="Thief of Time">Thief of Time</a></i></li>
    <li><i><a href="/wiki/The_Last_Hero" title="The Last Hero">The Last Hero</a></i></li>
    <li><i><a href="/wiki/The_Amazing_Maurice_and_his_Educated_Rodents" class="mw-redirect" title="The Amazing Maurice and his Educated Rodents">The Amazing Maurice and his Educated Rodents</a></i></li>
    <li><i><a href="/wiki/Night_Watch_(Discworld)" title="Night Watch (Discworld)">Night Watch</a></i></li>
    <li><i><a href="/wiki/The_Wee_Free_Men" title="The Wee Free Men">The Wee Free Men</a></i></li>
    <li><i><a href="/wiki/Monstrous_Regiment_(novel)" title="Monstrous Regiment (novel)">Monstrous Regiment</a></i></li>
    <li><i><a href="/wiki/A_Hat_Full_of_Sky" title="A Hat Full of Sky">A Hat Full of Sky</a></i></li>
    <li><i><a href="/wiki/Going_Postal" title="Going Postal">Going Postal</a></i></li>
    <li><i><a href="/wiki/Thud!" title="Thud!">Thud!</a></i></li>
    <li><i><a href="/wiki/Wintersmith" title="Wintersmith">Wintersmith</a></i></li>
    <li><i><a href="/wiki/Making_Money" title="Making Money">Making Money</a></i></li>
    <li><i><a href="/wiki/Unseen_Academicals" title="Unseen Academicals">Unseen Academicals</a></i></li>
    <li><i><a href="/wiki/I_Shall_Wear_Midnight" title="I Shall Wear Midnight">I Shall Wear Midnight</a></i></li>
    <li><i><a href="/wiki/Snuff_(Pratchett_novel)" title="Snuff (Pratchett novel)">Snuff</a></i></li>
    <li><i><a href="/wiki/Raising_Steam" title="Raising Steam">Raising Steam</a></i></li>
    <li><i><a href="/wiki/The_Shepherd%27s_Crown" title="The Shepherd&#39;s Crown">The Shepherd's Crown</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Short stories</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li>"<a href="/wiki/Troll_Bridge" title="Troll Bridge">Troll Bridge</a>"</li>
    <li>"<a href="/wiki/Theatre_of_Cruelty_(Discworld)" title="Theatre of Cruelty (Discworld)">Theatre of Cruelty</a>"</li>
    <li>"<a href="/wiki/The_Sea_and_Little_Fishes" title="The Sea and Little Fishes">The Sea and Little Fishes</a>"</li>
    <li>"<a href="/wiki/Death_and_What_Comes_Next" title="Death and What Comes Next">Death and What Comes Next</a>"</li>
    <li>"<a href="/wiki/A_Collegiate_Casting-Out_of_Devilish_Devices" title="A Collegiate Casting-Out of Devilish Devices">A Collegiate Casting-Out of Devilish Devices</a>"</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Mapps</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/The_Streets_of_Ankh-Morpork" title="The Streets of Ankh-Morpork">The Streets of Ankh-Morpork</a></i></li>
    <li><i><a href="/wiki/The_Discworld_Mapp" title="The Discworld Mapp">The Discworld Mapp</a></i></li>
    <li><i><a href="/wiki/A_Tourist_Guide_to_Lancre" title="A Tourist Guide to Lancre">A Tourist Guide to Lancre</a></i></li>
    <li><i><a href="/wiki/Death%27s_Domain" title="Death&#39;s Domain">Death's Domain</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Science</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/The_Science_of_Discworld" title="The Science of Discworld">The Science of Discworld</a></i>
    <ul><li><a href="/wiki/Lie-to-children" title="Lie-to-children">Lie-to-children</a></li></ul></li>
    <li><i><a href="/wiki/The_Science_of_Discworld_II:_The_Globe" title="The Science of Discworld II: The Globe">The Science of Discworld II: The Globe</a></i></li>
    <li><i><a href="/wiki/The_Science_of_Discworld_III:_Darwin%27s_Watch" title="The Science of Discworld III: Darwin&#39;s Watch">The Science of Discworld III: Darwin's Watch</a></i></li>
    <li><i><a href="/wiki/The_Science_of_Discworld_IV:_Judgement_Day" title="The Science of Discworld IV: Judgement Day">The Science of Discworld IV: Judgement Day</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Art</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/The_Pratchett_Portfolio" title="The Pratchett Portfolio">The Pratchett Portfolio</a></i></li>
    <li><i><a href="/wiki/The_Art_of_Discworld" title="The Art of Discworld">The Art of Discworld</a></i></li>
    <li><i><a href="/wiki/The_Unseen_University_Cut_Out_Book" title="The Unseen University Cut Out Book">The Unseen University Cut Out Book</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Other books</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/The_Discworld_Companion" title="The Discworld Companion">The Discworld Companion</a></i></li>
    <li><i><a href="/wiki/Nanny_Ogg%27s_Cookbook" title="Nanny Ogg&#39;s Cookbook">Nanny Ogg's Cookbook</a></i></li>
    <li><i><a href="/wiki/The_Discworld_Almanak" title="The Discworld Almanak">The Discworld Almanak</a></i></li>
    <li><i><a href="/wiki/Where%27s_My_Cow%3F" title="Where&#39;s My Cow?">Where's My Cow?</a></i></li>
    <li><i><a href="/wiki/Discworld_Diary" title="Discworld Diary">Discworld Diary</a></i></li>
    <li><i><a href="/wiki/Wit_and_Wisdom_of_Discworld" class="mw-redirect" title="Wit and Wisdom of Discworld">Wit and Wisdom of Discworld</a></i></li>
    <li><i><a href="/wiki/The_Folklore_of_Discworld" class="mw-redirect" title="The Folklore of Discworld">The Folklore of Discworld</a></i></li>
    <li><i><a href="/wiki/The_World_of_Poo" title="The World of Poo">The World of Poo</a></i></li></ul>
    </div></td></tr></tbody></table><div></div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%"><i><a href="/wiki/Johnny_Maxwell" title="Johnny Maxwell">Johnny Maxwell</a></i></th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Only_You_Can_Save_Mankind" title="Only You Can Save Mankind">Only You Can Save Mankind</a></i></li>
    <li><i><a href="/wiki/Johnny_and_the_Dead" title="Johnny and the Dead">Johnny and the Dead</a></i></li>
    <li><i><a href="/wiki/Johnny_and_the_Bomb" title="Johnny and the Bomb">Johnny and the Bomb</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%"><i><a href="/wiki/The_Long_Earth_(series)" title="The Long Earth (series)">The Long Earth</a></i></th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/The_Long_Earth" title="The Long Earth">The Long Earth</a></i></li>
    <li><i><a href="/wiki/The_Long_War_(novel)" title="The Long War (novel)">The Long War</a></i></li>
    <li><i><a href="/wiki/The_Long_Mars" title="The Long Mars">The Long Mars</a></i></li>
    <li><i><a href="/wiki/The_Long_Utopia" title="The Long Utopia">The Long Utopia</a></i></li>
    <li><i><a href="/wiki/The_Long_Cosmos" title="The Long Cosmos">The Long Cosmos</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Other novels</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/The_Carpet_People" title="The Carpet People">The Carpet People</a></i></li>
    <li><i><a href="/wiki/The_Dark_Side_of_the_Sun" title="The Dark Side of the Sun">The Dark Side of the Sun</a></i></li>
    <li><i><a href="/wiki/Strata_(novel)" title="Strata (novel)">Strata</a></i></li>
    <li><i><a href="/wiki/The_Unadulterated_Cat" title="The Unadulterated Cat">The Unadulterated Cat</a></i></li>
    <li><i><a href="/wiki/The_Nome_Trilogy" title="The Nome Trilogy">The Nome Trilogy</a></i></li>
    <li><i><a href="/wiki/Good_Omens" title="Good Omens">Good Omens</a></i></li>
    <li><i><a href="/wiki/Nation_(novel)" title="Nation (novel)">Nation</a></i></li>
    <li><i><a href="/wiki/Dodger_(novel)" title="Dodger (novel)">Dodger</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Collected shorts</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Once_More*_with_Footnotes" title="Once More* with Footnotes">Once More* with Footnotes</a></i></li>
    <li><i><a href="/wiki/A_Blink_of_the_Screen" title="A Blink of the Screen">A Blink of the Screen</a></i></li></ul>
    </div></td></tr></tbody></table></div>
    <div role="navigation" class="navbox" aria-labelledby="Cinderella_by_Charles_Perrault_and_the_Brothers_Grimm" style="padding:3px"><table class="nowraplinks collapsible autocollapse navbox-inner" style="border-spacing:0;background:transparent;color:inherit"><tbody><tr><th scope="col" class="navbox-title" colspan="2"><div class="plainlinks hlist navbar mini"><ul><li class="nv-view"><a href="/wiki/Template:Cinderella" title="Template:Cinderella"><abbr title="View this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">v</abbr></a></li><li class="nv-talk"><a href="/wiki/Template_talk:Cinderella" title="Template talk:Cinderella"><abbr title="Discuss this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">t</abbr></a></li><li class="nv-edit"><a class="external text" href="//en.wikipedia.org/w/index.php?title=Template:Cinderella&amp;action=edit"><abbr title="Edit this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">e</abbr></a></li></ul></div><div id="Cinderella_by_Charles_Perrault_and_the_Brothers_Grimm" style="font-size:114%;margin:0 4em"><i><a href="/wiki/Cinderella" title="Cinderella">Cinderella</a></i> by <a href="/wiki/Charles_Perrault" title="Charles Perrault">Charles Perrault</a> and  the <a href="/wiki/Brothers_Grimm" title="Brothers Grimm">Brothers Grimm</a></div></th></tr><tr><th scope="row" class="navbox-group" style="width:1%">Characters</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Buttons_(pantomime)" title="Buttons (pantomime)">Buttons</a></li>
    <li><a href="/wiki/Cinderella" title="Cinderella">Cinderella</a></li>
    <li><a href="/wiki/Ugly_sisters" title="Ugly sisters">Ugly sisters</a></li>
    <li><a href="/wiki/Fairy_godmother" title="Fairy godmother">Fairy godmother</a></li>
    <li><a href="/wiki/Wicked_stepmother" class="mw-redirect" title="Wicked stepmother">Wicked stepmother</a></li>
    <li><a href="/wiki/Prince_Charming" title="Prince Charming">Prince Charming</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Films</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Cinderella_(1899_film)" title="Cinderella (1899 film)">Cinderella</a></i> (1899)</li>
    <li><i><a href="/wiki/Cinderella_or_the_Glass_Slipper" title="Cinderella or the Glass Slipper">Cinderella or the Glass Slipper</a></i> (1912)</li>
    <li><i><a href="/wiki/Cinderella_(1914_film)" title="Cinderella (1914 film)">Cinderella</a></i> (1914)</li>
    <li><i><a href="/wiki/A_Lowland_Cinderella" title="A Lowland Cinderella">A Lowland Cinderella</a></i> (1921)</li>
    <li><i><a href="/wiki/A_Kiss_for_Cinderella_(film)" title="A Kiss for Cinderella (film)">A Kiss for Cinderella</a></i> (1925 film)</li>
    <li><i><a href="/wiki/Ella_Cinders_(1926_film)" class="mw-redirect" title="Ella Cinders (1926 film)">Ella Cinders</a></i> (1926)</li>
    <li><i><a href="/wiki/The_Magic_Shoes" title="The Magic Shoes">The Magic Shoes</a></i> (1935)</li>
    <li><i><a href="/wiki/First_Love_(1939_film)" title="First Love (1939 film)">First Love</a></i> (1939)</li>
    <li><i><a href="/wiki/Cinderella_(1947_film)" title="Cinderella (1947 film)">Cinderella</a></i> (1947)</li>
    <li><i><a href="/wiki/The_Glass_Slipper" title="The Glass Slipper">The Glass Slipper</a></i> (1955)</li>
    <li><i><a href="/wiki/Cinderella_(1955_film)" title="Cinderella (1955 film)">Cinderella</a></i> (1955)</li>
    <li><i><a href="/wiki/Cinderfella" title="Cinderfella">Cinderfella</a></i> (1960)</li>
    <li><i><a href="/wiki/Stop!_Look!_and_Laugh" title="Stop! Look! and Laugh">Stop! Look! and Laugh</a></i> (1960)</li>
    <li><i><a href="/wiki/More_Than_a_Miracle" title="More Than a Miracle">More Than a Miracle</a></i> (1967)</li>
    <li><i><a href="/wiki/T%C5%99i_o%C5%99%C3%AD%C5%A1ky_pro_Popelku" title="Tři oříšky pro Popelku">Tři oříšky pro Popelku</a></i> (1973)</li>
    <li><i><a href="/wiki/The_Slipper_and_the_Rose" title="The Slipper and the Rose">The Slipper and the Rose</a></i> (1976)</li>
    <li><i><a href="/wiki/Cinderella_(1979_film)" title="Cinderella (1979 film)">Cinderella</a></i> (1979)</li>
    <li><i><a href="/wiki/Cinderella_%2780" title="Cinderella &#39;80">Cinderella '80</a></i> (1984)</li>
    <li><i><a href="/wiki/Maid_to_Order" title="Maid to Order">Maid to Order</a></i> (1987)</li>
    <li><i><a href="/wiki/If_the_Shoe_Fits_(film)" title="If the Shoe Fits (film)">If the Shoe Fits</a></i> (1990)</li>
    <li><i><a href="/wiki/Ever_After" title="Ever After">Ever After</a></i> (1998)</li>
    <li><i><a href="/wiki/Ella_Enchanted_(film)" title="Ella Enchanted (film)">Ella Enchanted</a></i> (2004)</li>
    <li><i><a href="/wiki/Cinderella_(2006_film)" title="Cinderella (2006 film)">Cinderella</a></i> (2006)</li>
    <li><i><a href="/wiki/Elle:_A_Modern_Cinderella_Tale" title="Elle: A Modern Cinderella Tale">Elle: A Modern Cinderella Tale</a></i> (2010)</li>
    <li><i><a href="/wiki/Cinderella_(2015_Disney_film)" title="Cinderella (2015 Disney film)">Cinderella</a></i> (2015)</li></ul>
    </div><table class="nowraplinks navbox-subgroup" style="border-spacing:0"><tbody><tr><th scope="row" class="navbox-group" style="width:1%"><a href="/wiki/A_Cinderella_Story_(film_series)" title="A Cinderella Story (film series)"><i>A Cinderella Story</i> series</a></th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/A_Cinderella_Story" title="A Cinderella Story">A Cinderella Story</a></i> (2004)</li>
    <li><i><a href="/wiki/Another_Cinderella_Story" title="Another Cinderella Story">Another Cinderella Story</a></i> (2008)</li>
    <li><i><a href="/wiki/A_Cinderella_Story:_Once_Upon_a_Song" title="A Cinderella Story: Once Upon a Song">Once Upon a Song</a></i> (2011)</li>
    <li><i><a href="/wiki/A_Cinderella_Story:_If_the_Shoe_Fits" title="A Cinderella Story: If the Shoe Fits">If the Shoe Fits</a></i> (2016)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Animation</th><td class="navbox-list navbox-even" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Cinderella_Blues" title="Cinderella Blues">Cinderella Blues</a></i> (1931)</li>
    <li><i><a href="/wiki/Poor_Cinderella" title="Poor Cinderella">Poor Cinderella</a></i> (1934)</li>
    <li><i><a href="/wiki/Cinderella_Meets_Fella" title="Cinderella Meets Fella">Cinderella Meets Fella</a></i> (1938)</li>
    <li><i><a href="/wiki/Swing_Shift_Cinderella" title="Swing Shift Cinderella">Swing Shift Cinderella</a></i> (1945)</li>
    <li><i><a href="/wiki/Cinderella_(1950_film)" title="Cinderella (1950 film)">Cinderella</a></i> (1950)</li>
    <li><i><a href="/wiki/Se%C3%B1orella_and_the_Glass_Huarache" title="Señorella and the Glass Huarache">Señorella and the Glass Huarache</a></i> (1964)</li>
    <li><i><a href="/wiki/Cinderella_(1979_film)" title="Cinderella (1979 film)">Cinderella</a></i> (1979)</li>
    <li><i><a href="/wiki/The_Tender_Tale_of_Cinderella_Penguin" title="The Tender Tale of Cinderella Penguin">The Tender Tale of Cinderella Penguin</a></i> (1981)</li>
    <li><i><a href="/wiki/The_Magic_Riddle" title="The Magic Riddle">The Magic Riddle</a></i> (1991)</li>
    <li><i><a href="/wiki/Cinderella_(1994_film)" title="Cinderella (1994 film)">Cinderella</a></i> (1994)</li>
    <li><i><a href="/wiki/Happily_N%27Ever_After" title="Happily N&#39;Ever After">Happily N'Ever After</a></i> (2007)</li>
    <li><i><a href="/wiki/Year_of_the_Fish" title="Year of the Fish">Year of the Fish</a></i> (2008)</li>
    <li><i><a href="/wiki/Cinderella_the_Cat" title="Cinderella the Cat">Cinderella the Cat</a></i> (2017)</li>
    <li><i><a href="/wiki/Charming_(film)" title="Charming (film)">Charming</a></i> (2018)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Sequels</th><td class="navbox-list navbox-odd" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Princess_Cinderella" title="Princess Cinderella">Princess Cinderella</a></i> (1941)</li>
    <li><i><a href="/wiki/Cinderella_II:_Dreams_Come_True" title="Cinderella II: Dreams Come True">Cinderella II: Dreams Come True</a></i> (2002)</li>
    <li><i><a href="/wiki/Cinderella_III:_A_Twist_in_Time" title="Cinderella III: A Twist in Time">Cinderella III: A Twist in Time</a></i> (2007)</li></ul>
    </div></td></tr></tbody></table><div>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Television</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Hey,_Cinderella!" title="Hey, Cinderella!">Hey, Cinderella!</a></i> (1968)</li>
    <li><i><a href="/wiki/Cindy_(film)" title="Cindy (film)">Cindy</a></i> (1978)</li>
    <li><i><a href="/wiki/Cinderella_Monogatari" class="mw-redirect" title="Cinderella Monogatari">Cinderella Monogatari</a></i> (1996)</li>
    <li><i><a href="/wiki/Cinderella_(1997_film)" title="Cinderella (1997 film)">Cinderella</a></i> (1997)</li>
    <li><i><a href="/wiki/CinderElmo" title="CinderElmo">CinderElmo</a></i> (1999)</li>
    <li><i><a href="/wiki/Cinderella_(2000_film)" title="Cinderella (2000 film)">Cinderella</a></i> (2000)</li>
    <li><i><a href="/wiki/La_Cenicienta_(TV_show)" class="mw-redirect" title="La Cenicienta (TV show)">La Cenicienta</a></i> (2003)</li>
    <li><i><a href="/wiki/Bawang_Merah_Bawang_Putih_(TV_drama)" class="mw-redirect" title="Bawang Merah Bawang Putih (TV drama)">Bawang Merah Bawang Putih</a></i> (2004)</li>
    <li><i><a href="/wiki/Floricienta" title="Floricienta">Floricienta</a></i> (2004)</li>
    <li><i><a href="/wiki/Floribella#Floribella_Brazil" title="Floribella">Floribella</a></i> (2005 Brazil)</li>
    <li><i><a href="/wiki/Floribella#Portugal" title="Floribella">Floribella</a></i> (2006 Portugal)</li>
    <li><i><a href="/wiki/Grazilda" title="Grazilda">Grazilda</a></i> (2010)</li>
    <li><i><a href="/wiki/Rags_(2012_film)" title="Rags (2012 film)">Rags</a></i> (2012)</li>
    <li><i><a href="/wiki/Aik_Nayee_Cinderella" title="Aik Nayee Cinderella">Aik Nayee Cinderella</a></i> (2012)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Literary<br />adaptations</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Celestina_(novel)" title="Celestina (novel)">Celestina</a></i> (1791)</li>
    <li><i><a href="/wiki/Cinderella,_or_the_Little_Glass_Slipper" title="Cinderella, or the Little Glass Slipper">Cinderella, or the Little Glass Slipper</a></i> (1954)</li>
    <li><i><a href="/wiki/Nine_Coaches_Waiting" title="Nine Coaches Waiting">Nine Coaches Waiting</a></i> (1958)</li>
    <li><i><a href="/wiki/Carrie_(novel)" title="Carrie (novel)">Carrie</a></i> (1974)</li>
    <li><i><a href="/wiki/The_Coachman_Rat" title="The Coachman Rat">The Coachman Rat</a></i> (1989)</li>
    <li><i><a class="mw-selflink selflink">Witches Abroad</a></i> (1991)</li>
    <li><i><a href="/wiki/Ella_Enchanted" title="Ella Enchanted">Ella Enchanted</a></i> (1997)</li>
    <li><i><a href="/wiki/I_Was_a_Rat!_or_The_Scarlet_Slippers" title="I Was a Rat! or The Scarlet Slippers">I Was a Rat! or The Scarlet Slippers</a></i> (1999)</li>
    <li><i><a href="/wiki/Just_Ella" title="Just Ella">Just Ella</a></i> (1999)</li>
    <li><i><a href="/wiki/Confessions_of_an_Ugly_Stepsister" title="Confessions of an Ugly Stepsister">Confessions of an Ugly Stepsister</a></i> (1999)</li>
    <li><i><a href="/wiki/Chinese_Cinderella" title="Chinese Cinderella">Chinese Cinderella</a></i> (1999)</li>
    <li><i><a href="/wiki/The_Fairy_Godmother_(novel)" title="The Fairy Godmother (novel)">The Fairy Godmother</a></i> (2004)</li>
    <li><i><a href="/wiki/Phoenix_and_Ashes" title="Phoenix and Ashes">Phoenix and Ashes</a></i> (2004)</li>
    <li><i><a href="/wiki/Bella_at_Midnight" title="Bella at Midnight">Bella at Midnight</a></i> (2006)</li>
    <li><i><a href="/wiki/Ash_(novel)" class="mw-redirect" title="Ash (novel)">Ash</a></i> (2009)</li>
    <li><i><a href="/wiki/Princess_of_Glass" title="Princess of Glass">Princess of Glass</a></i> (2010)</li>
    <li><i><a href="/wiki/Cinder_(novel)" title="Cinder (novel)">Cinder</a></i> (2012)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Opera</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Cendrillon_(Isouard)" title="Cendrillon (Isouard)">Cendrillon</a></i> (1810 Isouard)</li>
    <li><i><a href="/wiki/La_Cenerentola" title="La Cenerentola">La Cenerentola</a></i> (1817 Rossini)</li>
    <li><i><a href="/wiki/Cendrillon" title="Cendrillon">Cendrillon</a></i> (1899 Massenet)</li>
    <li><i><a href="/wiki/Cendrillon_(Viardot)" title="Cendrillon (Viardot)">Cendrillon</a></i> (1904 Viardot)</li>
    <li><i><a href="/wiki/La_Cenicienta" title="La Cenicienta">La Cenicienta</a></i> (1966 Hen)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Ballet</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Cinderella_(Fitinhof-Schell)" title="Cinderella (Fitinhof-Schell)">Cinderella</a></i> (1893 Fitinhof-Schell)</li>
    <li><i><a href="/wiki/Aschenbr%C3%B6del" title="Aschenbrödel">Aschenbrödel</a></i> (1900 Strauss-Bayer)</li>
    <li><i><a href="/wiki/Cinderella_(Prokofiev)" title="Cinderella (Prokofiev)">Cinderella</a></i> (1945 Prokofiev)</li>
    <li><i><a href="/wiki/Cinderella_(Ashton)" title="Cinderella (Ashton)">Cinderella</a></i> (1948 Ashton)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Musicals</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Cinderella_and_the_Prince,_or_The_Castle_of_Heart%27s_Desire" title="Cinderella and the Prince, or The Castle of Heart&#39;s Desire">Cinderella and the Prince, or The Castle of Heart's Desire</a></i> (1904)</li>
    <li><i><a href="/wiki/Stubborn_Cinderella" title="Stubborn Cinderella">Stubborn Cinderella</a></i> (1909)</li>
    <li><i><a href="/wiki/Mr._Cinders" title="Mr. Cinders">Mr. Cinders</a></i> (1929)</li>
    <li><i><a href="/wiki/Cinderella_(musical)" title="Cinderella (musical)">Cinderella</a></i> (1957)</li>
    <li><i><a href="/wiki/Cindy_(musical)" title="Cindy (musical)">Cindy</a></i> (1964)</li>
    <li><i><a href="/wiki/The_Penny_Friend" title="The Penny Friend">The Penny Friend</a></i> (1966)</li>
    <li><i><a href="/wiki/The_Slipper_and_the_Rose_(musical)" title="The Slipper and the Rose (musical)">The Slipper and the Rose</a></i> (1984)</li>
    <li><i><a href="/wiki/Soho_Cinders" title="Soho Cinders">Soho Cinders</a></i> (2008)</li>
    <li><i><a href="/wiki/Cinderella_(2013_Broadway_production)" title="Cinderella (2013 Broadway production)">Cinderella</a></i> (2013)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Other</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li>Plays
    <ul><li><i><a href="/wiki/A_Kiss_for_Cinderella" title="A Kiss for Cinderella">A Kiss for Cinderella</a></i> (1916)</li></ul></li>
    <li>Comics
    <ul><li><i><a href="/wiki/Cinderella:_From_Fabletown_with_Love" title="Cinderella: From Fabletown with Love">Cinderella: From Fabletown with Love</a></i></li>
    <li><i><a href="/wiki/Cinderalla" title="Cinderalla">Cinderalla</a></i></li></ul></li>
    <li>Games
    <ul><li><i><a href="/wiki/Cinders_(visual_novel)" title="Cinders (visual novel)">Cinders</a></i></li></ul></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Songs</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li>"<a href="/wiki/Spread_a_Little_Happiness" title="Spread a Little Happiness">Spread a Little Happiness</a>" (1929)</li>
    <li>"<a href="/wiki/Bibbidi-Bobbidi-Boo" title="Bibbidi-Bobbidi-Boo">Bibbidi-Bobbidi-Boo</a>" (1949)</li>
    <li>"<a href="/wiki/A_Dream_Is_a_Wish_Your_Heart_Makes" title="A Dream Is a Wish Your Heart Makes">A Dream Is a Wish Your Heart Makes</a>" (1950)</li>
    <li>"<a href="/wiki/Cinderella_(Vince_Gill_song)" title="Cinderella (Vince Gill song)">Cinderella</a>" (1987)</li>
    <li>"<a href="/wiki/Hey_Cinderella" title="Hey Cinderella">Hey Cinderella</a>" (1993)</li>
    <li>"<a href="/wiki/It%27s_Midnight_Cinderella" title="It&#39;s Midnight Cinderella">It's Midnight Cinderella</a>" (1996)</li>
    <li>"<a href="/wiki/Cinderella_(Sweetbox_song)" title="Cinderella (Sweetbox song)">Cinderella</a>" (2001)</li>
    <li>"<a href="/wiki/Cinderella_(Shakaya_song)" title="Cinderella (Shakaya song)">Cinderella</a>" (2002)</li>
    <li>"<a href="/wiki/Cinderella_(i5_song)" title="Cinderella (i5 song)">Cinderella</a>" (2003)</li>
    <li>"<a href="/wiki/Stealing_Cinderella" title="Stealing Cinderella">Stealing Cinderella</a>" (2007)</li>
    <li>"<a href="/wiki/Cinderella_(Steven_Curtis_Chapman_song)" title="Cinderella (Steven Curtis Chapman song)">Cinderella</a>" (2007)</li>
    <li>"<a href="/wiki/C%5CC_(Cinderella%5CComplex)" title="C\C (Cinderella\Complex)">C\C (Cinderella\Complex)</a>" (2008)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Albums</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/A_Cinderella_Story:_Original_Soundtrack" title="A Cinderella Story: Original Soundtrack">A Cinderella Story</a></i> (2004 soundtrack)</li>
    <li><i><a href="/wiki/Disney%27s_Princess_Favorites" title="Disney&#39;s Princess Favorites">Disney's Princess Favorites</a></i> (2002)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Sociology</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Cinderella_complex" title="Cinderella complex">Cinderella complex</a></li>
    <li><a href="/wiki/Cinderella_effect" title="Cinderella effect">Cinderella effect</a></li>
    <li><a href="/wiki/The_Cinderella_Movement" title="The Cinderella Movement">The Cinderella Movement</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Commercials</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/A_Coach_for_Cinderella" title="A Coach for Cinderella">A Coach for Cinderella</a></i></li>
    <li><i><a href="/wiki/A_Ride_for_Cinderella" title="A Ride for Cinderella">A Ride for Cinderella</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Adult</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Cinder_Ellen_up_too_Late" title="Cinder Ellen up too Late">Cinder Ellen up too Late</a></i></li>
    <li><i><a href="/wiki/Cinderella_(1977_film)" title="Cinderella (1977 film)">Cinderella</a></i> (1977)</li>
    <li><i><a href="/wiki/Naughty_Cinderella" title="Naughty Cinderella">Naughty Cinderella</a></i></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">National<br />variation</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Bawang_Merah_Bawang_Putih" title="Bawang Merah Bawang Putih">Bawang Merah Bawang Putih</a> (Malay and Indonesian)</li>
    <li><a href="/wiki/Beauty_and_Pock_Face" title="Beauty and Pock Face">Beauty and Pock Face</a> (Chinese)</li>
    <li><a href="/wiki/Ch%C5%ABj%C5%8D-hime" title="Chūjō-hime">Chūjō-hime</a> (Japanese)</li>
    <li><a href="/wiki/Fair,_Brown_and_Trembling" title="Fair, Brown and Trembling">Fair, Brown and Trembling</a> (Irish)</li>
    <li><a href="/wiki/Finette_Cendron" title="Finette Cendron">Finette Cendron</a> (French)</li>
    <li><a href="/wiki/The_Green_Knight_(fairy_tale)" title="The Green Knight (fairy tale)">The Green Knight</a> (Danish)</li>
    <li><a href="/wiki/Katie_Woodencloak" title="Katie Woodencloak">Katie Woodencloak</a> (Norwegian)</li>
    <li><a href="/wiki/Kongji_and_Patzzi" class="mw-redirect" title="Kongji and Patzzi">Kongji and Patzzi</a> (Korean)</li>
    <li><i><a href="/wiki/Ochikubo_Monogatari" title="Ochikubo Monogatari">Ochikubo Monogatari</a></i> (Japanese)</li>
    <li>"<a href="/wiki/Rhodopis" title="Rhodopis">Rhodopis</a>" (Greek)</li>
    <li><a href="/wiki/Rushen_Coatie" title="Rushen Coatie">Rushen Coatie</a> (Scottish)</li>
    <li><a href="/wiki/The_Sharp_Grey_Sheep" title="The Sharp Grey Sheep">The Sharp Grey Sheep</a> (Scottish)</li>
    <li><a href="/wiki/The_Story_of_Tam_and_Cam" title="The Story of Tam and Cam">The Story of Tam and Cam</a> (Vietnamese)</li>
    <li><i><a href="/wiki/Sumiyoshi_Monogatari" title="Sumiyoshi Monogatari">Sumiyoshi Monogatari</a></i> (Japanese)</li>
    <li><a href="/wiki/The_True_Bride" title="The True Bride">The True Bride</a> (German)</li>
    <li><a href="/wiki/The_Wonderful_Birch" title="The Wonderful Birch">The Wonderful Birch</a> (Russian)</li>
    <li><a href="/wiki/Ye_Xian" title="Ye Xian">Ye Xian</a> (Chinese)</li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Related</th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><i><a href="/wiki/Catskin" title="Catskin">Catskin</a></i></li>
    <li><i><a href="/wiki/Into_the_Woods" title="Into the Woods">Into the Woods</a></i></li>
    <li><i><a href="/wiki/Into_the_Woods_(film)" title="Into the Woods (film)">Into the Woods</a></i> (2014 film)</li></ul>
    <ul><li><i><a href="/wiki/Politically_Correct_Bedtime_Stories" title="Politically Correct Bedtime Stories">Politically Correct Bedtime Stories</a></i></li>
    <li><a href="/wiki/List_of_Disney%27s_Cinderella_characters" title="List of Disney&#39;s Cinderella characters">Disney's characters</a></li>
    <li><i><a href="/wiki/Stop!_Look!_and_Laugh" title="Stop! Look! and Laugh">Stop! Look! and Laugh</a></i></li>
    <li><i><a href="/wiki/Waltz_Suite_(Prokofiev)" title="Waltz Suite (Prokofiev)">Waltz Suite</a></i></li>
    <li><i><a href="/wiki/Black_Cinderella_Two_Goes_East" title="Black Cinderella Two Goes East">Black Cinderella Two Goes East</a></i></li>
    <li><i><a href="/wiki/Cinderella_Monogatari" class="mw-redirect" title="Cinderella Monogatari">Cinderella Monogatari</a></i></li>
    <li><i><a href="/wiki/Cinderella%27s_Sister" class="mw-redirect" title="Cinderella&#39;s Sister">Cinderella's Sister</a></i></li>
    <li><a href="/wiki/Cinderella_(sports)" title="Cinderella (sports)">Cinderella</a> (sports)</li>
    <li><i><a href="/wiki/Lying_to_Be_Perfect" title="Lying to Be Perfect">Lying to Be Perfect</a></i></li>
    <li><i><a href="/wiki/Cinderella%27s_Eyes" title="Cinderella&#39;s Eyes">Cinderella's Eyes</a></i> (2011)</li></ul>
    </div></td></tr></tbody></table></div>
    
    <!-- 
    NewPP limit report
    Parsed by mw2179
    Cached time: 20181003142236
    Cache expiry: 1900800
    Dynamic content: false
    CPU time usage: 0.292 seconds
    Real time usage: 0.390 seconds
    Preprocessor visited node count: 1999/1000000
    Preprocessor generated node count: 0/1500000
    Post‐expand include size: 103342/2097152 bytes
    Template argument size: 2313/2097152 bytes
    Highest expansion depth: 18/40
    Expensive parser function count: 0/500
    Unstrip recursion depth: 0/20
    Unstrip post‐expand size: 2047/5000000 bytes
    Number of Wikibase entities loaded: 1/400
    Lua time usage: 0.054/10.000 seconds
    Lua memory usage: 2.65 MB/50 MB
    -->
    <!--
    Transclusion expansion time report (%,ms,calls,template)
    100.00%  244.280      1 -total
     54.46%  133.045      1 Template:Infobox_book
     44.50%  108.705      1 Template:Infobox
     22.13%   54.066      1 Template:ISBNT
     21.40%   52.287      1 Template:ISBN
     16.51%   40.331      5 Template:Navbox
     13.41%   32.746      1 Template:Catalog_lookup_link
     13.15%   32.114      2 Template:Succession_box
     10.05%   24.561      1 Template:Discworld_books
      5.52%   13.477      1 Template:Wikidata_image
    -->
    
    <!-- Saved in parser cache with key enwiki:pcache:idhash:610417-0!canonical and timestamp 20181003142235 and revision id 848046218
     -->
    </div><noscript><img src="//en.wikipedia.org/wiki/Special:CentralAutoLogin/start?type=1x1" alt="" title="" width="1" height="1" style="border: none; position: absolute;" /></noscript></div>					<div class="printfooter">
    						Retrieved from "<a dir="ltr" href="https://en.wikipedia.org/w/index.php?title=Witches_Abroad&amp;oldid=848046218">https://en.wikipedia.org/w/index.php?title=Witches_Abroad&amp;oldid=848046218</a>"					</div>
    				<div id="catlinks" class="catlinks" data-mw="interface"><div id="mw-normal-catlinks" class="mw-normal-catlinks"><a href="/wiki/Help:Category" title="Help:Category">Categories</a>: <ul><li><a href="/wiki/Category:1991_British_novels" title="Category:1991 British novels">1991 British novels</a></li><li><a href="/wiki/Category:Discworld_books" title="Category:Discworld books">Discworld books</a></li><li><a href="/wiki/Category:1991_fantasy_novels" title="Category:1991 fantasy novels">1991 fantasy novels</a></li></ul></div><div id="mw-hidden-catlinks" class="mw-hidden-catlinks mw-hidden-cats-hidden">Hidden categories: <ul><li><a href="/wiki/Category:Pages_to_import_images_to_Wikidata" title="Category:Pages to import images to Wikidata">Pages to import images to Wikidata</a></li></ul></div></div>				<div class="visualClear"></div>
    							</div>
    		</div>
    		<div id="mw-navigation">
    			<h2>Navigation menu</h2>
    			<div id="mw-head">
    									<div id="p-personal" role="navigation" class="" aria-labelledby="p-personal-label">
    						<h3 id="p-personal-label">Personal tools</h3>
    						<ul>
    							<li id="pt-anonuserpage">Not logged in</li><li id="pt-anontalk"><a href="/wiki/Special:MyTalk" title="Discussion about edits from this IP address [n]" accesskey="n">Talk</a></li><li id="pt-anoncontribs"><a href="/wiki/Special:MyContributions" title="A list of edits made from this IP address [y]" accesskey="y">Contributions</a></li><li id="pt-createaccount"><a href="/w/index.php?title=Special:CreateAccount&amp;returnto=Witches+Abroad" title="You are encouraged to create an account and log in; however, it is not mandatory">Create account</a></li><li id="pt-login"><a href="/w/index.php?title=Special:UserLogin&amp;returnto=Witches+Abroad" title="You&#039;re encouraged to log in; however, it&#039;s not mandatory. [o]" accesskey="o">Log in</a></li>						</ul>
    					</div>
    									<div id="left-navigation">
    										<div id="p-namespaces" role="navigation" class="vectorTabs" aria-labelledby="p-namespaces-label">
    						<h3 id="p-namespaces-label">Namespaces</h3>
    						<ul>
    							<li id="ca-nstab-main" class="selected"><span><a href="/wiki/Witches_Abroad" title="View the content page [c]" accesskey="c">Article</a></span></li><li id="ca-talk"><span><a href="/wiki/Talk:Witches_Abroad" rel="discussion" title="Discussion about the content page [t]" accesskey="t">Talk</a></span></li>						</ul>
    					</div>
    										<div id="p-variants" role="navigation" class="vectorMenu emptyPortlet" aria-labelledby="p-variants-label">
    												<input type="checkbox" class="vectorMenuCheckbox" aria-labelledby="p-variants-label" />
    						<h3 id="p-variants-label">
    							<span>Variants</span>
    						</h3>
    						<div class="menu">
    							<ul>
    															</ul>
    						</div>
    					</div>
    									</div>
    				<div id="right-navigation">
    										<div id="p-views" role="navigation" class="vectorTabs" aria-labelledby="p-views-label">
    						<h3 id="p-views-label">Views</h3>
    						<ul>
    							<li id="ca-view" class="collapsible selected"><span><a href="/wiki/Witches_Abroad">Read</a></span></li><li id="ca-edit" class="collapsible"><span><a href="/w/index.php?title=Witches_Abroad&amp;action=edit" title="Edit this page [e]" accesskey="e">Edit</a></span></li><li id="ca-history" class="collapsible"><span><a href="/w/index.php?title=Witches_Abroad&amp;action=history" title="Past revisions of this page [h]" accesskey="h">View history</a></span></li>						</ul>
    					</div>
    										<div id="p-cactions" role="navigation" class="vectorMenu emptyPortlet" aria-labelledby="p-cactions-label">
    						<input type="checkbox" class="vectorMenuCheckbox" aria-labelledby="p-cactions-label" />
    						<h3 id="p-cactions-label"><span>More</span></h3>
    						<div class="menu">
    							<ul>
    															</ul>
    						</div>
    					</div>
    										<div id="p-search" role="search">
    						<h3>
    							<label for="searchInput">Search</label>
    						</h3>
    						<form action="/w/index.php" id="searchform">
    							<div id="simpleSearch">
    								<input type="search" name="search" placeholder="Search Wikipedia" title="Search Wikipedia [f]" accesskey="f" id="searchInput"/><input type="hidden" value="Special:Search" name="title"/><input type="submit" name="fulltext" value="Search" title="Search Wikipedia for this text" id="mw-searchButton" class="searchButton mw-fallbackSearchButton"/><input type="submit" name="go" value="Go" title="Go to a page with this exact name if it exists" id="searchButton" class="searchButton"/>							</div>
    						</form>
    					</div>
    									</div>
    			</div>
    			<div id="mw-panel">
    				<div id="p-logo" role="banner"><a class="mw-wiki-logo" href="/wiki/Main_Page"  title="Visit the main page"></a></div>
    						<div class="portal" role="navigation" id="p-navigation" aria-labelledby="p-navigation-label">
    			<h3 id="p-navigation-label">Navigation</h3>
    			<div class="body">
    								<ul>
    					<li id="n-mainpage-description"><a href="/wiki/Main_Page" title="Visit the main page [z]" accesskey="z">Main page</a></li><li id="n-contents"><a href="/wiki/Portal:Contents" title="Guides to browsing Wikipedia">Contents</a></li><li id="n-featuredcontent"><a href="/wiki/Portal:Featured_content" title="Featured content – the best of Wikipedia">Featured content</a></li><li id="n-currentevents"><a href="/wiki/Portal:Current_events" title="Find background information on current events">Current events</a></li><li id="n-randompage"><a href="/wiki/Special:Random" title="Load a random article [x]" accesskey="x">Random article</a></li><li id="n-sitesupport"><a href="https://donate.wikimedia.org/wiki/Special:FundraiserRedirector?utm_source=donate&amp;utm_medium=sidebar&amp;utm_campaign=C13_en.wikipedia.org&amp;uselang=en" title="Support us">Donate to Wikipedia</a></li><li id="n-shoplink"><a href="//shop.wikimedia.org" title="Visit the Wikipedia store">Wikipedia store</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-interaction" aria-labelledby="p-interaction-label">
    			<h3 id="p-interaction-label">Interaction</h3>
    			<div class="body">
    								<ul>
    					<li id="n-help"><a href="/wiki/Help:Contents" title="Guidance on how to use and edit Wikipedia">Help</a></li><li id="n-aboutsite"><a href="/wiki/Wikipedia:About" title="Find out about Wikipedia">About Wikipedia</a></li><li id="n-portal"><a href="/wiki/Wikipedia:Community_portal" title="About the project, what you can do, where to find things">Community portal</a></li><li id="n-recentchanges"><a href="/wiki/Special:RecentChanges" title="A list of recent changes in the wiki [r]" accesskey="r">Recent changes</a></li><li id="n-contactpage"><a href="//en.wikipedia.org/wiki/Wikipedia:Contact_us" title="How to contact Wikipedia">Contact page</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-tb" aria-labelledby="p-tb-label">
    			<h3 id="p-tb-label">Tools</h3>
    			<div class="body">
    								<ul>
    					<li id="t-whatlinkshere"><a href="/wiki/Special:WhatLinksHere/Witches_Abroad" title="List of all English Wikipedia pages containing links to this page [j]" accesskey="j">What links here</a></li><li id="t-recentchangeslinked"><a href="/wiki/Special:RecentChangesLinked/Witches_Abroad" rel="nofollow" title="Recent changes in pages linked from this page [k]" accesskey="k">Related changes</a></li><li id="t-upload"><a href="/wiki/Wikipedia:File_Upload_Wizard" title="Upload files [u]" accesskey="u">Upload file</a></li><li id="t-specialpages"><a href="/wiki/Special:SpecialPages" title="A list of all special pages [q]" accesskey="q">Special pages</a></li><li id="t-permalink"><a href="/w/index.php?title=Witches_Abroad&amp;oldid=848046218" title="Permanent link to this revision of the page">Permanent link</a></li><li id="t-info"><a href="/w/index.php?title=Witches_Abroad&amp;action=info" title="More information about this page">Page information</a></li><li id="t-wikibase"><a href="https://www.wikidata.org/wiki/Special:EntityPage/Q1994566" title="Link to connected data repository item [g]" accesskey="g">Wikidata item</a></li><li id="t-cite"><a href="/w/index.php?title=Special:CiteThisPage&amp;page=Witches_Abroad&amp;id=848046218" title="Information on how to cite this page">Cite this page</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-coll-print_export" aria-labelledby="p-coll-print_export-label">
    			<h3 id="p-coll-print_export-label">Print/export</h3>
    			<div class="body">
    								<ul>
    					<li id="coll-create_a_book"><a href="/w/index.php?title=Special:Book&amp;bookcmd=book_creator&amp;referer=Witches+Abroad">Create a book</a></li><li id="coll-download-as-rdf2latex"><a href="/w/index.php?title=Special:ElectronPdf&amp;page=Witches+Abroad&amp;action=show-download-screen">Download as PDF</a></li><li id="t-print"><a href="/w/index.php?title=Witches_Abroad&amp;printable=yes" title="Printable version of this page [p]" accesskey="p">Printable version</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-lang" aria-labelledby="p-lang-label">
    			<h3 id="p-lang-label">Languages</h3>
    			<div class="body">
    								<ul>
    					<li class="interlanguage-link interwiki-bg"><a href="https://bg.wikipedia.org/wiki/%D0%92%D0%B5%D1%89%D0%B8%D1%86%D0%B8_%D0%B2_%D1%87%D1%83%D0%B6%D0%B1%D0%B8%D0%BD%D0%B0" title="Вещици в чужбина – Bulgarian" lang="bg" hreflang="bg" class="interlanguage-link-target">Български</a></li><li class="interlanguage-link interwiki-cs"><a href="https://cs.wikipedia.org/wiki/%C4%8Carod%C4%9Bjky_na_cest%C3%A1ch" title="Čarodějky na cestách – Czech" lang="cs" hreflang="cs" class="interlanguage-link-target">Čeština</a></li><li class="interlanguage-link interwiki-cy"><a href="https://cy.wikipedia.org/wiki/Witches_Abroad" title="Witches Abroad – Welsh" lang="cy" hreflang="cy" class="interlanguage-link-target">Cymraeg</a></li><li class="interlanguage-link interwiki-de"><a href="https://de.wikipedia.org/wiki/Total_verhext" title="Total verhext – German" lang="de" hreflang="de" class="interlanguage-link-target">Deutsch</a></li><li class="interlanguage-link interwiki-es"><a href="https://es.wikipedia.org/wiki/Brujas_de_viaje" title="Brujas de viaje – Spanish" lang="es" hreflang="es" class="interlanguage-link-target">Español</a></li><li class="interlanguage-link interwiki-fr"><a href="https://fr.wikipedia.org/wiki/M%C3%A9comptes_de_f%C3%A9es" title="Mécomptes de fées – French" lang="fr" hreflang="fr" class="interlanguage-link-target">Français</a></li><li class="interlanguage-link interwiki-it"><a href="https://it.wikipedia.org/wiki/Streghe_all%27estero" title="Streghe all&#039;estero – Italian" lang="it" hreflang="it" class="interlanguage-link-target">Italiano</a></li><li class="interlanguage-link interwiki-he"><a href="https://he.wikipedia.org/wiki/%D7%9E%D7%9B%D7%A9%D7%A4%D7%95%D7%AA_%D7%91%D7%97%D7%95%D7%A5-%D7%9C%D7%90%D7%A8%D7%A5" title="מכשפות בחוץ-לארץ – Hebrew" lang="he" hreflang="he" class="interlanguage-link-target">עברית</a></li><li class="interlanguage-link interwiki-nl"><a href="https://nl.wikipedia.org/wiki/Heksen_in_de_lucht" title="Heksen in de lucht – Dutch" lang="nl" hreflang="nl" class="interlanguage-link-target">Nederlands</a></li><li class="interlanguage-link interwiki-pl"><a href="https://pl.wikipedia.org/wiki/Wyprawa_czarownic" title="Wyprawa czarownic – Polish" lang="pl" hreflang="pl" class="interlanguage-link-target">Polski</a></li><li class="interlanguage-link interwiki-ro"><a href="https://ro.wikipedia.org/wiki/Prin_cele_str%C4%83in%C4%83t%C4%83%C8%9Bi" title="Prin cele străinătăți – Romanian" lang="ro" hreflang="ro" class="interlanguage-link-target">Română</a></li><li class="interlanguage-link interwiki-ru"><a href="https://ru.wikipedia.org/wiki/%D0%92%D0%B5%D0%B4%D1%8C%D0%BC%D1%8B_%D0%B7%D0%B0_%D0%B3%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B5%D0%B9" title="Ведьмы за границей – Russian" lang="ru" hreflang="ru" class="interlanguage-link-target">Русский</a></li><li class="interlanguage-link interwiki-sr"><a href="https://sr.wikipedia.org/wiki/%D0%92%D0%B5%D1%88%D1%82%D0%B8%D1%86%D0%B5_%D0%BD%D0%B0_%D0%BF%D1%83%D1%82%D1%83" title="Вештице на путу – Serbian" lang="sr" hreflang="sr" class="interlanguage-link-target">Српски / srpski</a></li><li class="interlanguage-link interwiki-fi"><a href="https://fi.wikipedia.org/wiki/Noitia_maisemissa" title="Noitia maisemissa – Finnish" lang="fi" hreflang="fi" class="interlanguage-link-target">Suomi</a></li>				</ul>
    				<div class="after-portlet after-portlet-lang"><span class="wb-langlinks-edit wb-langlinks-link"><a href="https://www.wikidata.org/wiki/Special:EntityPage/Q1994566#sitelinks-wikipedia" title="Edit interlanguage links" class="wbc-editpage">Edit links</a></span></div>			</div>
    		</div>
    				</div>
    		</div>
    				<div id="footer" role="contentinfo">
    						<ul id="footer-info">
    								<li id="footer-info-lastmod"> This page was last edited on 29 June 2018, at 13:06<span class="anonymous-show"> (UTC)</span>.</li>
    								<li id="footer-info-copyright">Text is available under the <a rel="license" href="//en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License">Creative Commons Attribution-ShareAlike License</a><a rel="license" href="//creativecommons.org/licenses/by-sa/3.0/" style="display:none;"></a>;
    additional terms may apply.  By using this site, you agree to the <a href="//foundation.wikimedia.org/wiki/Terms_of_Use">Terms of Use</a> and <a href="//foundation.wikimedia.org/wiki/Privacy_policy">Privacy Policy</a>. Wikipedia® is a registered trademark of the <a href="//www.wikimediafoundation.org/">Wikimedia Foundation, Inc.</a>, a non-profit organization.</li>
    							</ul>
    						<ul id="footer-places">
    								<li id="footer-places-privacy"><a href="https://foundation.wikimedia.org/wiki/Privacy_policy" class="extiw" title="wmf:Privacy policy">Privacy policy</a></li>
    								<li id="footer-places-about"><a href="/wiki/Wikipedia:About" title="Wikipedia:About">About Wikipedia</a></li>
    								<li id="footer-places-disclaimer"><a href="/wiki/Wikipedia:General_disclaimer" title="Wikipedia:General disclaimer">Disclaimers</a></li>
    								<li id="footer-places-contact"><a href="//en.wikipedia.org/wiki/Wikipedia:Contact_us">Contact Wikipedia</a></li>
    								<li id="footer-places-developers"><a href="https://www.mediawiki.org/wiki/Special:MyLanguage/How_to_contribute">Developers</a></li>
    								<li id="footer-places-cookiestatement"><a href="https://foundation.wikimedia.org/wiki/Cookie_statement">Cookie statement</a></li>
    								<li id="footer-places-mobileview"><a href="//en.m.wikipedia.org/w/index.php?title=Witches_Abroad&amp;mobileaction=toggle_view_mobile" class="noprint stopMobileRedirectToggle">Mobile view</a></li>
    							</ul>
    										<ul id="footer-icons" class="noprint">
    										<li id="footer-copyrightico">
    						<a href="https://wikimediafoundation.org/"><img src="/static/images/wikimedia-button.png" srcset="/static/images/wikimedia-button-1.5x.png 1.5x, /static/images/wikimedia-button-2x.png 2x" width="88" height="31" alt="Wikimedia Foundation"/></a>					</li>
    										<li id="footer-poweredbyico">
    						<a href="//www.mediawiki.org/"><img src="/static/images/poweredby_mediawiki_88x31.png" alt="Powered by MediaWiki" srcset="/static/images/poweredby_mediawiki_132x47.png 1.5x, /static/images/poweredby_mediawiki_176x62.png 2x" width="88" height="31"/></a>					</li>
    									</ul>
    						<div style="clear: both;"></div>
    		</div>
    		
    <script>(window.RLQ=window.RLQ||[]).push(function(){mw.config.set({"wgPageParseReport":{"limitreport":{"cputime":"0.292","walltime":"0.390","ppvisitednodes":{"value":1999,"limit":1000000},"ppgeneratednodes":{"value":0,"limit":1500000},"postexpandincludesize":{"value":103342,"limit":2097152},"templateargumentsize":{"value":2313,"limit":2097152},"expansiondepth":{"value":18,"limit":40},"expensivefunctioncount":{"value":0,"limit":500},"unstrip-depth":{"value":0,"limit":20},"unstrip-size":{"value":2047,"limit":5000000},"entityaccesscount":{"value":1,"limit":400},"timingprofile":["100.00%  244.280      1 -total"," 54.46%  133.045      1 Template:Infobox_book"," 44.50%  108.705      1 Template:Infobox"," 22.13%   54.066      1 Template:ISBNT"," 21.40%   52.287      1 Template:ISBN"," 16.51%   40.331      5 Template:Navbox"," 13.41%   32.746      1 Template:Catalog_lookup_link"," 13.15%   32.114      2 Template:Succession_box"," 10.05%   24.561      1 Template:Discworld_books","  5.52%   13.477      1 Template:Wikidata_image"]},"scribunto":{"limitreport-timeusage":{"value":"0.054","limit":"10.000"},"limitreport-memusage":{"value":2776654,"limit":52428800}},"cachereport":{"origin":"mw2179","timestamp":"20181003142236","ttl":1900800,"transientcontent":false}}});mw.config.set({"wgBackendResponseTime":487,"wgHostname":"mw2179"});});</script>
    	</body>
    </html>
    
    <class 'str'>


 Use the function **get** from the **requests** library to download the Wikipedia page using the **wikipedia_link** as an argument. Assign the object to the variable **raw_random_wikipedia_page**.

 Use the data attribute **text** to extract the XML as a text file a string and assign the result variable **page**:

# Part 3: Extracting the Title of the Article <a id='ref3'></a>  

 **Question 3 (part 1)**  Use the title of the Wikipedia article as the title of the band. The title of the article is surrounded by the XML node title as follows:  **&lt;title&gt;title - Wikipedia&lt;/title>**
. For example, if the title of the article was Python we would see the following:  **&lt;title&gt;Python - Wikipedia&lt;/title>**. Consider the example where the title of the article is Teenage Mutant Ninja Turtles the result would be:  **&lt;title&gt;Teenage Mutant Ninja Turtles - Wikipedia&lt;/title>**.  The first step is to find the XML node  **&lt;title&gt;** and **&lt;/title&gt;**indicating the start and end of the title. The string function  **find** maybe helpful, you can also use libraries like **xlxml**.


```python
import requests 
from lxml.html import fromstring
r = requests.get('https://en.wikipedia.org/wiki/Special:Random')
tree = fromstring(r.content)
band_title = tree.findtext('.//title')
band_title
```




    'La vita è - Wikipedia'



 **Question 3 (part 2)** Next get rid of the term ** - Wikipedia** from the title and assign the result to the **band_title**  For example you can use the function or method **strip** or **replace**. 



```python
band_title = band_title.strip( '- Wikipedia')
band_title
```




    'Al Noor Academy'





 **Question 4)** Repeat the second and third step, to extract the title of a second Wikipedia article but use the result to **album_title**


```python
wikipedia_link='https://en.wikipedia.org/wiki/Special:Random'
response = requests.get('https://en.wikipedia.org/wiki/Special:Random')
print (response)
```

    <Response [200]>



```python
print (response.text)
print(type(response.text))
```

    <!DOCTYPE html>
    <html class="client-nojs" lang="en" dir="ltr">
    <head>
    <meta charset="UTF-8"/>
    <title>DeLand Southwest, Florida - Wikipedia</title>
    <script>document.documentElement.className = document.documentElement.className.replace( /(^|\s)client-nojs(\s|$)/, "$1client-js$2" );</script>
    <script>(window.RLQ=window.RLQ||[]).push(function(){mw.config.set({"wgCanonicalNamespace":"","wgCanonicalSpecialPageName":false,"wgNamespaceNumber":0,"wgPageName":"DeLand_Southwest,_Florida","wgTitle":"DeLand Southwest, Florida","wgCurRevisionId":839797703,"wgRevisionId":839797703,"wgArticleId":109825,"wgIsArticle":true,"wgIsRedirect":false,"wgAction":"view","wgUserName":null,"wgUserGroups":["*"],"wgCategories":["Articles with short description","Coordinates on Wikidata","Census-designated places in Volusia County, Florida","Census-designated places in Florida"],"wgBreakFrames":false,"wgPageContentLanguage":"en","wgPageContentModel":"wikitext","wgSeparatorTransformTable":["",""],"wgDigitTransformTable":["",""],"wgDefaultDateFormat":"dmy","wgMonthNames":["","January","February","March","April","May","June","July","August","September","October","November","December"],"wgMonthNamesShort":["","Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"],"wgRelevantPageName":"DeLand_Southwest,_Florida","wgRelevantArticleId":109825,"wgRequestId":"W7Q@ggrAADIAAEVzvREAAAAA","wgCSPNonce":false,"wgIsProbablyEditable":true,"wgRelevantPageIsProbablyEditable":true,"wgRestrictionEdit":[],"wgRestrictionMove":[],"wgFlaggedRevsParams":{"tags":{}},"wgStableRevisionId":null,"wgCategoryTreePageCategoryOptions":"{\"mode\":0,\"hideprefix\":20,\"showcount\":true,\"namespaces\":false}","wgWikiEditorEnabledModules":[],"wgBetaFeaturesFeatures":[],"wgMediaViewerOnClick":true,"wgMediaViewerEnabledByDefault":true,"wgPopupsShouldSendModuleToUser":true,"wgPopupsConflictsWithNavPopupGadget":false,"wgVisualEditor":{"pageLanguageCode":"en","pageLanguageDir":"ltr","pageVariantFallbacks":"en","usePageImages":true,"usePageDescriptions":true},"wgMFExpandAllSectionsUserOption":true,"wgMFEnableFontChanger":true,"wgMFDisplayWikibaseDescriptions":{"search":true,"nearby":true,"watchlist":true,"tagline":false},"wgRelatedArticles":null,"wgRelatedArticlesUseCirrusSearch":true,"wgRelatedArticlesOnlyUseCirrusSearch":false,"wgULSCurrentAutonym":"English","wgNoticeProject":"wikipedia","wgCentralNoticeCookiesToDelete":[],"wgCentralNoticeCategoriesUsingLegacy":["Fundraising","fundraising"],"wgCoordinates":{"lat":29.009166666667,"lon":-81.309722222222},"wgWikibaseItemId":"Q2980057","wgScoreNoteLanguages":{"arabic":"العربية","catalan":"català","deutsch":"Deutsch","english":"English","espanol":"español","italiano":"italiano","nederlands":"Nederlands","norsk":"norsk","portugues":"português","suomi":"suomi","svenska":"svenska","vlaams":"West-Vlams"},"wgScoreDefaultNoteLanguage":"nederlands","wgCentralAuthMobileDomain":false,"wgCodeMirrorEnabled":true,"wgVisualEditorToolbarScrollOffset":0,"wgVisualEditorUnsupportedEditParams":["undo","undoafter","veswitched"],"wgEditSubmitButtonLabelPublish":true});mw.loader.state({"ext.gadget.charinsert-styles":"ready","ext.globalCssJs.user.styles":"ready","ext.globalCssJs.site.styles":"ready","site.styles":"ready","noscript":"ready","user.styles":"ready","ext.globalCssJs.user":"ready","ext.globalCssJs.site":"ready","user":"ready","user.options":"ready","user.tokens":"loading","ext.cite.styles":"ready","mediawiki.legacy.shared":"ready","mediawiki.legacy.commonPrint":"ready","wikibase.client.init":"ready","ext.visualEditor.desktopArticleTarget.noscript":"ready","ext.uls.interlanguage":"ready","ext.wikimediaBadges":"ready","ext.3d.styles":"ready","mediawiki.skinning.interface":"ready","skins.vector.styles":"ready"});mw.loader.implement("user.tokens@0tffind",function($,jQuery,require,module){/*@nomin*/mw.user.tokens.set({"editToken":"+\\","patrolToken":"+\\","watchToken":"+\\","csrfToken":"+\\"});
    });RLPAGEMODULES=["ext.cite.a11y","site","mediawiki.page.startup","mediawiki.user","mediawiki.page.ready","mediawiki.searchSuggest","ext.gadget.teahouse","ext.gadget.ReferenceTooltips","ext.gadget.watchlist-notice","ext.gadget.DRN-wizard","ext.gadget.charinsert","ext.gadget.refToolbar","ext.gadget.extra-toolbar-buttons","ext.gadget.switcher","ext.centralauth.centralautologin","mmv.head","mmv.bootstrap.autostart","ext.popups","ext.visualEditor.desktopArticleTarget.init","ext.visualEditor.targetLoader","ext.eventLogging.subscriber","ext.wikimediaEvents","ext.navigationTiming","ext.uls.eventlogger","ext.uls.init","ext.uls.compactlinks","ext.uls.interface","ext.3d","ext.centralNotice.geoIP","ext.centralNotice.startUp","skins.vector.js"];mw.loader.load(RLPAGEMODULES);});</script>
    <link rel="stylesheet" href="/w/load.php?debug=false&amp;lang=en&amp;modules=ext.3d.styles%7Cext.cite.styles%7Cext.uls.interlanguage%7Cext.visualEditor.desktopArticleTarget.noscript%7Cext.wikimediaBadges%7Cmediawiki.legacy.commonPrint%2Cshared%7Cmediawiki.skinning.interface%7Cskins.vector.styles%7Cwikibase.client.init&amp;only=styles&amp;skin=vector"/>
    <script async="" src="/w/load.php?debug=false&amp;lang=en&amp;modules=startup&amp;only=scripts&amp;skin=vector"></script>
    <meta name="ResourceLoaderDynamicStyles" content=""/>
    <link rel="stylesheet" href="/w/load.php?debug=false&amp;lang=en&amp;modules=ext.gadget.charinsert-styles&amp;only=styles&amp;skin=vector"/>
    <link rel="stylesheet" href="/w/load.php?debug=false&amp;lang=en&amp;modules=site.styles&amp;only=styles&amp;skin=vector"/>
    <meta name="generator" content="MediaWiki 1.32.0-wmf.23"/>
    <meta name="referrer" content="origin"/>
    <meta name="referrer" content="origin-when-crossorigin"/>
    <meta name="referrer" content="origin-when-cross-origin"/>
    <meta property="og:image" content="https://upload.wikimedia.org/wikipedia/commons/thumb/f/fe/Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg/1200px-Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg.png"/>
    <link rel="alternate" href="android-app://org.wikipedia/http/en.m.wikipedia.org/wiki/DeLand_Southwest,_Florida"/>
    <link rel="alternate" type="application/x-wiki" title="Edit this page" href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=edit"/>
    <link rel="edit" title="Edit this page" href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=edit"/>
    <link rel="apple-touch-icon" href="/static/apple-touch/wikipedia.png"/>
    <link rel="shortcut icon" href="/static/favicon/wikipedia.ico"/>
    <link rel="search" type="application/opensearchdescription+xml" href="/w/opensearch_desc.php" title="Wikipedia (en)"/>
    <link rel="EditURI" type="application/rsd+xml" href="//en.wikipedia.org/w/api.php?action=rsd"/>
    <link rel="license" href="//creativecommons.org/licenses/by-sa/3.0/"/>
    <link rel="canonical" href="https://en.wikipedia.org/wiki/DeLand_Southwest,_Florida"/>
    <link rel="dns-prefetch" href="//login.wikimedia.org"/>
    <link rel="dns-prefetch" href="//meta.wikimedia.org" />
    <!--[if lt IE 9]><script src="/w/load.php?debug=false&amp;lang=en&amp;modules=html5shiv&amp;only=scripts&amp;skin=vector&amp;sync=1"></script><![endif]-->
    </head>
    <body class="mediawiki ltr sitedir-ltr mw-hide-empty-elt ns-0 ns-subject page-DeLand_Southwest_Florida rootpage-DeLand_Southwest_Florida skin-vector action-view">		<div id="mw-page-base" class="noprint"></div>
    		<div id="mw-head-base" class="noprint"></div>
    		<div id="content" class="mw-body" role="main">
    			<a id="top"></a>
    			<div id="siteNotice" class="mw-body-content"><!-- CentralNotice --></div><div class="mw-indicators mw-body-content">
    </div>
    <h1 id="firstHeading" class="firstHeading" lang="en">DeLand Southwest, Florida</h1>			<div id="bodyContent" class="mw-body-content">
    				<div id="siteSub" class="noprint">From Wikipedia, the free encyclopedia</div>				<div id="contentSub"></div>
    				<div id="jump-to-nav"></div>				<a class="mw-jump-link" href="#mw-head">Jump to navigation</a>
    				<a class="mw-jump-link" href="#p-search">Jump to search</a>
    				<div id="mw-content-text" lang="en" dir="ltr" class="mw-content-ltr"><div class="mw-parser-output"><div class="shortdescription nomobile noexcerpt noprint searchaux" style="display:none">CDP in Florida, United States</div>
    <table class="infobox geography vcard" style="width:22em;width:23em"><tbody><tr><th colspan="2" style="text-align:center;font-size:125%;font-weight:bold;font-size:1.25em; white-space:nowrap"><span class="fn org">DeLand Southwest, Florida</span></th></tr><tr><td colspan="2" style="text-align:center;background-color:#cddeff; font-weight:bold;">
    <span class="category"><a href="/wiki/Census-designated_place" title="Census-designated place">CDP</a></span></td></tr><tr class="mergedtoprow"><td colspan="2" style="text-align:center">
    <a href="/wiki/File:Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg" class="image" title="Location in Volusia County and the state of Florida"><img alt="Location in Volusia County and the state of Florida" src="//upload.wikimedia.org/wikipedia/commons/thumb/f/fe/Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg/189px-Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg.png" width="189" height="200" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/f/fe/Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg/283px-Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/f/fe/Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg/378px-Volusia_County_Florida_Incorporated_and_Unincorporated_areas_De_Land_Southwest_Highlighted.svg.png 2x" data-file-width="850" data-file-height="900" /></a><br /><small>Location in <a href="/wiki/Volusia_County,_Florida" title="Volusia County, Florida">Volusia County</a> and the state of <a href="/wiki/Florida" title="Florida">Florida</a></small></td></tr><tr class="mergedbottomrow"><td colspan="2" style="text-align:center">
    Coordinates: <span class="plainlinks nourlexpansion"><a class="external text" href="//tools.wmflabs.org/geohack/geohack.php?pagename=DeLand_Southwest,_Florida&amp;params=29_0_33_N_81_18_35_W_region:US_type:city"><span class="geo-default"><span class="geo-dms" title="Maps, aerial photos, and other data for this location"><span class="latitude">29°0′33″N</span> <span class="longitude">81°18′35″W</span></span></span><span class="geo-multi-punct">&#xfeff; / &#xfeff;</span><span class="geo-nondefault"><span class="geo-dec" title="Maps, aerial photos, and other data for this location">29.00917°N 81.30972°W</span><span style="display:none">&#xfeff; / <span class="geo">29.00917; -81.30972</span></span></span></a></span><span style="font-size: small;"><span id="coordinates"><a href="/wiki/Geographic_coordinate_system" title="Geographic coordinate system">Coordinates</a>: <span class="plainlinks nourlexpansion"><a class="external text" href="//tools.wmflabs.org/geohack/geohack.php?pagename=DeLand_Southwest,_Florida&amp;params=29_0_33_N_81_18_35_W_region:US_type:city"><span class="geo-default"><span class="geo-dms" title="Maps, aerial photos, and other data for this location"><span class="latitude">29°0′33″N</span> <span class="longitude">81°18′35″W</span></span></span><span class="geo-multi-punct">&#xfeff; / &#xfeff;</span><span class="geo-nondefault"><span class="geo-dec" title="Maps, aerial photos, and other data for this location">29.00917°N 81.30972°W</span><span style="display:none">&#xfeff; / <span class="geo">29.00917; -81.30972</span></span></span></a></span></span></span></td></tr><tr class="mergedtoprow"><th scope="row"><a href="/wiki/List_of_sovereign_states" title="List of sovereign states">Country</a></th><td>
    <span class="flagicon"><img alt="" src="//upload.wikimedia.org/wikipedia/en/thumb/a/a4/Flag_of_the_United_States.svg/23px-Flag_of_the_United_States.svg.png" width="23" height="12" class="thumbborder" srcset="//upload.wikimedia.org/wikipedia/en/thumb/a/a4/Flag_of_the_United_States.svg/35px-Flag_of_the_United_States.svg.png 1.5x, //upload.wikimedia.org/wikipedia/en/thumb/a/a4/Flag_of_the_United_States.svg/46px-Flag_of_the_United_States.svg.png 2x" data-file-width="1235" data-file-height="650" />&#160;</span><a href="/wiki/United_States" title="United States">United States</a></td></tr><tr class="mergedrow"><th scope="row"><a href="/wiki/U.S._state" title="U.S. state">State</a></th><td>
    <span class="flagicon"><img alt="" src="//upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Flag_of_Florida.svg/23px-Flag_of_Florida.svg.png" width="23" height="15" class="thumbborder" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Flag_of_Florida.svg/35px-Flag_of_Florida.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Flag_of_Florida.svg/45px-Flag_of_Florida.svg.png 2x" data-file-width="750" data-file-height="500" />&#160;</span><a href="/wiki/Florida" title="Florida">Florida</a></td></tr><tr class="mergedrow"><th scope="row"><a href="/wiki/List_of_counties_in_Florida" title="List of counties in Florida">County</a></th><td>
    <span class="flagicon" style="padding-left:25px;">&#160;</span><a href="/wiki/Volusia_County,_Florida" title="Volusia County, Florida">Volusia</a></td></tr><tr class="mergedtoprow"><th colspan="2" style="text-align:center;text-align:left">Area<span style="font-weight:normal"></span></th></tr><tr class="mergedrow"><th scope="row">&#160;•&#160;Total</th><td>
    0.6&#160;sq&#160;mi (1.6&#160;km<sup>2</sup>)</td></tr><tr class="mergedrow"><th scope="row">&#160;•&#160;Land</th><td>
    0.6&#160;sq&#160;mi (1.6&#160;km<sup>2</sup>)</td></tr><tr class="mergedrow"><th scope="row">&#160;•&#160;Water</th><td>
    0&#160;sq&#160;mi (0&#160;km<sup>2</sup>)</td></tr><tr class="mergedtoprow"><th colspan="2" style="text-align:center;text-align:left">Population <span style="font-weight:normal">(2010)</span></th></tr><tr class="mergedrow"><th scope="row">&#160;•&#160;Total</th><td>
    1,052</td></tr><tr class="mergedtoprow"><th scope="row"><a href="/wiki/Time_zone" title="Time zone">Time zone</a></th><td>
    <a href="/wiki/UTC-5" class="mw-redirect" title="UTC-5">UTC-5</a> (<a href="/wiki/North_American_Eastern_Time_Zone" class="mw-redirect" title="North American Eastern Time Zone">Eastern (EST)</a>)</td></tr><tr class="mergedrow"><th scope="row"><span style="white-space:nowrap">&#160;•&#160;Summer (<a href="/wiki/Daylight_saving_time" title="Daylight saving time">DST</a>)</span></th><td>
    <a href="/wiki/UTC-4" class="mw-redirect" title="UTC-4">UTC-4</a> (EDT)</td></tr><tr class="mergedtoprow"><th scope="row"><a href="/wiki/Federal_Information_Processing_Standard" class="mw-redirect" title="Federal Information Processing Standard">FIPS code</a></th><td>
    12-16937<sup id="cite_ref-GR2_1-0" class="reference"><a href="#cite_note-GR2-1">&#91;1&#93;</a></sup></td></tr></tbody></table>
    <p><b>DeLand Southwest</b> is an unincorporated <a href="/wiki/Census-designated_place" title="Census-designated place">census-designated place</a> located in <a href="/wiki/Volusia_County,_Florida" title="Volusia County, Florida">Volusia County</a>, <a href="/wiki/Florida" title="Florida">Florida</a>, United States. The population was 1,052 at the 2010 census.<sup id="cite_ref-Census_2010_2-0" class="reference"><a href="#cite_note-Census_2010-2">&#91;2&#93;</a></sup>
    </p>
    <h2><span class="mw-headline" id="Geography">Geography</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=edit&amp;section=1" title="Edit section: Geography">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <p>DeLand Southwest is located at <span class="plainlinks nourlexpansion"><a class="external text" href="//tools.wmflabs.org/geohack/geohack.php?pagename=DeLand_Southwest,_Florida&amp;params=29_0_33_N_81_18_35_W_type:city"><span class="geo-default"><span class="geo-dms" title="Maps, aerial photos, and other data for this location"><span class="latitude">29°0′33″N</span> <span class="longitude">81°18′35″W</span></span></span><span class="geo-multi-punct">&#xfeff; / &#xfeff;</span><span class="geo-nondefault"><span class="geo-dec" title="Maps, aerial photos, and other data for this location">29.00917°N 81.30972°W</span><span style="display:none">&#xfeff; / <span class="geo">29.00917; -81.30972</span></span></span></a></span> (29.009037, -81.309675).<sup id="cite_ref-GR1_3-0" class="reference"><a href="#cite_note-GR1-3">&#91;3&#93;</a></sup>
    </p><p>According to the <a href="/wiki/United_States_Census_Bureau" title="United States Census Bureau">United States Census Bureau</a>, the CDP has a total area of 0.62 square miles (1.6&#160;km<sup>2</sup>), all land.
    </p>
    <h2><span class="mw-headline" id="Demographics">Demographics</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=edit&amp;section=2" title="Edit section: Demographics">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <p>As of the <a href="/wiki/Census" title="Census">census</a><sup id="cite_ref-GR2_1-1" class="reference"><a href="#cite_note-GR2-1">&#91;1&#93;</a></sup> of 2000, there were 1,169 people, 387 households, and 258 families residing in the CDP.  The <a href="/wiki/Population_density" title="Population density">population density</a> was 716.4/km² (1,862.9/mi²).  There were 459 housing units at an average density of 281.3/km² (731.4/mi²).  The racial makeup of the town was 25.15% <a href="/wiki/White_(U.S._Census)" class="mw-redirect" title="White (U.S. Census)">White</a>, 70.66% <a href="/wiki/African_American_(U.S._Census)" class="mw-redirect" title="African American (U.S. Census)">African American</a>, 0.09% <a href="/wiki/Native_American_(U.S._Census)" class="mw-redirect" title="Native American (U.S. Census)">Native American</a>, 0.43% <a href="/wiki/Asian_(U.S._Census)" class="mw-redirect" title="Asian (U.S. Census)">Asian</a>, 2.57% from <a href="/wiki/Race_(United_States_Census)" class="mw-redirect" title="Race (United States Census)">other races</a>, and 1.11% from two or more races. <a href="/wiki/Hispanic_(U.S._Census)" class="mw-redirect" title="Hispanic (U.S. Census)">Hispanic</a> or <a href="/wiki/Latino_(U.S._Census)" class="mw-redirect" title="Latino (U.S. Census)">Latino</a> of any race were 7.19% of the population.
    </p><p>There were 387 households out of which 29.5% had children under the age of 18 living with them, 33.3% were <a href="/wiki/Marriage" title="Marriage">married couples</a> living together, 30.0% had a female householder with no husband present, and 33.1% were non-families. 26.6% of all households were made up of individuals and 8.0% had someone living alone who was 65 years of age or older.  The average household size was 2.73 and the average family size was 3.32.
    </p><p>In the CDP, the population was spread out with 26.8% under the age of 18, 7.8% from 18 to 24, 23.8% from 25 to 44, 21.3% from 45 to 64, and 20.4% who were 65 years of age or older.  The median age was 38 years. For every 100 females, there were 79.0 males.  For every 100 females age 18 and over, there were 68.8 males.
    </p><p>The median income for a household in the CDP was $13,090, and the median income for a family was $18,929. Males had a median income of $17,083 versus $17,417 for females. The <a href="/wiki/Per_capita_income" title="Per capita income">per capita income</a> for the town was $8,373.  About 41.9% of families and 45.7% of the population were below the <a href="/wiki/Poverty_line" class="mw-redirect" title="Poverty line">poverty line</a>, including 50.9% of those under age 18 and 43.7% of those age 65 or over.
    </p>
    <h2><span class="mw-headline" id="References">References</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=edit&amp;section=3" title="Edit section: References">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
    <div class="reflist" style="list-style-type: decimal;">
    <div class="mw-references-wrap"><ol class="references">
    <li id="cite_note-GR2-1"><span class="mw-cite-backlink">^ <a href="#cite_ref-GR2_1-0"><sup><i><b>a</b></i></sup></a> <a href="#cite_ref-GR2_1-1"><sup><i><b>b</b></i></sup></a></span> <span class="reference-text"><cite class="citation web"><a rel="nofollow" class="external text" href="https://web.archive.org/web/20130911234518/http://factfinder2.census.gov/">"American FactFinder"</a>. <a href="/wiki/United_States_Census_Bureau" title="United States Census Bureau">United States Census Bureau</a>. Archived from <a rel="nofollow" class="external text" href="http://factfinder2.census.gov">the original</a> on 2013-09-11<span class="reference-accessdate">. Retrieved <span class="nowrap">2008-01-31</span></span>.</cite><span title="ctx_ver=Z39.88-2004&amp;rft_val_fmt=info%3Aofi%2Ffmt%3Akev%3Amtx%3Abook&amp;rft.genre=unknown&amp;rft.btitle=American+FactFinder&amp;rft.pub=United+States+Census+Bureau&amp;rft_id=http%3A%2F%2Ffactfinder2.census.gov&amp;rfr_id=info%3Asid%2Fen.wikipedia.org%3ADeLand+Southwest%2C+Florida" class="Z3988"></span><style data-mw-deduplicate="TemplateStyles:r861714446">.mw-parser-output cite.citation{font-style:inherit}.mw-parser-output q{quotes:"\"""\"""'""'"}.mw-parser-output code.cs1-code{color:inherit;background:inherit;border:inherit;padding:inherit}.mw-parser-output .cs1-lock-free a{background:url("//upload.wikimedia.org/wikipedia/commons/thumb/6/65/Lock-green.svg/9px-Lock-green.svg.png")no-repeat;background-position:right .1em center}.mw-parser-output .cs1-lock-limited a,.mw-parser-output .cs1-lock-registration a{background:url("//upload.wikimedia.org/wikipedia/commons/thumb/d/d6/Lock-gray-alt-2.svg/9px-Lock-gray-alt-2.svg.png")no-repeat;background-position:right .1em center}.mw-parser-output .cs1-lock-subscription a{background:url("//upload.wikimedia.org/wikipedia/commons/thumb/a/aa/Lock-red-alt-2.svg/9px-Lock-red-alt-2.svg.png")no-repeat;background-position:right .1em center}.mw-parser-output .cs1-subscription,.mw-parser-output .cs1-registration{color:#555}.mw-parser-output .cs1-subscription span,.mw-parser-output .cs1-registration span{border-bottom:1px dotted;cursor:help}.mw-parser-output .cs1-hidden-error{display:none;font-size:100%}.mw-parser-output .cs1-visible-error{font-size:100%}.mw-parser-output .cs1-subscription,.mw-parser-output .cs1-registration,.mw-parser-output .cs1-format{font-size:95%}.mw-parser-output .cs1-kern-left,.mw-parser-output .cs1-kern-wl-left{padding-left:0.2em}.mw-parser-output .cs1-kern-right,.mw-parser-output .cs1-kern-wl-right{padding-right:0.2em}</style></span>
    </li>
    <li id="cite_note-Census_2010-2"><span class="mw-cite-backlink"><b><a href="#cite_ref-Census_2010_2-0">^</a></b></span> <span class="reference-text"><cite class="citation web"><a rel="nofollow" class="external text" href="https://web.archive.org/web/20130911234518/http://factfinder2.census.gov/">"Profile of General Population and Housing Characteristics: 2010 Demographic Profile Data (DP-1): DeLand Southwest CDP, Florida"</a>. U.S. Census Bureau, American Factfinder. Archived from <a rel="nofollow" class="external text" href="http://factfinder2.census.gov">the original</a> on September 11, 2013<span class="reference-accessdate">. Retrieved <span class="nowrap">February 16,</span> 2012</span>.</cite><span title="ctx_ver=Z39.88-2004&amp;rft_val_fmt=info%3Aofi%2Ffmt%3Akev%3Amtx%3Abook&amp;rft.genre=unknown&amp;rft.btitle=Profile+of+General+Population+and+Housing+Characteristics%3A+2010+Demographic+Profile+Data+%28DP-1%29%3A+DeLand+Southwest+CDP%2C+Florida&amp;rft.pub=U.S.+Census+Bureau%2C+American+Factfinder&amp;rft_id=http%3A%2F%2Ffactfinder2.census.gov&amp;rfr_id=info%3Asid%2Fen.wikipedia.org%3ADeLand+Southwest%2C+Florida" class="Z3988"></span><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r861714446"/></span>
    </li>
    <li id="cite_note-GR1-3"><span class="mw-cite-backlink"><b><a href="#cite_ref-GR1_3-0">^</a></b></span> <span class="reference-text"><cite class="citation web"><a rel="nofollow" class="external text" href="https://www.census.gov/geo/www/gazetteer/gazette.html">"US Gazetteer files: 2010, 2000, and 1990"</a>. <a href="/wiki/United_States_Census_Bureau" title="United States Census Bureau">United States Census Bureau</a>. 2011-02-12<span class="reference-accessdate">. Retrieved <span class="nowrap">2011-04-23</span></span>.</cite><span title="ctx_ver=Z39.88-2004&amp;rft_val_fmt=info%3Aofi%2Ffmt%3Akev%3Amtx%3Abook&amp;rft.genre=unknown&amp;rft.btitle=US+Gazetteer+files%3A+2010%2C+2000%2C+and+1990&amp;rft.pub=United+States+Census+Bureau&amp;rft.date=2011-02-12&amp;rft_id=https%3A%2F%2Fwww.census.gov%2Fgeo%2Fwww%2Fgazetteer%2Fgazette.html&amp;rfr_id=info%3Asid%2Fen.wikipedia.org%3ADeLand+Southwest%2C+Florida" class="Z3988"></span><link rel="mw-deduplicated-inline-style" href="mw-data:TemplateStyles:r861714446"/></span>
    </li>
    </ol></div></div>
    <div role="navigation" class="navbox" aria-labelledby="Municipalities_and_communities_of_Volusia_County,_Florida,_United_States" style="padding:3px"><table class="nowraplinks collapsible autocollapse navbox-inner" style="border-spacing:0;background:transparent;color:inherit"><tbody><tr><th scope="col" class="navbox-title" colspan="3"><div class="plainlinks hlist navbar mini"><ul><li class="nv-view"><a href="/wiki/Template:Volusia_County,_Florida" title="Template:Volusia County, Florida"><abbr title="View this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">v</abbr></a></li><li class="nv-talk"><a href="/wiki/Template_talk:Volusia_County,_Florida" title="Template talk:Volusia County, Florida"><abbr title="Discuss this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">t</abbr></a></li><li class="nv-edit"><a class="external text" href="//en.wikipedia.org/w/index.php?title=Template:Volusia_County,_Florida&amp;action=edit"><abbr title="Edit this template" style=";;background:none transparent;border:none;-moz-box-shadow:none;-webkit-box-shadow:none;box-shadow:none; padding:0;">e</abbr></a></li></ul></div><div id="Municipalities_and_communities_of_Volusia_County,_Florida,_United_States" class="adr" style="font-size:114%;margin:0 4em">Municipalities and communities of <a href="/wiki/Volusia_County,_Florida" title="Volusia County, Florida"><span class="region">Volusia County, Florida</span></a>, <span class="country-name">United States</span></div></th></tr><tr><td class="navbox-abovebelow" colspan="3"><div id="County_seat:_DeLand"><a href="/wiki/County_seat" title="County seat"><span>County seat</span></a>: <b><a href="/wiki/DeLand,_Florida" title="DeLand, Florida"><span>DeLand</span></a></b></div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%"><a href="/wiki/City" title="City">Cities</a></th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Daytona_Beach,_Florida" title="Daytona Beach, Florida">Daytona Beach</a></li>
    <li><a href="/wiki/Daytona_Beach_Shores,_Florida" title="Daytona Beach Shores, Florida">Daytona Beach Shores</a></li>
    <li><a href="/wiki/DeBary,_Florida" title="DeBary, Florida">DeBary</a></li>
    <li><a href="/wiki/DeLand,_Florida" title="DeLand, Florida">DeLand</a></li>
    <li><a href="/wiki/Deltona,_Florida" title="Deltona, Florida">Deltona</a></li>
    <li><a href="/wiki/Edgewater,_Volusia_County,_Florida" title="Edgewater, Volusia County, Florida">Edgewater</a></li>
    <li><a href="/wiki/Flagler_Beach,_Florida" title="Flagler Beach, Florida">Flagler Beach</a>‡</li>
    <li><a href="/wiki/Holly_Hill,_Florida" title="Holly Hill, Florida">Holly Hill</a></li>
    <li><a href="/wiki/Lake_Helen,_Florida" title="Lake Helen, Florida">Lake Helen</a></li>
    <li><a href="/wiki/New_Smyrna_Beach,_Florida" title="New Smyrna Beach, Florida">New Smyrna Beach</a></li>
    <li><a href="/wiki/Oak_Hill,_Florida" title="Oak Hill, Florida">Oak Hill</a></li>
    <li><a href="/wiki/Orange_City,_Florida" title="Orange City, Florida">Orange City</a></li>
    <li><a href="/wiki/Ormond_Beach,_Florida" title="Ormond Beach, Florida">Ormond Beach</a></li>
    <li><a href="/wiki/Port_Orange,_Florida" title="Port Orange, Florida">Port Orange</a></li>
    <li><a href="/wiki/South_Daytona,_Florida" title="South Daytona, Florida">South Daytona</a></li></ul>
    </div></td><td class="navbox-image" rowspan="5" style="width:1px;padding:0px 0px 0px 2px"><div><div class="center"><div class="floatnone"><img alt="" src="//upload.wikimedia.org/wikipedia/commons/thumb/5/54/Map_of_Florida_highlighting_Volusia_County.svg/75px-Map_of_Florida_highlighting_Volusia_County.svg.png" width="75" height="75" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/5/54/Map_of_Florida_highlighting_Volusia_County.svg/113px-Map_of_Florida_highlighting_Volusia_County.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/5/54/Map_of_Florida_highlighting_Volusia_County.svg/150px-Map_of_Florida_highlighting_Volusia_County.svg.png 2x" data-file-width="7342" data-file-height="7321" /></div></div></div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%"><a href="/wiki/Town" title="Town">Towns</a></th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Pierson,_Florida" title="Pierson, Florida">Pierson</a></li>
    <li><a href="/wiki/Ponce_Inlet,_Florida" title="Ponce Inlet, Florida">Ponce Inlet</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%"><a href="/wiki/Census-designated_place" title="Census-designated place">CDPs</a></th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/DeLeon_Springs,_Florida" title="DeLeon Springs, Florida">DeLeon Springs</a></li>
    <li><a class="mw-selflink selflink">DeLand Southwest</a></li>
    <li><a href="/wiki/Glencoe,_Florida" title="Glencoe, Florida">Glencoe</a></li>
    <li><a href="/wiki/North_DeLand,_Florida" title="North DeLand, Florida">North DeLand</a></li>
    <li><a href="/wiki/Ormond-by-the-Sea,_Florida" title="Ormond-by-the-Sea, Florida">Ormond-by-the-Sea</a></li>
    <li><a href="/wiki/Samsula-Spruce_Creek,_Florida" title="Samsula-Spruce Creek, Florida">Samsula-Spruce Creek</a></li>
    <li><a href="/wiki/Seville,_Florida" title="Seville, Florida">Seville</a></li>
    <li><a href="/wiki/West_DeLand,_Florida" title="West DeLand, Florida">West DeLand</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%"><a href="/wiki/Unincorporated_area" title="Unincorporated area">Unincorporated<br />communities</a></th><td class="navbox-list navbox-even hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">
    <ul><li><a href="/wiki/Alamana,_Florida" title="Alamana, Florida">Alamana</a></li>
    <li><a href="/wiki/Allandale,_Florida" title="Allandale, Florida">Allandale</a></li>
    <li><a href="/wiki/Barberville,_Florida" title="Barberville, Florida">Barberville</a></li>
    <li><a href="/wiki/Bethune_Beach,_Florida" title="Bethune Beach, Florida">Bethune Beach</a></li>
    <li><a href="/wiki/Boden,_Florida" title="Boden, Florida">Boden</a></li>
    <li><a href="/wiki/Cassadaga,_Florida" title="Cassadaga, Florida">Cassadaga</a></li>
    <li><a href="/wiki/Cow_Creek,_Florida" title="Cow Creek, Florida">Cow Creek</a></li>
    <li><a href="/wiki/Creighton,_Florida" title="Creighton, Florida">Creighton</a></li>
    <li><a href="/wiki/Eldora,_Florida" title="Eldora, Florida">Eldora</a></li>
    <li><a href="/wiki/Emporia,_Florida" title="Emporia, Florida">Emporia</a></li>
    <li><a href="/wiki/Enterprise,_Florida" title="Enterprise, Florida">Enterprise</a></li>
    <li><a href="/wiki/Farmton,_Florida" title="Farmton, Florida">Farmton</a></li>
    <li><a href="/wiki/Fort_Florida,_Florida" title="Fort Florida, Florida">Fort Florida</a></li>
    <li><a href="/wiki/Glenwood,_Florida" title="Glenwood, Florida">Glenwood</a></li>
    <li><a href="/wiki/Lemon_Bluff,_Florida" title="Lemon Bluff, Florida">Lemon Bluff</a></li>
    <li><a href="/wiki/Maytown,_Florida" title="Maytown, Florida">Maytown</a></li>
    <li><a href="/wiki/Osteen,_Florida" title="Osteen, Florida">Osteen</a></li>
    <li><a href="/wiki/Pennichaw,_Florida" title="Pennichaw, Florida">Pennichaw</a></li>
    <li><a href="/wiki/Senyah,_Florida" title="Senyah, Florida">Senyah</a></li>
    <li><a href="/wiki/Volusia,_Florida" title="Volusia, Florida">Volusia</a></li>
    <li><a href="/wiki/Wilbur-by-the-Sea,_Florida" class="mw-redirect" title="Wilbur-by-the-Sea, Florida">Wilbur-by-the-Sea</a></li></ul>
    </div></td></tr><tr><th scope="row" class="navbox-group" style="width:1%">Footnotes</th><td class="navbox-list navbox-odd hlist" style="text-align:left;border-left-width:2px;border-left-style:solid;width:100%;padding:0px"><div style="padding:0em 0.25em">‡This populated place also has portions in an adjacent county or counties</div></td></tr></tbody></table></div>
    
    <!-- 
    NewPP limit report
    Parsed by mw2166
    Cached time: 20181001002031
    Cache expiry: 1900800
    Dynamic content: false
    CPU time usage: 0.340 seconds
    Real time usage: 0.435 seconds
    Preprocessor visited node count: 3525/1000000
    Preprocessor generated node count: 0/1500000
    Post‐expand include size: 51941/2097152 bytes
    Template argument size: 9210/2097152 bytes
    Highest expansion depth: 17/40
    Expensive parser function count: 0/500
    Unstrip recursion depth: 1/20
    Unstrip post‐expand size: 8223/5000000 bytes
    Number of Wikibase entities loaded: 1/400
    Lua time usage: 0.138/10.000 seconds
    Lua memory usage: 4.41 MB/50 MB
    -->
    <!--
    Transclusion expansion time report (%,ms,calls,template)
    100.00%  361.515      1 -total
     63.96%  231.224      1 Template:Infobox_settlement
     34.98%  126.469      1 Template:Infobox
     21.26%   76.854      1 Template:Reflist
     18.64%   67.392      3 Template:Cite_web
     15.56%   56.265      1 Template:Short_description
      9.77%   35.309      2 Template:Coord
      7.22%   26.089      1 Template:Convert
      6.15%   22.238      1 Template:Volusia_County,_Florida
      5.19%   18.772      1 Template:US_county_navigation_box
    -->
    
    <!-- Saved in parser cache with key enwiki:pcache:idhash:109825-0!canonical and timestamp 20181001002031 and revision id 839797703
     -->
    </div><noscript><img src="//en.wikipedia.org/wiki/Special:CentralAutoLogin/start?type=1x1" alt="" title="" width="1" height="1" style="border: none; position: absolute;" /></noscript></div>					<div class="printfooter">
    						Retrieved from "<a dir="ltr" href="https://en.wikipedia.org/w/index.php?title=DeLand_Southwest,_Florida&amp;oldid=839797703">https://en.wikipedia.org/w/index.php?title=DeLand_Southwest,_Florida&amp;oldid=839797703</a>"					</div>
    				<div id="catlinks" class="catlinks" data-mw="interface"><div id="mw-normal-catlinks" class="mw-normal-catlinks"><a href="/wiki/Help:Category" title="Help:Category">Categories</a>: <ul><li><a href="/wiki/Category:Census-designated_places_in_Volusia_County,_Florida" title="Category:Census-designated places in Volusia County, Florida">Census-designated places in Volusia County, Florida</a></li><li><a href="/wiki/Category:Census-designated_places_in_Florida" title="Category:Census-designated places in Florida">Census-designated places in Florida</a></li></ul></div><div id="mw-hidden-catlinks" class="mw-hidden-catlinks mw-hidden-cats-hidden">Hidden categories: <ul><li><a href="/wiki/Category:Articles_with_short_description" title="Category:Articles with short description">Articles with short description</a></li><li><a href="/wiki/Category:Coordinates_on_Wikidata" title="Category:Coordinates on Wikidata">Coordinates on Wikidata</a></li></ul></div></div>				<div class="visualClear"></div>
    							</div>
    		</div>
    		<div id="mw-navigation">
    			<h2>Navigation menu</h2>
    			<div id="mw-head">
    									<div id="p-personal" role="navigation" class="" aria-labelledby="p-personal-label">
    						<h3 id="p-personal-label">Personal tools</h3>
    						<ul>
    							<li id="pt-anonuserpage">Not logged in</li><li id="pt-anontalk"><a href="/wiki/Special:MyTalk" title="Discussion about edits from this IP address [n]" accesskey="n">Talk</a></li><li id="pt-anoncontribs"><a href="/wiki/Special:MyContributions" title="A list of edits made from this IP address [y]" accesskey="y">Contributions</a></li><li id="pt-createaccount"><a href="/w/index.php?title=Special:CreateAccount&amp;returnto=DeLand+Southwest%2C+Florida" title="You are encouraged to create an account and log in; however, it is not mandatory">Create account</a></li><li id="pt-login"><a href="/w/index.php?title=Special:UserLogin&amp;returnto=DeLand+Southwest%2C+Florida" title="You&#039;re encouraged to log in; however, it&#039;s not mandatory. [o]" accesskey="o">Log in</a></li>						</ul>
    					</div>
    									<div id="left-navigation">
    										<div id="p-namespaces" role="navigation" class="vectorTabs" aria-labelledby="p-namespaces-label">
    						<h3 id="p-namespaces-label">Namespaces</h3>
    						<ul>
    							<li id="ca-nstab-main" class="selected"><span><a href="/wiki/DeLand_Southwest,_Florida" title="View the content page [c]" accesskey="c">Article</a></span></li><li id="ca-talk"><span><a href="/wiki/Talk:DeLand_Southwest,_Florida" rel="discussion" title="Discussion about the content page [t]" accesskey="t">Talk</a></span></li>						</ul>
    					</div>
    										<div id="p-variants" role="navigation" class="vectorMenu emptyPortlet" aria-labelledby="p-variants-label">
    												<input type="checkbox" class="vectorMenuCheckbox" aria-labelledby="p-variants-label" />
    						<h3 id="p-variants-label">
    							<span>Variants</span>
    						</h3>
    						<div class="menu">
    							<ul>
    															</ul>
    						</div>
    					</div>
    									</div>
    				<div id="right-navigation">
    										<div id="p-views" role="navigation" class="vectorTabs" aria-labelledby="p-views-label">
    						<h3 id="p-views-label">Views</h3>
    						<ul>
    							<li id="ca-view" class="collapsible selected"><span><a href="/wiki/DeLand_Southwest,_Florida">Read</a></span></li><li id="ca-edit" class="collapsible"><span><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=edit" title="Edit this page [e]" accesskey="e">Edit</a></span></li><li id="ca-history" class="collapsible"><span><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=history" title="Past revisions of this page [h]" accesskey="h">View history</a></span></li>						</ul>
    					</div>
    										<div id="p-cactions" role="navigation" class="vectorMenu emptyPortlet" aria-labelledby="p-cactions-label">
    						<input type="checkbox" class="vectorMenuCheckbox" aria-labelledby="p-cactions-label" />
    						<h3 id="p-cactions-label"><span>More</span></h3>
    						<div class="menu">
    							<ul>
    															</ul>
    						</div>
    					</div>
    										<div id="p-search" role="search">
    						<h3>
    							<label for="searchInput">Search</label>
    						</h3>
    						<form action="/w/index.php" id="searchform">
    							<div id="simpleSearch">
    								<input type="search" name="search" placeholder="Search Wikipedia" title="Search Wikipedia [f]" accesskey="f" id="searchInput"/><input type="hidden" value="Special:Search" name="title"/><input type="submit" name="fulltext" value="Search" title="Search Wikipedia for this text" id="mw-searchButton" class="searchButton mw-fallbackSearchButton"/><input type="submit" name="go" value="Go" title="Go to a page with this exact name if it exists" id="searchButton" class="searchButton"/>							</div>
    						</form>
    					</div>
    									</div>
    			</div>
    			<div id="mw-panel">
    				<div id="p-logo" role="banner"><a class="mw-wiki-logo" href="/wiki/Main_Page"  title="Visit the main page"></a></div>
    						<div class="portal" role="navigation" id="p-navigation" aria-labelledby="p-navigation-label">
    			<h3 id="p-navigation-label">Navigation</h3>
    			<div class="body">
    								<ul>
    					<li id="n-mainpage-description"><a href="/wiki/Main_Page" title="Visit the main page [z]" accesskey="z">Main page</a></li><li id="n-contents"><a href="/wiki/Portal:Contents" title="Guides to browsing Wikipedia">Contents</a></li><li id="n-featuredcontent"><a href="/wiki/Portal:Featured_content" title="Featured content – the best of Wikipedia">Featured content</a></li><li id="n-currentevents"><a href="/wiki/Portal:Current_events" title="Find background information on current events">Current events</a></li><li id="n-randompage"><a href="/wiki/Special:Random" title="Load a random article [x]" accesskey="x">Random article</a></li><li id="n-sitesupport"><a href="https://donate.wikimedia.org/wiki/Special:FundraiserRedirector?utm_source=donate&amp;utm_medium=sidebar&amp;utm_campaign=C13_en.wikipedia.org&amp;uselang=en" title="Support us">Donate to Wikipedia</a></li><li id="n-shoplink"><a href="//shop.wikimedia.org" title="Visit the Wikipedia store">Wikipedia store</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-interaction" aria-labelledby="p-interaction-label">
    			<h3 id="p-interaction-label">Interaction</h3>
    			<div class="body">
    								<ul>
    					<li id="n-help"><a href="/wiki/Help:Contents" title="Guidance on how to use and edit Wikipedia">Help</a></li><li id="n-aboutsite"><a href="/wiki/Wikipedia:About" title="Find out about Wikipedia">About Wikipedia</a></li><li id="n-portal"><a href="/wiki/Wikipedia:Community_portal" title="About the project, what you can do, where to find things">Community portal</a></li><li id="n-recentchanges"><a href="/wiki/Special:RecentChanges" title="A list of recent changes in the wiki [r]" accesskey="r">Recent changes</a></li><li id="n-contactpage"><a href="//en.wikipedia.org/wiki/Wikipedia:Contact_us" title="How to contact Wikipedia">Contact page</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-tb" aria-labelledby="p-tb-label">
    			<h3 id="p-tb-label">Tools</h3>
    			<div class="body">
    								<ul>
    					<li id="t-whatlinkshere"><a href="/wiki/Special:WhatLinksHere/DeLand_Southwest,_Florida" title="List of all English Wikipedia pages containing links to this page [j]" accesskey="j">What links here</a></li><li id="t-recentchangeslinked"><a href="/wiki/Special:RecentChangesLinked/DeLand_Southwest,_Florida" rel="nofollow" title="Recent changes in pages linked from this page [k]" accesskey="k">Related changes</a></li><li id="t-upload"><a href="/wiki/Wikipedia:File_Upload_Wizard" title="Upload files [u]" accesskey="u">Upload file</a></li><li id="t-specialpages"><a href="/wiki/Special:SpecialPages" title="A list of all special pages [q]" accesskey="q">Special pages</a></li><li id="t-permalink"><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;oldid=839797703" title="Permanent link to this revision of the page">Permanent link</a></li><li id="t-info"><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;action=info" title="More information about this page">Page information</a></li><li id="t-wikibase"><a href="https://www.wikidata.org/wiki/Special:EntityPage/Q2980057" title="Link to connected data repository item [g]" accesskey="g">Wikidata item</a></li><li id="t-cite"><a href="/w/index.php?title=Special:CiteThisPage&amp;page=DeLand_Southwest%2C_Florida&amp;id=839797703" title="Information on how to cite this page">Cite this page</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-coll-print_export" aria-labelledby="p-coll-print_export-label">
    			<h3 id="p-coll-print_export-label">Print/export</h3>
    			<div class="body">
    								<ul>
    					<li id="coll-create_a_book"><a href="/w/index.php?title=Special:Book&amp;bookcmd=book_creator&amp;referer=DeLand+Southwest%2C+Florida">Create a book</a></li><li id="coll-download-as-rdf2latex"><a href="/w/index.php?title=Special:ElectronPdf&amp;page=DeLand+Southwest%2C+Florida&amp;action=show-download-screen">Download as PDF</a></li><li id="t-print"><a href="/w/index.php?title=DeLand_Southwest,_Florida&amp;printable=yes" title="Printable version of this page [p]" accesskey="p">Printable version</a></li>				</ul>
    							</div>
    		</div>
    			<div class="portal" role="navigation" id="p-lang" aria-labelledby="p-lang-label">
    			<h3 id="p-lang-label">Languages</h3>
    			<div class="body">
    								<ul>
    					<li class="interlanguage-link interwiki-zh-min-nan"><a href="https://zh-min-nan.wikipedia.org/wiki/De_Land_Southwest_(Florida)" title="De Land Southwest (Florida) – Chinese (Min Nan)" lang="zh-min-nan" hreflang="zh-min-nan" class="interlanguage-link-target">Bân-lâm-gú</a></li><li class="interlanguage-link interwiki-ceb"><a href="https://ceb.wikipedia.org/wiki/De_Land_Southwest" title="De Land Southwest – Cebuano" lang="ceb" hreflang="ceb" class="interlanguage-link-target">Cebuano</a></li><li class="interlanguage-link interwiki-de"><a href="https://de.wikipedia.org/wiki/DeLand_Southwest" title="DeLand Southwest – German" lang="de" hreflang="de" class="interlanguage-link-target">Deutsch</a></li><li class="interlanguage-link interwiki-es"><a href="https://es.wikipedia.org/wiki/DeLand_Southwest" title="DeLand Southwest – Spanish" lang="es" hreflang="es" class="interlanguage-link-target">Español</a></li><li class="interlanguage-link interwiki-fa"><a href="https://fa.wikipedia.org/wiki/%D8%AF%DB%8C%D9%84%D9%86%D8%AF_%D8%B3%D8%A7%D9%88%D8%AA%D9%88%D8%B3%D8%AA%D8%8C_%D9%81%D9%84%D9%88%D8%B1%DB%8C%D8%AF%D8%A7" title="دیلند ساوتوست، فلوریدا – Persian" lang="fa" hreflang="fa" class="interlanguage-link-target">فارسی</a></li><li class="interlanguage-link interwiki-it"><a href="https://it.wikipedia.org/wiki/DeLand_Southwest" title="DeLand Southwest – Italian" lang="it" hreflang="it" class="interlanguage-link-target">Italiano</a></li><li class="interlanguage-link interwiki-nl"><a href="https://nl.wikipedia.org/wiki/De_Land_Southwest" title="De Land Southwest – Dutch" lang="nl" hreflang="nl" class="interlanguage-link-target">Nederlands</a></li><li class="interlanguage-link interwiki-new"><a href="https://new.wikipedia.org/wiki/%E0%A4%A1%E0%A5%87_%E0%A4%B2%E0%A5%8D%E0%A4%AF%E0%A4%BE%E0%A4%82%E0%A4%A1_%E0%A4%B8%E0%A4%BE%E0%A4%89%E0%A4%A5%E0%A4%B5%E0%A5%87%E0%A4%B8%E0%A5%8D%E0%A4%9F,_%E0%A4%AB%E0%A5%8D%E0%A4%B2%E0%A5%8B%E0%A4%B0%E0%A4%BF%E0%A4%A1%E0%A4%BE" title="डे ल्यांड साउथवेस्ट, फ्लोरिडा – Newari" lang="new" hreflang="new" class="interlanguage-link-target">नेपाल भाषा</a></li><li class="interlanguage-link interwiki-uz"><a href="https://uz.wikipedia.org/wiki/De_Land_Southwest" title="De Land Southwest – Uzbek" lang="uz" hreflang="uz" class="interlanguage-link-target">Oʻzbekcha/ўзбекча</a></li><li class="interlanguage-link interwiki-pl"><a href="https://pl.wikipedia.org/wiki/DeLand_Southwest" title="DeLand Southwest – Polish" lang="pl" hreflang="pl" class="interlanguage-link-target">Polski</a></li><li class="interlanguage-link interwiki-pt"><a href="https://pt.wikipedia.org/wiki/De_Land_Southwest" title="De Land Southwest – Portuguese" lang="pt" hreflang="pt" class="interlanguage-link-target">Português</a></li><li class="interlanguage-link interwiki-ru"><a href="https://ru.wikipedia.org/wiki/%D0%94%D0%B5-%D0%9B%D0%B5%D0%BD%D0%B4-%D0%A1%D0%B0%D1%83%D1%82%D1%83%D1%8D%D1%81%D1%82_(%D0%A4%D0%BB%D0%BE%D1%80%D0%B8%D0%B4%D0%B0)" title="Де-Ленд-Саутуэст (Флорида) – Russian" lang="ru" hreflang="ru" class="interlanguage-link-target">Русский</a></li><li class="interlanguage-link interwiki-sr"><a href="https://sr.wikipedia.org/wiki/%D0%94%D0%B5%D0%BB%D0%B0%D0%BD%D0%B4_%D0%A1%D0%BE%D1%83%D1%82%D0%B2%D0%B5%D1%81%D1%82_(%D0%A4%D0%BB%D0%BE%D1%80%D0%B8%D0%B4%D0%B0)" title="Деланд Соутвест (Флорида) – Serbian" lang="sr" hreflang="sr" class="interlanguage-link-target">Српски / srpski</a></li><li class="interlanguage-link interwiki-sh"><a href="https://sh.wikipedia.org/wiki/DeLand_Southwest,_Florida" title="DeLand Southwest, Florida – Serbo-Croatian" lang="sh" hreflang="sh" class="interlanguage-link-target">Srpskohrvatski / српскохрватски</a></li>				</ul>
    				<div class="after-portlet after-portlet-lang"><span class="wb-langlinks-edit wb-langlinks-link"><a href="https://www.wikidata.org/wiki/Special:EntityPage/Q2980057#sitelinks-wikipedia" title="Edit interlanguage links" class="wbc-editpage">Edit links</a></span></div>			</div>
    		</div>
    				</div>
    		</div>
    				<div id="footer" role="contentinfo">
    						<ul id="footer-info">
    								<li id="footer-info-lastmod"> This page was last edited on 5 May 2018, at 18:54<span class="anonymous-show"> (UTC)</span>.</li>
    								<li id="footer-info-copyright">Text is available under the <a rel="license" href="//en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License">Creative Commons Attribution-ShareAlike License</a><a rel="license" href="//creativecommons.org/licenses/by-sa/3.0/" style="display:none;"></a>;
    additional terms may apply.  By using this site, you agree to the <a href="//foundation.wikimedia.org/wiki/Terms_of_Use">Terms of Use</a> and <a href="//foundation.wikimedia.org/wiki/Privacy_policy">Privacy Policy</a>. Wikipedia® is a registered trademark of the <a href="//www.wikimediafoundation.org/">Wikimedia Foundation, Inc.</a>, a non-profit organization.</li>
    							</ul>
    						<ul id="footer-places">
    								<li id="footer-places-privacy"><a href="https://foundation.wikimedia.org/wiki/Privacy_policy" class="extiw" title="wmf:Privacy policy">Privacy policy</a></li>
    								<li id="footer-places-about"><a href="/wiki/Wikipedia:About" title="Wikipedia:About">About Wikipedia</a></li>
    								<li id="footer-places-disclaimer"><a href="/wiki/Wikipedia:General_disclaimer" title="Wikipedia:General disclaimer">Disclaimers</a></li>
    								<li id="footer-places-contact"><a href="//en.wikipedia.org/wiki/Wikipedia:Contact_us">Contact Wikipedia</a></li>
    								<li id="footer-places-developers"><a href="https://www.mediawiki.org/wiki/Special:MyLanguage/How_to_contribute">Developers</a></li>
    								<li id="footer-places-cookiestatement"><a href="https://foundation.wikimedia.org/wiki/Cookie_statement">Cookie statement</a></li>
    								<li id="footer-places-mobileview"><a href="//en.m.wikipedia.org/w/index.php?title=DeLand_Southwest,_Florida&amp;mobileaction=toggle_view_mobile" class="noprint stopMobileRedirectToggle">Mobile view</a></li>
    							</ul>
    										<ul id="footer-icons" class="noprint">
    										<li id="footer-copyrightico">
    						<a href="https://wikimediafoundation.org/"><img src="/static/images/wikimedia-button.png" srcset="/static/images/wikimedia-button-1.5x.png 1.5x, /static/images/wikimedia-button-2x.png 2x" width="88" height="31" alt="Wikimedia Foundation"/></a>					</li>
    										<li id="footer-poweredbyico">
    						<a href="//www.mediawiki.org/"><img src="/static/images/poweredby_mediawiki_88x31.png" alt="Powered by MediaWiki" srcset="/static/images/poweredby_mediawiki_132x47.png 1.5x, /static/images/poweredby_mediawiki_176x62.png 2x" width="88" height="31"/></a>					</li>
    									</ul>
    						<div style="clear: both;"></div>
    		</div>
    		
    <script>(window.RLQ=window.RLQ||[]).push(function(){mw.config.set({"wgPageParseReport":{"limitreport":{"cputime":"0.340","walltime":"0.435","ppvisitednodes":{"value":3525,"limit":1000000},"ppgeneratednodes":{"value":0,"limit":1500000},"postexpandincludesize":{"value":51941,"limit":2097152},"templateargumentsize":{"value":9210,"limit":2097152},"expansiondepth":{"value":17,"limit":40},"expensivefunctioncount":{"value":0,"limit":500},"unstrip-depth":{"value":1,"limit":20},"unstrip-size":{"value":8223,"limit":5000000},"entityaccesscount":{"value":1,"limit":400},"timingprofile":["100.00%  361.515      1 -total"," 63.96%  231.224      1 Template:Infobox_settlement"," 34.98%  126.469      1 Template:Infobox"," 21.26%   76.854      1 Template:Reflist"," 18.64%   67.392      3 Template:Cite_web"," 15.56%   56.265      1 Template:Short_description","  9.77%   35.309      2 Template:Coord","  7.22%   26.089      1 Template:Convert","  6.15%   22.238      1 Template:Volusia_County,_Florida","  5.19%   18.772      1 Template:US_county_navigation_box"]},"scribunto":{"limitreport-timeusage":{"value":"0.138","limit":"10.000"},"limitreport-memusage":{"value":4626454,"limit":52428800}},"cachereport":{"origin":"mw2166","timestamp":"20181001002031","ttl":1900800,"transientcontent":false}}});mw.config.set({"wgBackendResponseTime":84,"wgHostname":"mw2225"});});</script>
    	</body>
    </html>
    
    <class 'str'>



```python
import requests 
from lxml.html import fromstring
r = requests.get('https://en.wikipedia.org/wiki/Special:Random')
tree = fromstring(r.content)
album_title = tree.findtext('.//title')
album_title
```




    'St. Vincent of Paul Catholic Church - Wikipedia'




```python
album_title = album_title.strip( '- Wikipedia')
album_title
```




    'St. Vincent of Paul Catholic Church'



 If you did everything correct the following cell should display the album and band name:



```python
print("Your band: ", band_title)
print("Your album: ", album_title)
```

    Your band:  Al Noor Academy
    Your album:  St. Vincent of Paul Catholic Church


## Part 4: Displaying the Album Cover  <a id='ref4'></a>

 Use the function **display_cover** to superimpose the band and album title over a random image, assign the result to the variable **album_cover **.

**Question 5)** use the function display_cover  to display the album cover with two random article titles representing the name of the band and the title of the album.


```python
from IPython.display import Image as IPythonImage
from PIL import Image
from PIL import ImageFont
from PIL import ImageDraw
```


```python
def display_cover(top,bottom ):
    """This fucntoin
    """
    import requests
    
    name='album_art_raw.png'
    # Now let's make get an album cover.
    # https://picsum.photos/ is a free service that offers random images.
    # Let's get a random image:
    album_art_raw = requests.get('https://picsum.photos/500/500/?random')
    # and save it as 'album_art_raw.png'
    with open(name,'wb') as album_art_raw_file:
       album_art_raw_file.write(album_art_raw.content)
    # Now that we have our raw image, let's open it 
    # and write our band and album name on it
    img = Image.open("album_art_raw.png")
    draw = ImageDraw.Draw(img)

    # We'll choose a font for our band and album title, 
    # run "% ls /usr/share/fonts/truetype/dejavu" in a cell to see what else is available,
    # or download your own .ttf fonts!
    band_name_font = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf", 25) #25pt font
    album_name_font = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf", 20) # 20pt font

    # the x,y coordinates for where our album name and band name text will start
    # counted from the top left of the picture (in pixels)
    band_x, band_y = 50, 50
    album_x, album_y = 50, 400

    # Our text should be visible on any image. A good way
    # of accomplishing that is to use white text with a 
    # black border. We'll use the technique shown here to draw the border:
    # https://mail.python.org/pipermail/image-sig/2009-May/005681.html
    outline_color ="black"

    draw.text((band_x-1, band_y-1), top, font=band_name_font, fill=outline_color)
    draw.text((band_x+1, band_y-1), top, font=band_name_font, fill=outline_color)
    draw.text((band_x-1, band_y+1), top, font=band_name_font, fill=outline_color)
    draw.text((band_x+1, band_y+1), top, font=band_name_font, fill=outline_color)

    draw.text((album_x-1, album_y-1), bottom , font=album_name_font, fill=outline_color)
    draw.text((album_x+1, album_y-1), bottom , font=album_name_font, fill=outline_color)
    draw.text((album_x-1, album_y+1), bottom , font=album_name_font, fill=outline_color)
    draw.text((album_x+1, album_y+1), bottom , font=album_name_font, fill=outline_color)

    draw.text((band_x,band_y),top,(255,255,255),font=band_name_font)
    draw.text((album_x, album_y),bottom,(255,255,255),font=album_name_font)

    return img
```

 Use the method save to save the image as **sample-out.png**:


```python
img=display_cover(top='Your band:  Al Noor Academy',bottom='Your album:  St. Vincent of Paul Catholic Church')
img.save('sample-out.png')
```

Use the function **IPythonImage** to display the image 



```python
IPythonImage(filename='sample-out.png')
```




![png](output_46_0.png)



### About the Authors:  
 [James Reeve]( https://www.linkedin.com/in/reevejamesd/) James Reeves is a Software Engineering intern at IBM.



 [Joseph Santarcangelo]( https://www.linkedin.com/in/joseph-s-50398b136/) has a PhD in Electrical Engineering, his research focused on using machine learning, signal processing, and computer vision to determine how videos impact human cognition. Joseph has been working for IBM since he completed his PhD.
 

 <hr>
Copyright &copy; 2018 [cognitiveclass.ai](cognitiveclass.ai?utm_source=bducopyrightlink&utm_medium=dswb&utm_campaign=bdu). This notebook and its source code are released under the terms of the [MIT License](https://bigdatauniversity.com/mit-license/).
