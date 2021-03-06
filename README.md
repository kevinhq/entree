# entree.rb

Entree is a ruby gem allowing accessibility audits to be run on URLs or files,
from the command line or within your Ruby applications.

This library was copied from Cameron Cundiff's (@ckundo) excellent
[access_lint.rb](https://github.com/accesslint/accesslint.rb) project. It has
been renamed to reflect what it's attempting to provide: entrance to the web for
everyone.

## About

Entree uses the
[HTML_CodeSniffer](https://github.com/squizlabs/HTML_CodeSniffer) client-side JS
application to make assertions on the DOM via PhantomJS. The rules that are applied are [listed below](#rules).

## Installation

First, install PhantomJS ([full guide](http://phantomjs.org/)). On OS X:

    $ brew install phantomjs

Then install the rubygem:

    $ gem install entree

## Usage

### Command Line

From the command line, specify a url or filename to be audited:

    $ entree audit http://archaccessibility.com # url or a path to a file
    # results ...

### Ruby

Run the audit from a Ruby application like so

    $ irb
    > require 'entree'
    => true
    > Entree::Audit.new('http://archaccessibility.com').run
    => results ...

### Results Object

```
{
  "ERROR"=>[
    {
      "type"=>"ERROR",
      "code"=>"WCAG2AA.Principle4.Guideline4_1.4_1_2",
      "nodeName"=>"input",
      "id"=>"#mce-EMAIL",
      "msg"=>"This email input element does not have a name available to an accessibility API. Valid names are: element content.",
      "outerHTML"=>"<input type=\"email\" value=\"\" name=\"EMAIL\" class=\"required email form-control\" id=\"mce-EMAIL\" placeholder=\"Email address\"></input>",
      "techniques"=>["H91"]
    }
  ],
  "WARNING"=>[
    {
      "type"=>"WARNING",
      "code"=>"WCAG2AA.Principle1.Guideline1_4.1_4_3",
      "nodeName"=>"label",
      "id"=>"",
      "msg"=>"This element is absolutely positioned and the background color can not be determined. Ensure the contrast ratio between the text and all covered parts of the background are at least 4.5:1.",
      "outerHTML"=>"<label class=\"sr-only\" for=\"mce-EMAIL\">...</label>",
      "techniques"=>["G18"]
    }
  ],
  "NOTICE"=>[
    {
      "type"=>"NOTICE",
      "code"=>"WCAG2AA.Principle2.Guideline2_4.2_4_2",
      "nodeName"=>"title",
      "id"=>"",
      "msg"=>"Check that the title element describes the document.",
      "outerHTML"=>"<title>...</title>",
      "techniques"=>["H25"]
    },
  ]
}
```

## Building

Currently just notes for myself.

From HTML_CodeSnippets.js, 

* copy `HTML_CodeSniffer/Contrib/PhantomJS/HTMLCS_Run.js` to `vendor`
* copy `HTML_CodeSniffer/build/HTMLCS.js` to `vendor`

## Rules

*Currently displaying access_lint.rb rules* 
For full descriptions of the audit rules, visit the [Accessibility Developer Tools project wiki](https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules).

Code                       | Title
---------------------------|----------------------------------------------------
[AX_ARIA_01][AX_ARIA_01]   | Elements with ARIA roles must use a valid, non-abstract ARIA role.
[AX_ARIA_02][AX_ARIA_02]   | ARIA attributes which refer to other elements by ID should refer to elements which exist in the DOM.
[AX_ARIA_03][AX_ARIA_03]   | Elements with ARIA roles must have all required attributes for that role.
[AX_ARIA_04][AX_ARIA_04]   | ARIA state and property values must be valid.
[AX_ARIA_05][AX_ARIA_05]   | role=main should only appear on significant elements.
[AX_ARIA_06][AX_ARIA_06]   | aria-owns should not be used if ownership is implicit in the DOM.
[AX_ARIA_07][AX_ARIA_07]   | An element's ID must not be present in more that one aria-owns attribute at any time.
[AX_ARIA_08][AX_ARIA_08]   | Elements with ARIA roles must ensure required owned elements are present.
[AX_ARIA_09][AX_ARIA_09]   | Elements with ARIA roles must be in the correct scope.
[AX_ARIA_10][AX_ARIA_10]   | This element has an unsupported ARIA attribute.
[AX_ARIA_11][AX_ARIA_11]   | This element has an invalid ARIA attribute.
[AX_ARIA_12][AX_ARIA_12]   | This element does not support ARIA roles, states and properties.
[AX_AUDIO_01][AX_AUDIO_01] | Audio elements should have controls.
[AX_COLOR_01][AX_COLOR_01] | Text elements should have a reasonable contrast ratio.
[AX_FOCUS_01][AX_FOCUS_01] | These elements are focusable but either invisible or obscured by another element.
[AX_FOCUS_02][AX_FOCUS_02] | Elements with onclick handlers must be focusable.
[AX_FOCUS_03][AX_FOCUS_03] | Avoid positive integer values for tabIndex.
[AX_HTML_01][AX_HTML_01]   | The web page should have the content's human language indicated in the markup.
[AX_HTML_02][AX_HTML_02]   | An element's ID must be unique in the DOM.
[AX_IMAGE_01][AX_IMAGE_01] | Meaningful images should not be used in element backgrounds.
[AX_TEXT_01][AX_TEXT_01]   | Controls and media elements should have labels.
[AX_TEXT_02][AX_TEXT_02]   | Images should have an alt attribute.
[AX_TEXT_04][AX_TEXT_04]   | The purpose of each link should be clear from the link text.
[AX_TITLE_01][AX_TITLE_01] | The web page should have a title that describes topic or purpose.
[AX_VIDEO_01][AX_VIDEO_01] | Video elements should use <track> elements to provide captions.

[AX_ARIA_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_01
[AX_ARIA_02]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_02
[AX_ARIA_03]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_03
[AX_ARIA_04]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_04
[AX_ARIA_05]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_05
[AX_ARIA_06]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_06
[AX_ARIA_07]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_07
[AX_ARIA_08]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_08
[AX_ARIA_09]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_09
[AX_ARIA_10]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_10
[AX_ARIA_11]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_11
[AX_ARIA_12]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_aria_12
[AX_AUDIO_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_audio_01
[AX_COLOR_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_color_01
[AX_FOCUS_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_focus_01
[AX_FOCUS_02]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_focus_02
[AX_FOCUS_03]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_focus_03
[AX_HTML_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_html_01
[AX_HTML_02]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_html_02
[AX_IMAGE_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_image_01
[AX_TEXT_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_text_01
[AX_TEXT_02]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_text_02
[AX_TEXT_04]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_text_04
[AX_TITLE_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_title_01
[AX_VIDEO_01]: https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules#ax_video_01

## Roadmap

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
