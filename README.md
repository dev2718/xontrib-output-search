<p align="center">
Get identifiers, names, paths, URLs and words from the previous command output and use them for the next command in <a href="https://xon.sh">xonsh</a>.
</p>
<p align="center">
Forget about using mouse or touchpad.<br> 
Forget about searching autocomplete plugins for every app you use.<br> 
</p>

<p align="center">  
If you like the idea of xontrib-output-search click ⭐ on the repo and stay tuned.
</p>

## Install
```shell script
xpip install -U git+https://github.com/anki-code/xontrib-output-search
echo 'xontrib load output_search' >> ~/.xonshrc
```

## Usage
After `xontrib load output_search` you can select tokens from latest not empty output:
* Press <kbd>Alt</kbd> + <kbd>F</kbd> hotkey
* Or type `f__` and press <kbd>Tab</kbd> key  

### Get any token from previous output
Text example:
```shell script
$ echo "Hello world"
Hello world
$ echo The second word is wo<Alt+F>
$ echo The second word is world
```

URL example: 
```shell script
$ echo "Try https://github.com/xxh/xxh"
Try https://github.com/xxh/xxh
$ git clone xx<Alt+F>
$ git clone https://github.com/xxh/xxh
```

`json` or `dict` example:
```shell script
$ echo '{"Try": "xontrib-output-search"}' # JSON data
{"Try": "xontrib-output-search"}
$ echo I should try se<Alt+F>
$ echo I should try xontrib-output-search
```    

`env`-like example:
```shell script
$ env | grep ^PATH=
PATH=/one/two:/three/four
$ ls fo<Alt+F>
$ ls /three/four
```    

#### It works for complex prefixes

Get the token from previous output after typing `git+`:
```shell script
$ echo "Try https://github.com/anki-code/xontrib-output-search"
Try https://github.com/anki-code/xontrib-output-search

$ pip install git+xo<Alt+F>
$ pip install git+https://github.com/anki-code/xontrib-output-search
```
Get the token from previous output while typing the URL path:
```shell script
$ echo "The id is 424242"
The id is 424242

$ curl https://test.com/id=4<Alt+F>
$ curl https://test.com/id=424242
```


## Development
### Clone and test
```shell script
cd ~
git clone https://github.com/anki-code/xontrib-output-search
cd xontrib-output-search
pytest
```

### Tokenizers
Tokenizers are functions which extract tokens from the output. You can create your tokenizer and add it to `_tokenizers`.

Current tokenizers:
```python
_tokenizers = {
    'dict': _tokenizer_dict,    # Extract keys and values from python dict or json
                                # Example: '{"key": "val as str"}' -> ['key', 'val as str']

    'env': _tokenizer_env       # Extract name and values from env-like text
                                # Example: 'PATH=/bin:/etc' -> ['PATH', '/bin:/etc', '/bin', '/etc']
    
    'split': _tokenizer_split,  # Splitting text by white spaces (space, tab, new line)
                                # Example: 'Split  me \n now!' -> ['Split', 'me', 'now!']

    'strip': _tokenizer_strip,  # Extract values from special charecters
                                # Example: '{Hello}' -> ['Hello']
}
```
## Known issues
#### `cat` is not captured
Workaround: `cat file | head`.

#### Alt+F combination may not working in PyCharm terminal
Workaround: `f__` + <kbd>Tab</kbd>.

## Thanks
I was inspired by [xontrib-histcpy](https://github.com/con-f-use/xontrib-histcpy). Thanks @con-f-use!
