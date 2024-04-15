---
layout: page
title: About
---

I'm a software engineer and work mostly in the backend with **Java**. I think web technologies are also not to be forgotten. The complexity *(from my view)* of the web is for me better to handle with **Angular** and **TypeScript**.

On this website I will write down some tricky things I encounter in my daily work and other sideprojects *(when I get around to it again)*. It should serve as a notebook for me. I would be even more pleased if they were helpful tips for you too.

[LinkedIn](https://linkedin.com/in/rslkvk)
[Github](https://github.com/rslkvk)

---
#### Here you can search for some topics: 


<style>
	#search-container {
	    max-width: 100%;
	}

	input[type=text] {
		font-size: normal;
	    outline: none;
	    padding: 1rem;
		background: rgb(236, 237, 238);
	    width: 100%;
		-webkit-appearance: none;
		font-family: inherit;
		font-size: 100%;
		border: none;
	}
	#results-container {
		margin: .5rem 0;
	}
</style>

<!-- Html Elements for Search -->
<div id="search-container">
<input type="text" id="search-input" placeholder="Search...">
<ol id="results-container"></ol>
</div>

<!-- Script pointing to search-script.js -->
<script src="/search.js" type="text/javascript"></script>

<!-- Configuration -->
<script type="text/javascript">
SimpleJekyllSearch({
  searchInput: document.getElementById('search-input'),
  resultsContainer: document.getElementById('results-container'),
  json: '/search.json',
  searchResultTemplate: '<li><a href="{url}" title="{desc}">{title}</a></li>',
  noResultsText: 'No results found',
  limit: 10,
  fuzzy: false,
  exclude: ['Welcome']
})
</script>
