---
layout: page
title: SEARCH
---

<!-- HTML elements for search -->
<input type="text" id="search-input" placeholder="搜索博客文章 - 输入标题/相关内容/日期/Tags.." style="width:370px;"/>
<ul id="results-container"></ul>

<!-- script pointing to jekyll-search.js -->
<script src="/js/simple-jekyll-search.min.js"></script>

<script>
SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '/search.json',
    searchResultTemplate: '<li><a href="{url}" title="{desc}">{title}</a></li>',
    noResultsText: '抱歉，没有搜索到文章',
    limit: 20,
    fuzzy: false
  })
</script>
