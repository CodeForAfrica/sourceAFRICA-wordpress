# sourceAFRICA WordPress plugin

The sourceAFRICA WordPress plugin lets you embed [sourceAFRICA](https://sourceafrica.net/) resources into WordPress content using [shortcodes](https://codex.wordpress.org/Shortcode_API).

    [sourceafrica url="https://sourceafrica.net/documents/19450-everest.html"]

This plugin is based on [DocumentCloud](https://www.documentcloud.org)'s WordPress plugin and is extended to support sourceAFRICA.

## Installation

1. Upload the contents of the plugin to `wp-content/plugins/sourceafrica`
2. Activate the plugin through the "Plugins" menu
3. In your posts, embed documents or notes using the sourceAFRICA button or the `[sourceAFRICA]` shortcode
4. Optional: Set a default width/height for all DocumentCloud embeds (which can be overridden on a per-embed basis with the `height/width` attributes) at Settings > DocumentCloud. (This default width will only be used if you set `responsive="false"` on an embed.)

**Using with DocumentCloud Plugin:** If you're currently using the DocumentCloud's plugin (from which this plugin was built), you'll NOT need to deactivate or delete it before installing this plugin.

## Usage

This plugin allows you to embed sourceAFRICA resources using either the raw URL on its own line:

    Here's something you should really take a look at:
    
    https://sourceafrica.net/documents/19450-everest.html
    
    Isn't that interesting?

Or a custom shortcode:

    [sourceafrica url="https://sourceafrica.net/documents/19450-everest.html"]

When you save, WordPress fetches and stores the actual embed code HTML from the sourceAFRICA servers using oEmbed. You can freely toggle between visual and HTML mode without mangling embed code, and your embed will always be up to date with the latest embed code.

By default, documents will have a responsive width (it will narrow and widen as necessary to fill available content area) and use the theme's default height. If you want to override this, you can either set `responsive="false"` or explicitly set a `width`:

    [sourceafrica url="https://sourceafrica.net/documents/19450-everest.html" width="600"]

You can set your own defaults in Settings > sourceAFRICA, but default widths will be ignored unless `responsive` is disabled:

    [sourceafrica url="https://sourceafrica.net/documents/19450-everest.html" responsive="false"]

To embed a note, just use any note-specific URL. Notes ignore `width/height` and always act responsively:

    [sourceafrica url="https://sourceafrica.net/documents/19450-everest.html"]

Here's the full list of embed options you can pass via shortcode attributes; some are specific to the type of resource you're embedding.

### All resources (documents and notes):

- `url` (**required**, string): Full URL of the sourceAFRICA resource.
- `container` (string): ID of element to insert the embed into; if excluded, embedder will create its own container.

### Documents only:

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

## Caching

Ideally, when WordPress hits our oEmbed service to fetch the embed code, it would obey the `cache_age` we return. Despite [conversation](https://core.trac.wordpress.org/ticket/14759) around this, it doesn't seem to.

Instead, it lets us choose between no cache at all (so *every pageload* triggers a call to our oEmbed service to get the embed code) or a supposed 24-hour cache stored in the `postmeta` table. Unfortunately, [DocumentCloud's tests](https://github.com/documentcloud/wordpress-documentcloud/issues/20) seem to show this cache is never expired, which means we can choose between no cache (thus possibly DDOSing ourselves) or a permanent cache (thus possibly having stale embed codes). We've chosen the latter; hopefully this cache does eventually expire, and our embed codes shouldn't change that often anyway.

If you find yourself absolutely needing to expire the cache, though, you have two choices:

1. Delete the appropriate `_oembed_*` rows from your `postmeta` table.
2. Modify the shortcode attributes for the embed, since this is recognized as a new embed by WordPress.

## Changelog

### 0.1
* Initial release. v0.3.1 of DocumentCloud's Plugin.

## License and History

The sourceAFRICA WordPress plugin is [GPLv2](http://www.gnu.org/licenses/gpl-2.0.html). Initial development of this plugin by Chris Amico (@eyeseast) supported by [NPR](http://www.npr.org) as part of [StateImpact](http://stateimpact.npr.org) project. Development continued by Justin Reese (@reefdog) at [DocumentCloud](https://www.documentcloud.org/) and extended by [Code for Africa](http://www.codeforafrica.org) to support [sourceAFRICA](https://sourceafrica.net).
