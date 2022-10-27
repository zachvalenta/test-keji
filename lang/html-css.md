# TODO

## 参考

🗄
* `js.md`
* `python.md` HTML

## current

## queue

https://www.jefftk.com/p/designing-low-upkeep-software
- [ ] header/footer https://www.erichgrunewald.com/
- [ ] audio https://mally.stanford.edu/index.html
```text
toc https://adtax.paulromer.net/
img https://www.artic.edu/collection https://www.moma.org/collection/ https://labs.openai.com/
sections (code, music notation)
footnotes https://stackoverflow.com/a/29384216/6813490 https://twobithistory.org/2018/08/18/ada-lovelace-note-g.html
```
- [ ] search
- [ ] notification: RSS https://github.com/jeffkaufman/webscripts/blob/e7261e894cee12df6b1f0a90d426764a802691dd/reverserss.py#L20
- [ ] notification: email
- [ ] rf current reviews
- [ ] comments: Twitter, Hacker News https://www.jefftk.com/p/designing-low-upkeep-software
> Folks wanted to talk about stuff where they already were, rather than centralizing that conversation on individual blogs. https://news.ycombinator.com/item?id=30853711

## done

* _22_: rf fs, try Pelican, redesign
* _20_: MkDocs
* _19_: water.css
* _17_: CSS selectors for UI testing
* _15_: struggle with positioning and assume I'll never be a developer

# CSS

📜 https://css-tricks.com/guides/ https://cssreference.io/ https://css.30secondsofcode.org https://cssbuilder.veliovgroup.com/ https://cssfordesigners.com/articles/things-i-wish-id-known-about-css https://web.dev/learn/css/
📙 https://wizardzines.com/zines/css/
🗄 `js.md` browser

> I don’t personally use Macs but I think everyone in B2C software needs to take lessons from Apple and the Mac community. They have proven, again and again, that people will pay a premium for products which are attractive. Often in B2C the first glimpse of the software makes the sale and everything after that is just justifying to the customer that their gut decision was the right one. https://www.kalzumeus.com/2009/03/07/how-to-successfully-compete-with-open-source-software/

howto
* link stylesheet `<link rel="stylesheet" style="text/css" href="../CSS/file.css">` https://stackoverflow.com/a/43947639
* charts https://chartscss.org/ https://uglyduck.ca/flexbox-bar-graphs/
* checklist https://drewdevault.com/new-server
* columns https://www.youtube.com/watch?v=hiIlFz8UN8Q
* dropdown https://uglyduck.ca/stripe-menu-css/
* tables https://uglyduck.ca/responsive-tables/

variables
* aka 'custom properties' https://developer.mozilla.org/en-US/docs/Web/CSS/--*
* https://www.youtube.com/watch?v=lgaxU7CRmxU
* how to https://uglyduck.ca/css-variables/ https://www.youtube.com/playlist?list=PL4cUxeGkcC9ii5PB2UMyYH7QFZWfGnVgZ
```css
:root {
    --base-color: #e0e0e0;
}

.header {
    border: 1px solid var(--base-color);
}
```

---

* aspect-ratio https://news.ycombinator.com/item?id=30280210&utm_term=comment
* blocks https://thesephist.github.io/blocks.css/
* _animation_: https://animejs.com/ https://fluca1978.github.io/2020/01/30/PostgreSQL_pgcatcheck.html https://www.youtube.com/watch?v=0-DY8J_skZ0 https://roughnotation.com/ https://jvns.ca/blog/2020/06/19/a-little-bit-of-plain-javascript-can-do-a-lot/
* _CSS-in-JS_: exactly what it sounds like; more composable, apparently https://frontarm.com/james-k-nelson/css-in-js-static-rendering/
* _debug_: https://github.com/lucagez/Debucsser https://www.youtube.com/watch?v=Sp9ZfSvpf7A
* _feature detection_: `@supports` https://www.youtube.com/watch?v=QG8Zv_doPOM 4:45
* _history_: https://www.w3.org/Style/CSS20/history.html https://eev.ee/blog/2020/02/01/old-css-new-css/ https://news.ycombinator.com/item?id=23915263
* _image_: trim off part to create polygon `clip-path` [6:00] masks [7:00] https://www.youtube.com/watch?v=QG8Zv_doPOM lazy loading https://victorzhou.com/blog/lazy-loading-images/
* _length values_: rem (calculated against root el) https://css-tricks.com/the-lengths-of-css/
* _methodologies_: BEM http://getbem.com/ Atomic https://acss.io/
* _testing_: https://about.gitlab.com/2019/03/13/quantifying-ux-validating-the-redesign-of-gitlabs-settings-pages/
* _usage_: linked stylesheet, `<style>`, inline

