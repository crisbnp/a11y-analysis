# Analyze a non-accessible web site

## Instructions

Identify a web site that you believe is NOT accessible, and create an action plan to improve its accessibility. Your first task would be to identify this site, detail the ways that you think it is inaccessible without using analytic tools, and then put it through a Lighthouse analysis. Take the results of this analysis and outline a detailed plan with a minimum of ten points showing how the site could be improved.

Rubric

Criteria Exemplary Adequate Needs Improvement
student report includes paragraphs on how the site is inadequate, the Lighthouse report captured as a pdf, a list of ten points to improve, with details on how to improve it

---

# Analysing [Indonesian Embassy in the UK](https://kemlu.go.id/london/en)'s website

## Reasons:

As an Indonesian who lives abroad in the UK, I do go to the website when I need to renew passport or find relevant information. As a government website, I would expect an accessible website that caters towards all users. I find it difficult to navigate the website as the hierachy of website is not clear and there are a lot of moving content which is hard to follow.

## Accessibility Review:

I want to make sure the website is accessible for users who rely heavily on keyboard to navigate by choice or otherwise. Users with motor impairments such as RSI or paralysis as well as screen readers.

📌 Check if it has a logical tab order and visible focus styles \
📌 Using screen reader - use VoiceOver built in Mac \
📌 Link and buttons should tell us what it's for and its state.

## My findings:

By inspecting the elements using Chrome Dev Tools and using VoiceOver screen readers on Mac, I can note that:

- There is very little application of semantic markups such as `<section>, <article>, <nav>`
- A lot of usage of divs, nesting div within div to create layout of the webpage with some divs without ARIA-roles.
- There is no hierachy to the website. Headings are not in the right order and if you are a screen reader user, it will be difficult to navigate the website.
- 'Skip to main content' tab for screen readers or keyboard users to make it easy for users to jump to main section is not available.
- I would expect ARIA attributes being used to explicitly state what the role of the div is but I don't see it.
- Links are not appropriately described.
- Using `<div>` for a drop down navigation and not describing its role within the div. I would expect an ARIA `role='navigation'` or use semantic `<nav>` tag with children list `<li>` elements and use CSS to make styling changes.
- Each of the 'mega button' navigation is hoverable and supposed to have a drop down children menu. This is not accessible for users who heavily rely on tab to navigate the website and who use screen readers. When I tested it using VoiceOver, and tried to click on the 'mega button' link - the drop down menu does not show up. This mega button also is not focusable when navigating with the keyboard
- image tags do not have alt attributes and link icons do not have discernable description.
- 'news flash' element is similar to stock ticker where the content (in this case, 3 different news links) move across the little red container. This will be difficult for users who have troubles reading quickly or following motion on a webpage. Although when you hover over the link, it stops moving but if you are a screen reader user, the VoiceOver will read the prepend symbols (\*\*) for every link title.
- carousel images and links do not have a pause/play button so as a user, I do not have control over how to consume the information at my own pace.
- Each container on the right hand side layout that contains more carousel of information and twitter has buttons to navigate to the left or right content but this does not have a description. When using screen readers, it is not conveyed to the user what these buttons do. Could be improved by describing it as 'next' or 'previous' and the title of that container is not picked up by screen readers. So as a user you wouldn't know what this button you are expected to click should take you to.
- It has a `<noscript>` tag which hides some content of the web page. When I disabled JavaScript on Chrome, I cannot access the content such as News and Information etc - so I believe this is inaccessible as user should still be able to access the contents needed even when JavaScript is disabled.

## I used 2 analysis tools:

1. Lighthouse in Chrome dev tools which generate reports for both desktop and mobile view
2. Wave (Web Accessibility Evaluation Tool) by WebAIM (wave.webaim.org)

Reports are as followed:

