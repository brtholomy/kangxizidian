# Kangxi Zidian stardict to dictd

## sources

https://simonwiles.net/projects/kangxi-zidian/

https://github.com/baskerville/sdunpack

## prepare

```
git clone https://github.com/baskerville/sdunpack
cargo build
cp target/debug/sdunpack /tmp/
```

```
curl -LJO https://simonwiles.net/files/kangxi-zidian/stardict-kangxizidian.tar.bz2
extract stardict-kangxizidian.tar.bz2
```

## unpack and repack

```
dictzip -d kangxizidian.dict.dz
/tmp/sdunpack kangxizidian.dict < kangxizidian.idx > kangxizidian.txt
```

## remove html

The stardict version comes with HTML that dictd doesn't want or need.

```
sed -E 's/^<a style="background:.*3px;" href="http:\/\/www.kangxizidian.com\/kangxi\/(.*?)\.gif">(.*?)$/\2\nhttp:\/\/www.kangxizidian.com\/kangxi\/\1.gif/g' kangxizidian.txt
```

etc.

Then proceed with the `dictfmt` command:

```
dictfmt --utf8 --index-keep-orig --headword-separator '|' -s "康熙字典" -t kangxizidian < kangxizidian.txt
dictzip kangxizidian.dict
sudo cp kangxizidian.dict.dz kangxizidian.index /usr/share/dictd/
```
