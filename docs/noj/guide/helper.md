# Helper Functions

## version()
Get current NOJ version based on git
```php
function version();
```

### params
None

### example
```php
$version = version();
```

### explanation
None

### availability
Accessible since 0.1.1

***

## getCustomUrl()
Get customUrl for NOJ NavBar.
```php
function getCustomUrl();
```

### params
None

### example
```php
$urlArr = getCustomUrl();
```

### explanation
None

### availability
Accessible since 0.2.2

***

## emailVerified()
Judge whether email is berified.
```php
function emailVerified();
```

### params
None

### example
```php
$isEmailVerified = emailVerified();
```

### explanation
None

### availability
Accessible since 0.2.2

***

## babel_path()
Get the path of Babel folder.
```php
function babel_path($path='');
```

### params
path:
   * **type:** string
   * **default:** ""
   * **description:** path related to Babel path

### example
```php
$extensionDir = babel_path('Extension/');
```

### explanation
None

### availability
Accessible since 0.3.0

***

## glob_recursive()
Find pathnames matching a pattern recursively.
```php
function glob_recursive($pattern, $flags = 0);
```

### params
pattern:
   * **type:** string
   * **description:** The pattern. No tilde expansion or parameter substitution is done.

flags:
   * **type:** int
   * **default:** 0
   * **description:** Valid flags: `GLOB_MARK`

### example
```php
$babelJSON = glob_recursive('babel.json');
if (empty($babelJSON)){
    throw new \Exception('Not Found');
} else {
    $babelPath=dirname($babelJSON[0]);
}
```

### explanation
None

### availability
Accessible since 0.3.0

***

## adminMenu()
Get the Admin Panel Menu.
```php
function adminMenu();
```

### params
None

### example
```php
$extensionDir = babel_path('Extension/');
```

### explanation
None

### availability
Accessible since 0.3.1

***

## getOpenSearchXML()
Get the XML of OpenSearch.
```php
function getOpenSearchXML();
```

### params
None

### example
```php
Route::get('/opensearch.xml', function () {
    return response(getOpenSearchXML(), 200)->header("Content-type","text/xml");
});
```

### explanation
None

### availability
Accessible since 0.3.1

***

## delFile()
Delete all files of a folder.
```php
function delFile($dirName);
```

### params
dirName:
   * **type:** string
   * **description:** The path of target folder.

### example
```php
delFile(babel_path('Tmp'));
```

### explanation
None

### availability
Accessible since 0.3.1

***

## convertMarkdownToHtml()
Convert Markdown to HTML.
```php
function convertMarkdownToHtml($md);
```

### params
md:
   * **type:** string
   * **description:** The source Markdown files.

### example
```php
echo convertMarkdownToHtml("# NOJ\n\nYet Another Online Judge\n");
```

### explanation
None

### availability
Accessible since 0.3.2

***

## sendMessage()
Send message to users.
```php
function sendMessage($config);
```

### params
config:
   * **type:** array
   * **description:** Config of Message.

### example
```php
sendMessage([
    'receiver' => $receiverInfo["id"],
    'sender' => Auth::user()->id,
    'title' => "{$sender_name} invites you to group {$basic['name']}",
    'content' => "Hi, Dear **{$receiverInfo['name']}**,\n\n  **{$sender_name}** has just invited you to join the group **[{$basic['name']}]({$url})**. Take a look and meet other fascinating people right now!\n\nSincerely, NOJ"
]);
```

### explanation
None

### availability
Accessible since 0.3.2

***

## formatHumanReadableTime()
Format time to human readable time. 
```php
function formatHumanReadableTime($data);
```

### params
data:
   * **type:** string
   * **description:** Time.

### example
```php
echo formatHumanReadableTime('2018-10-24 10:24:00');
```

### explanation
None

### availability
Accessible since 0.3.2

***

## formatProblemSolvedTime()
Convert seconds into hours, minutes and seconds
```php
function formatProblemSolvedTime($seconds);
```

### example
```php
echo formatProblemSolvedTime(3600);
```

### explanation
None

### availability
Accessible since 0.4.0

