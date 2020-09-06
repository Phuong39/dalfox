<h1 align="center">
  <br>
  <a href=""><img src="https://user-images.githubusercontent.com/13212227/89670501-45b4a600-d91c-11ea-95d9-0b3802259dfd.png" alt="" width="260px;"></a>
  <br>
  DalFox(Finder Of XSS)
  <br>
  <img src="https://img.shields.io/github/v/release/hahwul/dalfox?style=flat-square"> 
  <a href="https://snapcraft.io/dalfox"><img alt="dalfox" src="https://snapcraft.io/dalfox/badge.svg" /></a>
  <img src="https://img.shields.io/github/languages/top/hahwul/dalfox?style=flat-square"> <img src="https://api.codacy.com/project/badge/Grade/17cac7b8d1e849a688577f2bbdd6ecd0"> <a href="https://goreportcard.com/report/github.com/hahwul/dalfox"><img src="https://goreportcard.com/badge/github.com/hahwul/dalfox"></a> <img src="https://img.shields.io/github/issues-closed/hahwul/dalfox?style=flat-square"> 
<a href="https://twitter.com/intent/follow?screen_name=hahwul"><img src="https://img.shields.io/twitter/follow/hahwul?style=flat-square"></a>
</h1>
Finder Of XSS, and Dal is the Korean pronunciation of moon.

## What is DalFox 🌘🦊
DalFox is a fast, powerful parameter analysis and XSS scanner, based on a golang/DOM parser. supports friendly Pipeline, CI/CD and testing of different types of XSS. I talk about naming. Dal(달) is the Korean pronunciation of moon and fox was made into Fox(Find Of XSS).

## Key features
Mode: `url` `sxss` `pipe` `file` `server`

| Class         | Key Feature                   | Description                                                  |
| ------------- | ----------------------------- | ------------------------------------------------------------ |
| Discovery     | Parameter analysis            | - Find reflected param<br />- Find alive/bad special chars, event handler and attack code <br />- Identification of injection points(HTML/JS/Attribute) |
|               | Static analysis               | - Check bad-header like CSP, XFO, etc.. with req/res base    |
|               | Parameter Mining              | - Find new param with Dictonary attack (default is GF-Patterns)<br />- Support custom dictonary file (`--mining-dict-word`)<br />- FInd new param with DOM |
|               | Built-in Grepping             | - It Identify the basic info leak of SSTi, Credential, SQL Error, and so on |
| Scanning      | XSS Scanning                  | - Reflected xss / stored xss <br />- DOM base verifying<br />- Blind XSS testing with param, header(`-b` , `--blind` options)<br />- Only testing selected parameters (`-p`, `--param`)<br />- Only testing parameter analysis (`--only-discovery`) |
|               | Friendly Pipeline             | - Single url mode (`dalfox url`)<br />- From file mode (`dalfox file urls.txt`)<br />- From IO(pipeline) mode (`dalfox pipe`)<br />- From raw http request file mode (`dalfox file raw.txt --rawdata`) |
|               | Optimizaion query of payloads | - Check the injection point through abstraction and generated the fit payload.<br />- Eliminate unnecessary payloads based on badchar |
|               | Encoder                       | - All test payloads(build-in, your custom/blind) are tested in parallel with the encoder.<br />- To Double URL Encoder<br />- To HTML Hex Encoder |
|               | Sequence                      | - Auto-check the special page for stored xss (`--trigger`) <br />- Support (`--sequence`) options for Stored XSS , only `sxss` mode |
| HTTP          | HTTP Options                  | - Follow redirects (`--follow-redirects`)<br />- Add header (`-H`, `--header`)<br />- Add cookie (`-C`, `--cookie`)<br />- Add User-Agent (`--user-agent`)<br />- Set timeout (`--timeout`)<br />- Set Delay (`--delay`)<br />- Set Proxy (`--proxy`)<br />- Set ignore return codes (`--ignore-return`) |
| Concurrency   | Worker                        | - Set worker's number(`-w`, `--worker`)                      |
|               | N * hosts                     | - Use multicast mode (`--multicast`) , only `file` / `pipe` mode |
| Output        | Output                        | - Only the PoC code and useful information is write as Stdout<br />- Save output (`-o`, `--output`) |
|               | Format                        | - JSON / Plain (`--format`)                                  |
|               | Printing                      | - Silence mode (`--silence`)<br />- You may choose not to print the color (`--no-color`) |
| Extensibility | REST API                      | - API Server and Swagger (`dalfox server`)                   |
|               | Found Action                  | - Lets you specify the actions to take when detected. <br />- Notify, for example (`--found-action`) |
|               | Custom Grepping               | - Can grep with custom regular expressions on response<br />- If duplicate detection, it performs deduplication (`--grep`) |
| Package       | Package manger                | - homebrew<br />- snapcraft                                  |
|               | Docker ENV                    | - docker hub<br />- gitub docker hub                         |