* _block_: takes 100% of available width by default

* snippets
```css
el {
    text-align: center;  /* text - center in div https://stackoverflow.com/a/10853894/6813490 */
    text-decoration: none;  /* link - rm underline */
    list-style-type: none;  /* no style --> extra styling https://www.youtube.com/watch?v=2awepiNoaZI */
}
```

## layout

📜 https://every-layout.dev/ https://css-tricks.com/guides/layout/ https://github.com/phuoc-ng/csslayout https://github.com/f-prime/Blunt https://web.dev/one-line-layouts/ https://news.ycombinator.com/item?id=24818485
> * Pure https://github.com/pure-css/pure/

* _requirements_: full screen on mobile, centered on web cf. Dan Luu
```css
body {
    /* https://jrl.ninja/etc/1/ */
    max-width: 38rem;
    padding: 2rem;
    margin: auto;
}
```

* _flexible_: squish to fit
* _responsive_: stack https://css-tricks.com/snippets/css/css-grid-starter-layouts/ https://www.freecodecamp.org/news/responsive-web-design-how-to-make-a-website-look-good-on-phones-and-tablets/
* _Flexbox_: 1 dimension
* _grid_: 2 dimensions https://www.youtube.com/playlist?list=PL4cUxeGkcC9hH1tAjyUPZPjbj-7s200a4 https://github.com/iamshaunjp/css-grid-playlist https://css-tricks.com/snippets/css/complete-guide-grid/ https://testdriven.io/blog/css-grid/

display
* _static_: default
* _relative_: ability to be positioned relative to its own place (were it static) and for other other elements to be positioned relative to it
* _absolute_: positioned to nearest relative parent (or <html>), removed from flow of elements
* _fixed_: removed from flow of elements, positioned to viewport (which doesn’t change as page scrolls i.e. doesn’t change as move through the body)

* align=center https://github.blog/2020-04-09-github-protips-tips-tricks-hacks-and-secrets-from-lee-reilly/

* snippets
```css
/* center horizontally https://github.com/iamshaunjp/css-grid-playlist/blob/lesson-2/index.html */
margin: 0 auto;

/* align el https://stackoverflow.com/a/8577183/6813490 */
input {
    display: inline-block;
}

grid {
    display: grid;
}
```

## selectors

semantics
* _selector_: syntax for describing set of elements
* _descendent_: nested anywhere inside parent; `div div.descendent`
* _child_: nested directly inside parent; `div > div.child`

pseudo
* _pseudo-selector_: selector preceded w/ colon https://css-tricks.com/pseudo-class-selectors/ e.g. target https://css-tricks.com/a-whole-website-in-a-single-html-file/
* _pseudo-class_: select existing element based on state of DOM e.g. `:hover`
* _pseudo-element_: allow styling certain part of an element e.g. `:first-letter`

howto
* test css selector in dev tools: `$$('<urSelectorHere>')`
* _adjacent_: next to; `div + div.adjacent`
* _starts with_: `[attr^="tocolor-"]` https://stackoverflow.com/a/5110337/6813490
* _contains_: `[attr*="tocolor-"]`
* _multiple classes_: `foo.bar` https://css-tricks.com/multiple-class-id-selectors/
* _element type + class_: `div.select2-container`
* _element type + attr_: `div[data-name='team_name’]`

## Tailwind

* downsides: the sites all look the same, CDN not recommended, assumes you're using npx and postcss
* https://www.youtube.com/watch?v=21HuwjmuS7A
* https://builtwithtailwind.com/
* https://jvns.ca/blog/2018/11/01/tailwind--write-css-without-the-css/
* https://github.com/dohliam/dropin-minimal-css
* https://news.ycombinator.com/item?id=23270581

