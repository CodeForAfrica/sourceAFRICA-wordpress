=== DocumentCloud ===
Contributors: chrisamico, reefdog, davidlemayian
Tags: sourceafrica, documentcloud, documents, journalism, reporting, research
Requires at least: 3.2
Tested up to: 4.2.2
Stable tag: trunk
License: GPLv2
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Embed sourceAFRICA resources in WordPress content.

== Description ==

[sourceAFRICA](https://sourceafrica.net/) is a service provided by [African Network of Centers for Investigative Reporting](http://investigativecenters.org) that allows journalists to analyze, annotate, and publish documents, hosted by [Code for Africa](http://www.codeforafrica.org]. Initial development of this plugin supported by [NPR](http://www.npr.org) as part of [StateImpact](http://stateimpact.npr.org) project and continues to be supported by [DocumentCloud](https://www.documentcloud.org).

This plugin allows you to embed sourceAFRICA resources using either the raw URL on its own line:

    Here's something you should really take a look at:
    
    https://sourceafrica.net/documents/19450-everest.html
    
    Isn't that interesting?

Or a custom shortcode:

    [sourceafrica url="https://sourceafrica.net/documents/19450-everest.html"]

When you save, WordPress fetches and stores the actual embed code HTML from the sourceAFRICA servers using oEmbed. You can freely toggle between visual and HTML mode without mangling embed code, and your embed will always be up to date with the latest embed code.

By default, documents will have a responsive width (it will narrow and widen as necessary to fill available content area) and use the theme's default height. If you want to override this, you can either set `responsive="false"` or explicitly set a `width`:

    [sourceafrica url="https://sourceafrica.net/documents/19450-everest.html" width="600"]

You can set your own defaults in Settings > DocumentCloud, but default widths will be ignored unless `responsive` is disabled:

    [documentcloud url="https://sourceafrica.net/documents/19450-everest.html" responsive="false"]

To embed a note, just use any note-specific URL. Notes ignore `width/height` and always act responsively:

    [documentcloud url="https://sourceafrica.net/documents/19450-everest.html#document/p1/a142"]

Here's the full list of embed options you can pass via shortcode attributes; some are specific to the type of resource you're embedding.

**All resources (documents and notes):**

- `url` (**required**, string): Full URL of the sourceAFRICA resource.
- `container` (string): ID of element to insert the embed into; if excluded, embedder will create its own container.

**Documents only:**

- `height` (integer): Height (in pixels) of the embed.
- `width` (integer): Width (in pixels) of the embed. If used, will implicitly set `responsive="false"`.
- `responsive` (boolean): Use responsive layout, which dynamically adjusts width to fill content area. Defaults `true`.
- `responsive_offset` (integer): Distance (in pixels) to vertically offset the viewer for some responsive embeds.
- `default_page` (integer): Page number to have the document scroll to by default.
- `default_note` (integer): ID of the note that the document should highlight by default.
- `notes` (boolean): Show/hide notes:
- `search` (boolean): Hide or show search form.
- `sidebar` (boolean): Hide or show sidebar. Defaults `false`.
- `pdf` (boolean): Hide or show link to download original PDF. Defaults `true`.
- `text` (boolean): Hide or show text tab. Defaults `true`.
- `zoom` (boolean): Hide or show zoom slider.
- `format` (string): Indicate to the theme that this is a wide asset by setting this to `wide`. Defaults `normal`.

You can read more about publishing and embedding sourceAFRICA resources on https://sourceafrica.net/help/publishing.

== Installation ==

1. Upload the contents of the plugin to `wp-content/plugins/documentcloud`
2. Activate the plugin through the "Plugins" menu
3. In your posts, embed documents or notes using the sourceAFRICA button or the `[sourceAFRICA]` shortcode
4. Optional: Set a default width/height for all sourceAFRICA embeds (which can be overridden on a per-embed basis with the `height/width` attributes) at Settings > sourceAFRICA. (This default width will only be used if you set `responsive="false"` on an embed.)

**Using with DocumentCloud Plugin:** If you're currently using the DocumentCloud's plugin (from which this plugin was built), you'll NOT need to deactivate or delete it before installing this plugin.

== Changelog ==

= 0.1 =
* Initial release. v0.3.1 of DocumentCloud's Plugin.

== Upgrade Notice ==

= 0.1 =
Nada
