+++
title = "Org-Mode Formatting and General"
description = """
  Test the workaround for wrapping Org headings in HTML tags like
  <kbd>section</kbd> and <kbd>div</kbd>.
  """
date = 2017-07-31
lastmod = 2021-02-19T01:35:25+01:00
tags = ["formatting"]
draft = false
+++

## Markup - Org vs Markdown {#markup-org-vs-markdown}

Below table shows the translation of Org markup to Markdown markup in
the exported `.md` files.

| Org                | Markdown                                                             | In Hugo rendered HTML                    |
|--------------------|----------------------------------------------------------------------|------------------------------------------|
| `*bold*`           | `**bold**`                                                           | **bold**                                 |
| `/italics/`        | `_italics_`                                                          | _italics_                                |
| `=monospace=`      | `` `monospace` ``                                                    | `monospace`                              |
| `~key-binding~`    | `` `key-binding` ``                                                  | <kbd>key-binding</kbd>                   |
|                    | - if `org-hugo-use-code-for-kbd` is nil [default]                    |                                          |
| `~key-binding~`    | `<kbd>key-binding</kbd>`                                             |                                          |
|                    | - if `org-hugo-use-code-for-kbd` is non-nil                          |                                          |
|                    | - Requires **CSS** to render the `<kbd>` tag as something special.   |                                          |
| `+strike-through+` | `~~strike-through~~`                                                 | ~~strike-through~~                       |
| `_underline_`      | `<span class = "underline">underline</span>`                         | <span class="underline">underline</span> |
|                    | - Requires **CSS** to render this `underline` class as an underline. |                                          |


## Hyphens and spaces in categories {#hyphens-and-spaces-in-categories}

The Org tags do not allow spaces. So the trick we use is replace

-   **single** underscore becomes a -
    In Org `@abc_def` becomes Hugo category `abc-def`

-   **double** underscores becomes a spaces.
    An Org tag `@abc__def` becomes Hugo category `abc def`

-   **triple** underscore becomes a \_
    An Org tag `@arb___def` becomes Hugo category `abc_def`


### Prefer Hyphen Categories {#prefer-hyphen-categories}


## Tags - Ensure that certain sections does not become exported {#tags-ensure-that-certain-sections-does-not-become-exported}

By placing your cursor on a heading, press `C-c, C-c` you will assign tags

Tags allows one to assign groupings of the files by writing `:some-tag-name:`
One can also assign tags at the heading of an article with `:@top-tag:`
You can also ensure that certain headings wont be exported by adding the tag: `:noexport:`


## Add comments {#add-comments}

```org
#+begin_description
Test the case where the title contains only the date, making it look
like a Hugo TOML date field.
#+end_description
```


## Math {#math}

Math can be displayed in many ways, either centered directly with `$$ $$` or with LaTeX source blocks:


### TODO {#todo}

\\[x \forall \mathcal{X} \in \\{1, 2, \cdots, n\\}\\]
\\[\sum\_{i=1}^{Q}w\_i^2\\]


## Code {#code}

```python
class GP(gp.models.ExactGP):
    def __init__(self, cov, train_x, train_y):
        super(GP, self).__init__(train_x, train_y, GaussianLikelihood())
        self.mean = gp.means.ConstantMean()
        self.cov = cov

    def forward(self, x):
        return MultivariateNormal(self.mean(x), self.cov(x))

    def predict(self, x):
        """Returns the posterior mean together with
        the boundaries for the 95% credible intervals.
        """
        self.eval()
        with torch.no_grad():
            pred = self.likelihood(self(x))
            lower, upper = pred.confidence_region()

        return pred.mean, lower, upper

    def spectral_density(self, smk) -> MixtureSameFamily:
        """Returns the Mixture of Gaussians over the spectral density
        of the provided spectral mixture kernel."""
        mus = smk.mixture_means.detach().reshape(-1, 1)
        sigmas = smk.mixture_scales.detach().reshape(-1, 1)
        mix = Categorical(smk.mixture_weights.detach())
        comp = Independent(Normal(mus, sigmas), 1)
        return MixtureSameFamily(mix, comp)
```


## Use Org Code markup for `kbd` tag (default behavior) {#use-org-code-markup-for-kbd-tag--default-behavior}

This is the default behavior. So `~C-h f~` will show up as `` `C-h f` ``
and then `<code>C-h f</code>` in the final Hugo generated HTML.

Example:

-   Few of Emacs help keybindings: <kbd>C-h f</kbd>, <kbd>C-h v</kbd>


## Example blocks with line number annotation {#example-blocks-with-line-number-annotation}

-   [Org reference](https://orgmode.org/manual/Literal-examples.html)
-   [Hugo `highlight` shortcode with line numbers](https://gohugo.io/content-management/syntax-highlighting/)


### Default new line number start {#default-new-line-number-start}

{{< highlight text "linenos=table, linenostart=1">}}
line 1
 line 2
{{< /highlight >}}


## Wrapping Org headings in HTML tags {#wrapping-org-headings-in-html-tags}

`ox-hugo` Issue #[160](https://github.com/kaushalmodi/ox-hugo/issues/160)
