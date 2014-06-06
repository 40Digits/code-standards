# HTML

**Contents**

- [Validation](#validation)
- [Self-Closing Elements](#self-closing-elements)
- [Attributes and Tags](#attributes-and-tags)
- [Quotes](#quotes)
- [Indentation](#indentation)


## Validation

All HTML pages should be verified against [the W3C validator](http://validator.w3.org/) to ensure that the markup is well formed. This in and of itself is not directly indicative of good code, but it helps to weed out problems that are able to be tested via automation. It is no substitute for manual code review. (For other validators, see [HTML Validation](http://codex.wordpress.org/Validating_a_Website#HTML_-_Validation) in the Codex.)


## Self-Closing Elements

All tags must be properly closed. For tags that can wrap nodes such as text or other elements, termination is a trivial enough task. For tags that are self-closing, the forward slash should have exactly one space preceding it.

**Correct:**

```
<br />
```

**Compact, but incorrect:**

```
<br/>
```

The [W3C](http://w3.org/TR/xhtml1/#C_2) specifies that a single space should precede the self-closing slash.


## Attributes and Tags

All tags and attributes must be written in lowercase. Additionally, attribute values should be lowercase when the purpose of the text therein is only to be interpreted by machines. For instances in which the data needs to be human readable, proper title capitalization should be followed.

**For machines:**

```
<meta http-equiv="content-type" content="text/html; charset=utf-8" />
```

**For humans:**

```
<a href="http://example.com/" title="Description Here">Example.com</a>
```


## Quotes

According to the W3C specifications for XHTML, all attributes must have a value, and must use double- or single-quotes ([source](http://www.w3.org/TR/xhtml1/#h-4.4)). The following are examples of proper and improper usage of quotes and attribute/value pairs.

**Correct:**

```
<input type="text" name="email" disabled="disabled" />
<input type='text' name='email' disabled='disabled' />
```

**Incorrect:**

```
<input type=text name=email disabled>
```

In HTML, attributes do not all have to have values, and attribute values do not always have to be quoted. While all of the examples above are valid HTML, **failing to quote attributes can lead to security vulnerabilities**. Always quotes attributes.


## Indentation

As with PHP, HTML indentation should always reflect logical structure. Use tabs and not spaces.

When mixing PHP and HTML together, indent PHP blocks to match the surrounding HTML code. Closing PHP blocks should match the same indentation level as the opening block.

**Correct:**

```php
<?php if ( ! have_posts() ) : ?>
    <div id="post-1" class="post">
        <h1 class="entry-title">Not Found</h1>
        <div class="entry-content">
            <p>Apologies, but no results were found.</p>
            <?php get_search_form(); ?>
        </div>
    </div>
<?php endif; ?>
```

**Incorrect:**

```php
<?php if ( ! have_posts() ) : ?>
   <div id="post-0" class="post error404 not-found">
      <h1 class="entry-title">Not Found</h1>
      <div class="entry-content">
         <p>Apologies, but no results were found.</p>
<?php get_search_form(); ?>
      </div>
  </div>
<?php endif; ?>
```