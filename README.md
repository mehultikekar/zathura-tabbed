# mupdf + zathura + tabbed

[Zathura](https://pwmt.org/projects/zathura) document viewer using [mupdf](http://mupdf.com) backend and embedded in [tabbed](http://tools.suckless.org/tabbed).

## Compiling

Download sources for mupdf, [girara](https://pwmt.org/projects/girara), zathura, [zathura-pdf-mupdf](https://pwmt.org/projects/zathura-pdf-mupdf), tabbed

### mupdf

`make XCFLAGS=-fPIC release`

### girara

```
make PREFIX=/opt/zathura install
make PREFIX=/opt/zathura install-headers
```

### zathura

`env PKG_CONFIG_PATH=/opt/zathura/lib/pkgconfig make PREFIX=/opt/zathura WITH_SQLITE=0 WITH_MAGIC=0 LDFLAGS="-Wl,-rpath='\$\$ORIGIN/../lib'" install`

### zathura-pdf-mupdf

1. edit config.mk: prepend to INC -I<mupdf>/include, prepend to LIB -L<mupdf>/build/release
2. You might need to install a few system libraries and dev files like libopenjp2 and libssl (for libcrypto)
3. `env PKG_CONFIG_PATH=/opt/zathura/lib/pkgconfig make`
4. Copy `pdf.so` to `/opt/zathura/lib/zathura/pdf.so`

### tabbed

`make prefix=/opt/zathura install`

### Finishing touches

```
cp zathura-tabbed /opt/zathura/bin/
mkdir ~/.config/zathura
cp zathurarc ~/.config/zathura/
cp zathura.desktop ~/.local/share/applications/
xdg-mime default zathura.desktop application/pdf application/oxps application/epub+zip
```

Add `/opt/zathura/bin` to path at login (In `~/.profile` for example)

### Current versions

 - Xubuntu 15.04
 - mupdf-1.7a
 - girara-0.2.4
 - zathura-0.3.3
 - zathura-pdf-mupdf-0.2.8
 - tabbed (git commit 55dc32b27b73c121cab18009bf087e95ef3d9c18)