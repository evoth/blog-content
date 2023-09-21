---
title: This Website!
summary: "Portfolio and blog site created with Hugo SSG, Tailwind CSS, and good old JavaScript"
weight: 40
resources:
  - name: thumb
    src: portfolio-v2-thumb.svg
    params:
      alt: The letters "EV" on a dark gray background.
  - name: hero
    src: portfolio-v2-hero.svg
    params:
      alt: The letters "EV" on a dark gray background.
links:
    - title: GitHub Repository
      url: https://github.com/evoth/blog
    - title: Blog Content Submodule
      url: https://github.com/evoth/blog-content
    - title: Website
      url: https://ethanvoth.com
---

Check back soon for more detailed insight on this project's inspiration, process, and lessons! For now, here's information from the [GitHub repo](https://github.com/evoth/blog):

## Plan

A content-rich personal website featuring project posts and descriptions that communicate my problem solving approach and breadth of knowledge.

## Current State

A visually appealing way to display my personal projects. I've laid the foundations for the vision above, but I just have to start writing the content!

## Todo

- Fix spacing
    - Concept shortcode
- Better responsiveness for mobile
    - Home page
        - Smaller text sizes below medium breakpoint
- Sufficient button titles (TOC and others)
- Concept framing
- (Better) Footer
    - Info about me? (see https://spf13.com/)
    - Recent stuff? (see https://atega-hugo.netlify.app/)
- Get local copy of Google fonts?
    - This only seemed like a problem when testing w/o cache-- in prod they'll just be loaded once then cached in browser
- **COMMENT AND ORGANIZE**
    - Especially partials
        - Explain input/output
        - Organize into folders
        - MODULARIZE
    - Organize layouts with partials for different sections
- Accessibility
    - ARIA
    - Test with accessibility tools
    - Use visibility instead of display where appropriate to match visuals with accessibility tree
    - Good tooltips and labels, button/link titles, etc.
    - Image alt text (figure out how to do it for divs with background-image and svg, or how to replace with img)
    - Contrast
    - Intuitive navigation/layout
    - Research other stuff
- Semantic HTML
    - Correct use of tags and attributes and structure
- Metadata (and SEO by extension)
    - Schema
    - OpenGraph
- Eliminate last pseudo elements
- Correct post published/updated dates (figure out GitInfo with submodules)
- Darker zinc-300 color? Or maybe add zinc-250 and shift everything down
- References behavior more like TOC
- Include references on TOC?
- Series buttons (and other metadata) at bottom
- Organize Tailwind mess using components and stuff
    - Reduce repeated sets of classes
    - MAKE CLASSES (USING APPLY) FOR COMMON COMBINATIONS LIKE "zinc-200 dark:zinc-800"
- Weird glitch where there's too much padding below references until reflow
    - Caused by tooltips overflowing (I think I fixed this when working on footer but check to make sure)
- Disable SVG animation and similar for prefers-reduced-motion
    - Disable svg-freeze elements as well (maybe just modify classes to be disabled for prm)
    - Ability to manually pause animations as well
- Minify CSS/JS, Tailwind classes and reformat HTML
- Bundle JS or combine into modules instead of having a bunch of separate scripts
- HTML comments (there are some on a branch but they're woefully outdated)
- Fill out different types of pages
    - Concepts
        - Should link to articles which contain them
    - Projects
        - Should link to relevant articles and have galleries, github link, etc.
        - GitHub link
        - Technologies/languages
        - Timeline
        - Links
    - Series and tags are pretty straightforward
    - Posts page should link/preview series, tags, concepts?, projects?
    - All should be paginated if necessary
    - Placeholders if not much content
    - Better navigation
        - Back to previous page
            - E.g., link back to all tags on tag term page
        - Breadcrumb?
    - POSTS SHOULD HAVE RELATED POSTS, POSTS IN SAME SERIES (or just arrows), etc.
- Just use parentheses plus dot (). instead of index if it makes it easier to read
- Add keywords to front matter just 'cause
- Add svg icon names to front matter for placeholder generation
- Repeated code between references and tooltip-- create partial for metadata generation
- Reevaluate list vs single partial organization (esp. containers)
- Fix spacing at top of post (has to do with TOC?)
- **Pagination**
- Think about front matter for taxonomy/section pages, standard way to include markdown in hero, etc.
- Check for mismatched opening/closing tags
- Make stuff more colorful, visually appealing
- RSS n such
- View all buttons for card lists?
- When scraping link metadata, get more data if needed (image/alt text)
- Bug when no single card in card list is the max width, meaning the list is smaller than the max and gets centered
- Add more metadata to card?
    - Date
    - Taxonomy terms
- Adding a term to a page in card lists section doesn't give the right title
- Card list heading tooltips are bugged if mouse only barely hovers over top or bottom
- Code block themes
    - Have the included ones, but also custom light/dark ones to match website themes
    - Ability to select themes
- TOC can overlap related pages (because of h-0)
- SVG "watermarks"
- For svg thumbs, simply round off time instead of setting to 0
- Fill in front matter
    - Thumb/hero alt
    - Other stuff
- Delay before animation activation?
- Hero images for list pages?
- Make ad-hoc heros paused until suitable version can be created
- Change ptl-adb-ffmpeg bg to purple?
- Behavior/placeholder for absent pages
- Sidenote bug (there are others) where the outline doesn't work if two lines just barely overlap
- More robust handling of markdown (paragraphs) in sidenotes
- That weird bug when a tooltip is closing but your mouse moves to the level of another fragment of the same link and the tooltip updates but not in the right way
- Somehow segment link preview data/thumbs from main repo
- Populate missing front matter dates with date of first commit
- Use Tailwind line-clamp instead of limiting number of words?
    - Or at least shorten by character count instead of word count
- Weird flickering with tooltip next to period in sidenote when resizing
- Tooltip arrow line thing
- Access plot json as resource in plotly shortcode?
- Subtitle for card list
- Prevent page from appearing in card list on same page
- Add content
    - Don't forget links and references
- Deploy (GitHub pages?)
- Google Search Console?
- SEO, metadata, etc. as mentioned above