---
layout: layout
title: REM, REST made easy
---

### REST easy.

Markdown!!!

```javascript
tw('search').get({q: 'fleetwood mac', rpp: 5}, function(err, json) {
    console.log('There are', json.results.length, 'results for Fleetwood Mac. #awesome');
});
// requires authentication:
tw('statuses/update').post({status: message}, function (err, json) {
    console.log(err, json)
})
```