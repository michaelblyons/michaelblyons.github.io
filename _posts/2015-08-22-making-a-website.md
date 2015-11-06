---
layout: post
title: Making a Website
---

I feel like these first-posts are clich&eacute; and well-nigh obligatory. I had a general sense for some time that I wanted a web presence, and that I didn't want it to be run by the whims of, say, Facebook, or some other entity whose business is selling me.

When I finally set out to register a domain, I discovered that in between my thought to register lyons.io and _actually doing so,_ someone already had. I trawled around for the availability of lyons with various other TLDs, and finally remembered the trend of pulling it into the site name.

It's kitschy, I know, but ten bucks a year for a six-char domain is pretty sweet.


Once I had the (virtual) paperwork in, I spent a good long while without actually using it.

When I set out to make an actual website, I realized that I had a sense of things I _didn't_ like, but not a whole lot that I particularly wanted to do:

## Layout

I was fairly adamant that there should be a maximum width to the content. Reading E.D. Hirsch's **Cultural Literacy** had convinced me that columns of text should be narrow enough to take three or fewer distinct eye positions to read all the words. Otherwise, the flow is lost and your readers are distracted by the difficulty of reading, even if they don't know why.

Columns themselves have trouble mapping to a web format, since the principal "more content" mechanism is scrolling, rather than turning a discrete page. I've seen websites that attempt to use multiple columns to display content, and I have been less than impressed.

With the content focus I was intent on, there would be a lot of horizontal space left over. I didn't expect to have much in the way of important sidebar content, so I shifted my header and footer to the sidebar. For any post longer than a page, though, I was still going to have a long column of empty space, so I set out to pin the header, footer, and navigation in place.

I also wanted to adapt my design to a variety of screen sizes, "Responsive Design" in the web development lexicon.

## Tech

These turned out to be virtually incompatible goals, surprisingly. The tricks I knew to pin things in place absolutely refused to stay in place when the screen was narrowed.

Eventually, I made a full-width `position: fixed` element with no height at the top of the screen. I then added a centered element to it with width criteria that matched the rest of the website. Other elements inside that one would finally obey the rules I wanted, and I duplicated them on the bottom for the footer.

This works out to be:

```html
<style>
    .top {
        position: fixed;
        width: 100%;
    }
    .top-center {
        max-width: 1000px;
        margin: 0 auto;
    }
    .sidebar-width {
        width: 30%;
        max-width: 300px;
    }
    main {
        max-width: 1000px;
        margin: 0 auto;
    }
    section {
        float: right;
        width: 70%;
    }
</style>
<div class="top">
    <div class="top-center">
        <div class="sidebar-width">
            <header></header>
        </div>
    </div>
</div>
<main>
    <section>
    </section>
</main>
```

### Jekyll

After the layout was more or less working, I set out to run the blog software that merges my posts into the pages with the layout I built. Github [uses `jekyll`][gh-j] to to do this merging. It's a Ruby gem, and I (having decided to use Python preferentially over Ruby) didn't have much of a Ruby setup on the OSX machine I do most of my work on.

Apple's XCode comes with ruby, and I leaned upon it some time ago to install [HomeBrew][brew], but I hadn't touched it since. Installing gems turned out to be somewhat of a bear, with various people suggesting that I use RVM or `rbenv` to manage multiple Ruby versions.

The problem is that I don't _want_ to manage multiple Ruby versions. The smaller the footprint ruby has on my system, the better I will feel. I wanted to use Apple's Ruby, which is more than capable for the task at hand. I didn't want to run the gem installer as root, though.

After going through the `rbenv` instructions, I found some instructions that suggested that I could change the gem install path, [which I did][so-gem]. Then, I deleted the Ruby version I had just downloaded with `rbenv`, and `jekyll` installed fine. I did have to symlink it myself to a `$PATH`-enabled location.

As of this writing, I still don't have syntax highlighting for code blocks.

## Art

I'm not much of an artist and not a photographer at all, so I didn't have much in the way of imagery. I do, however, have some art around the house, including a small wall hanging of an elephant.

I took a picture of it with my phone's crummy camera, and traced it with the pathing tools in [Gimp][]. Gimp is not really meant for heavy SVG work, but I wasn't up for installing Inkscape or the like for my first pass.

I have Photoshop, courtesy of the office, but I've sunk many more hours into FOSS tools than I have into Adobe's suite.

Back to the elephant, I initially tried color sampling to assign colors, and boy [was it ever ugly!][ugliphant] I ended up picking some neutral grays with extra red to brown them a little. I plan to make another pass or two on the guy in the future. My wife is particularly amused by the idea to bulge his eye when you hover over him.

I eventually intend to swap the center bar out for an SVGed bamboo. I'm hoping that it doesn't end up too busy.

[brew]: http://brew.sh
[gimp]: http://gimp.org
[ugliphant]: https://github.com/michaelblyons/michaelblyons.github.io/blob/cd6a90f92ca25bf0392afb0af86330bdbb28690b/images/elephant.svg
[so-gem]: http://stackoverflow.com/a/32027131/241211
[gh-j]: https://help.github.com/articles/using-jekyll-with-pages/