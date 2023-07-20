# Digital Publishing System Framework

_v1.0.0_

This is a specification for requirements for a system for publishing documentation, papers, articles, books, blogs, and other content online. Its focus is on creating Open Content and Open Educational Resources that provides anyone with a free and perpetual permission to Retain, Revise, Remix, Reuse, and Redistribute it[^oer].

[^oer]: Defining the "Open" in Open Content and Open Educational Resources was written by David Wiley and published freely under a Creative Commons Attribution 4.0 license at http://opencontent.org/definition/

Its purpose is to establish a standard for building Digital Publishing Systems, based on established standards, and apply this to broad and narrow features such systems should support, and the requirements therein. It is opinionated and declarative, and not applicable to all publishing systems.

## <a name="specification"></a>Specification

The following describes functional features and technical requirements that the publishing system must supply or support, using common [imperatives](#imperatives). Feature Requirements describe high-level concepts and standards of the system, and Technical Requirements describe lower-level details of the implementations. As such, the System is:

> A _System_ is a set of doctrines, ideas, or principles usually intended to explain the arrangement or working of an organized whole -- adapted from [Merriam-Webster](https://www.merriam-webster.com/dictionary/system)

And Implementations are:

> An _Implementation_ is an act or instance of constructing something: the process of making something active or effective -- adapted from [Merriam-Webster](https://www.merriam-webster.com/dictionary/implementation)

### <a name="feature-requirements"></a>Feature Requirements

| Feature                                                                 | MUST | SHOULD | MAY |
| ----------------------------------------------------------------------- | ---- | ------ | --- |
| [Open Formats using Open Standards](#open-formats-using-open-standards) | ✖    |        |     |
| [Interoperable standards](#interoperable-standards)                     | ✖    |        |     |
| [Maintainability](#maintainability)                                     | ✖    |        |     |
| [Extensible Components](#extensible-components)                         | ✖    |        |     |
| [Flexible Layouts and templates](#flexible-layouts-and-templates)       | ✖    |        |     |
| [Structured and Responsive Styles](#structured-and-responsive-styles)   | ✖    |        |     |
| [Progressive enhancement](#progressive-enhancement)                     | ✖    |        |     |

#### <a name="open-formats-using-open-standards"></a>Open Formats using Open Standards

Digital publishing systems have always relied on standardized formats[^standardized-publishing-formats] -- everything from [TeX](#abbr-tex) to [XML](#abbr-xml) to [HTML](#abbr-html) -- but the standardization of content quickly and slowly falls apart to allow for special- or edge-cases of use. These open formats are not used uniformly even within the ecosystem of a single publishing system. The modern solution to this, supported by not so much technological as standards-focused advancement, is going back to plain text.

[^standardized-publishing-formats]: For an overview, see http://fileformats.archiveteam.org/wiki/Electronic_Publishing_formats

Implementations MUST support [Markdown](https://en.wikipedia.org/wiki/Markdown) as a format for content. It is strictly preferred for its simplicity as a standard, and flexibility and extensibility from variants that enhance but does not degrade the core of it. [CommonMark](https://commonmark.org/)[^djot] is the most applicable specification of Markdown, which for example [GitHub Flavored Markdown](https://github.github.com/gfm/) implements. Further, as plain text with a plain syntax, it is transferable between different implementations of the system.

[^djot]: An even stricter, less ambiguous, but more full-featured specification is Djot, see https://github.com/jgm/djot

#### <a name="interoperable-standards"></a>Interoperable standards

The [Open Formats using Open Standards](#open-formats-using-open-standards) and [Compatible Interoperability](#compatibile-interoperability) features implicitly prohibit vendor lock-in for content, which is the typical result when [CMS](#abbr-cms)' define and maintain their own standards for how content is implemented. An interoperable standard -- "a characteristic of a product or system to work with other products or systems", from [Wikipedia](https://en.wikipedia.org/wiki/Interoperability) -- is warranted. Being able to use the same content, structured in the same way, across implementations makes the cost of trying out new systems much lower, and [feature-parity](https://martinfowler.com/articles/patterns-legacy-displacement/feature-parity.html) can be broadly achieved. In this regard content and metadata is ephemeral, and Markdown with YAML FrontMatter becomes a de facto standard.

The implementation thereafter enhances rendering and associations between content, such that it becomes more [accessible](#accessible). This embraces and facilitates the principle "[Create Once, Publish Everywhere](https://web.archive.org/web/20170522060044/https://www.programmableweb.com/news/cope-create-once-publish-everywhere/2009/10/13)".

#### <a name="maintainability"></a>Maintainability

As digital technologies advance, so do standards and possibilities. What works today will not tomorrow, as any experienced web developer knows. However, major steps have been taken in making it easy for developers to track [feature-support](https://caniuse.com/ciu/about) in [Evergreen-browsers](#evergreen). As such, implementations MUST with each release clearly indicate the date of the release, and SHOULD describe what version of the [Browserslist](https://browsersl.ist/) it was tested with.

No requirement can be imposed on implementers for how or how long they should support and maintain their implementation, but making them [Open Source](#open-source-source-available) makes their further development possible and allows an ecosystem of other developers to contribute more easily.

#### <a name="extensible-components"></a>Extensible Components

The system for publishing a site MUST differentiate between Core and Added functionality. Given that its main purpose is publishing content digitally, this functionality mostly concerns how documents appear and behave in a web browser. These are termed _Components_, and _Core Components_ should be **general** and flexible enough to be adapted by _Added Components_ into more **specific** variants, which can further be altered by _Extra Components_ into **special** types.

##### <a name="core-components"></a>Core Components

Common Page Types that implementations MUST include:

- Default Page: A generic type of Page
- Listing: A generic type for displaying a Collection of Pages
- Index: A type for displaying a multiple Collections of Pages
- Docs: A type for rendering Documentation, especially hierarchically-structured content
- Article: A template for an article, a paper, a document, or other type of standalone content
- Search: A helper-type which implements search-fields

Additionally, nested Page Types should extend the Layout and Style through templating, such that they remain extensible and reusable in context. For example, a `Default Page` may warrant different treatment as a part of a set of documentation as opposed to a blog post.

##### <a name="added-components"></a>Added Components

Page Types that implementations SHOULD include:

- Blog: A replica of `Index`, but targeted to chronological sorting and categorical filtering
- Post: A subset of `Default Page`, but includes the option for a hero-image
- Diagram: A type type for rendering structured diagrams

##### <a name="extra-components"></a>Extra Components

Page Types that implementations MAY include:

- Book: A replica of `Listing`, used for organization of chapters
- Chapter: A replica of `Listing`, used for organization of pages
- Handout: A subset of `Article`, optimized for distributable notes -- such as [Tufte Handouts](https://edwardtufte.github.io/tufte-css/)
- CV: A type for rendering a standalone resumé

Of course, there are no limits to how much functionality implementations may offer through added Page Types, but the above describes some specific sets.

#### <a name="flexible-layouts-and-templates"></a>Flexible Layouts and templates

Implementations MUST use a [templating engine](http://www.simple-is-better.org/template/) for [Layouts](#abbr-layout). That is, a standardized method of turning data -- most often plain text -- into [HTML](#abbr-html), supporting reusable Layouts in the form of templates and template partials, variables and functions, text replacement, file inclusion, conditional evaluation and loops. This is essential for separating presentation from logic, and lowering the entry for users. [Many such engines are available](#abbr-layout), used by many Content Management Systems ([CMS](#abbr-cms)), for many programming-languages. A CMS will usually include one or more of these by default.

#### <a name="structured-and-responsive-styles"></a>Structured and Responsive Styles

Implementations MUST have separate stylesheets ([CSS](#abbr-css)) for structure and styling. One stylesheet should define all structural aspects of the semantic elements that the HTML lays out -- shaping the appearance of the overall Layout. The design MUST be [responsive](#abbr-responsive-design), to accommodate different devices viewing the same Layout in a coherent and recognizable manner. Subsequent stylesheets -- distinct Styles -- follow a basic principle: They apply color, fonts, or other rules that accentuate structural elements. Building and maintaining a consistent [Style Guide](http://styleguides.io/) makes it easier to adopt and adapt Layouts and Styles.

#### <a name="progressive-enhancement"></a>Progressive enhancement

Implementations MUST be built on the design principle of Progressive Enhancement:

> [A] strategy in web design that puts emphasis on web content first, allowing everyone to access the basic content and functionality of a web page, whilst users with additional browser features or faster Internet access receive the enhanced version" -- [Wikipedia](https://en.wikipedia.org/wiki/Progressive_enhancement)

In practice, this means that the presentation of and the content itself must be strictly separated, such that the availability of the content is not limited by how the presentation of it is built. This ties in with the [Open Formats using Open Standards](#open-formats-using-open-standards) feature: Plain text documents are maximally available to all users and clients, and [HTML](#abbr-html) enhances the presentation of these by structuring them within a Layout. [CSS](#abbr-css) further styles it to enhance how readable it is, and finally [JS](#abbr-js) adds enhanced functionality such as interactivity.[^gracefuldegradation]

[^gracefuldegradation]: In many ways, Progressive Enhancement is a reversal of the approach of Graceful Degradation, see https://www.w3.org/wiki/Graceful_degradation_versus_progressive_enhancement