alternatives
* water.css https://watercss.netlify.com/ https://github.com/kognise/water.css/issues/160
* Pure https://github.com/pure-css/pure/
* https://newcss.net/
* https://bulma.io/
* https://simplecss.org/

# DESIGN

* https://macwright.com/2016/12/28/what-little-i-know-about-design.html
* _nav bar_ https://mattsegal.dev/index.html https://lchsk.com/index.html https://bastian.rieck.me/outreach/
* _sections_: https://www.ben-evans.com/
* background: tan (FT, https://uglyduck.ca/) general https://news.ycombinator.com/item?id=22933697 https://css-tricks.com/a-few-background-patterns-sites https://doodad.dev/pattern-generator/ video https://pivotfinland.com/pytest-sugar SVG https://www.masterywithsql.com/
* highlights: https://millerti.me http://joelcalifa.com/ https://www.idiotinside.com/2017/08/19/set-theory-and-python-tips-tricks/ http://songexploder.net/about

## color

🗄 `shell.md` color

* dark mode https://tinyprojects.dev/ https://uglyduck.ca/quick-dirty-theme-switcher/ https://uglyduck.ca/lazy-dev-dark-mode/ https://medium.com/js-dojo/how-to-enable-dark-mode-on-your-website-with-pure-css-32640335474 https://css-tricks.com/reverse-text-color-mix-blend-mode/
* https://designsystem.digital.gov/design-tokens/color/overview/ https://liyasthomas.github.io/colorbook/ https://css-tricks.com/nerds-guide-color-web/ https://www.happyhues.co/ highlight/selection https://man7.org/linux/man-pages/dir_by_project.html#man-pages--man7 https://www.genomicsplc.com/ https://css-tricks.com/overriding-the-default-text-selection-color-with-css/ https://www.youtube.com/watch?v=jmepqJ5UbuM https://nipponcolors.com/ https://colornames.org/
* swatches https://www.rust-lang.org/ shift https://bra.twurst.com/ palette https://latacora.com/ https://tinnedfruit.com/ Addison Wesley background streak
* https://matthewstrom.com/writing/how-to-pick-the-least-wrong-colors/

* pastel https://github.com/sharkdp/pastel
```sh
# conversions
pastel format name fff3cd  # name for hex
pastel format hex cornsilk  # hex for name

# complements
pastel color gold | pastel complement
pastel textcolor hotpink  # background color

# misc
pastel mix <color_one> <color_two>  # mix
pastel list  # x11 colors
pastel paint black --on springgreen " INFORMATION " --bold  # adhoc
```

## images

* old timey https://adamj.eu/colophon/
* David Byrne book
* https://www.3leafaudio.com/ https://www.jefftk.com/pictures/ https://cotonoha.io/en.html

misc
* animation: hover https://bsago.me/blog https://animejs.com/ https://sobolevn.me/2020/06/how-async-should-have-been gsap https://greensock.com/
* audio: http://mally.stanford.edu/ https://github.com/Tonejs/Tone.js
* gifs: https://adamj.eu/contact/

## typography

📙 https://practicaltypography.com/

semantics
* _type_: font + layout
* _font_: set of textual glyphs
* just a `.tff` file https://practicaltypography.com/font-basics.html
* _glyph_: single shape https://practicaltypography.com/ligatures-in-programming-fonts-hell-no.html
* synonym for icon https://www.nerdfonts.com/
* packaged w/ font https://the.exa.website/features/icons

tools
* Pollen https://docs.racket-lang.org/pollen/ https://news.ycombinator.com/item?id=20029372
* TeX https://news.ycombinator.com/item?id=20027807 https://news.ycombinator.com/item?id=7823337 https://news.ycombinator.com/item?id=7822057 https://news.ycombinator.com/item?id=20027116

layout
* _line spacing_: 130% point size
* _line length_: 80 char https://practicaltypography.com/typography-in-ten-minutes.html http://www.designishistory.com/1920/jan-tschichold/
* sidenote: https://goodwill.awardwinninghuman.com/ https://www.w3.org/Style/CSS20/history.html https://pomb.us/build-your-own-react/ https://bsago.me/posts/waltzing-with-wireshark https://www.micahlerner.com/2021/05/23/reflecting-on-2020.html https://github.com/mlerner/mlerner.github.io/blob/master/_plugins/sidenote.rb
* https://practicaltypography.com/type-composition.html
* https://practicaltypography.com/text-formatting.html
* https://practicaltypography.com/page-layout.html
* https://typographyforlawyers.com/page-layout.html
* https://practicaltypography.com/sample-documents.html
* https://typographyforlawyers.com/sample-documents.html

fonts in use
* Brave: Times (serif) Helvetica (sans) Courier (monospace)
* iTerm: Fira Mono regular (me) Monaco (default); Vim inherits https://stackoverflow.com/a/63647904
* site: https://rhodesmill.org/brandon/ https://fonts.google.com/specimen/Prociono https://www.theleagueofmoveabletype.com/prociono
* VS Code: Menlo
> tried Fira Sans but couldn't get Markdown tables to line up
> line length was much lower in VS Code, don't understand why this would change

fonts https://www.nerdfonts.com/
* taxonomy http://www.designishistory.com/1450/type-classification/
* recs https://practicaltypography.com/font-recommendations.html https://practicaltypography.com/free-fonts.html
* _Clarendon_: used for newspaper in the 19th century https://www.typotheque.com/articles/brief_history_of_webfonts
* _Computer Modern_: Donald Knuth https://czep.net/about/
* _Concourse_: popular w/ software people https://practicaltypography.com/concourse.html https://wsvincent.com/site-design/ https://danielmiessler.com/colophon/
* _Editor_: https://www.worksinprogress.co/issue/why-didnt-suicides-rise-during-covid/
* _Fira Code_: ligature crazy spin-off of Fira Mono https://practicaltypography.com/ligatures-in-programming-fonts-hell-no.html
* _Fira Mono_: https://practicaltypography.com/courier-alternatives.html
* _Hack_: monospace https://github.com/source-foundry/Hack 
* _Litera_: https://quarchive.com/getting-started
* _Recursive_: warm https://github.com/arrowtype/recursive/
* _Signifier_: https://klim.co.nz/retail-fonts/signifier/

design
* it goes deep https://news.ycombinator.com/item?id=24631681
* differentiate btw 0 and O https://news.ycombinator.com/item?id=27066965
* color https://news.ycombinator.com/item?id=24303042
* _point size_: 20 pixels for web
* _weight_: width https://en.wikipedia.org/wiki/Font#Weight
* _book weight_: regular https://news.ycombinator.com/item?id=30400828
* _monospace_: equal space btw char http://www.ii.com/vim-unicode-digraphs/
* for software dev bc alignment https://stackoverflow.com/a/218639
* _ligature_: combine n characters into 1 e.g. `!=`
* _proportional_: diff space btw char
* for prose https://stackoverflow.com/a/218749
* aka variable https://www.recursive.design/

system vs. web
* _system font_: stored locally https://practicaltypography.com/system-fonts.html 📍 https://news.ycombinator.com/item?id=31543054
* aka desktop font https://meta.stackexchange.com/questions/364048/we-are-switching-to-system-fonts-on-may-10-2021
* macOS install: double click on font file, click installer
* manage w/ Font Book
* use font editor https://github.com/fontforge/fontforge
* _OpenType_: fmt for desktop font https://en.wikipedia.org/wiki/OpenType https://github.com/arrowtype/recursive/
> ❓ what prevents people from grabbing font files from browser/repos?
* webpages use to rely on desktop fonts https://www.typotheque.com/articles/brief_history_of_webfonts
> There was, however, a catch: while images could be loaded to webpages from remote servers, fonts could be loaded only from the client's computer...font foundries were reluctant to expose their products to piracy, so font licenses generally prevented webpage owners from using the fonts online.
* _web font_: hosted online
* e.g. Google Fonts, Adobe TypeKit https://fonts.google.com/
* user can set font from browser to override site https://news.ycombinator.com/item?id=27068036 https://news.ycombinator.com/item?id=27065041
* perf https://iainbean.com/posts/2021/5-steps-to-faster-web-fonts/
* _font-face_: w/out this you have to rely on system font https://css-tricks.com/snippets/css/using-font-face-in-css/
```css
/* https://stackoverflow.com/a/3245187 */
@font-face {
    font-family: fira-mono;
    src: url("fira-mono.otf") format("opentype");
}
@font-face {
    font-family: fira-mono-bold;
    src: url("fira-mono-bold.otf") format("opentype");
}
body {
  font-family: fira-mono, fallback;
}

<style>
    @font-face {
    font-family: "elevate-display-font";
    font-weight: 500;
    font-style: normal;
    src: url("https://maddo.xxx/assets/fonts/heldane-500-normal-latin.woff2")
        format("woff2"),
        url("https://maddo.xxx/assets/fonts/heldane-500-normal-latin.woff")
        format("woff");
    unicode-range: U+0-7F, U+A0, U+200A, U+2014, U+2018, U+2019, U+201C,
        U+201D, U+2022, U+2026;
    }
</style>
```

file fmt https://practicaltypography.com/triplicate.html
* _OTF_: macOS
* can use on web, convert to WOFF https://stackoverflow.com/a/3245187
* _TTF_: Windows
* for web https://stackoverflow.com/a/24990647
* _WOFF_: websites https://practicaltypography.com/concourse.html
* load faster https://css-tricks.com/snippets/css/using-font-face-in-css/#aa-woff-woff2
* created so that people could sell fonts i.e has way to embed license info https://developer.mozilla.org/en-US/docs/Web/Guide/WOFF
> The WOFF format was initially created as a reaction to OTF and TTF, in part, because these formats could easily (and illegally) be copied.

# ZA

* EME encrypted media extensions https://stackoverflow.com/questions/46212264/example-encrypted-media-extensions-encryption/46374671#46374671
* accessibility, blindness https://news.ycombinator.com/item?id=30339187
* BYO Jinja https://notes.eatonphil.com/writing-a-template-library-in-python.html
* _perf_: https://developers.google.com/speed/pagespeed/insights/ https://webhint.io https://www.webpagetest.org/ https://github.com/trimstray/the-book-of-secret-knowledge#black_small_square-performance https://github.com/theodo/falco https://1mb.club/
* _PWA (progressive enhancement)_: https://technology.blog.gov.uk/2016/09/19/why-we-use-progressive-enhancement-to-build-gov-uk/ https://www.youtube.com/playlist?list=PL4cUxeGkcC9gTxqJBcDmoi5Q2pzDusSL7
* _semantic web_: element describes content e.g. `<footer>` `<section>` https://twobithistory.org/2018/06/10/birth-of-the-web.html#fnref:11 https://twobithistory.org/2018/05/27/semantic-web.html https://news.ycombinator.com/item?id=30166788
* _UI_: elements https://codepen.io/topics/ is hard https://overreacted.io/the-elements-of-ui-engineering/
* _validation_: `<input maxlength= "15" type="url" regex="<regex>" required>` must be of type url, must input something and match regex, limit 15 chars
* _WYSIWYG_: Wix, SquareSpace https://webflow.com/
* _W3C_: https://24ways.org/2018/researching-a-property-in-the-css-specifications/

CMS 🗄 SSG
* _website builder_: optimized for non-dev
* e.g. Wix, SquareSpace
* _CMS - traditional_: splits middle btw dev and non-dev e.g. has UI (vs. CLI) 
* e.g. Wordpress https://kevq.uk/the-case-for-wordpress https://softwareengineeringdaily.com/2020/04/30/jamstack-content-management-with-scott-gallant-jordan-patterson-and-nolan-phillips/ 12:00
* _CMS - headless_: API on top of content
* uses Git server as backend (vs. MySQL like in WP) [SED 17:00]
> not static anymore insofar as you need a frontend framework? [SED 3:55]
* e.g. Ghost (hosting, newsletters, Stripe, membership) alternatives (Netlify, Wagtail, Django, Perch)

## HTML

📜 https://htmlreference.io/

* _attribute_: metadata
* _canvas_: draw, make charts
* auto reload: `<meta http-equiv="refresh" content="3">`
* head: https://www.matuzo.at/blog/html-boilerplate/

howto
* link - use button https://stackoverflow.com/a/2906586/6813490
* link - preload: `<link rel="preload">` = "go fetch this heavy resource before you (browser) get busy rendering"; perf thing
* image - Youtube preview thumbnail: https://stackoverflow.com/a/18681824/6813490
* dropdown/collapsible https://news.ycombinator.com/item?id=29669812 🗄 `personal-site` nested

forms
```html
<form method="post">
    <input type="text">
</form>
```
* dates https://uglyduck.ca/basic-form-styling/
* `action`: URL to send data
* `enctype`: HTML parlance for media type for forms https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/enctype 🗄 `4-application.md`
* `method`: HTTP verb https://stackoverflow.com/questions/8395269-->
* `role`: accessibility thing https://stackoverflow.com/a/18664038/6813490
* `type`: text, file, submit; submit is only useful for input elements (button el default to submit anyway https://stackoverflow.com/a/10079197/6813490)

## Markdown

* RENDERME https://news.ycombinator.com/item?id=30336703
* metadata https://github.com/blacksmithgu/obsidian-dataview
* spec https://github.blog/2017-03-14-a-formal-spec-for-github-markdown/
* asciidoc vs. Markdown https://news.ycombinator.com/item?id=27744509
* href https://github.com/pemistahl/grex
* linting https://mkaz.blog/code/linting-markdown-syntax/
* Latex http://www.danielallington.net/2016/09/the-latex-fetish/ https://increment.com/open-source/the-lingua-franca-of-latex/
* formal spec https://githubengineering.com/a-formal-spec-for-github-markdown/
* code syntax support https://github.com/github/linguist/blob/master/lib/linguist/languages.yml
* Pandoc has their own version of Markdown? https://yihui.name/en/2018/09/target-blank/
* Markdown to PowerPoint https://yhatt.github.io/marp https://www.youtube.com/watch?v=CkIweDviGH8
* HTML to Markdown https://github.com/JohannesKaufmann/html-to-markdown
* [dropdowns!](https://raw.githubusercontent.com/30-seconds/30-seconds-of-code/master/README.md)
* [diff](https://stackoverflow.com/a/40883538)
* Github moving to CommonMark https://github.com/github/markup/issues/498#issuecomment-158257453 Stack Overflow too https://meta.stackexchange.com/q/348746/434172
* table fmt: Jira, Markdown/RST, Latex https://jsvine.github.io/intro-to-visidata/basics/saving-sheets/
* Markdown for Google Docs https://www.theverge.com/2022/3/29/23002138/google-docs-markdown-support-formatting-update

conversion to HTML
* https://github.com/susam/texme
* Markdown to HTML w/ Python CLI https://python-markdown.github.io/cli/ `python -m markdown 1997-graham-hackers-painters.md > pg.html` -> doesn't handle quotes, output is vanilla would need to figure way to add CSS
* _mistune_: https://github.com/lepture/mistune
* _markdown_: `python -m markdown rn.md > rn.html` https://python-markdown.github.io/cli/ used in MkDocs https://github.com/mkdocs/mkdocs/blob/master/requirements/project.txt
* _markdown2_: https://github.com/trentm/python-markdown2 supports (maybe) ghfm https://github.com/mkdocs/mkdocs/issues/263#issuecomment-65362418
```sh
python -m markdown2 --extras fenced-code-blocks my-debug-checklist.md > debug.html
```

add styles
* `water.css` w/ Beatiful Soup in script https://stackoverflow.com/a/19123463/6813490 
* more advanced https://github.com/cburmeister/cburmeister.github.io/blob/master/Makefile pandoc https://serverless.pub/lambda-utility-layers/ https://github.com/kickstartcoding/cheatsheets

## PDF

---

https://docs.racket-lang.org/quad/
Markdown https://docs.racket-lang.org/quad/

https://rtpg.co/2016/09/17/make-an-ebook.html
* _design_: https://news.ycombinator.com/item?id=24108950 https://gds.blog.gov.uk/2018/07/16/why-gov-uk-content-should-be-published-in-html-and-not-pdf/
* _annotation_: PDF Expert, Flexcil, https://news.ycombinator.com/item?id=23230218 https://github.com/xournalpp/xournalpp
* _archival_: https://github.com/danburzo/percollate https://github.com/pirate/ArchiveBox
* _readers - macOS_: PDF Expert (freemium version won't let you save) PDF Element ($90/year) Preview (search doesn't seem to work for most documents https://duckduckgo.com/?q=macos+preview+search+doesn%27t+work&atb=v161-1&ia=web text in sidebar doesn't correspond to hightlight, some hightlights produce no text in sidebar, can't enter emoji into notes, limited keyboard shortcuts) Nitro PDF
* _to plain text_: https://github.com/axa-group/Parsr https://github.com/jsvine/pdfplumber
* _from plain text_: http://richardmavis.info/using-web-technologies-to-print-a-book https://coreyburmeister.com/continuous-integration-and-deployment-for-my-resume/
* _from HTML_: https://jvns.ca/blog/2020/06/19/a-little-bit-of-plain-javascript-can-do-a-lot/ https://www.princexml.com/
* _split_: select subset and drag into Finder

---

https://github.com/jorisschellekens/borb
https://news.ycombinator.com/item?id=26691626
* _ereader_ https://johnfactotum.github.io/foliate/
[PDF is bad]()
* PDF reader w/ Vim bindings: Zathura http://jhshi.me/2016/03/09/zathura-pdf-viewer-for-vim-lovers/index.html#.Xg4gThdKh-U not available on macOS https://www.reddit.com/r/vim/comments/3prfd0/pdf_reader_with_vim_keybindings_for_mac_osx/
* https://github.com/burtonator/polar-bookshelf https://pwmt.org/projects/zathura/ https://goodreader.com/
* mobile: [Joplin](https://github.com/laurent22/joplin), IAWriter
* https://www.pdfa.org/a-technical-and-cultural-assessment-of-the-mueller-report-pdf/

## static site (SSG)

🗄
* `km.md` documentation
* `system.md` architecture/noDB

features https://twitter.com/danluu/status/1244051446313574402
* templating
* page metadata e.g. title/desc, date, tags https://www.janmeppe.com/blog/I-dont-like-my-blog-anymore/
* search: Stork https://stork-search.net/ TinySearch https://github.com/tinysearch/tinysearch https://news.ycombinator.com/item?id=23474134 DDG https://vadosware.io/ https://ddg.patdryburgh.com/ lunr.js https://github.com/olivernn/lunr.js https://brainbaking.com/search/?q=database
* RSS generation
* minification
* tags: https://github.com/erwald/blog/blob/master/_data/series.json https://www.erichgrunewald.com/posts/the-kingdom-of-tamego/ https://github.com/jeffkaufman/webscripts/blob/e1c8a399536bb92e3f09886eea9fb925e710c981/intros.json https://www.jefftk.com/news/money

```sh
# https://fvsch.com/static-site-generators
├── content
│   ├── 2018-09-07-cool-blog-post.txt
│   └── 2018-10-01-other-blog-post.txt
└── output
    ├── cool-blog-post.html
    ├── index.html
    ├── other-blog-post.html
    └── rss.xml
```

SSGs https://jamstack.org/generators/
* BYO https://www.youtube.com/watch?v=Ph7oJDR71Jc https://github.com/mitsuhiko/rstblog
* _Eleventy_: https://www.11ty.dev/ https://www.erichgrunewald.com/ https://news.ycombinator.com/item?id=31293971
* _Hugo_: broken https://twitter.com/danluu/status/1244024025019342851 https://yawpitchroll.com/posts/hugo-probably-is-not-for-you/
* way more popular than Jekyll https://blog.golang.org/8years
* bad once nesting exceeds top-level? https://gohugo.io/templates/lists/ https://discourse.gohugo.io/t/list-pages-of-sub-sub-folders/9436/2
* _Metalsmith_: Javascript https://github.com/metalsmith/metalsmith
* _Zola_: Rust; no assumptions regarding the structure of your site https://www.getzola.org/documentation/getting-started/overview/#first-steps-with-zola https://haskellbook.com/ 

Python SSGs
* _Hyde_: https://github.com/hyde/hyde
* _Lektor_: crappy install https://www.getlektor.com/ https://lucumr.pocoo.org/2015/12/21/introducing-lektor/
* _Makesite_: https://github.com/sunainapai/makesite
* _Nikola_: https://getnikola.com/
* _Pelican_: ✅ https://github.com/getpelican/pelican https://tech.marksblogg.com/website-cdn-with-pelican-and-s3cmd.html https://github.com/zachvalenta/pelican-site
* features: templating, metadata, tags
