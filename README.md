# SQL Doc

A script for generating documentation from SQL file comments.

Inspired by protoc-gen-doc (https://github.com/pseudomuto/protoc-gen-doc)

Requires Python 3; tested with 3.6.

## Usage
As simple as:
```bash
python3 sql-doc.py --src=examples --out=examples/README.md
```

You can also write to stdout by leaving out the `out` parameter:
```bash
python3 sql-doc.py --src=examples
```

By default, the script search for files ending in `.sql`.
This can be overridden with (include the dot):
```bash
python3 sql-doc.py --src=examples --file_extension=.foo --out=examples/README.md
```


## Rules
### Comment Parsing

- Blank lines are ignored.
- Starting from the top of the file, comment lines are added to the comment block.
- Once a non-comment appears, the remainder, including later comments, is added to the code block.
- Files without (starting) comments will still be included.
- Lines are *not sanitised* during parsing, only formatted.

### Section Creation

- Each directory below the sources root (`src`) forms a section, iff there is
at least one SQL file in it.
- Subdirectories become subsections.
- This behaviour is overridden with a special `docpath:` keyword (see below).

### Special Keywords
The aim is to limit special keywords to a minimum. This is to let writers focus on content, not keywords.

#### docpath
The `docpath` keyword overrides the section determination logic for the file.
Example: `-- docpath: foo/bar` will place the file in the subsection `bar` of the section `foo`.

## License
Copyright 2020 Hayo van Loon

Licensed under the Apache License, Version 2.0 (the "License"); you may not use 
this file except in compliance with the License. You may obtain a copy of the 
License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed 
under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR 
CONDITIONS OF ANY KIND, either express or implied. See the License for the 
specific language governing permissions and limitations under the License.