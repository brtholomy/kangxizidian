# Kangxi Zidian stardict to dictd

https://simonwiles.net/projects/kangxi-zidian/
https://github.com/baskerville/sdunpack

git clone https://github.com/baskerville/sdunpack
cargo build
cp target/debug/sdunpack /tmp/

---

curl -LJO https://simonwiles.net/files/kangxi-zidian/stardict-kangxizidian.tar.bz2
extract stardict-kangxizidian.tar.bz2

---

dictzip -d kangxizidian.dict.dz
/tmp/sdunpack kangxizidian.dict < kangxizidian.idx > kangxizidian.txt
dictfmt --utf8 --index-keep-orig --headword-separator '|' -s "康熙字典" -t kangxizidian < kangxizidian.txt
dictzip kangxizidian.dict
sudo cp kangxizidian.dict.dz kangxizidian.index /usr/share/dictd/

---

remove crap:

```
sed -E 's/^<a style="background:.*3px;" href="http:\/\/www.kangxizidian.com\/kangxi\/(.*?)\.gif">(.*?)$/\2\nhttp:\/\/www.kangxizidian.com\/kangxi\/\1.gif/g' kangxizidian.head.txt
```

and do the rest with emacs.
