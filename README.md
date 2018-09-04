# npm-maven-plugin

Fetch [npm](https://npmjs.org/) modules in your Maven build.

# Build

    mvn clean install

# Usage

Add the following plugin inside build -> plugins:

```xml
<plugin>
    <groupId>com.follett.fss.thirdparty</groupId>
    <artifactId>npm-maven-plugin</artifactId>
    <version>1.2</version>
    <executions>
        <execution>
            <phase>generate-sources</phase>
            <goals>
                <goal>fetch-modules</goal>
            </goals>
            <configuration>
                <downloadDependencies>true*/false</downloadDependencies>
                <outputDirectory>src/main/resources/META-INF* or something/else</outputDirectory>
                <packages>
                    <package>colors:0.5.1</package>
                    <package>jshint:0.8.1</package>
                    <package>@fortawesome/fontawesome-free:5.3.1</package>
                </packages>
            </configuration>
        </execution>
    </executions>
</plugin>
```

By default modules are downloaded recursively in `src/main/resources/META-INF` but other path can be specified with the 'outputDirectory' parameter.

Use `downloadDependencies=false` to just get the specified package.

Handles scoped packages (version 1.2)

# Authors / Contributors

Alberto Pose (@thepose)

Robert Csakany (https://github.com/robertcsakany)

# License
Copyright 2012 MuleSoft, Inc.

Licensed under the Common Public Attribution License (CPAL), Version 1.0.


# Technical Stuff

## Build me

This skips tests with lots of warnings

    $ mvn clean install -DskipTests -DskipITs

This deploys to nexus version `-FSC` to avoid collisions with the standard version.

    $ mvn clean deploy-plugin -DskipTests -DskipITs

## Pulling a Unscoped package

 curl -v  http://nexus.fsc.follett.com/nexus/repository/npm-npmjs/colors/-/colors-0.5.1.tgz

YAML response

```

---
maintainers:
- email: dabh@stanford.edu
  name: dabh
- email: marak.squires@gmail.com
  name: marak
keywords:
- ansi
- terminal
- colors
dist-tags:
  latest: 1.3.2
  next: 1.2.0-rc0
author:
  name: Marak Squires
_rev: '5569'
description: get colors in your node.js console
readme: "# colors.js\n[![Build Status](https://travis-ci..."
repository:
  type: git
  url: git+ssh://git@github.com/Marak/colors.js.git
users:
  avianflu: true
  gux: true
  xiaobing: true
bugs:
  url: https://github.com/Marak/colors.js/issues
license: MIT
versions:

  0.3.0:
    name: colors
    description: get colors in your node.js console like what
    more: here

  1.3.2:
    name: colors
    description: get colors in your node.js console
    version: 1.3.2
    author:
      name: Marak Squires
    contributors:
    - name: DABH
      url: https://github.com/DABH
    homepage: https://github.com/Marak/colors.js
    bugs:
      url: https://github.com/Marak/colors.js/issues
    keywords:
    - ansi
    - terminal
    - colors
    repository:
      type: git
      url: git+ssh://git@github.com/Marak/colors.js.git
    license: MIT
    scripts:
      lint: eslint . --fix
      test: node tests/basic-test.js && node tests/safe-test.js
    engines:
      node: ">=0.1.90"
    main: lib/index.js
    files:
    - examples
    - lib
    - LICENSE
    - safe.js
    - themes
    - index.d.ts
    - safe.d.ts
    devDependencies:
      eslint-config-google: "^0.9.1"
      eslint: "^5.4.0"
    gitHead: 4a6d75d01c4389a9e9f7288cc2434b95decbcd58
    _id: colors@1.3.2
    _npmVersion: 6.4.0
    _nodeVersion: 8.11.2
    _npmUser:
      name: dabh
      email: dabh@stanford.edu
    dist:
      integrity: sha512-rhP0JSBGYvpcNQj4s5AdShMeE5ahMop96cTeDl/v9qQQm2fYClE2QXZRi8wLzc+GmXSxdIqqbOIAhyObEXDbfQ==
      shasum: 2df8ff573dfbf255af562f8ce7181d6b971a359b
      tarball: http://nexus.fsc.follett.com/nexus/repository/npm-npmjs/colors/-/colors-1.3.2.tgz
      fileCount: 22
      unpackedSize: 53884
      npm-signature: "-----BEGIN PGP SIGNATURE-----\r\nVersion: OpenPGP.js v3.0.4\r\nComment:
        https://openpgpjs.org\r\n\r\nwsFcBAEBCAAQBQJbfbASCRA9TVsSAnZWagAAupgP/RLhkx6+gaWO1J8LFqSK\nfLEiSYsTJxe/EmilFi7w/+QBc8Ye0vehdJkvtvfASZfKTI4hM/1RArQsbWDr\nI+FCN1g23KOXAW2kblwsLdOOsYtanULRVHf6KVdVqbhnNpeKOLH52CODo343\nNoy3OGyVR/FRxwNZ6j7xECJj4Q8ET5/q+fodW8vHOuHm8xz7mr8FZrvWWggc\nCih41IedHCR/N8oeWmJtHWR1viD5NINxQr1k8/srD+VVIiRa7C7GG4yMcc7b\nxX2cGBT+CFs0oEjvfsMFaZdbmVLeJWv5B00xQxbRkrIKvA63057sHO7WLA/I\nEKCucGz0HF9N55x4mOIhrX2r89qMNhnsvEUMY66GXMnfPGSdOyKDa7GmicYV\nwX7Vm2mmneAWwF+IsSpyx5H9i+Ul0kg4vcbcmS1uXVh7aJBwqTlhPSk0SanN\n6tiIh/F7QVS4Z1tWJB+7ZahshZRT+I/pxag12/GFkcu3zWns9HgZlPwp5dvK\nztRLcvzNjNsiuCAyLVDOh1iFcNnhOGoKcI5J9Og/CiI/VaTZmsT38RJ8qHQv\nqaewEh7JcYbuRgffwOe/a1IZF/eUctSrfh0IfNRTosM3wHIh1f7aIHCF+S67\n9j8kLY8RCxLQH7h5XxH+yQxa0TAwhKObL4qYZqlTKEpMaIPXpMeyAB1R/8X9\nWnT0\r\n=ZBF8\r\n-----END
        PGP SIGNATURE-----\r\n"
    maintainers:
    - email: dabh@stanford.edu
      name: dabh
    - email: marak.squires@gmail.com
      name: marak
    directories: {}
    _npmOperationalInternal:
      host: s3://npm-registry-packages
      tmp: tmp/colors_1.3.2_1534963730147_0.3209457183870088
name: colors
time:
  modified: '2018-09-04T09:35:29.648Z'
  created: '2011-03-15T10:12:18.245Z'
  0.3.0: '2011-03-15T10:12:18.245Z'
  1.3.1: '2018-07-22T22:06:27.574Z'
  1.3.2: 2018-08-22T18:48:*50.238Z
readmeFilename: README.md
contributors:
- name: DABH
  url: https://github.com/DABH
_id: colors
homepage: https://github.com/Marak/colors.js

```

## Pulling a Scoped package

The download URL is at

    versions."5.3.1".dist.tarball=> https://registry.npmjs.org/@fortawesome/fontawesome-free/-/fontawesome-free-5.3.1.tgz

The YAML version of the JSON response, edited:

```yaml
---
_id: "@fortawesome/fontawesome-free"
_rev: 15-5c82a65398c8c10fcf143ddf4faf2223
name: "@fortawesome/fontawesome-free"
dist-tags:
  prerelease: 5.1.0-11
  latest: 5.3.1
versions:
  5.1.0:
    description: The iconic font, CSS, and SVG framework
    ...
  5.1.1:
    description: The iconic font, CSS, and SVG framework
    ...
  5.3.0:
    description: The iconic font, CSS, and SVG framework
    ...
  5.3.1:
    description: The iconic font, CSS, and SVG framework
    keywords:
    - font
    - awesome
    - fontawesome
    - icon
    - svg
    - bootstrap
    homepage: https://fontawesome.com
    bugs:
      url: http://github.com/FortAwesome/Font-Awesome/issues
    author:
      name: Dave Gandy
      email: dave@fontawesome.com
      url: http://twitter.com/davegandy
    contributors:
    - name: Brian Talbot
      url: http://twitter.com/talbs
      ...
    repository:
      type: git
      url: git+https://github.com/FortAwesome/Font-Awesome.git
    engines:
      node: ">=6"
    dependencies: {}
    version: 5.3.1
    name: "@fortawesome/fontawesome-free"
    main: js/fontawesome.js
    style: css/fontawesome.css
    license: "(CC-BY-4.0 AND OFL-1.1 AND MIT)"
    _id: "@fortawesome/fontawesome-free@5.3.1"
    _npmVersion: 6.3.0
    _nodeVersion: 8.11.3
    _npmUser:
      name: robmadole
      email: robmadole@gmail.com
    dist:
      integrity: sha512-jt6yi7iZVtkY9Jc6zFo+G2vqL4M81pb3IA3WmnnDt9ci7Asz+mPg4gbZL8pjx0nGFBsG0Bmd7BjU9IQkebqxFA==
      shasum: 5466b8f31c1f493a96754c1426c25796d0633dd9
      tarball: https://registry.npmjs.org/@fortawesome/fontawesome-free/-/fontawesome-free-5.3.1.tgz
      fileCount: 1427
      unpackedSize: 9583061
      npm-signature: "-----BEGIN PGP SIGNATURE-----\r\nVersion: OpenPGP.js v3.0.4\r\nComment:
        https://openpgpjs.org\r\n\r\nwsFcBAEBCAAQBQJbhYiSCRA9TVsSAnZWagAAR+EP/ichhVBWyLs1YgKKgaWm\nlAGj6Bh2SEHjubJKYtd68zDoFpAjqCy3St+wwtFPKfAuKNXtpycBmztM7Nr8\nMxPmDqWqliYHz7XQQ+69Bo2DIIxyfydtsaU9yCxMEf4sv2cwvzQEARyqA/rg\nvEPHJUqTcrZZUS1zj7AwFivkSfLcLKcEIpwZKO4N36Y/Q8mnudckWlE9UFMS\nh8h8m5pF7iSCk12zqvrpRjhYeJ8DoUhS+orOJCB+dvhbfeygL4N7OLApXpZ3\nn128jb02k/R5DGjXHfBLFDQDEQuInY16825k5+TMq65ZD12zp1FqIu3kQNaf\n8cLLAREBoMthln0m50QvI0wPC/wnQACrjHlL1B7auE2jQnhtJs26YcTY+7le\nE/h0JAiBe/VXHVltj/vxblbl9PODQOjPZKZo8bUbu6hft+kNFOekkSQudH04\nj/LFe9hlG7YQqpzwcXeq4z6mlIyeL4uLACyECqlY60oa3LgOxHZW+PlRPO8P\nKMc4vqv9lCxp8fqw/z0b38k638fZMSlNJsQSWHtX4lu/U+eZRIialPYqwG0f\nov15V1c6Th5NcfnhXvMZ1D8p8H/JLSauFyS8f2hMKirZQ8IpSWxEdkxeNcDw\nu9raWSraH82i8WM+DeisCYthqMRMOc4PqxXjUNWI9VS7SqbTcsDNAv5Di1iP\nqAMa\r\n=npaP\r\n-----END
        PGP SIGNATURE-----\r\n"
    maintainers:
    - email: devoto13@gmail.com
      name: devoto13
      ...
    directories: {}
    _npmOperationalInternal:
      host: s3://npm-registry-packages
      tmp: tmp/fontawesome-free_5.3.1_1535477905316_0.566900679740663
time:
  created: '2018-03-12T21:39:33.198Z'
  modified: '2018-08-28T17:38:29.662Z'
  5.3.0: '2018-08-27T17:20:10.347Z'
  5.3.1: '2018-08-28T17:38:25.580Z'
maintainers:
- email: devoto13@gmail.com
  name: devoto13
description: The iconic font, CSS, and SVG framework
homepage: https://fontawesome.com
keywords:
- font
- awesome
- fontawesome
- icon
- svg
- bootstrap
repository:
  type: git
  url: git+https://github.com/FortAwesome/Font-Awesome.git
contributors:
- name: Brian Talbot
  url: http://twitter.com/talbs
author:
  name: Dave Gandy
  email: dave@fontawesome.com
  url: http://twitter.com/davegandy
bugs:
  url: http://github.com/FortAwesome/Font-Awesome/issues
license: "(CC-BY-4.0 AND OFL-1.1 AND MIT)"
readmeFilename: README.md
_attachments: {}
```

### Happy hacking!
