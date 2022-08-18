# Scroll Sensitive Navigation

[Example](https://slack.dev/bolt-js/deployments/heroku)

As you scroll on the main panel, the navigation lights up on the left. There's code that toggles the `completed` class on nav elements (in tutorial_nav.js):

```javascript
var navTag = 'h3';

window.addEventListener('DOMContentLoaded', (event) => {
    var sections = document.querySelectorAll(navTag);
    var navParent = document.querySelector('.tutorial-nav-list');

    function createNavElement(title, href) {
        var navElement = document.createElement('li');

        var navCircle = document.createElement('div');
        navCircle.setAttribute('class', 'circle ' + href);

        var navAnchor = document.createElement('a');
        navAnchor.setAttribute('href', '#' + href);
        navAnchor.innerText = title;

        navElement.appendChild(navCircle);
        navElement.appendChild(navAnchor);

        return navElement;
    }

    sections.forEach(function (navHeader) {
        var newElement = createNavElement(navHeader.innerText, navHeader.id);
        navParent.appendChild(newElement);
    });
});

window.addEventListener('scroll', (event) => {
    var sections = document.querySelectorAll(navTag);

    sections.forEach(function (navHeader) {
        var navElement = document.querySelector('.' + navHeader.id);

        if (
            window.scrollY >=
            navHeader.getBoundingClientRect().top + window.pageYOffset - 5
        ) {
            navElement.setAttribute(
                'class',
                'circle completed ' + navHeader.id
            );
        } else {
            navElement.setAttribute('class', 'circle ' + navHeader.id);
        }
    });
});
```
