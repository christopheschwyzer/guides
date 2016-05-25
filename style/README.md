# Style

## Formatting
* Every file should end with an EOL
* EOL is \n
* Use four spaces for indentation (two for JS)
* Prefer single over double quotes
* Use the JetBrain IDE's codestyle templates

## Naming
* Do not use **abbreviations** (for exceptions: capitalize them like normal words. E.g. `Css`)
* If the individual item as well as a **collection of items** is used, suffix the collection with "List". E.g. `eggList`.
* Chose **systematic names** reading from *general* to *specific* from left to right, rather than grammatically correct names. E.g. `streamChannelMessageType` or `ratingAverage`).
* **Methods** usually begin with a verb. E.g. `getSomething`, `setSomething`, `deleteSomethingElse`

## PHP

### Exceptions
Wrap variable output in backticks:
```php
throw new CM_Exception_NotAllowed('Parameter `' . $param . '` is not allowed.');
// or:
throw new CM_Exception_NotAllowed("Parameter `{$param}` is not allowed.");
```

### Coding standards
* Internal types: Use type-safe comparison, cast/check early.
* Use type hinting whenever possible. Prefer objects to internal types as arguments.
* Usage of *ternary operator* is discouraged, but allowed in simple non-nested variable assignments, like:
```php
$state = isset($requestBody['state']) ? (string) $requestBody['state'] : null;
```
* Within classes, we define first the class constants, then the non-static class properties, the static class properties, the constructor, the abstract methods, the non-static methods and finally the static methods.
Within each category, items are ordered by their visibility (starting with the highest one) and finally sorted alphabetically.
The only exception to the alphabetical sorting are setters, which should be defined right after their respective getter.

Some/Example.php
```php
<?php

abstract class Some_Example {

	const FOO = 1;

	/** @var int */
	private $_fooBar;

	/** @var bool */
	public static $enabled;

	/**
	 * @param int $fooBar
	 */
	public function __construct($fooBar) {
		$this->_fooBar = (int) $fooBar;
	}

	/**
	 * @return float|null
	 */
	abstract public function getSome();

	/**
	 * @return bool
	 */
	public function getPublic() {
	}

	/**
	 * @param bool $state
	 * @param bool|null $foo
	 * @param string[]|null $bar
	 */
	public function setPublic($state, $foo = null, array $bar = null) {
		if (null === $foo) {
			$foo = false;
		}
		if (null === $bar) {
			$bar = array();
		}
	}

	/**
	 * @return bool|int|float|string|array|Object|Object[]
	 */
	private function _getPrivate() {
		if (true) {
			return true;
		} else {
			return 'hallo' . PHP_EOL;
		}
		return false;
	}

	/**
	 * @return Some_Example
	 */
	public static function getElse() {
		return new static(12);
	}
}
```

## Ruby
In most cases use parentheses around the arguments of method invocations, but:
- Omit parentheses for method calls with no arguments.
- Omit parentheses around parameters for methods that are part of an internal DSL (e.g. Rake, Rails, RSpec), methods that have "keyword" status in Ruby (e.g. `attr_reader`, `puts`) and attribute access methods. Use parentheses around the arguments of all other method invocations.

## HTML / CSS / JS
### Coding Standards
* Use CamelCase
* Use "-" for related child selectors (e.g. "clipSlide" & "clipSlide-handle")
* Use exclusive CSS class for JS bindings

### Example (toggleNext jQuery Plugin)
#### HTML
```html
<div class="toggleNext">Some Link</div>
<div class="toggleNext-content">
	Some Content
</div>
```
#### CSS
```css
.toggleNext {
	cursor: pointer;
}

.toggleNext-content {
	display: none;
}
```

#### JS
Docu styles are according to http://usejsdoc.org/.
```js
(function($) {
  /**
   * @param {String} required This is a required argument of type String.
   * @param {Object} [optional] This is an optional argument of type Object.
   */
  $.fn.toggleNext = function(required, optional) {
    this.optional = optional || {};
		return this.each(function() {
			var $toggler = $(this);
			var content = $toggler.next('.toggleNext-content');

			if (!content.length || $toggler.data('toggleNext')) {
				return;
			}

			var icon = $('<span />').addClass('icon toggle');
			$toggler.prepend(icon);

			if ($toggler.hasClass('active')) {
				icon.addClass('active');
				content.show();
			}

			$toggler.on('click.toggleNext', function() {
				$toggler.toggleClass('active');
				icon.toggleClass('active');
				content.slideToggle(100);
			});
			$toggler.data('toggleNext', true);
		});

	};
})(jQuery);
```

## Translations
### Heading Letter Case (for Headings, Menus, Tooltips, Buttons,...)
First and last word, as well as all open class words capitalized:
* Nouns
* Main verbs (not auxiliary verbs: be (am, are, is, was, were, being), can, could, do (did, does, doing), have (had, has, having), may, might, must, shall, should, will, would)
* Adjectives
* Adverbs
* Interjections

#### Examples
* The Vitamins are in my Fresh California Raisins.
* Terms of Use

### Add Translation
Use this translation method for words, short reusable sentences.
```smarty
{translate 'Some cool phrase'}
```
```smarty
{translate 'Some cool phrase with {$variable}' variable=$variable}
```
### Add Key Translation
Use this translation method for internal generated words, long texts, unique sentences.
```smarty
{translate '.language.key'}
```
```php
<?php
$langauge = CM_Model_Language::findByAbbreviation('en');
$language->setTranslation('.language.key', 'Translation without variables');
```

### Add Translation with Variables
```smarty
{translate '.language.key' variable=$variable}
```
```php
<?php
$language = CM_Model_Language::findByAbbreviation('en');
$language->setTranslation('.language.key', 'Transalation with {$variable}');
```

### Delete Translation
```php
<?php
CM_Model_LanguageKey::deleteByName('Some cool phrase');
CM_Model_LanguageKey::deleteByName('Some cool phrase with {$variable}');
CM_Model_LanguageKey::deleteByName('.language.key');
```
