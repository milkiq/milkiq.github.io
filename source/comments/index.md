---
title: comments
date: 2018-01-24 20:29:19
---

<div id="container"></div>
<link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
<script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
<script>
var gitment = new Gitment({
  id: 'comments', // 可选。默认为 location.href
  owner: 'milkiq',
  repo: 'milkiq.github.io',
  oauth: {
    client_id: 'b27ced273a4edf430541',
    client_secret: 'cd6a2c21239f948471d7eb434290b41b89ec0ca7',
  },
})
gitment.render('container')
</script>