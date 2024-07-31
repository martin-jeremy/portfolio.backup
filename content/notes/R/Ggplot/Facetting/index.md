---
title: Facetting and Highlighting
weight: 10
menu:
  notes:
    name: Facetting and Highlighting
    identifier: notes-r-ggplot-facetting
    parent: notes-r-ggplot
    weight: 10
---

<!-- Facetting with ggplot -->
{{< note title="Facetting with ggplot">}}

Code snippet to play with facetting a ggplot. 

A reduced version of [`{starwars}`](https://dplyr.tidyverse.org/reference/starwars.html) will be the toy dataset:

![all](/notes/R/facetting/00.png)

---

**Classical Facetting:**

```r
 ggplot(starwars.light) +
   geom_point(aes(x = height, y = mass, col = species), size = 2.5) +
   facet_wrap(~species)
```

![classical_facets](/notes/R/facetting/01.png)

---

**Facetting with an ALL facet:**

```r
 ggplot(starwars.light) +
   geom_point(aes(x = height, y = mass, col = species), size = 2.5, data = starwars.light) +
   geom_point(aes(x = height, y = mass, col = starwars.light$species), size = 2.5, data = transform(starwars.light, species = 'All')) +
   facet_wrap(~species)
```

![classical_all_facets](/notes/R/facetting/02.png)

---

**Two way facetting:**

Note that I changed `facet_wrap()` to `facet_grid()`

```r
 ggplot(starwars.light) +
   geom_point(aes(x = height, y = mass, col = gender), size = 2.5) +
   facet_grid(gender~species)
```

![two_way_facets](/notes/R/facetting/03.png)

To add an `(all)` margin to the plot, just add `margin = TRUE` in the facet_grid

```r
 ggplot(starwars.light) +
   geom_point(aes(x = height, y = mass, col = gender), size = 2.5) +
   facet_grid(gender~species, margin = TRUE)
```

![two_way_facets_w_margin](/notes/R/facetting/04.png)

{{< /note >}}

<!-- Highlighting with ggplot -->
{{< note title="Highlighting with ggplot">}}

The trick here, consist to initialize the ggplot space with a dataset without the categorical information (here, species):

![all_no_species](/notes/R/facetting/05.png)

---

**Facetting with highlighting:**

```r
 ggplot(select(starwars.light, -species)) +
   geom_point(aes(x = height, y = mass), size = 2.5, col = 'gray') +
   geom_point(aes(x = height, y = mass, col = species), size = 2.5, data = starwars.light) +
   facet_wrap(~species)
```

![highlight_facets](/notes/R/facetting/06.png)

---

**Facetting with highlighting and all panel:**

```r
 ggplot(select(starwars.light, -species)) +
   geom_point(aes(x = height, y = mass), size = 2.5, col = 'gray') +
   geom_point(aes(x = height, y = mass, col = species), size = 2.5, data = starwars.light) +
   geom_point(aes(x = height, y = mass, col = starwars.light$species), size = 2.5, data = transform(starwars.light, species = 'All')) +
   facet_wrap(~species)
```

![highlight_all_facets](/notes/R/facetting/07.png)

---

**Two way highlighting:**

Note that I changed `facet_wrap()` to `facet_grid()`

```r
 ggplot(select(starwars.light, -gender)) +
   geom_point(aes(x = height, y = mass), size = 2.5, col = 'gray') +
   geom_point(aes(x = height, y = mass, col = gender), size = 2.5, data = starwars.light) +
   facet_grid(gender~species)
```

![two_way_facets](/notes/R/facetting/08.png)

To add an `(all)` margin to the plot, just add `margin = TRUE` in the facet_grid

```r
 ggplot(select(starwars.light, -gender)) +
   geom_point(aes(x = height, y = mass), size = 2.5, col = 'gray') +
   geom_point(aes(x = height, y = mass, col = gender), size = 2.5, data = starwars.light) +
   facet_grid(gender~species, margin = TRUE)
```

![two_way_facets_w_margin](/notes/R/facetting/09.png)

{{< /note >}}