1. [Lighthouse Report - Desktop View](./kemlu-desktop-lighthouse-report.pdf)
2. [Lighthouse Report - Mobile View](./kemlu-mobile-lighthouse.pdf)
3. [Wave Report](https://wave.webaim.org/report#/https://kemlu.go.id/london/en#!)

## Detailed plans on how to improve the website based on Lighthouse Report for Desktop

Accessibility Score: 75%

1. **Problem**: Button elements are empty or have no value text \
   **Example**: `<button class="btn btn-secondary btn-sm" type="button" onclick="pencarian('perwakilan')"> <i class="fa fa-search"></i> </button>`
   **Improvement**: As this button element is using an `<i>` for the icon, a descriptive text must be presented to idicate the function of the button. In this case, it is a search button. Adding `aria-label="Search"` will suffice. \
   **Improvement example**: `<button aria-label="Search" class="btn btn-secondary btn-sm" type="button" onclick="pencarian('perwakilan')"> <i class="fa fa-search"></i> </button>`
2. **Problem**: Linked image elements do not have `alt` attributes and do not have alternative text resulting in an empty link. \
   **Example**: `<a class="navbar-brand" href="https://kemlu.go.id/london/en"> <img src="https://kemlu.go.id/images/garuda.png" width="60px" class="d-inline-block align-top"> </a>` \
   **Improvement**: In this example, this image is the National Emblem of Indonesia. By clicking this link, it will take users to the Home page of the website. Add `alt` attribute to say this will take users to the home page. If the intention is to use it as an image, the `alt` attribute should be an empty string. \
   **Improvement example**:`<a class="navbar-brand" href="https://kemlu.go.id/london/en"> <img alt="Indonesian Embassy in the UK home" src="https://kemlu.go.id/images/garuda.png" width="60px" class="d-inline-block align-top"> </a>`
3. **Problem**: Links do not have a discernable, focusable and unique text or name
   **Example**: `<div class="col-3 inline text-right" id="bottom-slide-nav"> <a href="#carouselExampleControls2" role="button" data-slide="prev"> <i class="fas fa-lg fa-arrow-circle-left text-light"></i> </a> <a href="#carouselExampleControls2" role="button" data-slide="next"> <i class="fas fa-lg fa-arrow-circle-right text-light"></i></a></div>` \
   **Improvements**: In the example above, the links have `aria-role='button'` and a user should be able to click or interact using keyboard and know what the functionality of these links - in this case, controlling the carousel by clicking next or previous. We can remove the link or provide text within the link to describe the functionality so we don't confuse the users. Alternatively, we can use a `<button>` tag and add `aria-label="Previous"` as an attribute. \
   **Improvement example**: `<a href="#carouselExampleControls2" role="button" data-slide="prev"> <i class="fas fa-lg fa-arrow-circle-left text-light"></i> Previous</a>`
4. **Problem**: Keyboard navigation could be improved. Heading elements are not in a sequentially-descending order and the whole webpage does not have a first level heading.
   **Example**: Skips `<h1></h1>` element and page starts with `<h3></h3>`
   **Improvements**: Making sure that heading content of the website is sequential so top-level heading should be an `<h1>` tag and follows by `<h2>` and so on. This will help users to navigate the website.
   **Improvement Example**: I will start with making sure the title of the page is an `<h1>` tag and then any other containers that have a heading as the sequential heading tag.
5. **Problem**: `[user-scalable="no"]` is used in the `<meta name="viewport">` element or the `[maximum-scale]` attribute is less than 5. This disable zoom and can be problematic for users with low vision. \
   **Example**: `<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=0">` \
   **Improvement**: Avoid disabling browser zoom by the removing `[user-scalable="no"]` and ensuring the `[maximum-scale]` attribute is set to greater than 5 \
   **Improvement Example**: `<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=10">`
6. **Problem**: The page does not have a logial tab order.
   **Example**: The header banner at the top of the page contains 4 social icons and a search bar. When you tab through the page, it does not follow the visual layout as it will tab through the search bar and then go back to the social icons.
   **Improvement**: As the focus order seems wrong, elements should be rearranged in the DOM to make the tabl order more natural.
7. **Problem**: Custom interactive controls are not keyboard focusable and do not indicate their purpose and state.
   **Example**: The 'mega button' navigation is supposed to be a a custom interactive navigation where a hidden menu or _submenu_ is shown on a hover event but users who rely on screen readers and keyboard will have trouble interacting and cannot access the content of the navigation.
   **Improvements**: \
   a) Rearrange how the submenu is laid out in the DOM. At the moment, it uses a parent div and on hover, shows another div containing different links. Ideally this should be wrapped in a `<nav>` tag with children elements of `<ul>` then `<li>`.  
   b) Using parent menu item as toggle button where user can still _tab_ through the main parent navigation elements and able to _enter_ on a parent menu item and drop down menu will then become visible.
   c) Using `[tabindex]` attribute to make this custom control focusable
8. **Problem**: Parent links of 'mega button' navigations are broken same-page link as it contains empty `[href=""]` attribute. \
   **Example**: `<div class="mega"> <a href="#!" class=""> ... </div>`]
   **Improvement**: Remove the same-page link or ensure the target link exists.
9. **Problem**: Not using HTML5 landmark elements to improve navigation \
   **Example**: Landmark elements such as `<main>` , `<nav>`, etc can be used to improve key board navigation for assistive technology as there are so many nested `<div>` being implemented. \
   **Improvement**: Using `<main>` tag for wrapping the main content of the webpage. Using `<nav>` to wrap navigation links. Using `<section>` to wrap containers that contain a section of similar content. Using `<article>` to wrap each news article.
10. **Problem**: Colours contrast - background and foreground colours do not have a sufficient contrast ratio. \
    **Example**: Paragraph tag under the 'News and Information' tab are difficult to read. \
    **Improvement**: Ensure text has sufficient colour contrast. Using colour picker and checking if they meet the minimum colour contrast rations which is: 3:1 for text that is 18 pt, or 14 pt and bold 4.5:1 for all other text
