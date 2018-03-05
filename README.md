# heroku-buildpack-ffmpeg

```
apt-get update -qq && apt-get -y install \
  autoconf \
  automake \
  build-essential \
  cmake \
  git \
  libass-dev \
  libfreetype6-dev \
  libtheora-dev \
  libtool \
  libvorbis-dev \
  libxcb1-dev \
  mercurial \
  pkg-config \
  texinfo \
  wget \
  zlib1g-dev
```

```
cd ~/ffmpeg_sources && \
wget -O ffmpeg-snapshot.tar.bz2 http://ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2 && \
tar xjvf ffmpeg-snapshot.tar.bz2 && \
cd ffmpeg && \
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
  --prefix="$HOME/ffmpeg_build" \
  --pkg-config-flags="--static" \
  --extra-cflags="-I$HOME/ffmpeg_build/include" \
  --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
  --extra-libs="-lpthread -lm" \
  --bindir="$HOME/bin" \
  --enable-gpl \
  --enable-static \
  --enable-libfdk-aac \
  --enable-libmp3lame \
  --enable-libopus \
  --enable-libvorbis \
  --disable-debug \
  --disable-ffplay \
  --disable-indev=sndio \
  --disable-outdev=sndio \
  --enable-nonfree && \
PATH="$HOME/bin:$PATH" make && \
make install
hash -r
```

https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu