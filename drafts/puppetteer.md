# Puppeteer

```javascript
const _temp = await page.evaluateHandle(() => temp);
await page.evaluate((x) => {}, _temp);
```

```javascript
let incognitoContext;
async function getPage(incognito = false) {
    let page;
    if (incognito) {
        incognitoContext ||= await browser.createIncognitoBrowserContext();
        page = await incognitoContext.newPage();
    } else {
        page = await browser.newPage();
    }
    await page.setCacheEnabled(false);
    page.setDefaultTimeout(100000);
    return page;
}

async function waitPageLoad(page, url) {
    const response = await page.goto(url, {
        waitUntil: 'networkidle0',
    });
    return response;
}
```

- [puppeteer hangs in headless mode](https://stackoverflow.com/questions/59912590/puppeteer-hangs-in-headless-mode)
- for me, it was the devtools
