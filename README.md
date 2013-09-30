Heroku buildpack for ffmpeg
=======================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for using [ffmpeg](http://www.ffmpeg.org/) in your project.  
It doesn't do anything else, so to actually compile your app you should use [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi) to combine it with a real buildpack.

This version of ffmpeg was built with the following config options:

    ./configure --enable-shared \
    --disable-asm \
    --disable-filters \
    --disable-muxers \
    --disable-demuxers \
    --disable-encoders \
    --disable-decoders \
    --enable-encoder=vorbis \
    --enable-encoder=mpeg4 \
    --enable-decoder=gif \
    --enable-decoder=vorbis \
    --enable-decoder=mpeg4 \
    --prefix=/app/vendor/ffmpeg

Usage
-----
To use this buildpack, you should prepare .buildpacks file that contains this buildpack url and your real buildpack url.  

    $ cat .buildpacks
    https://github.com/HYPERHYPER/heroku-buildpack-ffmpeg.git
    https://github.com/heroku/heroku-buildpack-ruby.git 

The first build pack is the git URL to this repo.
The second build pack is for a Rails app, see [https://github.com/heroku](https://github.com/heroku) for other app build packs.
    
    $ heroku config:set BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git

    $ git push heroku master
    ...

You can verify installing ffmpeg by following command.

    $ heroku run "ffmpeg -version"
