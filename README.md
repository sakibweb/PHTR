# PHTR
## PHTR - PHP Translation Library

PHTR is a lightweight PHP library that simplifies text translation using various translation services without requiring API keys for some services. It supports multiple translation servers, automatic language detection, array and HTML input, and caching for improved performance.

## Features

- **Multiple Server Support:** Easily switch between different translation providers (Google Translate, LibreTranslate, Lingva, MyMemory, and more).
- **Automatic Language Detection:**  Automatically detects the source language if not explicitly provided.
- **Array and HTML Input:**  Translates both plain text and arrays, preserving keys. Also handles simple HTML.
- **Caching:** Caches previously translated texts to reduce redundant requests and improve performance.
- **Extensible:**  Easily add support for new translation services.
- **No API Keys Required (for some services):**  Some services like Google Translate and LibreTranslate are accessible without API keys through their web interfaces, which PHTR leverages.

## Installation

Simply include the `PHTR.php` file in your project. No additional dependencies are required.

```php
include 'PHTR.php';
```

## Usage

### Basic Translation

```php
// Translate a single string
echo PHTR::translate("Hello, world!", 'google', 'en', 'es'); // Output: Hola, mundo!

// Translate an array
$data = ['greeting' => 'Hello', 'farewell' => 'Goodbye'];
$translatedData = PHTR::translate($data, 'libre', 'en', 'fr'); 
print_r($translatedData); // Output: ['greeting' => 'Bonjour', 'farewell' => 'Au revoir']

// Translate simple HTML content
$html = '<b id="data">Hello, world!</b>';
$translatedHTML = PHTR::translate($html, 'google', 'en', 'de');
echo $translatedHTML; // Output: <b id="data">Hallo Welt!</b>
```

### Automatic Translation

```php
// Automatically translate using the first available service
$text = "This is a test.";
$translatedText = PHTR::auto($text, 'fr');
echo $translatedText; // Output (if Google Translate is available): Ceci est un test.
```

### Server-Specific Translations

You can specify the translation server using the `$serverName` parameter. See the `$servers` array in the `PHTR.php` file for the supported server names.

### Language Codes

Use standard two-letter language codes (e.g., 'en', 'es', 'fr'). Set `$source` to `'auto'` for automatic language detection.  The `getLanguageCode()` function allows you to use more descriptive language identifiers like "English" or "Spanish" or even country codes like "US" or "FR". See the `$languageMapping` property for details.

### Adding New Servers

To add support for new translation servers, update the `$servers` array with the service's URL and implement the `buildUrl` and `parseResponse` methods accordingly to handle the specific API format of the new service.

## Examples
More examples are available in the `examples` directory of this repository.

## Limitations

- Free translation services may have usage limits and quality variations.
- The accuracy of automatic language detection depends on the underlying service and the input text.
- Complex HTML or markup may not be translated correctly.  Consider translating only the plain text content within tags if needed.
- This library currently uses the web interfaces of some translation services.  While convenient for not requiring API keys, these interfaces may change, and the library might require updates to keep working.


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
