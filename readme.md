# download [![Build Status](http://img.shields.io/travis/kevva/download.svg?style=flat)](https://travis-ci.org/kevva/download)

> Download and extract files effortlessly

## Install

```sh
$ npm install --save download
```

## Usage

If you're fetching an archive you can set `extract: true` in options and
it'll extract it for you.

```js
var Download = require('download');

var download = new Download({ extract: true, strip: 1, mode: '755' })
	.get('http://example.com/foo.zip')
	.get('http://example.com/cat.jpg')
	.dest('dest');

download.run(function (err, files) {
	if (err) {
		throw err;
	}

	console.log('File downloaded successfully!');
});
```

## API

### new Download(opts)

Creates a new `Download` instance.

### .get(url, [dest])

Type: `String`

Add a file to download.

### .dest(dir)

Type: `String`

Set the destination folder to where your files will be downloaded.

### .rename(name)

Type: `Function|String`

Rename your files using [gulp-rename](https://github.com/hparra/gulp-rename).

### .run(cb)

Type: `Function`

Downloads your files and returns an error if something has gone wrong.

#### cb(err, files)

The callback will return an array of vinyl files.

## Options

### extract

Type: `Boolean`  
Default: `false`

If set to `true`, try extracting the file using [decompress](https://github.com/kevva/decompress/).

### mode

Type: `String`  

Set mode on the downloaded file, i.e `{ mode: '755' }`.

### strip

Type: `Number`  
Default: `0`

Equivalent to `--strip-components` for tar.

## CLI

```bash
$ npm install --global download
```

```sh
$ download --help

Usage
  download <url>
  download <url> > <file>
  download --out <directory> <url>
  cat <file> | download --out <directory>

Example
  download http://foo.com/file.zip
  download http://foo.com/cat.png > dog.png
  download --extract --strip 1 --out dest http://foo.com/file.zip
  cat urls.txt | download --out dest

Options
  -e, --extract           Try decompressing the file
  -o, --out               Where to place the downloaded files
  -s, --strip <number>    Strip leading paths from file names on extraction
```

## License

MIT © [Kevin Mårtensson](http://kevinmartensson.com)