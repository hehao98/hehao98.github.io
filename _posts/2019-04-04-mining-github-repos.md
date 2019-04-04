---
title: 'Mining GitHub Repository Information using the Official REST API'
date: 2019-04-04
permalink: /posts/2019/04/mining-github-repo/
tags:
  - English
  - Python
  - Mining Software Repositories
---

GitHub provides a (not very convinent and well documented) HTTP API for requesting information from GitHub. We can use `https://api.github.com/search/repositories` for requesting repository information in JSON format. You can apply various search conditions and sort them if necessary. For example, if you want to collect 1000 most starred repositories whose language is Java, you can use the following request. 

```
https://api.github.com/search/repositories?q=language:java&sort=stars&order=desc
```

See the following links for a complete documentation.

1. [https://developer.github.com/v3/search/](https://developer.github.com/v3/search/)
2. [https://help.github.com/en/articles/searching-for-repositories](https://help.github.com/en/articles/searching-for-repositories)

However, there are several restrictions (restriction 1 is not documented):

1. Only one page of results (30) are returned for each request
2. You are limited to send only 10 requests per minute (if authenticated, 30 requests per minute).
3. You can only get up to 1000 search results for one set of given conditions.

Therefore, you cannot get more than 1000 results for a given search request, limiting the scale of possible analysis. You also cannot send more than 10 requests per minute. Also, you have to fetch results page by page using the `page` parameter, using this list of URL

```
https://api.github.com/search/repositories?q=language:java&sort=stars&order=desc&page=1
https://api.github.com/search/repositories?q=language:java&sort=stars&order=desc&page=2
...
https://api.github.com/search/repositories?q=language:java&sort=stars&order=desc&page=34
```

Note that the maximum page number is 34 due to the 1000 result restriction.

If you made any error during the request, the error message will be in the `message` field in the returned JSON object. Otherwise, the array of repository information will be in the `item` field.

## Example Implementation in Python

```python
'''
Returns a json object that contains information of GitHub repos returned by GitHub REST v3 API

Example search url: https://api.github.com/search/repositories?q=language:java&sort=stars&order=desc
This URL collects GitHub Java project sorted by starts in descending order.
Remember that:
1. The results are returned in pages, so you have to fetch them page by page
2. You are limited to send only 10 requests per minute
3. You can only get up to 1000 search results

Reference Documentation: 
https://developer.github.com/v3/search/
https://help.github.com/en/articles/searching-for-repositories
'''
def get_repolist_by_stars(num=30, lang=''):
    url = 'https://api.github.com/search/repositories'
    params = {'q':'stars:>1000', 'sort':'stars', 'order':'desc', 'page':'1'}
    repolist = []

    if lang != '':
        params['q'] = 'language:' + lang

    print('Sending HTTP requests to GitHub, may need several minutes to complete...')

    for i in range(1, int(num / 30) + 2):
        params['page'] = str(i)
        json = requests.get(url, params).json()
        if json['items'] == None:
            print('Error: No result in page ' + str(i) + '!') 
            print('Message from GitHub: ' + str(json.get('message')))

        repolist.extend(json['items'])

        print('Downloaded repository information in page ' + str(i))
        time.sleep(7) # This rate is imposed by GitHub

    return repolist[0:num]
```

