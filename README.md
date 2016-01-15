# My Curriculum Vitae

This repository contains my curriculum vitae.

No more, no less.

# Why ?

As a software engineer, I wanted my CV to follow my professional practices :

* Source text based to easily use SCMs, merging, diffing, history
* Publicly available, shareable, editable
* HTML W3C compliant but also PDF format to ease reading


I also wanted to (re)-learn some basics of the front [(and back)][8] end
development, using a task runner, livereload, and other facilities.

Ruby is also used because, it is just **fun** to
combine heterogenous tools.


# What ?

* Content of the CV is in
[YAML format][1].
* HTML and PDF rendered versions can also be found here :
  - [HTML version](./src/export/cv.html)
  - PDF version (not available yet)
* Rendering from YAML to HTML is done with [HAML engine][2]
* This is mainly a fork of [dduportal](https://github.com/dduportal/curriculum_vitae), thanks for this great work !

# How ?

## Easy method : [Docker][6] and [Compose][7]

[Docker][6] is used to make the packaging easy and portable
[Compose][7] will take care of mounting files, forwarding ports, etc.

Ensure you have [Docker][6] and [Compose][7] clients
configured to reach a working Docker Engine

Then, just run  to launch the [Gulp][5] process :
```
$ docker-compose up
```

Open you browser to the page, using your Docker Engine IP :
```
http://<YOUR DOCKER ENGINE IP>:4000
```

## Not-so-easy method : Local Gulp and local Bundler

> TIP : the Dockerfile is a good idea to understand
> how to do that.

If you know your way with [Gulp][5], [NPM][3], and [Bundler](4)
or just do not want to use [Docker][6],
you should follow those instructions in the right order :

1. Install [NPM][3]. We use it to manage dependencies.

2. Then you need a [Ruby Bundler installation][4]
to manage dependencies of Ruby Gem
with this command :
    ```
    # With Ruby and Bundler installed
    $ bundle install
    ...
    ```

3. Then you can bootstrap dependencies with [NPM][3] :
    ```
    # Will install all the dev. modules locally
    $ npm install
    ...
    ```

4. [Gulp][5] is used as workflow engine by running tasks :
    ```
    $ gulp
    # It will run the default task that renders, serves pages
    # with live-reload enabled
    ```

5. Open your browser to http://localhost:4000

# Deploying

The folder ```./src/export``` :
* Is not stored inside git (cf ```.gitignore```)
* Is both generated and served by the [Gulp][5] workflow

If you want to deploy the content of this folder to another directory,
just mount it with [docker-compose][7] and provide and environment variable.

For example, using [docker-compose extending feature](https://docs.docker.com/compose/extends/) :

1. Create a file name ```docker-compose.override.yml``` at the repository root
(note that this file will not be git-tracked for security reasons) :
```yml
gulp-server:
    volumes:
      - ~/some/folder:/folder/to/deploy
    environment:
      - DEPLOY_DIR=/folder/to/deploy
```

2. Then, just call the gulp ```deploy```target :
```
$ docker-compose run gulp-server deploy
```

3. OR run ```gulp deploy```if you are in local mode:
```
$ DEPLOY_DIR=~/some/folder gulp deploy
```


# Licensing

This repository is provided on the [ISC license](http://www.gnu.org/licenses/license-list.html#ISC).

You will find the License [here](./LICENSE.md).

It means you can use the content only
if you make it appear with the same license.


[1]: http://yaml.org
[2]: http://haml.info
[3]: https://npmjs.org
[4]: http://bundler.io
[5]: http://gulpjs.com
[6]: https://docker.com
[7]: https://docs.docker.com/compose/
[8]: http://www.commitstrip.com/en/2015/09/08/how-to-mess-with-your-project-manager/?setLocale=1
