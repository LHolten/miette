<a name="0.10.0"></a>
## 0.10.0 (2021-08-17)

Lots of goodies in this release! I'm working hard on the [1.0.0
Roadmap](https://github.com/zkat/miette/issues/10), so things are changing
pretty quick, and I thought it would be nice to release this checkpoint.
#### Bug Fixes

* **protocol:**  keep the owned spans ([49151bb0](https://github.com/zkat/miette/commit/49151bb0950c0db9d2743c8fb78dcacfc27bc750))

#### Features/Breaking Changes

* **derive:**  Allow anything Clone + Into<SourceSpan> to be used as a Span ([385171eb](https://github.com/zkat/miette/commit/385171eb8178ce2e7d6d2d2849b78e0f09feb721))
* **offsets:**
  *  nice utility function to get an offset from a Rust callsite ([26f409c5](https://github.com/zkat/miette/commit/26f409c5252c3fda5ead140eb4d5ec282f47f0f7))
  *  utility function for converting from line/col to offset ([75c23127](https://github.com/zkat/miette/commit/75c2312755bf714c112badf6310b2bff1633f6bc))
  *  more utility From impls for SourceSpan ([95200366](https://github.com/zkat/miette/commit/95200366a1639b0b729db460ae1e50cce6fee9de))
* **protocol:**
  *  add Source impls for Cow and Arc ([53074d34](https://github.com/zkat/miette/commit/53074d3488e1404331fc1ca3c5e068ac57e9a852))
  *  reference-based DiagnosticReport! ([f390520b](https://github.com/zkat/miette/commit/f390520b45823d65055f9f872016e4ee27c0c20a))



<a name="0.9.0"></a>
## 0.9.0 (2021-08-17)

Yay new version already! A pretty significant API change, too! ��

#### Breaking Changes

`SourceSpan`s have changed a bit: for one, they're based on offset/length now,
instead of start/end. For two, they have a new `Option<String>` field,
`label`, which is meant to be used by reporters in different contexts. For
example, highlight snippets will use them as the labels for underlined
sections of code, while the snippet context will use the label as the "file
name" for the Source they point to.

  * **protocol:** new SourceSpans with labels ([acfeb9c5](https://github.com/zkat/miette/commit/acfeb9c5b0e390c924194ee0363fc49fa8defbac))

#### Bug Fixes

* **derive:**  allow unused variables for the snippets method ([f704d6a9](https://github.com/zkat/miette/commit/f704d6a9ae971dfe61fe9a0e0b4a1a7f98fd37bc))

#### Features

* **protocol:** implement From<(usize, usize)> for SourceSpan ([36b86df9](https://github.com/zkat/miette/commit/36b86df9f51984405efa6f38be8bbb984d605207))



<a name="0.8.1"></a>
## 0.8.1 (2021-08-17)

Just a small bump to update the readme (and docs.rs in the process) with the
new snippet derive stuff. No notable changes.

<a name="0.8.0"></a>
## 0.8.0 (2021-08-17)

You can full-on use `#[derive(Diagnostic)]` to define snippets now. That's a
big deal.

#### Features

* **derive:**  Support for deriving snippet method (#18) ([f6e6acf2](https://github.com/zkat/miette/commit/f6e6acf2d2c301fd411c7c9c4b63a2b19aa69242))

<a name="0.7.0"></a>
## 0.7.0 (2021-08-16)

Welp. `0.6.0` was basically completely broken, so I tore out the
`darling`-based derive macros and rewrote the whole thing using `syn`, and
things are much better now!

There's still a few bits and bobs to add, like snippets (oof. big.), and full
help format string support (they don't quite work in enums right now), but
otherwise, this is pretty usable~

#### Features

* **derive:**  improved derive support, including partial help format string support! ([9ef0dd26](https://github.com/zkat/miette/commit/9ef0dd261fa537b280f32ea6f149785a69e33938))

#### Bug Fixes

* **derive:**  move to plain syn to fix darling issues ([9a78a943](https://github.com/zkat/miette/commit/9a78a943950078c879a1eb06baf819348139e1de))


<a name="0.6.0"></a>
## 0.6.0 (2021-08-15)

We haz a basic derive macro now!

#### Features

* **derive:**  added basic derive macro ([0e770270](https://github.com/zkat/miette/commit/0e7702700de8a4cd9022d660aaf363b735943d55))


<a name="0.5.0"></a>
## 0.5.0 (2021-08-14)

I decided to yank some handy (optional) utilities from a project I'm using
`miette` in. These should make using it more ergonomic.

#### Features

* **utils:**  various convenience utilities for creating and working with Diagnostics ([a9601368](https://github.com/zkat/miette/commit/a960136802834bd3741ef637d91f73287870b1ad))


<a name="0.4.0"></a>
## 0.4.0 (2021-08-11)

Time for another (still experimental!) change to `Diagnostic`. It will
probably continue to change as miette gets experimented with, until 1.0.0
stabilizes it. But for now, expect semi-regular breaking changes of this kind.

Oh and I tracked down a rogue `\n` that was messing with the default reporter
and managed to get out of it with at least some of my sanity.

#### Breaking Changes

* **protocol:**  Simplify protocol return values further ([02dd1f84](https://github.com/zkat/miette/commit/02dd1f84d45c01fb4de2d31c158a7b6e08455f72), breaks [#](https://github.com/zkat/miette/issues/))

#### Bug Fixes

* **reporter:**
  *  fix reporter and tests... again ([d201dde4](https://github.com/zkat/miette/commit/d201dde4b559a2baa4259a0845582a5d14453c5a))
  *  fix extra newline after header ([0d2e3312](https://github.com/zkat/miette/commit/0d2e3312a4a262e99a131bc893097d295e59e8ca))


<a name="0.3.1"></a>
## 0.3.1 (2021-08-11)

This is a tiny release to fix a reporter rendering bug.

#### Bug Fixes

* **reporter:**  fix missing newline before help text ([9d430b6f](https://github.com/zkat/miette/commit/9d430b6f477fd8991ce217dffdbce8fbd28dcd7e))



<a name="0.3.0"></a>
## 0.3.0 (2021-08-08)

This version is the result of a lot of experimentation with getting the
`Diagnostic` API right, particularly `Diagnostic::snippets()`, which is
something that should be writable in several different ways. As such, it
includes some breaking changes, but they shouldn't be too hard to figure out.

#### Breaking Changes

* **protocol:**
  *  improvements to snippets API ([3584dc60](https://github.com/zkat/miette/commit/3584dc600c2b8b0f84a2a0c59856da9a9dc7fbab))
  *  help is a single Display ref now. ([80e7dabb](https://github.com/zkat/miette/commit/80e7dabbe450d4a78ed18174e2a383a6a1ed0557))

#### Bug Fixes

* **tests:**  updating tests ([60bdf47e](https://github.com/zkat/miette/commit/60bdf47e297999b48345b39ba1a3aacbbf79e6fc))

<a name="0.2.1"></a>
## 0.2.1 (2021-08-05)

I think this is the right thing to do re: From!

#### Bug Fixes

* **protocol:**  fix the default From<:T Diagnostic> implementation to cover more cases. ([781a51f0](https://github.com/zkat/miette/commit/781a51f03765c7351a95b34e8391f6a0cf5fc37c))

<a name="0.2.0"></a>
## 0.2.0 (2021-08-05)

Starting to get some good feedback on the protocol and APIs, so some improvements were made.

#### Breaking changes

You might need to add `+ Send + Sync + 'static` to your `Box<dyn Diagnostic>`
usages now, since `Diagnostic` no longer constrains on any of them.

Additionally, `Diagnostic::help()`, `Diagnostic::code()`, and `SpanContents`
have had signature changes that you'll need to adapt to.

* **protocol:**  protocol improvements after getting feedback ([e955321c](https://github.com/zkat/miette/commit/e955321cbd67372dfebb71a829ddb89baf9b169a))
* **protocol:**  Make use of ? and return types with Diagnostics more ergonomic ([50238d75](https://github.com/zkat/miette/commit/50238d75a2db2dccbe2ae2cba78d0dd6eac4ef2a))

<a name="0.1.0"></a>
## 0.1.0 (2021-08-05)

I'm really excited to put out this first release of `miette`! This version
defines the current protocol and includes a basic snippet reporter. It's fully
documented and ready to be used!

_Disclaimer_: This library is still under pretty heavy development, and you should only use this if you're interested in using something experimental. Any and all design comments and ideas are welcome over on [GitHub](https://github.com/zkat/miettee)

#### Bug Fixes

* **api:**  stop re-exporting random things wtf??? ([2fb9f93c](https://github.com/zkat/miette/commit/2fb9f93cbf02c4d41a5538e98c8bea72f40c5430))
* **protocol:**  use references for all return values in Diagnostic ([c3f41b97](https://github.com/zkat/miette/commit/c3f41b972da0e89220e7d9de08f420912ec8973a))

#### Features

* **protocol:**  sketched out a basic protocol ([e2387ce2](https://github.com/zkat/miette/commit/e2387ce2edd4165d04f47a084f3f1492a5de8d9d))
* **reporter:**  dummy reporter implementation + tests ([a437f445](https://github.com/zkat/miette/commit/a437f44511768e52cfedd856b5b1432c0716f378))
* **span:**  make span end optional ([1cb0ad38](https://github.com/zkat/miette/commit/1cb0ad38524696a733f6134092ffd998f76fb142))



<a name="0.0.0"></a>
## 0.0.0 (2021-08-03)

Don't mind me, just parking this crate name.

