# ApeSmit

## What is ApeSmit?
Based on http://www.florian-diesch.de/software/apesmit/.

ApeSmit is a very simple Python module to create XML sitemaps as defined at http://www.sitemaps.org. ApeSmit doesn’t contain any web spider or something like that, it just writes the data you provide to a file using the proper syntax.

“apesmit” is an anagram of “sitemap”

## Status
ApeSmit is alpha software. So far it seems to work for me but it may have severe bugs I didn’t noticed yet. Use it at your own risk.

ApeSmit is still under development and the API may change in the future.

## Requirements
ApeSmit only needs the Python standard lib

## Usage
First we create an instance of SiteMap:
```
sm=Sitemap(changefreq='weekly')
```
The changefreq keyword sets a default value for that parameter.

Now we add some URL’s to our sitemap:
```
sm.add('http://www.example.com/')
```
We may use some parameters:
```
sm.add('http://www.example.com/news/', changefreq='daily',
                                        priority=1.0,
                                        lastmod='1891-1-1')
```
There’s a shortcut for URL’s that changed today:
```
sm.add('http://www.example.org/about.html', lastmod='today')
```
That’s all for now. Next we need a file to write the sitemap in:
```
out=open('sitemap.xml', 'w')
```
Now we write our sitemap and then close the file:
```
sm.write(out)
out.close()
```
Or we can write a Sitemap index file:
```
sm.write(out, 'sitemapindex')
out.close()
```

And that’s the content of our shiny new sitemap:
```
<?xml version='1.0' encoding='UTF-8'?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9
        http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
        xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
 <url>
  <loc>http://www.example.com/</loc>
  <changefreq>weekly</changefreq>
 </url>
 <url>
  <loc>http://www.example.com/news/</loc>
  <lastmod>1891-1-1</lastmod>
  <changefreq>daily</changefreq>
  <priority>1.0</priority>
 </url>
 <url>
  <loc>http://www.example.org/about.html</loc>
  <lastmod>2008-04-03</lastmod>
  <changefreq>weekly</changefreq>
 </url>
</urlset>
```
