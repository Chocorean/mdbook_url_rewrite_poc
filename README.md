# Addressing https://github.com/rust-lang/mdBook/issues/2958

While reviewing [#3046](https://github.com/rust-lang/mdBook/pull/3046), I realized the original issue could have been closed if OP knew they could use the `resource` helper.

In [`theme/fonts/fonts.css`](theme/fonts/fonts.css), the font url is declared with `resource`:

```css
@font-face {
    font-family: 'custom-font';
    src: url('{{ resource "fonts/Roboto.ttf" }}') format('truetype');
}
```

Because the font lives under `./theme/fonts/`, it will automatically be added to the list of static files, and get a fingerprint.
It also unlocks the `resource` helper to find its name in the output files.

I believe using `resource` inside the `url()` css function resolves [the original issue](https://github.com/rust-lang/mdBook/issues/2958) and renders [this PR](https://github.com/rust-lang/mdBook/issues/2958) irrelevant.
