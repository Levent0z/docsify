# Express

```javascript
// Make eslint happy
/* global __ditname process */
const express = require('express');
const path = require('path');
const app = express();

// Serve only the static files from the dist directory
app.use(express.static(__dirname));
app.get('/manage/ready', (req, res) => res.json({ status: 'READY' }));
app.get('/*', (req, res) => {
    if (req.path !== '/') {
        res.redirect('/');
    } else {
        res.sendFile(path.join(__dirname + '/index.html'));
    }
});
const port = process.env.PORT || 8080;
app.listen(port);
```