And the various options required for the testing :D

## How to Install
You can find some additional installation variations in the [Installation Guide](https://github.com/hahwul/dalfox/wiki/1.-Installation).

## Usage
```plain
    _..._
  .' .::::.   __   _   _    ___ _ __ __
 :  :::::::: |  \ / \ | |  | __/ \\ V /
 :  :::::::: | o ) o || |_ | _( o )) (
 '. '::::::' |__/|_n_||___||_| \_//_n_\
   '-.::''
Parameter Analysis and XSS Scanning tool based on golang
Finder Of XSS and Dal is the Korean pronunciation of moon. @hahwul
Usage:
  dalfox [command]

Available Commands:
  file        Use file mode(targets list or rawdata)
  help        Help about any command
  pipe        Use pipeline mode
  server      Start API Server
  sxss        Use Stored XSS mode
  url         Use single target mode
  version     Show version

Flags:
  -b, --blind string              Add your blind xss (e.g -b hahwul.xss.ht)
      --config string             Using config from file
  -C, --cookie string             Add custom cookie
      --custom-payload string     Add custom payloads from file
  -d, --data string               Using POST Method and add Body data
      --delay int                 Milliseconds between send to same host (1000==1s)
      --follow-redirects          Following redirection
      --format string             stdout output format(plain/json) (default "plain")
      --found-action string       If found weak/vuln, action(cmd) to next
      --grep string               Using custom grepping file (e.g --grep ./samples/sample_grep.json)
  -H, --header string             Add custom headers
  -h, --help                      help for dalfox
      --ignore-return string      Ignore scanning from return code (e.g --ignore-return 302,403,404)
      --mining-dict               Find new parameter with dictionary attack, default is Gf-Patterns=>XSS (default true)
      --mining-dict-word string   custom wordlist file for param mining (e.g --mining-dict-word word.txt)
      --mining-dom                Find new parameter in DOM (attribute/js value) (default true)
      --no-color                  not use colorize
      --only-discovery            Only testing parameter analysis
  -o, --output string             Write to output file
  -p, --param string              Only testing selected parameters
      --proxy string              Send all request to proxy server (e.g --proxy http://127.0.0.1:8080)
      --silence                   Not printing all logs
      --timeout int               Second of timeout (default 10)
      --user-agent string         Add custom UserAgent
  -w, --worker int                Number of worker (default 100)

Use "dalfox [command] --help" for more information about a command.
```

```
$ dalfox [mode] [flags]
```

Single target mode
```plain
$ dalfox url http://testphp.vulnweb.com/listproducts.php\?cat\=123\&artist\=123\&asdf\=ff -b https://hahwul.xss.ht
```

Multiple target mode from file
```plain
$ dalfox file urls_file --custom-payload ./mypayloads.txt
```

Pipeline mode
```plain
$ cat urls_file | dalfox pipe -H "AuthToken: bbadsfkasdfadsf87"
```

Other tips, See [wiki](https://github.com/hahwul/dalfox/wiki) for detailed instructions!

## Screenshots
| ![1414](https://user-images.githubusercontent.com/13212227/89736704-4ed17e80-daa6-11ea-90d8-32f915911b52.png) | ![1415](https://user-images.githubusercontent.com/13212227/89736705-5002ab80-daa6-11ea-9ee8-d2def396c25a.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Single URL Scanning                                          | API Server and Swagger                                       |
| ![1416](https://user-images.githubusercontent.com/13212227/89736707-509b4200-daa6-11ea-9ca6-8055fa714401.png) | ![1419](https://user-images.githubusercontent.com/13212227/89736914-087d1f00-daa8-11ea-87e6-e33b78e2d344.png) |
| Built-in and Custom Grepping                                 | Pipeline Scanning                                            |

## Contribute
Check it [this](https://github.com/hahwul/dalfox/blob/master/CONTRIBUTING.md)
