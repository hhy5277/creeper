![Creeper](https://raw.githubusercontent.com/wspl/creeper/master/art/Creeper.png)

## About

Creeper is a *next-generation* crawler which fetches web page by creeper script. As a cross-platform embedded crawler, you can use it for your news app, subscribe program, etc.

## Get Started

#### Installation

```
$ go get github.com/wspl/creeper
```

#### Hello World!

Create `hacker_news.crr`

```
page(@page=1) = "https://news.ycombinator.com/news?p={@page}"

news[]: page -> $("tr.athing")
	title: $(".title a.storylink").text
	site: $(".title span.sitestr").text
	link: $(".title a.storylink").href
```

Then, create `main.go`

```go
package main

import "github.com/wspl/creeper"

func main() {
	c := creeper.Open("./hacker_news.crr")
	c.Array("news").Each(func(c *creeper.Creeper) {
		println("title: ", c.String("title"))
		println("site: ", c.String("site"))
		println("link: ", c.String("link"))
		println("===")
	})
}
```

Build and run. Console will print something like:

```
title:  Samsung chief Lee arrested as S.Korean corruption probe deepens
site:  reuters.com
link:  http://www.reuters.com/article/us-southkorea-politics-samsung-group-idUSKBN15V2RD
===
title:  ReactOS 0.4.4 Released
site:  reactos.org
link:  https://reactos.org/project-news/reactos-044-released
===
title:  FeFETs: How this new memory stacks up against existing non-volatile memory
site:  semiengineering.com
link:  http://semiengineering.com/what-are-fefets/
```